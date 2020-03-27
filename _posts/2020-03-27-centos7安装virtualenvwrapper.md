---
title: mysql开启远程连接
date: 2018-10-13
categories: 数据库
author: Pyrans
description: 修改mysql配置&创建远程连接用户
tags:
    - mysql
---

使用pip安装，centos自带的python2.7似乎并不带有pip，这里我们首先安装一个pip:

~~~linux
yum install python-pip
~~~

安装好之后使用 `pip freeze`  可以查看一下状态，如果pip版本过低，或许需要升级一下：

~~~linux
pip install --upgrade pip
~~~

开始安装virtualenvwrapper

~~~linux
pip install virtualenv virtualenvwrapper
~~~

安装完成设置环境变量:    `vim ~/.bashrc`

~~~linux
export WORKON_HOME=.vir                # 这里等于号后面输入的是放置环境变量的目录，可以自己取名字
source /usr/bin/virtualenvwrapper.sh   # 这里输入virtualenvwrapper的路径，一般都在这个目录下面
~~~

设置完毕，刷新环境变量:    `source ~/.bashrc`

常用指令：

~~~linux
创建虚拟环境：mkvirtualenv [-p 路径] 名字 # []中的字符省略则默认python2.7
激活虚拟环境：workon 环境名称
退出虚拟环境：deactive
列出所有环境：lsvirtualenv -b
进入当前环境目录：cdvirtualenv
复制环境: cpvirtualenv 被复制的环境名称 复制出的环境名称
删除环境：rmvirtualenv 环境名称
~~~

参考链接：<a href="https://www.jianshu.com/p/4fecadbc5a48">https://www.jianshu.com/p/4fecadbc5a48</a>

