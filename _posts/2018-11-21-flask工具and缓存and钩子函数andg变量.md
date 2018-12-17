---
title: flask工具and缓存and钩子函数andg变量
description: bootstrap&debugtoolbar&缓存&钩子函数&g变量
date: 2018-11-21
author: Pyrans
categories: 框架
tags:
- flask
---



## flask-bootstrap

用处: 帮助我们直接集成了bootstrap的东西

用法: 安装模块`pip install flask-bootstrap`

实例化bootstrap：

~~~
from flask-bootstrap import Bootstrap
bootstrap = Bootstrap(app)

bootstrap.init_app(app)
~~~

使用: 

使用时，在页面继承: `bootstrap/base.html`

然后完善base.html里写的block,就可以正常去复制粘贴bootstrap的样式了

模板还定义了很多其他块，都可在衍生模板中使用，下表列出了所有可用的块：

| 块名         | 说明                      |
| ------------ | ------------------------- |
| doc          | 整个html文档              |
| html_attribs | html标签属性              |
| html         | html标签中的内容          |
| head         | head标签中的内容          |
| title        | title标签中的内容         |
| metas        | 一组meta标签              |
| styles       | 层叠样式表定义            |
| body_attribs | body标签的属性            |
| body         | body标签中的内容          |
| navbar       | 用户定义的导航条          |
| content      | 用户定义的页面内容        |
| scripts      | 文档底部的JavaScript 声明 |

## debugtoolbar

用处：帮我们查看开发相关配置和后端的sql 路由等等

 写法：

​	from flask_debugtoolbar import DebugToolbarExtension

​	debug = DebugToolbarExtension(app)

使用需设置SECRET_KEY

设置`DEBUG = True`即可开启，如果想让他消失：DEBUG=FALSE

## 缓存

**安装模块**: `pip install flask-caching`

**完整教程**: <a href='https://pythonhosted.org/Flask-Caching/' target='_block'>官方文档</a>

**简单教程**: 

* 导入模块: `from flask-caching import Cache`
* 实例化

~~~
1.简单使用
cache = Cache(
	config={
        'cache_type': 'simple'
	}
)

2.指定数据库储存
cache = Cache(
	config={
	"cache_type": 'redis',
    "cache_redis_url": "redis://用户名：密码@ip:端口/数据库
	}
) 
~~~

* 注册`cache.init_app(app)`

**使用方法**:

* 使用装饰器: @cache.cached(timeout=过期时间，单位为秒)
* 使用原生: `cache.set(key, value, 过期时间)`

* 获取缓存: `cache.get(key)`
* 删除缓存: `cache.delete(key)`

## 钩子函数

作用:  在每次请求之前执行. 通常使用这个钩子函数预处理一些变量, 视图函数可以更好调用

类似与Django中的中间件

使用:  `@蓝图.before_request`

例子：

~~~
@blue.before_request
def heheda():
    # 再看ip如果在30秒内访问10次  就返回json
    user_agent = request.user_agent
    if not user_agent:
        return jsonify({'code': 10000, 'msg': '钩子函数测试'}), 500
    ip = request.remote_addr
    key = ip + 'test'
    times = cache.get(key)
    if not times:
        times = 0
    if times >= 10:
        return 'Come on Baby', 404
    else:
        cache.set(key, int(times) + 1, 30)
~~~

## g变量

g对象是专门用来保存用户的数据的,在一次请求中的所有的代码的地方,都可以使用

前端也可以访问到
