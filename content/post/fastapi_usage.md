---
date: '2025-06-13T11:14:12+08:00'
draft: false
title: 'FastAPI框架使用'
categories:
  - tech
keywords:
  - Python
  - FastAPI
tags:
  - Python
  - FastAPI
---

# 基础

## 框架介绍

`FastAPI`，一个用于构建 API 的现代、快速（高性能）的web框架。建立在`Starlette`和`Pydantic`基础上的，`Pydantic`是一个基于Python类型提示来定义数据验证、序列化和文档的库。`Starlette`是一种轻量级的ASGI框架/工具包，是构建高性能Asyncio服务的理性选择。

## Hello, FastAPI

安装项目依赖：`pip install fastapi uvicorn`

项目代码：

```python
from fastapi import FastAPI

# 实例是创建你所有API的交互对象
app = FastAPI()


@app.get("/")
async def root():
    return {"message": "Hello World"}
```

然后可以通过以下命令运行服务器: `uvicorn main:app --reload`, 就可以通过 `http://127.0.0.1:8000`进行服务访问。此外还可以通过 `http://127.0.0.1:8000/docs`查看fastapi自动创建的交互式API文档。


# FastAPI基础

## 路径操作装饰器

fastapi支持各种请求方式

```python
@app.get()
@app.post()
@app.put()
@app.patch()
@app.delete()
@app.options()
@app.head()
@app.trace()
```


路径装饰器参数：

```python
@app.post(
    "/items/{item_id}",
    response_model=Item,
    status_code=status.HTTP_200_OK,
    tags=["AAA"],
    summary="this is summary",
    description="this is description",
    response_description= "this is response_description",
    deprecated=False,
)
async def create_item(item_id: int):
   pass

# 路径函数中声明不属于路径参数的其他函数参数时，它们将被自动解释为"查询字符串"参数
# 即就是 url? 之后用&分割的 key-value 键值对。
@app.get("/jobs/{kd}")
async def search_jobs(kd: str, city: Optional[str] = None, xl: Optional[str] = None):  # 有默认值即可选，否则必选
    if city or xl:
        return {"kd": kd, "city": city, "xl": xl}
    return {"kd": kd}
```


## 请求体数据

FastAPI 基于 Pydantic ，Pydantic 主要用来做类型强制检查（校验数据）。不符合类型要求就会抛出异常。

```python
class Addr(BaseModel):
    province: str
    city: str


class User(BaseModel):
    name = 'root'
    age: int = Field(default=0, lt=100, gt=0)
    birth: Optional[date] = None
    friends: List[int] = []
    description: Union[str, None] = None

    # addr: Union[Addr, None] = None  # 类型嵌套

    @validator('name')
    def name_must_alpha(cls, v):
        assert v.isalpha(), 'name must be alpha'
        return v


class Data(BaseModel):  # 类型嵌套
    users: List[User]


app = FastAPI()


@app.post("/data/")
async def create_data(data: Data):
    # 添加数据库
    return data
```

和声明查询参数时一样，当一个模型属性具有默认值时，它不是必需的。否则它是一个必需属性。将默认值设为 None 可使其成为可选属性。FastAPI 会自动将定义的模型类转化为JSON Schema，Schema 成为 OpenAPI 生成模式的一部分，并显示在 API 交互文档中，查看 API 交互文档如下，该接口将接收`application/json`类型的参数。

>FastAPI 支持同时定义 Path 参数、Query 参数和请求体参数，FastAPI 将会正确识别并取数据。
> 1. 参数在 url 中也声明了，它将被解释为 path 参数
> 2. 参数是单一类型（例如int、float、str、bool等），它将被解释为 query 参数
> 3. 参数类型为继承 Pydantic 模块的BaseModel类的数据模型类，则它将被解释为请求体参数

## form表单数据

FastAPI 可以使用Form组件来接收表单数据。

```python
@app.post("/regin")
def regin(username: str = Form(..., max_length=16, min_length=8, regex='[a-zA-Z]'),
          password: str = Form(..., max_length=16, min_length=8, regex='[0-9]')):
    print(f"username:{username},password:{password}")
    return {"username": username}
```

## 文件上传

```python
# file: bytes = File()：适合小文件上传
@app.post("/files/")
async def create_file(file: bytes = File()):
    print("file:", file)
    return {"file_size": len(file)}


@app.post("/multiFiles/")
async def create_files(files: List[bytes] = File()):
    return {"file_sizes": [len(file) for file in files]}


# file: UploadFile：适合大文件上传

@app.post("/uploadFile/")
async def create_upload_file(file: UploadFile):
    with open(f"{file.filename}", 'wb') as f:
        for chunk in iter(lambda: file.file.read(1024), b''):
            f.write(chunk)

    return {"filename": file.filename}


@app.post("/multiUploadFiles/")
async def create_upload_files(files: List[UploadFile]):
    return {"filenames": [file.filename for file in files]}
```

## Request对象

有些情况下我们希望能直接访问Request对象。例如我们在路径操作函数中想获取客户端的IP地址，需要在函数中声明Request类型的参数，FastAPI 就会自动传递 Request 对象给这个参数，我们就可以获取到 Request 对象及其属性信息，例如 header、url、cookie、session 等。


```python
from fastapi import Request


@app.post("/request/")
async def read_request(request: Request):
    print(request.headers)
    print(request.cookies)
    print(request.client.host)
    return {"client_host": request.client.host}
```

## 静态文件

```python
from fastapi.staticfiles import StaticFiles

app = FastAPI()
app.mount("/static",StaticFiles(directory="static"))
```

## 响应模型相关操作

1. response_model

FastAPI 提供了 response_model 参数，声明 return 响应体的模型。

```python
@app.post("/items/", response_model=Item)
async def create_item(item: Item):
    ...
```

FastAPI将使用`response_model`进行以下操作：（1）将输出数据转换为response_model中声明的数据类型。（2）验证数据结构和类型，将输出数据限制为该model定义的格式（3）添加到OpenAPI中，在自动文档系统中使用。


```python
class UserIn(BaseModel):
    username: str
    password: str
    email: EmailStr
    full_name: Union[str, None] = None


class UserOut(BaseModel):
    username: str
    email: EmailStr
    full_name: Union[str, None] = None


@app.post("/user/", response_model=UserOut)
async def create_user(user: UserIn):
    return user
```

# Tortoise ORM操作

Tortoise ORM 是受 Django 启发的易于使用的异步ORM.