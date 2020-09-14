## 登录界面案例

HTML（文本标记语言）在被传递给浏览器的时候是以纯文本的形式传递，本身也是以纯文本的形式存储。HTML文件被传递到了浏览器之后，浏览器会自动根据html的规则对其进行渲染，从而实现复杂的页面效果。浏览器如何对HTML文本进行渲染是由浏览器厂商和W3C组织进行规范的，CSS是用于对HTML页面进行修饰的，本质上也是一种文本文件，可以嵌套在HTML文件中传输到浏览器进行渲染，也可以作为单独的文本对指定html页面进行修饰。

### HTML登录页面1.0

```python
# home函数内部情况 views.py
def home(request):
    html = '''
<html>
  <head>
    <title>xxx系统登录页面 | 登录</title>
  </head>
  <body>
    <form action="">
      <h1>xxx系统</h1>
      <input type="text" />
      <button>登录</button>
      <!-- 或<input type="submit" value="登录"> -->
    </form>
  </body>
</html>
...
...

    '''
    return HttpResponse(html)
```

```html
<!-- html页面 -->
<html>
  <head>
    <title>xxx系统登录页面 | 登录</title>
  </head>
  <body>
    <form action="">
      <h1>xxx系统</h1>
      <input type="text" />
      <button>登录</button>
      <!-- 或<input type="submit" value="登录"> -->
    </form>
  </body>
</html>
```

```css
<style>
      * {
        margin: 0;
        padding: 0;
      }
      body {
        background: #efefed;
        display: flex;
        justify-content: center;
        align-items: center;
      }
      .login-form {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-bottom: 6em;
      }
      input[type="text"] {
        width: 20em;
        margin-top: 1em;
        height: 2em;
      }
      button {
        margin-top: 0.5em;
        width: 20em;
        padding: 0.5em 0;
        border-radius: 4px;
        border: 1px solid #ccc;
        background: #009688;
        color: #fff;
      }
    </style>
```

在1.0版本中我们直接返回html文本，这样做的优点是简单，缺点就是难以维护，有没有办法将html代码抽离出来呢？

### HTML登录页面2.0

```python
# myapp/views.py
# 导入库
import os

from django.shortcuts import render

# Create your views here.
from django.http import HttpResponse

# 导入settings
from django.conf import settings

def home(request):
    # 路径拼接
    path = os.path.join(settings.BASE_DIR,'static','index.html')# 添加static/index.html文件
    # 读取文本
    with open(path, 'r',encoding='utf-8') as f:
        html = f.read()
    return HttpResponse(html)
```

```html
<!-- 前端代码 -->
<html>
  <head>
    <title>xxx系统登录页面 | 登录</title>
  </head>
  <body>
    <form action="" class="login-form">
      <h1>xxx系统</h1>
      <input type="text" />
      <button>登录</button>
      <!-- 或<input type="submit" value="登录"> -->
    </form>
    <style>
      * {
        margin: 0;
        padding: 0;
      }
      body {
        background: #efefed;
        display: flex;
        justify-content: center;
        align-items: center;
      }
      .login-form {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-bottom: 6em;
      }
      input[type="text"] {
        width: 20em;
        margin-top: 1em;
        height: 2em;
      }
      button {
        margin-top: 0.5em;
        width: 20em;
        padding: 0.5em 0;
        border-radius: 4px;
        border: 1px solid #ccc;
        background: #009688;
        color: #fff;
      }
    </style>
  </body>
</html>
```

### 配置STATICFILES_DIR

```
/myproject/settings.py
STATICFILES_DIR = [
	os.path.join(BASE_DIR,'static')
]

//static文件夹为自己建立，可以自由选择路径存放和起其他名字
```



## 前后端分离

<img src="https://i.loli.net/2020/09/14/EV61unqNy2OTIbt.png" alt="image-20200914193507837" style="zoom:67%;" />