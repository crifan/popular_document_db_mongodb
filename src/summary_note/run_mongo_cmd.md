# 运行mongo命令

举例：想要给某个集合重建索引

* `pymongo`代码中
  ```python
  import pymongo

  MongoDbName = "shortLink"
  MongoUri = 'mongodb://127.0.0.1:27017/%s' % MongoDbName

  mongoClient = pymongo.MongoClient(MongoUri)
  mongoDb = mongoClient[MongoDbName]

  mongoDb.command({"reIndex":"gameShortLink"})
  ```
* `mongo shell`中
  ```bash
  use shortLink
  db.command({ reIndex: "gameShortLink" })
  ```

官网文档：

[collection – Collection level operations — PyMongo 3.12.0 documentation](https://pymongo.readthedocs.io/en/stable/api/pymongo/collection.html#pymongo.collection.Collection.create_index)

[reIndex — MongoDB Manual](https://docs.mongodb.com/manual/reference/command/reIndex/)

