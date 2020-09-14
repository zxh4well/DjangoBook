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

