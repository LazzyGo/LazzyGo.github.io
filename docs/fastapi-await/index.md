# Fastapi用和不用await的区别

### 测试代码

用100个并发请求分别测试下面4个接口：
```python
from fastapi import APIRouter
import time
import asyncio

router = APIRouter()


@router.get("/a")
async def a():
    time.sleep(1)
    return {"message": "异步模式，但是同步执行sleep函数，执行过程是串行的"}


@router.get("/b")
async def b():
    loop = asyncio.get_event_loop()
    await loop.run_in_executor(None, time.sleep, 1)
    return {"message": "线程池中运行sleep函数"}


@router.get("/c")
async def c():
    await asyncio.sleep(1)
    return {"message": "异步模式，且异步执行sleep函数"}


@router.get("/d")
def d():
    time.sleep(1)
    return {"message": "同步模式，但是FastAPI会放在线程池中运行，所以很快"}
```

### 运行结果
 - a接口：100秒
 - b接口：1秒
 - c接口：1秒
 - d接口：3秒

### 结论

{{< admonition type=tip title="a接口" >}}
fastapi框架会将async函数会放到event loop中运行。

虽然使用了async，但是函数内部并没有用到await，所以堵塞了。

执行过程是串行的，所以总耗时100秒。
{{< /admonition >}}

{{< admonition type=success title="b接口" >}}
利用asyncio异步IO获取当前的event loop。
然后将time.sleep(1)放到一个event loop中去运行，函数内部用到了await，所以无堵塞。

执行过程是并行的，所以总耗时1秒。
{{< /admonition >}}



{{< admonition type=abstract title="c接口" >}}
使用异步IO的sleep取代了普通的同步sleep。
原理与b接口一致。

执行过程是并行的，所以总耗时1秒。
{{< /admonition >}}




{{< admonition type=tip title="d接口" >}}
这个函数没有async修饰，即一个普通函数。
但是FastAPI会将函数放到thread pool中执行。

服务器是8核CPU，线程池的默认配置是核心数*5=40。

服务器在第一秒和第二秒分别处理40个请求，第三秒处理20个请求。
所以100个并发总耗时3秒。
{{< /admonition >}}

{{< admonition type=quote title="总结" >}}
这个函数没有async修饰，即一个普通函数。
官方说，无论你是否使用async，FastAPI都会采用异步的方式处理。

但是，如果你定义了async函数，函数体却是同步的调用（例：a接口），将导致函数执行过程变成串行。
{{< /admonition >}}

> 原文：https://blog.csdn.net/qq_29518275/article/details/109360617

