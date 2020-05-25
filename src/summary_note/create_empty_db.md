# 新建空数据库和空集合

想要新建一个空的MongoDB的数据库，以及在空数据库中创建一个空的集合。

思路是：新建一个db，给db插入一个值，再删掉，就得到空的db的collection（和空的db数据库）了。

具体做法：

```bash
use newDb
db.newCollection.insert({"fakeKey": "fakeValue"})
db.newCollection.find() # 会输出刚插入的记录的_id
db.newCollection.deleteOne({"_id": ObjectId("newInsertedId")})
```

然后用：

```bash
db.newCollection.find()
```

会看到输出是空的 -》 说明的确已经新建一个空的db和空的collection了。

提示：

在此期间可以随时用：

```bash
db
```

查看当前所处的数据库

和

```bash
show dbs
```

看看当前有哪些数据库

和：

```bash
show collections
```

看看当前数据库中有哪些集合

## 举例：新建一个db=storybook和collection=main

步骤：

```bash
> use storybook
switched to db storybook
> show dbs
admin    0.000GB
dialog   0.272GB
gridfs  13.869GB
local    0.000GB
> db.main.insert({"fakeKey": "fakeValue"})
WriteResult({ "nInserted" : 1 })
> show collections
main
> db
storybook
> db.main.find()
{ "_id" : ObjectId("5bd2bddb6ec5fdeabfbd6ecb"), "fakeKey" : "fakeValue" }
> db.main.deleteOne({"_id": ObjectId("5bd2bddb6ec5fdeabfbd6ecb")})
{ "acknowledged" : true, "deletedCount" : 1 }
> db.main.find()
>
```
