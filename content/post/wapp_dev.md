---
date: '2025-04-02T14:56:52+08:00'
draft: false
title: '微信小程序开发记录'
categories:
  - tech
keywords:
  - 微信小程序
tags:
  - 微信小程序
---

# 基础

## 与网页开发的区别

开发语言都是javascript。

​网页开发中， 渲染任务和脚本任务是互斥的，而在小程序中二者是**分别运行在不同的线程**。小程序的逻辑层和渲染层是分开的，逻辑层运行在不同于渲染层的独立 JS 运行时中，因此并不能直接使用 DOM API 和 BOM API。这一区别导致了前端开发非常熟悉的一些库，例如 jQuery、 Zepto 等，在小程序中是无法运行的。同时逻辑层的 JS 运行时与 NodeJS 环境也不尽相同，所以一些 NPM 的包在小程序中也是无法运行的。

| 运行环境 | 逻辑环境 | 渲染层 |
|----------|----------|----------|
| iOS    | JavascriptCore   | WKWebView   |
| 安卓    | V8   |   chromium定制内核 |
| 小程序开发者工具    | NWJS   |   Chrome WebView |


## 宿主环境

微信客户端native给小程序所提供的环境为**宿主环境**。小程序借助宿主环境提供的能力，可以完成许多普通网页无法完成的功能。

小程序的渲染层和逻辑层分别由2个线程管理：渲染层的界面使用了WebView 进行渲染；逻辑层采用JsCore线程运行JS脚本。一个小程序存在多个界面，所以渲染层存在多个WebView线程，这两个线程的通信会经由微信客户端做中转，逻辑层发送网络请求也经由Native转发，小程序的通信模型下图所示。

![MiniApp Architecture](/images/tech/wechat_transport.png)

## 代码构成

小程序中包含四类文件：

1. `.json` 后缀的 JSON 配置文件
2. `.wxml` 后缀的 WXML 模板文件
3. `.wxss` 后缀的 WXSS 样式文件
4. `.js` 后缀的 JS 脚本逻辑文件

### JSON配置文件

在小程序中，JSON扮演的是静态配置的角色。在项目的根目录有一个`app.json`和 `project.config.json`，此外在`pages/logs`目录下还有一个`logs.json`。

**app.json**
`app.json`是当前小程序的全局配置，包括了小程序的所有页面路径、界面表现、网络超时时间、底部 tab 等。

```json
{
  "pages":[
    "pages/index/index",
    "pages/logs/logs"
  ],
  "window":{
    "backgroundTextStyle":"light",
    "navigationBarBackgroundColor": "#fff",
    "navigationBarTitleText": "Weixin",
    "navigationBarTextStyle":"black"
  }
}
```

配置各个项的含义:

1. `pages`字段 —— 用于描述当前小程序所有页面路径，这是为了让微信客户端知道当前你的小程序页面定义在哪个目录。
2. `window`字段 —— 定义小程序所有页面的顶部背景颜色，文字颜色定义等。


**工具配置 project.config.json**:

存放针对工具的个性化配置，其中会包括编辑器的颜色、代码上传时自动压缩等等一系列选项，保证迁移开发工具或者环境时保持一致性。

**页面配置 page.json**
这里的`page.json`其实用来表示`pages/logs`目录下的`logs.json`这类和小程序页面相关的配置。

如果你整个小程序的风格是蓝色调，那么你可以在 app.json 里边声明顶部颜色是蓝色即可。实际情况可能不是这样，可能你小程序里边的每个页面都有不一样的色调来区分不同功能模块，因此我们提供了`page.json`，让开发者可以独立定义每个页面的一些属性，例如刚刚说的顶部颜色、是否允许下拉刷新等等。

### WXML模板

WXML类似html, 用来描述页面的结构，也是由标签、属性等等构成。但是也有很多不一样的地方。

