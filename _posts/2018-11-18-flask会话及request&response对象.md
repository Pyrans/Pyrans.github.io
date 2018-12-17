---
title: 会话&访问对象&abort
description: flask中的会话&request与response对象&abort
date: 2018-11-18
author: Pyrans
categories: 框架
tags:
    - flask
---



## cookie

浏览器端的会话机制，能存数据，支持过期，不支持跨浏览器、域名，且安全性不能够保证

设置: response.set_cookie(key, value, 时间(单位为秒))

删除: response.delete_cookie

获取: request.cookies.get(key)

## session

服务器端的会话机制，能支持过期，base64的摘要，要依赖于cookie

flask中默认存到内存

flask中操作需导入模块：from flask import session

在app创建是添加SECRET_KEY:  app.config["SECRET_KEY"] = "中间随便填写一段字符串"

设置: session[key] = value

删除: session.pop(key)

获取: session.get(key)

## session的持久化

导入模块: from flask_session import Session

导入设置: 

app.config["SECRET_KEY"] = "中间随便填写一段字符串"

app.config['SESSION_TYPE'] = 'redis'     # 指定session存储方案

app.config['SESSION_KEY_PREFIX'] = 'myapp:' #设置缓存的开头 可以不设置,默认127.0.0.1 6379 0号库

app.config['SESSION_REDIS'] = StrictRedis(host="127.0.0.1", db=5) #定制化的将session存到redis的指定位置(若不设置则使用默认库)

实例化session:

sess = Session()

sess.init_app(app)

## request对象

~~~
属性
	url		完整请求地址
	base_url	去掉GET参数的URL
	host_url	只有主机和端口号的URL
	path		路由中的路径
	method		请求方法
	remote_addr	请求的客户端地址
	args		GET请求参数
	form		POST，PUT， DELETE请求参数
	files		文件上传
	headers		请求头
	cookies		请求中的cookie
~~~

## response对象

设置response:

1. make_response 
   * 例子: response = make_response('\<h1> test\</h1>')
   * ​          return reponse
2. redirect 重定向
   * 例子: reponse = redirect(url_for('蓝图名.函数名'))
   * ​          return response     # 会重定向到指定的路径

## abort

abort(状态码)

在函数中添加abort,可以强行到转到指定的状态码

例子:

~~~
@blue.route('/response')
def my_response():
    abort(403)   # 主动终止， 括号中为状态码
    return '呵呵', 500
~~~

