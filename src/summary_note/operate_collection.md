# 操作collection

## 给collection改名

`mongo shell`或代码（比如`Python`的`Pymongo`）语法：

```bash
db.yourCollection.renameCollection("newCollectionName")
```

举例：

```bash
db.gameShortLink_20210816.renameCollection("gameShortLink_20210816_mockFailed")
```

注：`MongoDB Compass`中不支持collection改名