1. 标签名字不一样：小程序的 WXML 用的标签是`view`,`button`,`text`等等，这些标签就是小程序给开发者包装好的基本能力，我们还提供了地图、视频、音频等等组件能力。
2. 支持`wx:if`等特殊的属性以及`{{ }}`这样的表达式
3. WXML语言使用数据绑定功能来完成界面的实时更新，使用`{{变量名}}`来绑定WXML文件和对应JS文件中的data对象属性。用在属性值时，需注意**必须包裹在双引号**中。

```xml
<view class="container">
  <view class="userinfo">
    <button wx:if="{{!hasUserInfo && canIUse}}"> 获取头像昵称 </button>
    <block wx:else>
      <image src="{{userInfo.avatarUrl}}" background-size="cover"></image>
      <text class="userinfo-nickname">{{userInfo.nickName}}</text>
    </block>
  </view>
  <view class="usermotto">
    <text class="user-motto">{{motto}}</text>
  </view>
</view>
```

> + wxml中的属性是大小写敏感的，也就是class和Class在wxml中是不同的属性
> + 没有被定义的变量或者设置为undefined的变量不会被同步到WXML

wxml的逻辑语法/条件逻辑/列表渲染

```xml
<text>{{ a == 10 ? "a is 10" : "a is not 10" }}</text>
<!-- 支持运算和字符串拼接 -->
<view>{{"hello " + name}}</view>
<!-- 条件逻辑 -->
<view wx:if="{{length > 5}}"> 1 </view>
<view wx:else> 3 </view>
<!-- 一次判断多个组件标签 -->
<block wx:if="{{true}}">
  <view> view1 </view>
  <view> view2 </view>
</block>
<!-- 列表 -->
<view wx:for="{{array}}">
  {{index}}: {{item.message}}
</view>
<view wx:for="{{array}}" wx:for-index="idx" wx:for-item="itemName">
  {{idx}}: {{itemName.message}}
</view>
```

列表渲染：默认数组的当前项的下标变量名默认为 `index`，数组当前项的变量名默认为 `item`。可以使用`wx:for-item`指定数组当前元素的变量名，使用 `wx:for-index`指定数组当前下标的变量名。

如果列表中的项



### WXSS样式

WXSS具有CSS大部分的特性，做了扩充和修改。

1. 新增了尺寸单位: WXSS 在底层支持新的尺寸单位`rpx`，解决不同宽度和设备像素比换算的烦恼
2. 提供了全局的样式和局部样式: `app.wxss`作为全局样式，会作用于当前小程序的所有页面，局部页面样式`page.wxss`仅对当前页面生效
3. 仅支持部分`CSS`选择器

### JS逻辑交互

可以在 JS 中调用小程序提供的丰富的 API，利用这些 API 可以很方便的调起微信提供的能力，例如获取用户信息、本地存储、微信支付等。

```javascript
Page({
  getUserProfile(e) {
    // 推荐使用wx.getUserProfile获取用户信息，开发者每次通过该接口获取用户个人信息均需用户确认，开发者妥善保管用户快速填写的头像昵称，避免重复弹窗
    wx.getUserProfile({
      desc: '展示用户信息', // 声明获取用户个人信息后的用途，后续会展示在弹窗中，请谨慎填写
      success: (res) => {
        console.log(res)
        this.setData({
          userInfo: res.userInfo,
          hasUserInfo: true
        })
      }
    })
  },
})
```

## 启动和渲染流程

微信客户端在打开小程序之前，会把整个小程序的代码包下载到本地。紧接着通过`app.json`的`pages`字段就可以知道你当前小程序的所有页面路径, 如下面的配置代表有两个页面，分别位于`pages/index/index`和`pages/logs/logs`。而在`pages`中的第一个页面就是打开小程序看到的第一个页面。

```json
{
  "pages":[
    "pages/index/index",
    "pages/logs/logs"
  ]
}
```

小程序启动之后，在`app.js`定义的`App`实例的`onLaunch`回调会被执行。整个小程序只有一个`App` 实例，是全部页面共享的。

```javascript
App({
  onLaunch: function () {
    // 小程序启动之后 触发
  }
})
```

