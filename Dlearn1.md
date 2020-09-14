## Django的工作模式



### Django的任务处理流程

<img src="https://i.loli.net/2020/09/14/a3ctj9SKEfNTi2F.png" alt="image-20200914160544748" style="zoom: 49%;" />

<img src="https://i.loli.net/2020/09/14/SVAIkZFpCXcEw5l.png" alt="image-20200914160923018" style="zoom: 50%;" />

### Django创建应用流程

1、创建django项目目录

```
django-admin startmyproject [projectName]
```

- 文件目录

```
django-admin startmyproject myproject
```

```
|─myproject
    │  manage.py
    │
    └─myproject
            asgi.py	
            settings.py	//配置文件
            urls.py	//路由入口
            wsgi.py	
            __init__.py

```

- 添加请求处理

```
1、urls.py添加路由
2、添加对应处理方法
3、启动Django本地Web服务：python manage.py runserver [自定义端口]
```

- 注意：

  ①、首页编写路径时，应该保存Routes为空：

```python
urlpatterns = [
    path('',home,name='home'),
    path('admin/', admin.site.urls),
]
```

​	②、HttpResponse类的使用

```python
# 导入模块，用于给客户端返回请求的对象
from django.http import HttpResponse
```



2、创建django应用App

```
python manage.py startapp [appName]
```

- 文件目录

```
└─myproject
    │  manage.py
    │
    ├─myapp	//new
    │  │  admin.py
    │  │  apps.py
    │  │  models.py
    │  │  tests.py
    │  │  views.py
    │  │  __init__.py
    │  │
    │  └─migrations
    │          __init__.py
    │
    └─myproject
        │  asgi.py
        │  settings.py
        │  urls.py
        │  wsgi.py
        │  __init__.py
        │
        └─__pycache__	//new
                settings.cpython-38.pyc
                __init__.cpython-38.pyc
```

### HelloWorld案例实现

1、修改setting.py文件：`cd myproject/myproject`	`vim setting.py`

```
# 拉到文件末尾修改语言和时间区
LANGUAGE_CODE = 'zh-Hans'	#语言

TIME_ZONE = 'Asia/Shanghai'	#时区

USE_I18N = True

USE_L10N = True

USE_TZ = False	#数据库时间本地化
```

2、编写urls路径：`myproject\myproject\urls.py`

```python
from django.contrib import admin
from django.urls import path
from myapp.views import home	# 导入视图模块

urlpatterns = [
    path('', home,name='home'),	# 路径添加
    path('admin/', admin.site.urls),
]

```

- 模块的位置在`应用（myapp）.文件名（views）`中，模块名称自定义为home

3、编写views视图：`myproject\myapp\views.py`

```python
# Create your views here.
from django.http import HttpResponse # 导入HttpResponse模块

def home(request):	# 编写home模块
    return HttpResponse('hello world')
```

4、运行模块：`python manage.py runserver`

```
// 运行成功，服务器启动成功
C:\Users\Antax\Desktop\TEST\myproject>python manage.py runserver
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

Django version 3.1.1, using settings 'myproject.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.
[14/Sep/2020 17:32:09] "GET / HTTP/1.1" 200 11
```

- 文件目录：

```
└─myproject
    │  db.sqlite3 //new
    │  manage.py
    │
    ├─myapp
    │  │  admin.py
    │  │  apps.py
    │  │  models.py
    │  │  tests.py
    │  │  views.py
    │  │  __init__.py
    │  │
    │  ├─migrations
    │  │      __init__.py
    │  │
    │  └─__pycache__
    │          views.cpython-38.pyc
    │          __init__.cpython-38.pyc
    │
    └─myproject
        │  asgi.py
        │  settings.py
        │  urls.py
        │  wsgi.py
        │  __init__.py
        │
        └─__pycache__
                settings.cpython-38.pyc
                urls.cpython-38.pyc
                wsgi.cpython-38.pyc
                __init__.cpython-38.pyc
```

