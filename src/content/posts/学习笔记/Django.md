---
title: django初学笔记
published: 2024-05-19
tags: [python, django, 学习笔记]
category: 学习笔记
draft: false
---

- [创建项目](#创建项目)
  - [初始目录](#初始目录)
  - [setting.py文件](#settingpy文件)
  - [启动项目](#启动项目)
  - [创建App应用](#创建app应用)
- [基本视图函数](#基本视图函数)
- [数据迁移](#数据迁移)
- [路由](#路由)
  - [子路由](#子路由)
  - [路由传参](#路由传参)
- [模型](#模型)
  - [定义模型](#定义模型)
  - [使用模型](#使用模型)
- [后台管理系统](#后台管理系统)
- [媒体文件](#媒体文件)
  - [单文件上传](#单文件上传)
  - [保存文件到后端](#保存文件到后端)
  - [多文件上传](#多文件上传)



# 创建项目

![QQ截图20240518145035](https://123321xpc-images.oss-cn-hangzhou.aliyuncs.com/imgs/md-images/django.assets/QQ%E6%88%AA%E5%9B%BE20240518145035.png)



## 初始目录

![QQ截图20240518144810](https://123321xpc-images.oss-cn-hangzhou.aliyuncs.com/imgs/md-images/django.assets/QQ%E6%88%AA%E5%9B%BE20240518144810.png)



## setting.py文件

```python
from pathlib import Path

# 项目根目录
BASE_DIR = Path(__file__).resolve().parent.parent

# 项目密钥
SECRET_KEY = 'django-insecure-e3zz2&zc)uzt60(@glg5au$g1@yqfk9=70ud^gnw+#ua4=a7^_'

# 是否调试模式
DEBUG = True

# 被允许的主机/域名
ALLOWED_HOSTS = ['*']


# 定义应用
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'mytest.apps.MytestConfig',
]


# 定义中间件
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

# 根路由路径
ROOT_URLCONF = 'djangoProject.urls'


# 模板配置
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates']
        ,
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]


WSGI_APPLICATION = 'djangoProject.wsgi.application'


DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# 密码验证
AUTH_PASSWORD_VALIDATORS = [
    {
        'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator',
    },
    {
        'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator',
    },
]

# 国际化
LANGUAGE_CODE = 'en-us'
TIME_ZONE = 'UTC'
USE_I18N = True
USE_TZ = True

# 静态文件配置(CSS, JavaScript, Images)
STATIC_URL = 'static/'

# Default primary key field type
# https://docs.djangoproject.com/en/5.0/ref/settings/#default-auto-field

# 默认主键类型
DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

```



## 启动项目

```
python .\manage.py runserver
```



## 创建App应用

```
python .\manage.py startapp App
```

![QQ截图20240518151540](https://123321xpc-images.oss-cn-hangzhou.aliyuncs.com/imgs/md-images/django.assets/QQ%E6%88%AA%E5%9B%BE20240518151540.png)



# 基本视图函数

- 在`mytest`包下的`views.py`中：

```python
# 视图函数
def index(request):
    pass
    return HttpResponse("hello world")
```



# 数据迁移

```
python .\manage.py makemigrations
```



```
python .\manage.py migrate
```



# 路由

- 之后在项目包的`urls.py`中：

```python
from django.urls import path
from mytest import views

urlpatterns = [
            # url     路由函数       名字    
    path('index/', views.index, name='index'),
]
```



## 子路由

- 在`mytest`包新建视图函数
- 之后新建文件`mytest_urls.py`，在里面定义子路由，如下：

```python
from django.urls import path
from mytest.views import index2

urlpatterns = [
    # 子路由路径   视图函数名   别名
    path('index2/', index2, name='index2')
]
```



## 路由传参

- 在设置路由路径时：

```
path('index3/<int:id>/', index3, name='index3')
```

- 在对应视图函数中接收参数（注意，参数名必须和路径中的一致）：

```python
def index3(request, id):
    # 查询数据库获取数据
    print(id)
    test = testModel.objects.all()
    return HttpResponse(test)
```

> 注：可传递多个参数



# 模型

## 定义模型

- 在`mytest/models`中：

```python
class testModel(models.Model):
    name = models.CharField(max_length=30, unique=True)
    age = models.IntegerField(default=18)
```

- 注意：创建模型后要迁移数据，迁移完后，数据库会多出一张表，如下图：

![QQ截图20240518155410](https://123321xpc-images.oss-cn-hangzhou.aliyuncs.com/imgs/md-images/django.assets/QQ%E6%88%AA%E5%9B%BE20240518155410.png)



## 使用模型

```python
def index3(request):
    # 查询数据库获取数据
    test = testModel.objects.all()
    return HttpResponse(test)
```



# 后台管理系统

- 创建超级管理员账号密码

```
python manage.py createsuperuser
```

- 在`mytest/admin`下注册模型

![QQ截图20240518161224](https://123321xpc-images.oss-cn-hangzhou.aliyuncs.com/imgs/md-images/django.assets/QQ%E6%88%AA%E5%9B%BE20240518161224.png)

- 在项目路由中添加`url`

```
path('admin/', admin.site.urls),
```

- 之后访问`/admin`即可。



# 媒体文件

在`setting.xml`中配置媒体文件根目录：

```python
MEDIA_ROOT = BASE_DIR / 'static/uploads'
```





## 单文件上传

前端将文件上传后，后端：

```python
def index4(request):
    # 使用FIOES.get()获取文件
    file = request.FILES.get("file")
    # 获取文件名称(file.jpg)
    file.name
```



## 保存文件到后端

- 在视图函数中：

```python
from django.conf import settings
import os


def index4(request):
    # 使用FIOES.get()获取文件
    file = request.FILES.get("file")

    # 保存文件路径
    file_path = os.path.join(settings.MEDIA_ROOT, file.name)

    # 保存文件             追加方式
    with open(file_path, "ab") as fp:
        for chunk in file.chunks():
            # 写入文件
            fp.write(chunk)
            # 清空缓存
            fp.flush()
        # 关闭文件
        fp.close()
```



## 多文件上传

```python
def index4(request):
    # 使用FIOES.get()获取文件
    files = request.FILES.get("file")

    # 保存文件
    for file in files:
        # 构造每个文件路径
        file_path = os.path.join(settings.MEDIA_ROOT, file.name)
        # 之后单个文件操作即可
        with open(file_path, "ab") as fp:
            for chunk in file.chunks():
                # 写入文件
                fp.write(chunk)
                # 清空缓存
                fp.flush()
            # 关闭文件
            fp.close()
```





