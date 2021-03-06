---
title: 熟悉Django的模板语言——Python第四周第二节
layout: post
tags: 
- django
- python
---



# 熟悉Django的模板语言



#### 新建一个站点app

```shell
python3 manage.py startapp django_web
```

目录

```shell
templates站点资源
views.py 负责去取数据和取templates
models.py 负责去数据库取数据

settings.py 默认设置，安全设置

```

#### 添加app到INSTALLED_APPS  

#### 添加视图函数

```python
def index(request):
    # 定向到index页面
    return render(request, 'index.html')
```

#### 添加URL

```python
from django_web.views import index
# app的视图函数中引入

# 分配一个url 网址

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^index/', index)  #正则 ^匹配index前缀的站点 ，调用index函数
]
```

运行

```shell
python3 manage.py runserver
```

发现CSS失效

#### 引入资源文件

将CSS和资源目录打包为static文件夹，将其放置在项目根目录下

django模板语言

```python
{% raw %}
{% load static %}  #获取所有static路径
<link rel="stylesheet" type="text/css" href="{% static 'css/new_blah.css' %}">

{% endraw %}
```

#### 设置static

在settings.py中设置static

```python
STATICFILES_DIRS = (os.path.join(BASE_DIR, 'static'),)
```



#### request步骤

1. 经过Url
2. 指向于对应的View
3. View和templates去找网页和数据



```python
You have 13 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
#暂时不管
```





#### 分页功能

1. 理解上下文
2. 使用模板语言
3. 只做分页器

#### render()：渲染

```python
render(request,'html',context)
```



接收三个函数

- request 用户点击的request
- x.html 我们指定模板的名称
- context 上下文

#### Context

There's a <u>Starman</u> waiting in the sky

替换掉选中的文字其他部分不变



#### 使用Context替换

1. 设置context

   ```python
   def index(request):
       # 定向到index页面
       context = {
           'title': 'Just a title',
           'des': 'Just a description',
           'score': '1.0'
       }
       return render(request, 'index.html', context)
   ```

2. 在html中替换，对应响应的context

   ```python
   <h3><a href="#">{{ title }}</a></h3>
   <p class="description">{{ des }}</p>

   ```

   ​

context的值从数据库中取，Model连接数据库



#### Model设置

django自带的是sqlite，我们自己使用的是mongodb，

在settings里引入

```python
from mongoengine import connect
connect('zhuanzhuan', host='127.0.0.1', port=27017)
```

之所以在settings里引入，是因为django在运行的过程中，是先从settings中读取数据进行加载

在Model层引入

```python
from mongoengine import *
```

```python
class ArtInfo(Document):
    # 数据库中的必须全部取出
    title = StringField()
    img = StringField()
    area = StringField()
    price = StringField()
    look_time = StringField()

    meta = {
        'collection': 'item_info'  # 寻找地方
    }

for i in ArtInfo.objects[:2]:   #[:2] 相当于mongo中的limit功能
    print(i.title, i.img, i.price)
    
```

在View层中实例化

```python
def index(request):
    # 实例化
    item_info = ArtInfo.objects[:1]

    # 定向到index页面
    context = {
        'title': item_info[0].title,
        'des': item_info[0].area,
        'score': item_info[0].price
    }
    return render(request, 'index.html', context)
```



使用分页函数

```python
# 调用templates视图函数
def index(request):
    limit = 4
    # 实例化
    item_info = ArtInfo.objects[:1]
    paginatior = Paginator(item_info, limit) #每4个一页
    page = request.GET.get('page', 1)  # 把request变成了页码
    Loaded = paginatior.page(page)

    # 定向到index页面
    context = {
        'ArtInfo': Loaded
    }
    return render(request, 'index.html', context)
```



设置HTML

```django
{#            开始循环   #}
            {% for item in ArtInfo %}
                <li>
                    <img src="{{ item.img }}" width="100" height="91">
                    <div class="article-info">
                        <h3><a href="#">{{ item.title }}</a></h3>
                        <p class="meta-info">
                            <span class="meta-cate">fun</span>
                            <span class="meta-cate">Wow</span>
                        </p>
                        <p class="description">{{ item.area }}</p>
                    </div>
                    <div class="rate">
                        <span class="rate-score">{{ item.price }}</span>
                    </div>
                </li>
            {% endfor %}
```

```django
<div class = "main-content-pagitor">
{#        < pre 1 of 2 next>#}
        {% if ArtInfo.has_previous %}
            <a href="?page={{ ArtInfo.previous_page_number }}">< Pre</a>
        {% endif %}
            <span> {{ ArtInfo.number }} of {{ ArtInfo.paginator.num_pages }}</span>
        {% if ArtInfo.has_next %}
            {% comment %}如果有下一页，就显示这个连接, next_page_number {% endcomment %}
            <a href="?page={{ ArtInfo.next_page_number }}">Next ></a>
        {% endif %}
    </div>
```

