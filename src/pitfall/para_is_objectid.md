# 参数_id是ObjectId对象而不是字符串

直接说具体的坑是：Pymongo中的很多函数，比如exists等，传入的参数id是ObjectId对象而不是id的字符串

发现并解决坑的具体过程：

此处，gridfs的官网文档：

[gridfs – Tools for working with GridFS — PyMongo 3.6.1 documentation](http://api.mongodb.com/python/current/api/gridfs/index.html#gridfs.GridFS.put)

> exists(document_or_id=None, session=None, **kwargs)

函数来说，没有说明`document_or_id`是个特殊的`ObjectId`的这个类的实例，而其例子：

```python
>>> fs.exists(file_id)
>>> fs.exists({"_id":file_id})
>>> fs.exists(_id=file_id)
>>> fs.exists({"filename": "mike.txt"})
>>> fs.exists(filename="mike.txt")
```

很容易让人误解就是普通的_id的值的字符串，比如：

`"5abc96dfa4bc715f473f0297"`

或

`"ObjectId('5abc96dfa4bc715f473f0297')"`

搞得尝试半天也无法正常执行，找不到本来已存在的文件。

幸亏：

[django - Querying by "_id" doesn't return file in MongoDB in Python, using PyMongo - Stack Overflow](https://stackoverflow.com/questions/12339583/querying-by-id-doesnt-return-file-in-mongodb-in-python-using-pymongo/12344404)

中解释的，对于pymongo

2.2版本之前：

```python
from pymongo.objectid import ObjectId
```

2.2版本之后：

```python
from bson.objectid import ObjectId
```

然后才能用于exists：

```python
fileIdToDelete = '5abc8d77a4bc71563222d455'
fileObjectIdToDelete = ObjectId(fileIdToDelete)
if fsCollection.exists(fileObjectIdToDelete):
    fsCollection.delete(fileObjectIdToDelete)
```

并且注意到作者是2012年，6年前就回复了该答案，结果此处pymongo在6年后，都没有及时更新此内容，真是醉了。

希望mongodb的文档以后能及时更新啊。
