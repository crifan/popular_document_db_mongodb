# PyMongo

用Python通过API操作的MongoDB，最常见的库是：`PyMongo`

## 基本使用

运行服务端：

```bash
mongod
```

代码中导入

```python
import pymongo
```

连接Client

```python
from pymongo import MongoClient
client = MongoClient()
```

如果需要，可以指定host和port：

```python
client = MongoClient('localhost', 27017)
```

或者通过`URI`指定更多参数：

```python
client = MongoClient('mongodb://localhost:27017/')
```

创建数据库：

```python
db = client.test_database
```

也可以用字典属性方式访问数据库：

```python
db = client['test-database']
```

访问集合：

```python
collection = db.test_collection
```

也可以用字典属性方式访问集合：

```python
collection = db['test-collection']
```

然后就可以正常操作了。

比如：插入（文档）数据

```python
demoDict = {"name": "Crifan"}
new_doc_id = collection.insert_one(demoDict).inserted_id
print("new_doc_id=%s" % new_doc_id)
```

更多基本操作用法可官网教程：

[Tutorial — PyMongo 3.9.0 documentation](https://api.mongodb.com/python/current/tutorial.html)

更多心得和总结可参考后续章节：

[PyMongo心得](https://book.crifan.com/books/popular_document_db_mongodb/website/summary_note/pymongo/)

## 资料

* 官网
  * 旧
    * 版本：`<= 3.9`
      * PyMongo教程
        * [Tutorial — PyMongo 3.9.0 documentation](http://api.mongodb.com/python/current/tutorial.html)
          * Mongo的Client
            * [mongo_client – Tools for connecting to MongoDB — PyMongo 3.9.0 documentation](http://api.mongodb.com/python/current/api/pymongo/mongo_client.html#pymongo.mongo_client.MongoClient)
      * API概览
        * [API Documentation — PyMongo 3.9.0 documentation](http://api.mongodb.com/python/current/api/index.html)
  * 最新：readthedocs.io
    * 版本：`>= 3.10`
      * [PyMongo 3.10.1 Documentation — PyMongo 3.10.1 documentation](https://pymongo.readthedocs.io/en/stable/)
* 第三方
  * [nummy/pymongo-tutorial-cn: pymongo中文教程](https://github.com/nummy/pymongo-tutorial-cn)