一个页面包含4种文件，以`logs`页面为例，微信客户端会先根据`logs.json`配置生成一个界面，顶部的颜色和文字你都可以在这个 json 文件里边定义好。紧接着客户端就会装载这个页面的 WXML 结构和 WXSS 样式。最后客户端会装载`logs.js`。

```javascript
Page({
  data: { // 参与页面渲染的数据
    logs: []
  },
  onLoad: function () {
    // 页面渲染后 执行
  }
})
```

`Page`是一个页面构造器，这个构造器就生成了一个页面。在生成页面的时候，小程序框架会把`data`数据和`index.wxml`一起渲染出最终的结构

## 组件

小程序提供了丰富的基础组件给开发者，开发者可以像搭积木一样，组合各种组件拼合成自己的小程序。在小程序里边，你只需要在 WXML 写上对应的组件标签名字就可以把该组件显示在界面上，例如，你需要在界面上显示地图:

```xml
<map bindmarkertap="markertap" longitude="广州经度" latitude="广州纬度"></map>
```

也可以通过`style`或者`class`来控制组件的外层样式，以便适应你的界面宽度高度等等。

## API

为了让开发者可以很方便的调起微信提供的能力，例如获取用户信息、微信支付等等，小程序提供了很多 API 给开发者去使用。例如获取用户位置信息和调用微信扫一扫：

```javascript
wx.getLocation({
  type: 'wgs84',
  success: (res) => {
    var latitude = res.latitude // 纬度
    var longitude = res.longitude // 经度
  }
})
wx.scanCode({
  success: (res) => {
    console.log(res)
  }
})
```

> 多数 API 的回调都是异步，你需要处理好代码逻辑的异步问题

## 版本管理&发布

### 小程序的版本

一般的软件开发流程，开发者编写代码自测开发版程序，直到程序达到一个稳定可体验的状态时，开发者会把这个体验版本给到产品经理和测试人员进行体验测试，最后修复完程序的Bug后发布供外部用户正式使用。小程序的版本根据这个流程设计了小程序版本的概念。

1. **开发版本**：使用开发者工具，可将代码上传到开发版本中。 开发版本只保留每人最新的一份上传的代码。点击提交审核，可将代码提交审核。开发版本可删除，不影响线上版本和审核中版本的代码。
2. **体验版本**: 可以选择某个开发版本作为体验版，并且选取一份体验版。
3. **审核中版本**: 只能有一份代码处于审核中。有审核结果后可以发布到线上，也可直接重新提交审核，覆盖原审核版本。
4. **线上版本**: 线上所有用户使用的代码版本，该版本代码在新版本代码发布后被覆盖更新。

### 发布上线

一个小程序从开发完到上线一般要经过 预览-> 上传代码 -> 提交审核 -> 发布等步骤。

**预览**

使用开发者工具可以预览小程序，帮助开发者检查小程序在移动客户端上的真实表现。点击开发者工具顶部操作栏的预览按钮，开发者工具会自动打包当前项目，并上传小程序代码至微信的服务器，成功之后会在界面上显示一个二维码，扫码即可看到小程序在手机客户端上的真实表现。

**上传代码**

上传代码是用于提交体验或者审核使用的。点击开发者工具顶部操作栏的上传按钮，填写版本号以及项目备注，需要注意的是，这里版本号以及项目备注是为了方便管理员检查版本使用的，开发者可以根据自己的实际要求来填写这两个字段。

上传成功之后，登录小程序管理后台 - 版本管理 - 开发版本 就可以找到刚提交上传的版本了。可以将这个版本设置 *体验版* 或者是 *提交审核*。

**提交审核**

在开发版本的列表中，点击 *提交审核* 按照页面提示，填写相关的信息，即可以将小程序提交审核。

**发布**

审核通过之后，管理员的微信中会收到小程序通过审核的通知。此时可以点击发布，即可发布小程序。小程序提供了两种发布模式：全量发布和分阶段发布（即灰度发布）。


# 配置详解

## 全局配置说明

`app.json`文件用来对微信小程序进行全局配置。文件内容为一个 JSON 对象, 以下是一些常用的属性：

