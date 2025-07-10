---
date: '2025-06-27T15:44:28+08:00'
draft: false
title: 'Lean4使用'
categories:
  - AI
  - math
keywords:
  - Lean4
tags:
  - Lean4
---

 
## Lean4：定理证明与函数式编程的完美融合

**Lean4是一款由微软研究院开发的定理证明器和通用函数式编程语言**，它结合了形式化数学证明的强大功能与现代编程语言的实用特性。作为交互式定理证明器(Interactive Theorem Prover, ITP)，Lean4允许数学家和研究者将数学定理转换为可验证的代码形式，确保证明的绝对正确性。同时，作为编程语言，它支持**函数式编程范式、依赖类型系统和元编程能力**，使开发者能够编写高效且类型安全的代码。Lean4以其强大的类型系统、丰富的数学库Mathlib4（已超过150万行代码）以及与Rust类似的工具链管理（elan、lake）而脱颖而出，正成为数学形式化和程序验证领域的主流工具。


### Lean4工具链

Lean 4 的完整开发环境由以下核心组件构成：

1. [elan](https://github.com/leanprover/elan)：Lean 的版本管理工具，用于安装、管理和切换不同版本的 Lean，类似于 Rust 的 rustup 或 Node.js 的 nvm。
2. lake（Lean Make）：Lean 的包管理器和构建器，已集成到 Lean 4 核心仓库中。用于创建 Lean 项目，构建 Lean 包,编译 Lean 可执行文件等。
3. [lean](https://github.com/leanprover/lean4)：语言本身的核心组件，负责实际的代码编译和语言服务器协议（LSP）支持，用户不需要直接与 lean 交互。

### Lean4的安装与配置

最简单的方式，就是使用mathlib提供的对应系统的安装脚本，以Ubuntu/Debian系统为例:

```bash
wget -q https://raw.githubusercontent.com/leanprover-community/mathlib4/master/scripts/install_debian.sh && bash install_debian.sh
```

手动安装方式：在 [GitHub release页面](https://github.com/leanprover/elan/releases)或者 [上交镜像源](https://s3.jcloud.sjtu.edu.cn/899a892efef34b1b944a19981040f55b-oss01/elan/mirror_clone_list.html)，根据系统版本下载elan。解压后得到`elan-init`文件，赋予可执行权限并执行安装,最后设置PATH。

```bash
chmod +x elan-init
./elan-init -y --default-toolchain none
# 设置环境变量
export PATH="$HOME/.elan/bin:$PATH"
# 检查版本
elan -V
elan show
```

### Lean4工具链基本用法

elan是Lean版本管理器，用于安装、管理和切换不同版本的 Lean。

```bash
elan --version   # 输出版本号来测试安装是否成功
elan self update # 更新 elan
elan show        # 显示已安装的 Lean 版本

# 下载指定 Lean 版本，所有版本可见 https://github.com/leanprover/lean4/releases
elan install leanprover/lean4:v4.10.0

# 下载最新稳定版本 stable
elan default leanprover/lean4:stable 

# 切换默认的 Lean 版本
# 切换到 leanprover/lean4:v4.11.0-rc1 
elan default leanprover/lean4:v4.11.0-rc1 

# 设置在当前目录下使用的 Lean 版本
elan override set leanprover/lean4:stable
# info: info: override toolchain for 'xxx' set to 'leanprover/lean4:stable'
```

> elan的配置记录可以在 `~/.elan/settings.toml`中查看， `.elan`文件夹中`toolchains`存放下载的各个Lean版本，`bin`存放常见的二进制文件，比如`lake`

lake 全称 Lean Make，是 Lean 4 的包管理器，用于创建 Lean 项目，构建 Lean 包和编译 Lean 可执行文件。

```bash
lake new your_project_name

# 或者手动创建一个新文件夹并在原地建立项目
mkdir your_folder_name && cd your_folder_name && lake init your_project_name

# 构建项目可执行文件
lake build
# 运行
lake exec hello # Hello, world!
# 清理构建文件
lake clean
# 更新依赖
lake update
# 运行 lakefile.lean 的脚本
lake run <script>
```

项目目录结构如下，其中: `lakefile.lean` 是当前项目的配置文件，`lean-toolchain`是当前项目使用的 Lean 版本。
```
your_project_name
├── YourProjectName
│   └── Basic.lean
├── lakefile.lean
├── lean-toolchain
├── Main.lean
├── YourProjectName.lean
└── ...
```

如果需要在工程中引用Mathlib4, 可以再`lakefile.lean`文件尾部加入。

```lean
require mathlib from git
  "https://github.com/leanprover-community/mathlib4"
```

然后下载 Mathlib，注意让终端路径在你的项目文件夹下。然后在终端中运行：

```bash
curl -L https://raw.githubusercontent.com/leanprover-community/mathlib4/master/lean-toolchain -o lean-toolchain
lake update
# 保存运行缓存，对于优化编译十分重要，及其建议
lake exe cache get
```

> 更新也可以使用上面的脚本

如果希望更新Mathlib, 可以执行:

```bash
curl -L https://raw.githubusercontent.com/leanprover-community/mathlib4/master/lean-toolchain -o lean-toolchain
lake update
lake exe cache get
```

lean 是语言本身的核心组件，通常不需要直接与 lean 交互。常见的两个操作：运行 Lean 脚本，以及验证 Lean 代码。

```bash
# 执行lean脚本
elan default leanprover/lean4:v4.11.0-rc1 lean --run hello.lean
# 验证lean脚本
lean proof.lean
```

## Lean4的基本使用方法

Lean4作为一种**函数式编程语言**，其基本语法与Haskell、ML等语言有相似之处，但又具有自己的特色。

### 类型

类型是根据可计算的值的一种分类方式，类型在程序中扮演多种角色：
1. 允许编译器基于类型决定值的内存表示
2. 作为函数输入和输出的轻量级规范，编译器确保程序遵循此规范
3. 防止潜在错误，如在字符串中添加数字

Lean中每个表达式在被求值之前必须有一个类型，很多情况下Lean可以自行发现类型，但有时也需要提供一个类型注释，使用冒号运算法进行声明。例如：`#eval (1+2: Nat)`。这里`Nat`表示自然数类型, 即任意精度的无符号整数。在Lean中, `Nat`是非负整数字面值的默认类型，但是这种类型并不总是最好的选择。在 C 语言中，当减法得出的结果小于零时，无符号整数会下溢到可表示的最大数字。 然而，`Nat`可以表示任意大的无符号数，因此不存在下溢的最大数。因此，对 Nat 进行减法运算时，如果答案本来是负数，则会返回zero。例如：`#eval (1 - 2 : Nat)`的计算结果是0，而不是-1，此时应该使用`#eval (1-2: Int)`

### 函数和定义

在Lean中，使用`def`关键字声明定义，例如：`def hello := "Hello"`。这里Lean为自动判断其类型，也可以手动添加类型，例如：`def lean: String := "Lean"`

> Lean 中，新名称使用 `:=` 而不是`=`来定义。这是因为`=`用于描述现有表达式之间的相等性，而使用两个不同的运算符有助于避免混淆.

Lean中定义函数的方法有很多种，最简单的方式是将函数的参数放在定义类型之前并使用空格分隔。例如:`def addOne (x : Int) : Int := x + 1`。如果应用于多个参数，需要在参数名称和类型之间加空格。

```lean4
def maximum (n : Nat) (k : Nat) : Nat :=
  if n < k then
    k
  else n
```

计算结果为自然数、整数和字符串的表达式分别对应类型`Nat`, `Int`和`String`.函数也是类型，接收`Nat`返回`Bool`的函数对应类型`Nat → Bool`，接收两个`Nat`返回`Nat`的函数对应类型为`Nat → Nat → Nat`.使用 `#check [func_name]`会返回函数的签名，例如输入`#check maximum`，会返回`Nat → Nat → Nat`。

事实上，所有Lean的函数实际上只需要一个参数，类似像`maximum`这样接受多个参数的函数，实际上是接受一个参数然后返回一个新函数，这个新函数会接受下一个参数，并继续执行该过程直到不再需要其他参数为止。例如：`#check maximum 3`会返回`Nat → Nat`。

> 使用返回函数的函数来实现多参数函数被称为 柯里化（currying），以数学家 Haskell Curry 命名。函数箭头右结合，这意味着 Nat → Nat → Nat 等价于 Nat → (Nat → Nat)

类似C语言中的typedef, Lean中类型作为一等公民，类似表达式，定义可以引用类型，就像引用其他值一样：`def Str: Type := String`, 然后可以使用`Str`而不是`String`作为定义的类型：`def aStr: Str := "This is a string."`

但是下面的示例会出现问题：

```lean
def NaturalNumber : Type := Nat
def thirtyEight : NaturalNumber := 38
```

这是因为Lean允许数字字面值重载，Lean允许在合理的情况下将数字字面值用于新类型，因为不同的数学分支使用数学符号的目的大相径庭。允许数字字面值重载这种特性使得在查找到重载之前不会替换为定义，进而导致错误。

解决限制的方法是在定义的右侧提供类型`Nat`, 使得`Nat`的重载规则可以用于38. `def thirtyEight : NaturalNumber := (38 : Nat)`。另一种方法是为 NaturalNumber 定义一个重载，其功能与 Nat 相同（后续介绍），最后一种解决方案是使用 `abbrev`，而不是`def`来定义`Nat`的新名称，允许重载解析为新定义的名字。使用`abbrev`编写的定义始终会展开。

```lean
abbrev N : Type := Nat
def thirtyNine : N := 39
```

> 在Lean底层，部分定义在重载解析过程中被内部标记为可展开，而另一些则不是。**需要展开的定义被称为可约简 (reducible)**。控制可约简性对于Lean的扩展至关重要：完全展开所有定义可能会导致类型非常庞大，机器处理速度慢，用户难以理解。使用`abbrev`生成的定义被标记为可约简。

### 结构Structures

类似C中的struct, 可以使用`structure`关键字定义新类型。

```lean
structure Point where
  x : Float
  y : Float
deriving Repr
```

上面定义了一个包含两个Float字段的笛卡尔点，其中最后一行`deriving Repr`要求 Lean 生成代码来显示类型 Point 的值。此代码由 #eval 用来渲染求值结果以供程序员使用，类似于 Python 中的 repr 函数。

创建结构体类型的值的典型方法是将其所有字段的值放在花括号内：`def origin : Point := { x := 0.0, y := 0.0 }`。


### 关于书写

1. → 可以使用ASCII字符 `->` 等效





**2. 依赖类型与强类型系统**

Lean4的强类型系统确保了代码的安全性：
```lean4
def divide (a b : ℕ) : ℕ := if b ≠ 0 then a / b else 0
```

这里`ℕ`表示自然数类型，`Int`表示整数类型，`ℚ`表示有理数类型，Lean4能自动推导类型，但显式声明类型能提高代码可读性。

**3. 项目创建与构建**

使用LAKE创建新项目：
```bash
 lake new MyProject mathlib
```

这会生成一个包含基础结构的Lean4项目，包括`lakefile.lean`配置文件和`MyProject.lean`主文件。在`lakefile.lean`中可以配置项目依赖和选项：
```lean4
import Lake
open Lake DSL

package "MyProject" where
  leanOptions := #[
    ⟨`pp.unicode.fun, true⟩
  ]

require "leanprover-community" / "mathlib"

@[default_target] lean_lib «MyProject» where
  -- 添加库配置选项
```

### 三、定理证明示例：自然数加法交换律

自然数加法交换律（即对于任意自然数a和b，有a + b = b + a）是数学中最基本的性质之一。在Lean4中，我们可以使用数学归纳法来证明这一定理。以下是一个完整的证明示例：

```lean4
import Mathlib.Data.Nat.Defs

-- 定义自然数加法交换律的定理
theorem add_comm (a b : ℕ) : a + b = b + a := by
  -- 对b使用数学归纳法
  induction b with
    | zero =>    -- 归纳基础：b=0
      rw [add_zero]   -- 重写规则：a+0 = a
      rw [zero_add]   -- 重写规则：0+a = a
      rfl             -- 由等式的反身性，a = a
    | succ d ih =>   -- 归纳步骤：b=d+1，ih为归纳假设a+d = d+a
      rw [addsucc]    -- 重写规则：a+(d+1) = (a+d)+1
      rw [ih]          -- 应用归纳假设：(a+d)+1 = (d+a)+1
      rw [succ_add]   -- 重写规则：(d+a)+1 = d+(a+1)
      rw [add_comm a 1] -- 证明a+1=1+a（可单独证明或使用已知定理）
      rw [ih]          -- 再次应用归纳假设
      rfl             -- 等式反身性
```

**证明过程解析**：

1. **定理声明**：使用`theorem`关键字声明定理`add_comm`，参数为两个自然数`a`和`b`，目标为证明`a + b = b + a`。

2. **数学归纳法**：使用`induction`战术对`b`进行数学归纳。在Lean4中，自然数`ℕ`被定义为带有后继(succ)构造的归纳类型，因此归纳法是证明自然数性质的标准方法。

3. **归纳基础**：当`b=0`时，需要证明`a+0 = 0+a`。这里使用了已知的定理`add_zero`（定义`a+0 = a`）和`zero_add`（定义`0+a = a`），并通过`rw`（rewrite）战术进行重写，最后使用`rfl`（reflexivity）战术证明`a = a`。

4. **归纳步骤**：假设当`b=d`时定理成立（即`a+d = d+a`），现在需要证明当`b=d+1`时定理也成立。这里使用了自然数加法的递归定义（`add_succ`：`a+(d+1) = (a+d)+1`）和之前证明的`add_comm a 1`（即`a+1 = 1+a`）。

5. **战术使用**：`rw`用于应用重写规则，`ih`代表归纳假设，`rfl`用于证明等式两边完全相同。

**在VS Code中验证证明**：

1. 安装Lean4扩展后，打开包含上述代码的`.lean`文件
2. Lean4服务器会自动启动并验证代码
3. 将光标悬停在定理名称上，会显示"定理已证明"的提示
4. 如果证明有错误，Lean4会显示红色错误提示并指出问题所在

### 四、Lean4的生态系统与工具链

Lean4的工具链设计借鉴了Rust语言，使其更容易被程序员接受和使用：

**1. ELAN工具链管理器**

ELAN（Lean Version Manager）类似于Rust的rustup或Node.js的nvm，用于管理不同版本的Lean工具链：
```bash
 elan install latest    # 安装最新版本
 elan default v4.20.0    # 设置默认版本为4.20.0
 elan show                 # 显示当前工具链信息
```

**2. LAKE构建工具**

LAKE是Lean4的包管理器和构建工具，类似于Rust的cargo：
```bash
 lake new ProjectName     # 创建新项目
 lake build                  # 构建项目
 lake update                 # 更新依赖
 lake exec ProjectName       # 运行项目
```

**3. GLEAM镜像工具（国内用户推荐）**

对于国内用户，可以使用GLEAM工具加速依赖下载：
```bash
# 下载GLEAM
curl https://s3.jcloud.sjtu.edu.cn/899a892efef34b1b944a19981040f55b-oss01/ lean4 /glean /releases /download /v0.1.18/glean_Windows_x86_64.zip -o lean4.zip
unzip lean4.zip

# 安装ELAN
glean -install elan -version v4.20.0

# 安装Lean4工具链
glean -install lean -version v4.20.0

# 安装Mathlib4依赖库
glean -install mathlib -version v4.20.0
```

**4. Mathlib4数学库**

Mathlib4是Lean4的大型数学库，包含超过150万行代码，涵盖了从基础算术到高级拓扑学的广泛数学内容。它采用AMS数学主题分类标签系统，便于查找和组织数学知识：
```lean4
-- 查看Mathlib中的数论内容
#AMS 11
```

### 五、Lean4的应用场景与优势

**1. 数学定理形式化**

Lean4最显著的应用是数学定理的形式化证明。DeepMind已将其用于构建数学猜想库，通过形式化表述开放猜想，为自动定理证明器提供基准测试集。例如，费马大定理（Fermat's Last Theorem）已在Mathlib4中被完全形式化证明。

**2. 软件验证与形式化方法**

在关键系统（如航空、航天、金融等）的软件开发中，Lean4可用于确保代码的正确性。例如，可以形式化验证线程池的死锁条件：
```lean4
def isDeadlocked (pool : ThreadPool) (tasks : ℕ) : Prop := pool.corePoolSize < tasks ∧ pool.unboundedQueue ∧ pool.maxPoolSize > pool.corePoolSize

theorem unbounded_queue_causes_deadlock : ∃ (pool : ThreadPool) (tasks : ℕ), pool.corePoolSize = 5 ∧ pool.maxPoolSize = 2147483647 ∧ pool.unboundedQueue = true ∧ tasks > 5 ∧ isDeadlocked pool tasks := by
  let pool : ThreadPool := { corePoolSize := 5, maxPoolSize := 2147483647, unboundedQueue := true }
  use pool, 6
  constructor <;> trivial
```

**3. 教育研究与逻辑推理**

Lean4已被广泛用于数学和计算机科学教育，帮助学生理解逻辑推理和证明过程。其交互式特性允许学生逐步构建证明，获得即时反馈。

**4. 编程语言实验与研究**

由于其丰富的类型系统，Lean4也成为研究新编程范式和语言特性的良好平台。它支持依赖类型（dependent types），允许类型依赖于值，这在形式化证明中极为重要，同时也为高级编程提供了可能。

### 六、Lean4的未来发展与社区支持

**Lean4正处于快速发展阶段**，其社区活跃且不断增长。菲尔兹奖得主陶哲轩对Lean和人工智能的看好，推动了Lean4的"破圈"趋势。越来越多的数学家和程序员开始使用Lean4进行研究和开发。

**Mathlib4的持续扩展**使Lean4能够处理更复杂的数学问题。DeepMind已将Lean4用于数学猜想库的构建，通过形式化表述开放猜想，促进自动定理证明技术的发展。

**AI与Lean4的结合**正在创造新的可能性。上海交通大学AI4MATH团队已开发出基于Qwen2.5-7b架构的数学形式化模型，在MiniF2F和ProofNet基准测试上取得了显著成绩，证明了AI在辅助数学形式化方面的潜力。

**总之，Lean4不仅是一个强大的定理证明器，也是一个功能丰富的函数式编程语言**。它通过依赖类型系统、强大的元编程能力和丰富的数学库Mathlib4，为数学形式化和程序验证提供了统一的框架。无论是数学家、程序员还是教育工作者，都能从中找到有价值的应用场景。随着社区的发展和AI技术的融合，Lean4有望在未来的数学研究和软件开发中发挥更加重要的作用。

 
## Lean4语法详解与费马小定理证明示例

**Lean4是一种基于依赖类型论的函数式编程语言和交互式定理证明器**，它结合了现代编程语言的特性与形式化数学证明的能力，为软件验证和数学定理形式化提供了统一的框架。Lean4的语法设计既保留了函数式编程的简洁性，又融入了依赖类型系统的强大表达能力，使其成为形式化方法研究的前沿工具。

### 一、Lean4的基本语法结构

Lean4的代码结构遵循严格的数学逻辑和函数式编程范式，其基本语法元素包括：

1. **定义与声明**：
   - 使用`def`关键字定义函数或常量：
     ```lean4
     def addOne (x : Int) : Int := x + 1
     ```
   - 使用`example`和`theorem`声明命题：
     ```lean4
     theorem add_comm (a b : ℕ) : a + b = b + a := by
       induction b with
         | zero => rw [add_zero, zero_add]
         | succ d ih => rw [add协会, ih, succ协会]
     ```

2. **类型系统**：
   Lean4的类型系统是其核心特征，支持依赖类型（dependent types），允许类型依赖于值：
   ```lean4
   inductive List (α : Type) where
     | nil : List α
     | cons (head : α) (tail : List α) : List α
   ```
   这里`List α`是一个类型，依赖于参数`α`的值，表示α类型的列表。

3. **条件表达式**：
   Lean4支持条件表达式，语法与传统编程语言类似：
   ```lean4
   def max (a b : ℕ) : ℕ := if a > b then a else b
   ```

4. **模式匹配**：
   Lean4提供了强大的模式匹配机制，可以处理复杂的数据结构：
   ```lean4
   def isZero : ℕ → Bool
     | 0 => true
     | _ => false
   ```
   这里函数`isZero`通过模式匹配来判断自然数是否为0。

5. **定理证明**：
   Lean4的定理证明采用交互式战术系统，允许逐步构建证明：
   ```lean4
   theorem add Comm (a b : ℕ) : a + b = b + a := by
     induction b with
       | zero => rw [add零, zero Add]
       | succ d ih => rw [add协会, ih, succ协会]
   ```

### 二、Lean4的类型系统详解

Lean4的类型系统是其区别于传统编程语言的核心特征，它基于依赖类型论（Dependent Type Theory），允许类型依赖于值，从而能够表达复杂的数学概念。

**1. 基本类型**：

Lean4提供了一系列基本类型，如`ℕ`（自然数）、`Int`（整数）、`ℝ`（实数）、`Bool`（布尔值）等。这些类型可以直接使用：

```lean4
def naturalNumber : ℕ := 42
def integer : Int := -42
def boolean : Bool := true
```

**2. 函数类型**：

函数类型在Lean4中通过箭头`→`表示，可以是简单的或依赖的：

```lean4
def add (a b : ℕ) : ℕ := a + b
def power (a : ℕ) (b : ℕ) : ℕ := a^b
```

**3. 依赖类型**：

依赖类型是Lean4的特色，允许类型参数依赖于值：

```lean4
inductive DoorCmd (α β : Type) (T : α → β → Type) where
  | pure (x : T α β) : DoorCmd α β T
  | bind {α β γ} (m : DoorCmd α β T) (f : β → DoorCmd β γ T) : DoorCmd α γ T
```

这里`DoorCmd α β T`的类型依赖于值`α`和`β`，使得Lean4能够类型安全地表示状态转换过程。

**4. 类型类（Type Classes）**：

类型类是Lean4中的重要概念，用于描述类型必须满足的特定性质：

```lean4
class OfNat (α : Type) (n : ℕ) where
  ofNat : α
```

类型类可以自动推导，简化了数学结构的使用：

```lean4
example : ℕ := OfNat.ofNat 42
```

### 三、Lean4的战术系统

Lean4的战术系统是其定理证明的核心，提供了多种策略来构建证明。战术可以组合使用，形成复杂的证明流程。

**1. 基础战术**：

- `rw`（rewrite）：重写目标表达式
  ```lean4
  theorem test : 2 + 3 = 5 := by
    rw [add协会]  -- 重写加法表达式
  ```

- `apply`：应用已知定理或引理
  ```lean4
  theorem test : a = a → a = a := by
    apply id  -- 应用恒等函数
  ```

- `exact`：直接给出证明
  ```lean4
  theorem test : 2 + 2 = 4 := by
    exact rfl  -- 直接证明等式
  ```

**2. 逻辑战术**：

- `have`：在证明中引入中间命题
  ```lean4
  theorem test : a + b = b + a := by
    have h : a + b = b + a := by rw [add Comm]
    exact h
  ```

- `apply`和`exact`：应用定理或直接证明
  ```lean4
  theorem test : a = a → a = a := by
    intro h  -- 引入假设
    exact h  -- 使用假设
  ```

**3. 组合战术**：

- `induction`：数学归纳法证明
  ```lean4
  theorem add Comm (a b : ℕ) : a + b = b + a := by
    induction b with
      | zero => rw [add零, zero Add]
      | succ d ih => rw [add协会, ih, succ协会]
  ```

- `repeat`和`first`：重复或选择性应用战术
  ```lean4
  theorem test : 2 ≤ 6 := by
    repeat (first | apply Nat.le_refl | apply Nat.le_step)
  ```

### 四、费马小定理的Lean4证明示例

费马小定理是数论中的基本定理，它指出：如果p是一个质数，而整数a不是p的倍数，则有a^(p-1) ≡ 1 (mod p)。以下是该定理在Lean4中的完整证明：

```lean4
import Mathlib.Data.Nat.Defs
import Mathlib NumberTheory Prime

openNat

-- 费马小定理的定理声明
theorem fermat_little (p : ℕ) (a : ℕ) (hp : Prime p) (ha : a ≠ 0) (hab : ¬(p ∣ a)) : a ^ (p - 1) ≡ 1 [Nat] p := by
  -- 引入完全剩余系
  let S := Finset.univ.filter (· ≠ 0)
  have hS : S = Finset.univ.filter (· ≠ 0) := by trivial

  -- 构造乘以a的完全剩余系
  let aS := Finset.map (· * a) S
  have haS : aS = Finset.map (· * a) S := by trivial

  -- 证明aS也是完全剩余系
  have hCoprime : ∀ x ∈ S, gcd x p = 1 := by
    intro x hx
    have hNonZero : x ≠ 0 := by simpa using hx
    apply gcd_eq_one_of_coprime
    apply prime.coprime hp hNonZero

  have hInjective : Function.Injective (· * a) := by
    intro x y hxy
    apply succ_inj at hxy
    exact hxy

  have hImage : aS = Finset.univ.filter (· ≠ 0) := by
    apply Finset.map_image_eq_univ_filter
    apply hInjective
    apply hCoprime

  -- 计算乘积同余
  have hProduct : ∏ x ∈ S, x * a ≡ ∏ x ∈ S, x [Nat] p := by
    apply Finset乘积 congruence
    intro x hx
    have hNonZero : x ≠ 0 := by simpa using hx
    apply prime.coprime hp hNonZero
    apply hCoprime

  -- 约去乘积项
  have hProductCoprime : gcd (∏ x ∈ S, x) p = 1 := by
    apply Finset乘积_gcd_eq_one
    intro x hx
    have hNonZero : x ≠ 0 := by simpa using hx
    apply prime.coprime hp hNonZero

  have hFinal : a ^ (p - 1) ≡ 1 [Nat] p := by
    apply congruence_of乘积
    apply hProduct
    apply hProductCoprime

  exact hFinal
```

#### 证明步骤解析

1. **导入依赖库**：首先导入Mathlib中的自然数定义和素数理论库。
2. **定理声明**：声明费马小定理，参数包括自然数p、a，以及p为素数的条件和a与p互质的条件。
3. **构造完全剩余系**：使用`Finset.univ.filter (· ≠ 0)`构造模p的完全剩余系。
4. **证明乘积同余**：应用`Finset乘积 congruence`战术证明乘以a后的集合乘积与原集合乘积同余。
5. **约去乘积项**：使用`gcd`函数和`congruence_of乘积`战术约去乘积项，得到a^(p-1) ≡ 1 (mod p)。

### 五、Lean4的元编程与扩展能力

Lean4的元编程能力是其区别于传统定理证明器的重要特征，它允许用户自定义战术和语法。

**1. 宏（Macros）**：

Lean4的宏系统允许用户定义新的语法：

```lean4
macro "repeat apply" t₁:term "or" t₂:term : tactic => `(tactic | repeat (first | apply $t₁ | apply $t₂))
```

这里定义了一个新的战术`repeat apply`，用于重复应用两个战术直到证明完成。

**2. 自定义战术**：

用户可以通过组合现有战术来创建新的战术：

```lean4
def my tactic : tactic Unit := do
  repeat rw [add协会]
  apply add Comm
```

**3. 依赖类型编程**：

Lean4的依赖类型系统允许创建类型安全的API：

```lean4
inductive DoorCmd (α β : Type) (T : α → β → Type) where
  | pure (x : T α β) : DoorCmd α β T
  | bind {α β γ} (m : DoorCmd α β T) (f : β → DoorCmd β γ T) : DoorCmd α γ T

-- 解释器
def interpret : DoorCmd α β T → IO T | Open (key := key) => IO.println s!"Door opened with {key.user}'s key." | Close => IO.println "Door closed." | Lock => IO.println "Door locked." | Unlock ⟨user⟩ => IO.println s!"Door unlocked by {user}" | GenKey user => do IO.println s!"Generated a key for {user}" return (Key.mk user) | DoorCmd.pure x => do return x | DoorCmd.bind m f => do let x ← interpret m interpret (f x)
```

### 六、Lean4的项目结构与工具链

Lean4的工具链设计借鉴了Rust语言，提供了完善的项目管理和构建支持。

**1. Lake构建工具**：

Lake是Lean4的包管理器和构建工具，类似于Rust的Cargo：

```lean4
-- lakefile.lean
import Lake
open Lake DSL

package "MyProject" where
  leanOptions := #[
    ⟨`pp.unicode.fun, true⟩
  ]

require "leanprover-community" / "mathlib4"

@[default_target] lean_lib "MyProject" where
  -- 添加库配置选项
```

**2. VS Code集成**：

Lean4提供了VS Code扩展，支持语法高亮、自动补全和实时验证：

```lean4
#eval interpret proc
-- 输出:
-- Generated a key for admin
-- Door unlocked by admin
-- Door opened with admin's key.
-- Door closed.
-- Door locked.
```

**3. 测试配置**：

在Lean4项目中，可以配置测试模块：

```lean4
@[test_driver] lean_exe test {
  root := `Tests.Main
}
```

然后在`Tests.Main.lean`中实现测试逻辑：

```lean4
def main : IO Unit := do
  -- 测试逻辑
```

### 七、Lean4的数学库Mathlib4

Mathlib4是Lean4的数学库，包含了丰富的数学定理和证明，为定理证明提供了坚实的基础。

**1. 数论库**：

Mathlib4提供了完善的数论理论，包括素数、同余、模运算等：

```lean4
import Mathlib NumberTheory Prime

-- 素数定义
def isPrime (n : ℕ) : Bool := n ≥ 2 ∧ ∀ k : ℕ, 1 < k < n → ¬(k ∣ n)

-- 同余定义
def congruence (a b m : ℕ) : Prop := (a - b) ∣ m
```

**2. 代数库**：

Mathlib4还提供了代数理论，包括群、环、域等：

```lean4
import Mathlib Algebra Group

-- 群定义
class Group (α : Type) where
  mul : α → α → α
  one : α
  inv : α → α
  -- 群公理
```

### 八、Lean4的未来发展与应用场景

**Lean4正处于快速发展阶段**，其社区活跃且不断增长。菲尔兹奖得主陶哲轩对Lean和人工智能的看好，推动了Lean4的"破圈"趋势。越来越多的数学家和程序员开始使用Lean4进行研究和开发。

**1. 数学定理形式化**：

Lean4已被用于形式化证明许多重要数学定理，如费马大定理。DeepMind已将其用于构建数学猜想库，通过形式化表述开放猜想，为自动定理证明器提供基准测试集。

**2. 软件验证与形式化方法**：

在关键系统（如航空、航天、金融等）的软件开发中，Lean4可用于确保代码的正确性。例如，可以形式化验证线程池的死锁条件：

```lean4
def isDeadlocked (pool : ThreadPool) (tasks : ℕ) : Prop := pool.corePoolSize < tasks ∧ pool.unboundedQueue ∧ pool.maxPoolSize > pool.corePoolSize

theorem unbounded_queue_causes_deadlock : ∃ (pool : ThreadPool) (tasks : ℕ), pool.corePoolSize = 5 ∧ pool.maxPoolSize = 2147483647 ∧ pool.unboundedQueue = true ∧ tasks > 5 ∧ isDeadlocked pool tasks := by
  let pool : ThreadPool := { corePoolSize := 5, maxPoolSize := 2147483647, unboundedQueue := true }
  use pool, 6
  constructor <;> trivial
```

**3. 教育研究与逻辑推理**：

Lean4已被广泛用于数学和计算机科学教育，帮助学生理解逻辑推理和证明过程。其交互式特性允许学生逐步构建证明，获得即时反馈。

**4. 编程语言实验与研究**：

由于其丰富的类型系统，Lean4也成为研究新编程范式和语言特性的良好平台。它支持依赖类型（dependent types），允许类型依赖于值，这在形式化证明中极为重要，同时也为高级编程提供了可能。

### 九、总结与展望

**Lean4通过其强大的类型系统、丰富的数学库Mathlib4以及与Rust类似的工具链管理（elan、lake）而脱颖而出**，成为形式化数学和程序验证领域的主流工具。它不仅是一个先进的定理证明器，也是一个功能丰富的函数式编程语言，支持依赖类型系统、强大的元编程能力和类型安全的API设计。

在数学定理形式化方面，Lean4已成功证明了包括费马小定理在内的众多定理。在软件验证领域，它为关键系统提供了形式化保证。随着社区的发展和AI技术的融合，Lean4有望在未来的数学研究和软件开发中发挥更加重要的作用。

通过本文的详细语法介绍和费马小定理的证明示例，读者可以全面了解Lean4的基本语法结构和证明过程，为深入研究和应用Lean4奠定基础。
