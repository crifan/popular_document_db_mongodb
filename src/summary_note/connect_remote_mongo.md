# 连接远程MongoDB的方式

背景：

在远程阿里云ECS服务器中有个MongoDB数据库：

* IP：`47.96.131.109`
* Port：`32018`

其中有个：

* gridfs数据库
  * 用户名：gridfs
  * 角色：dbOwner

且服务端mongod正在运行了

下面是如何去连接该远程的mongo数据库几种方式：

## 服务器中本地连接

服务器上本地客户端：`mongo shell`

```bash
[root@xxx-general-01 ~]# mongo --port 32018
MongoDB shell version: 3.2.19
connecting to: 127.0.0.1:32018/test
```

进去后再：

```bash
use gridfs
db.auth("gridfs”, "password")
```

或者直接：

```bash
mongo gridfs --port 32018 -u gridfs -p password --authenticationDatabase gridfs
```

## Mac本地连接远端MongoDB

Mac中本地`mongo shell`去连接远程MongoDB

### 以gridfs用户去登录

以用户gridfs去登录，且（限定了）只（能）访问数据库gridfs：

```bash
mongo 47.96.131.109:32018/gridfs  -u gridfs -p password --authenticationDatabase gridfs
```

或：

```bash
mongo gridfs --host 47.96.131.109 --port 32018  -u gridfs -p password --authenticationDatabase gridfs
```

### 以admin用户去登录

以用户admin去登录，没有限定访问哪个数据库（后续则可以访问其他数据，前提是admin本身有这个权限）：

```bash
mongo --host 47.96.131.109 --port 32018 -u root -p pwd --authenticationDatabase admin
```

## Python的pymongo代码连接远程MongoDB

```python
import pymongo
from pymongo import MongoClient
import gridfs

# from pymongo.objectid import ObjectId
# from pymongo import objectid
from bson.objectid import ObjectId

from gridfs import GridFS

MongoHost = "47.96.131.109"
MongoPort = 32018

MongoUseAuth = True
# MongoUseAuth = False

# with auth
MongoUsername = "gridfs"
MongoPassword = “password"
MongoAuthenticationDatabase = "gridfs"

mongodbUri = ""
if MongoUseAuth :
    mongodbUri = "mongodb://%s:%s@%s:%s/%s" % (
        quote_plus(MongoUsername), \
        quote_plus(MongoPassword), \
        MongoHost, \
        MongoPort, \
        MongoAuthenticationDatabase \
    )
    #'mongodb://gridfs:password@47.96.131.109:32018/gridfs'
else:
    mongodbUri = "mongodb://%s:%s" % (
        MongoHost, \
        MongoPort
    )
    #'mongodb://localhost:32018'
    #'mongodb://47.96.131.109:32018’

mongoClient = MongoClient(mongodbUri)
gridfsDb = mongoClient.gridfs
fsCollection = GridFS(gridfsDb)
```

## PyCharm中mongo4idea中的连接远端MongoDB

配置参数：

* General
  * 截图：
    * ![mongo4idea_config_general](../assets/img/mongo4idea_config_general.png)
  * 文字：
    * Server url(s)：`47.96.131.109:32018`
    * User Database：`gridfs`
* Authentication
  * 截图：
    * ![mongo4idea_config_authentication](../assets/img/mongo4idea_config_authentication.png)
  * 文字：
    * Username：`gridfs`
    * Password：`your_password`
    * Auth. database：`gridfs`
    * Auth. mechanism：`SCRAM-SHA-1`

即可成功连接：

![mongo4idea_test_connection_successful](../assets/img/mongo4idea_test_connection_successful.png)