```json
{
  // 包含的页面
  "pages": [
    "pages/home/home"
  ],
  "window": {
    // 导航栏的颜色
    "navigationBarBackgroundColor": "#ff0000",
    // 导航栏文字颜色
    "navigationBarTextStyle": "white",
    // 导航栏的文字
    "navigationBarTitleText": "小程序 Demo"     
  }
}
```



# 场景应用

## 基本布局方法——Flex布局

传统网页开发使用盒模型，如`display: inline|inline-box, position`等实现布局，缺乏灵活性。更建议使用flex布局。

```css
.container{
  display: flex;
  flex-direction: column;
  justify-content: center;
}
```

> 在代码示例中以container表示容器的类名。容器内的元素简称为“项目”，在代码示例中以item表示项目的类名。 

在不固定高度信息的情况下，只需要在容器中设置以下两个属性即可实现内容不确定下的垂直居中。

flex不是一个属性，而是包含了一套新的属性集。属性集包括用于设置容器，和用于设置项目两部分。

设置容器的属性有：

```css
display:flex;

flex-direction:row（默认值） | row-reverse | column |column-reverse

flex-wrap:nowrap（默认值） | wrap | wrap-reverse

justify-content:flex-start（默认值） | flex-end | center |space-between | space-around | space-evenly

align-items:stretch（默认值） | center  | flex-end | baseline | flex-start

align-content:stretch（默认值） | flex-start | center |flex-end | space-between | space-around | space-evenly
```

设置项目的属性有:

```css
order:0（默认值） | <integer>

flex-shrink:1（默认值） | <number>

flex-grow:0（默认值） | <number>

flex-basis:auto（默认值） | <length>

flex:none | auto | @flex-grow @flex-shrink @flex-basis

align-self:auto（默认值） | flex-start | flex-end |center | baseline| stretch
```

坐标轴：默认的情况下，水平方向的是主轴（main axis），垂直方向的是交叉轴（cross axis）。项目是在主轴上排列，排满后在交叉轴方向换行。需要注意的是，交叉轴垂直于主轴，它的方向取决于主轴方向。

![axis](/images/tech/flex_axis.png)

# 底层框架

## 双线程模型

微信选择 **Hydrid技术** 来进行渲染。即界面主要由成熟的 Web 技术渲染，辅之以大量的接口提供丰富的客户端原生能力。同时，每个小程序页面都是用不同的WebView去渲染，这样可以提供更好的交互体验，更贴近原生体验，也避免了单个WebView的任务过于繁重。此外，界面渲染这一块我们定义了一套内置组件以统一体验，并且提供一些基础和通用的能力，进一步降低开发者的学习门槛。值得一提的是，内置组件有一部分较复杂组件是用客户端原生渲染的，以提供更好的性能。

web技术存在一些不可控因素和安全风险，例如JS脚本随意跳转网页或改变页面上的任务一内容，一些敏感内容（只能展示，开发者不能直接拿到数据）通过JS直接获取。因此为了解决管控与安全问题，我们必须阻止开发者使用一些浏览器提供的，诸如跳转页面、操作DOM、动态执行脚本的开放性接口，同时显然逐个禁止是不可能的（JS灵活，浏览器接口丰富，需要紧随浏览器内核更新），因此小程序采取的方式是提供一个沙箱环境来运行开发者的JavaScript 代码。这个沙箱环境不能有任何浏览器相关接口，只提供纯JavaScript 的解释执行环境，那么像HTML5中的ServiceWorker、WebWorker特性就符合这样的条件。

得益于客户端系统有JavaScript 的解释引擎（在iOS下是用内置的 JavaScriptCore框架，在安卓则是用腾讯x5内核提供的JsCore环境），我们可以创建一个单独的线程去执行 JavaScript，在这个环境下执行的都是有关小程序业务逻辑的代码，也就是我们前面一直提到的逻辑层。而界面渲染相关的任务全都在WebView线程里执行，通过逻辑层代码去控制渲染哪些界面，那么这一层当然就是所谓的渲染层。这就是小程序双线程模型的由来。

小程序的双线程模型决定了**任何数据传递都是线程间的通信**。

