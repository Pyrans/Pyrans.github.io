---
title: 使用python代码操作数据库
description: 远端使用python操作数据库
date: 2018-10-13
author: Pyrans
categories: 数据库
tags:
    - mysql
---



## PyCharm连接MySQL数据库

```python
#导入pymysql模块,用来帮助操作mysql数据库
import  pymysql

"""
连接mysql数据库-
用户名, 密码, 主机名,端口号
host = None, con 指定主机名,   ip地址, 127.0.0.1和localhost代表主机
user = None,   指定用户名
password = "",  指定密码
database = None,  指定连接的数据库
port = 0,    指定数据库端口号  默认是3306
charset = '',  指定编码
"""

# 创建数据库连接
connect = pymysql.Connect(host="192.168.45.123",user="test",password="123123",database="test",charset="utf8")
# 获取cursor对象
# 执行sql语句
cursor = connect.cursor();
cursor.execute("select * from classes;");
# 获取执行后的结果
res = cursor.fetchone();
print(res)
res = cursor.fetchone();
print(res)
res = cursor.fetchone();
print(res)
# 关闭连接
cursor.close()
connect.close()
```


​	
​	

## PyCharm连接MySQL数据库创建新表
```python
import pymysql
"""
连接mysql数据库
用户名, 密码, 主机名,端口号
host = None, con 指定主机名,   ip地址, 127.0.0.1和localhost代表主机
user = None,   指定用户名
password = "",  指定密码
database = None,  指定连接的数据库
port = 0,    指定数据库端口号  默认是3306
charsset = '',  指定编码
"""
connect = pymysql.Connect(host="192.168.45.123", user="test", password="123123", database="test",
                          charset="utf8")
# 获得cursor对象
cursor = connect.cursor()
# 创建一个表
createSql = "CREATE TABLE shop(id INT PRIMARY  KEY  auto_increment,name VARCHAR(20),price INT);"

cursor.execute(createSql)

# 关闭资源
cursor.close()
connect.close()
```
* **表的删、改、查操作与之类似**





## PyCharm连接MySQL数据库添加数据
```python
# 导入pymysql模块,用来帮助操作mysql数据库
import  pymysql

"""
连接mysql数据库-
用户名, 密码, 主机名,端口号
host = None, con 指定主机名, ip地址, 127.0.0.1和localhost代表主机
user = None,   指定用户名
password = "",  指定密码
database = None,  指定连接的数据库
port = 0,    指定数据库端口号  默认是3306
charset = '',  指定编码
"""
connect = pymysql.Connect(host="192.168.45.123",user="test",password="123123",database="test",charset="utf8")

# 执行sql语句
# 获得cursor对象,cursor对象用来执行sql语句的
cursor = connect.cursor()

# 增、删、改需要用到回滚
try:
    sqlInsert1 = "insert into shop values(0,'辣条',99);"
    sqlInsert2 = "insert into shop values(0,'泡面',6);"
    sqlInsert3 = "insert into shop values(0,'茶叶',9);"
    sqlInsert4 = "insert into shop values(0,'哈啤',64);"
    sqlInsert5 = "insert into shop values(0,'天鹅蛋',91);"
    sqlInsert6 = "insert into shop values(0,'保温杯',66);"
    cursor.execute(sqlInsert5)
    cursor.execute(sqlInsert6)
    # commit提交
    connect.commit()

except:
    # 出现异常会回滚sql
    # 用sql进行数据操作的时候,通常需要保证数据的完整性
    # 当需要同时执行多条sql语句时, 其中的任意一条执行出错,就可能导致所有数据出错,
    # 需要回滚到执行这些sql语句之前的状态
    connect.rollback()

# 关闭连接
cursor.close()
connect.close()
```
* **数据的删除、修改、查询操作与之类似**


## PyCharm连接MySQL数据库查询数据
```python
# 导入pymysql模块,用来帮助操作mysql数据库
import pymysql

"""
连接mysql数据库
用户名, 密码, 主机名,端口号
host = None, con 指定主机名,   ip地址, 127.0.0.1和localhost代表主机
user = None,   指定用户名
password = "",  指定密码
database = None,  指定连接的数据库
port = 0,    指定数据库端口号  默认是3306
charset = '',  指定编码
"""
connect = pymysql.Connect(host="192.168.45.123", user="test", password="123123", database="test",
                          charset="utf8")
# 执行sql语句
# 获得cursor对象,cursor对象是用来执行sql语句的
cursor = connect.cursor()

# 查询
selectSql = "select * from shop"
cursor.execute(selectSql)

# 查询结果在cursor中
# cursor.fetchone() 获取一个结果
# cursor.fetchall()  获取所有的结果
# cursor.fetchmany(size) 获取指定数量的结果
# cursor.rowcount 获取结果的行数

# result01 = cursor.fetchone()
# print(result01)
# print(result01[1])
# 结果是元组形式,且元组中的值会与数据库的表的字段对应

# result02 = cursor.fetchone()
# print(result02)
# print(result02[1])

result03 = cursor.fetchall()
# result03 = cursor.fetchmany(2)
#
# for result in result03:
#     print(result[1])

print(result03)

for i in range(cursor.rowcount):
    # print(all)
    print(result03[i][1])

# 关闭连接
cursor.close()
connect.close()
```

