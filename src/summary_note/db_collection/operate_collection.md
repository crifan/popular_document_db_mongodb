# 操作集合

## 给集合collection改名

`mongo shell`或代码（比如`Python`的`Pymongo`）语法：

```bash
db.yourCollection.renameCollection("newCollectionName")
```

举例：

```bash
db.gameShortLink_20210816.renameCollection("gameShortLink_20210816_mockFailed")
```

注：`MongoDB Compass`中不支持collection改名

## 删除集合collection

`mongo shell`中去删除一个集合，用：

```bash
db.collection.drop()
```

举例：

```bash
db.gameShortLink_20210816.drop()
```

[db.collection.drop() — MongoDB Manual](https://docs.mongodb.com/manual/reference/method/db.collection.drop/#mongodb-method-db.collection.drop)