## Skyline渲染引擎

小程序一直以来采用的都是 AppService 和 WebView 的双线程模型，但由于其繁重的历史包袱和复杂的渲染流程，使得 Web 在移动端的表现与原生应用仍有一定差距。为了进一步优化小程序性能，提供更为接近原生的用户体验，我们在 WebView 渲染之外新增了一个渲染引擎 **Skyline**，其使用更精简高效的渲染管线，并带来诸多增强特性，让 Skyline 拥有更接近原生渲染的性能体验。

原生的WebView上执行过多的 JS 逻辑可能阻塞渲染，导致界面卡顿。在 Skyline 环境下，我们尝试改变这一情况：Skyline 创建了一条渲染线程来负责 Layout, Composite 和 Paint 等渲染任务，并在 AppService 中划出一个独立的上下文，来运行之前 WebView 承担的 JS 逻辑、DOM 树创建等逻辑。这种新的架构相比原有的 WebView 架构，有以下特点：

+ 界面更不容易被逻辑阻塞，进一步减少卡顿
+ 无需为每个页面新建一个 JS 引擎实例（WebView），减少了内存、时间开销
+ 框架可以在页面之间共享更多的资源，进一步减少运行时内存、时间开销
+ 框架的代码之间无需再通过 JSBridge 进行数据交换，减少了大量通信时间开销


![skyline](/images/tech/wechat_skyline.png)

### 特性

skyline只保留更现代的 CSS 集合，精简了大量CSS特性。同时添加了大量特性，使开发者能够构建出类原生体验的小程序。

支持与webview混合使用

```json
// page.json
// skyline 渲染
{
    "renderer": "skyline"
}
// webview 渲染
{
    "renderer": "webview"
}

// app.json
{
  "subPackages": [
    {
      "root": "packageA",
      "pages": ["pages/cat"],
      "componentFramework": "glass-easel",
      "renderer": "skyline",
    },
  ],
}
```




## 小程序和客户端的通信原理

# 组件系统

## exparser vs. glass-easel

