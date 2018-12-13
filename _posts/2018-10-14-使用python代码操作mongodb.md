---
title: 使用python操作mongodb
description: python远程操作mongodb
date: 2018-10-14
author: Pyrans
tags:
    - mongodb
    - python
---



## python连接MongoDB数据库--插入数据

	import pymongo
	# host=None,  ip地址
	# port=None,  端口号
	# 创建连接
	mongoClient = pymongo.MongoClient(host="192.168.45.123", port=27017)
	school = mongoClient.school
	
	school.newclass.insert({"name": "Python1806", "students_num": 33})
	mongoClient.close()


## python连接MongoDB数据库--查询数据
	import pymongo
	# host=None,
	# port=None,
	from bson import ObjectId
	# 创建连接
	mongoClient = pymongo.MongoClient(host="192.168.45.123", port=27017)
	school = mongoClient.school
	# 查看所有数据
	result01 = school.student.find()
	print(result01)
	for res in result01:
	    print(res)
	
	print("--" * 20)
	
	# 查看指定id的数据
	result02 = school.student.find({"_id": ObjectId("5bc6289e7088a826a31f5810")})
	print(result02)
	for res in result02:
	    print(res)
	
	# 查询结果排序
	result03 = school.student.find().sort("age", 1)
	for res in result03:
	    print(res)
	
	mongoClient.close()




## python连接MongoDB数据库--删除数据
	import pymongo
	# host=None,
	# port=None,
	# 创建连接
	mongoClient = pymongo.MongoClient(host="192.168.45.123", port=27017)
	school = mongoClient.school
	# 查询删除之前的结果
	result01 = school.student.find()
	for res in result01:
	    print(res)
	
	print("--"*20)
	
	# 删除数据
	school.student.remove({"name": "LiSi"})
	# 查询删除之后的结果
	result02 = school.student.find()
	for res in result02:
	    print(res)
	mongoClient.close()




## python连接MongoDB数据库--修改数据
	import pymongo
	# host=None,
	# port=None,
	# 创建连接
	mongoClient = pymongo.MongoClient(host="192.168.45.123", port=27017)
	school = mongoClient.school
	# 查询修改之前的结果
	result = school.student.find({"name":"TianQi"})
	print(result.next())
		
	print("--"*20)
	
	# 修改数据
	school.student.update({"name": "TianQi"}, {"$set": {"age": 18}})
	# 查询修改之后的结果
	result = school.student.find({"name":"TianQi"})
	print(result.next())
	mongoClient.close()