Exparser是微信小程序当前的组件组织框架，新版本组件框架[glass-easel](https://github.com/wechat-miniprogram/glass-easel)。glass-easel 可以让同样的组件代码运行在 web 、小程序等不同环境下，也就是支持不同的**后端**。在 web 环境下运行时，后端是浏览器的 DOM 接口；在小程序环境下运行时，后端则是小程序环境接口。

glass-easel 完整具备小程序自定义组件相关特性，如组件模板、通信与事件、生命周期等等。此外， glass-easel 还实现了一些实用的新特性，也具有更好的 TypeScript 支持。


## exparser框架

Exparser的组件模型与WebComponents标准中的ShadowDOM高度相似。Exparser会维护整个页面的节点树相关信息，包括节点的属性、事件绑定等，相当于一个**简化版的Shadow DOM**实现。

在使用自定义组件的小程序页面中，Exparser将接管所有的自定义组件注册与实例化。从外部接口上看，小程序基础库提供有Page和Component两个构造器。以Component为例，在小程序启动时，构造器会将开发者设置的properties、data、methods等定义段，写入Exparser的组件注册表中。这个组件在被其它组件引用时，就可以根据这些注册信息来创建自定义组件的实例。Page构造器的大体运行流程与之相仿，只是参数形式不一样。这样每个页面就有一个与之对应的组件，称为“页面根组件”。

在初始化页面时，Exparser会创建出页面根组件的一个实例，用到的其他组件也会响应创建组件实例（这是一个递归的过程）。组件创建的过程大致有以下几个要点：

1. 根据组件注册信息，从组件原型上创建出组件节点的JS对象，即组件的`this`；
2. 将组件注册信息中的data 复制一份，作为组件数据，即`this.data`；
3. 将这份数据结合组件WXML，据此创建出Shadow Tree，由于Shadow Tree中可能引用有其他组件，因而这会递归触发其他组件创建过程；
4. 将ShadowTree拼接到Composed Tree上，并生成一些缓存数据用于优化组件更新性能；
5. 触发组件的`created`生命周期函数；
6. 如果不是页面根组件，需要根据组件节点上的属性定义，来设置组件的属性值；
7. 当组件实例被展示在页面上时，触发组件的`attached`生命周期函数，如果Shadw Tree中有其他组件，也逐个触发它们的生命周期函数。

### 组件间通信

不同组件实例间的通信有WXML属性值传递、事件系统、selectComponent和relations等方式。其中，WXML属性值传递是从父组件向子组件的基本通信方式，而事件系统是从子组件向父组件的基本通信方式。

Exparser的事件系统完全模仿Shadow DOM的事件系统。在通常的理解中，事件可以分为冒泡事件和非冒泡事件，但在ShadowDOM体系中，冒泡事件还可以划分为在Shadow Tree上冒泡的事件和在Composed Tree上冒泡的事件。如果在Shadow Tree上冒泡，则冒泡只会经过这个组件Shadow Tree上的节点，这样可以有效控制事件冒泡经过的范围。

### 原生组件

内置组件中有一些组件较为特殊，它们并不完全在Exparser的渲染体系下，而是由客户端原生参与组件的渲染，这类组件我们称为“原生组件”。例如地图组件：

```xml
<map latitude="39.92" longtitude="116.46"></map>
```

原生组件的渲染：在原生组件内部，其节点树非常简单，基本上可以认为只有一个div元素。在渲染层开始运行时，通常会经历以下几个步聚：

1. 组件被创建，包括组件属性会依次赋值。
2. 组件被插入到DOM树里，浏览器内核会立即计算布局，此时我们可以读取出组件相对页面的位置（x, y坐标）、宽高。
3. 组件通知客户端，客户端在相同的位置上，根据宽高插入一块原生区域，之后客户端就在这块区域渲染界面
4. 当位置或宽高发生变化时，组件会通知客户端做相应的调整

> 原生组件在WebView这一层的渲染任务是很简单，只需要渲染一个占位元素，之后客户端在这块占位元素之上叠了一层原生界面。因此，**原生组件的层级会比所有在WebView层渲染的普通组件要高**。

原生组件的好处：

引入原生组件主要有3个好处：

1. 扩展Web的能力。比如像输入框组件（input, textarea）有更好地控制键盘的能力。
2. 体验更好，同时也减轻WebView的渲染工作。比如像地图组件（map）这类较复杂的组件，其渲染工作不占用WebView线程，而交给更高效的客户端原生处理。
3. 绕过setData、数据通信和重渲染流程，使渲染性能更好。比如像画布组件（canvas）可直接用一套丰富的绘图接口进行绘制。


| 组件名  | 名称           | 是否有 **context** | 描述                               |
|---------|----------------|--------------------|------------------------------------|
| video   | 视频           | 是                 | 播放视频                           |
| map     | 地图           | 是                 | 展示地图                           |
| canvas  | 画布           | 是                 | 提供一个可以自由绘图的区域         |
| picker  | 弹出式选择器    | 否                 | 初始时没有界面，点击时弹出选择器   |

> 交互比较复杂的原生组件都会提供“context”，用于直接操作组件, 例如：以canvas为例，小程序提供了`wx.createCanvasContext`方法来创建canvas的context。

**原生组件的渲染限制**：

原生组件脱离在WebView渲染流程外，这带来了一些限制。最主要的限制是一些CSS样式无法应用于原生组件，例如，不能在父级节点使用overflow:hidden来裁剪原生组件的显示区域；不能使用transformrotate让原生组件产生旋转等。

开发者最为常见的问题是，原生组件会浮于页面其他组件之上（相当于拥有正无穷大的z-index值）使其它组件不能覆盖在原生组件上展示。想要解决这个问题，可以考虑使用`cover-view`和`cover-image`组件。这两个组件也是原生组件，同样是脱离WebView的渲染流程外，而原生组件之间的层级就可以按照一定的规则控制。

# WeUI组件库

微信官方提供的组件库，一套基于样式库weui-wxss开发的小程序扩展组件库，同微信原生视觉体验一致的UI组件库。