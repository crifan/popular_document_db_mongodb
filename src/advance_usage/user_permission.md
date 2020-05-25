# 用户和权限

为了数据安全，可以针对同一个数据库，以及不同的内部的集合，创建和允许不同的用户和权限，去访问。

MongoDB支持 `基于用户权限的访问控制=`RBAC`=`Role-Based Access Control`

一个用户可以有一个或多个角色Role，决定了能访问哪个数据库，能进行什么操作

如何验证权限：

* 方式：启动mongod时加`--auth`参数
* 方式2：设置：[security.authorization](https://docs.mongodb.com/manual/reference/configuration-options/#security.authorization)
  * 配置文件中去设置
    * `security`的`authorization`为`enabled`

在开启认证auth==开启访问控制之前，需要你在admin数据库中，创建一个是带有`userAdmin`或`userAdminAnyDatabase`权限的用户

-》否则意味着你没有一个拥有管理权限的用户，就没法创建其他普通用户了

不过对于创建用户本身来说：在开启访问控制之前或者之后，都是可以的。

关于权限的详细解释如下：

* Authentication Database
    * 创建一个用户的时候，需要制定对应数据库的
        * 这个数据库就是该用户的Authentication Database
        * 不过一个用户的权限，可以不限定Authentication Database，只要针对别的数据库给了相应权限即可
    * 创建用户
        * 主要含义：增加一个用户，对于某个资源resource，允许某些操作action（就有了某些权限privilege）
            * resource：
                * 典型的只有一个db
                * 也可以针对其他的，比如collection：
                    * { db: "products", collection: "inventory" }
        * 典型写法：
            * createUser
                * 其中参数：
                    * role的参数：
                        * 可以用系统内置的，比如：
                            * read
                            * readWrite
                            * dbAdmin
                            * dbOwner
                            * userAdmin
                        * 也可以用用户自定义的role
        * 在创建用户时没有指定对应role的话，可以后续用：grantRolesToUser去额外加上role
        * 用户的唯一标识是： 用户名+授权数据库
            * 换句话说：如果在创建用户时，两个用户名一样，但是授权数据库不同，也是不同的用户
            * 如果想要用一个用户对多个数据库都有权限，那么应该是：创建单个用户，带上对应角色role，而这个role是允许访问多个数据库的
    * MongoDB中是把所有用户相关信息都保存到admin数据库中的system.users中了
        * 包括：用户名，密码，用户的授权数据库
        * 不建议直接操作该数据库，而建议（在mongo shell中）用用户管理命令，比如：
            * createUser
            * grantRolesToUser
            * usersInfo
            * 等等

后来想到一个比喻：

* Authentication=认证=识别用户（的身份）：是否是之前添加过（认识的）的用户，否则不让进
    * 就像要进去一间屋子，需要一把钥匙
    * 对于Mongo shell：
        * 需要提供：
            * 用户名username
            * 密码password
            * 对应的哪个数据库database
        * 对应着 mongo shell（或其他mongo API）的参数：
            * `--username <username>`, `-u <username>`
            * `--password <password>`, `-p <password>`
            * `--authenticationDatabase <dbname>`
        * 或者，先进去，再认证：
            * 先运行mongo，在shell里再去:
                * `use xxxDb`
                * `db.auth("username", "password")`
    * 而对于其他语言的Driver
        * Python
            * pymongo
                * MongoClient初始化时传递对应参数即可
                    * mongoClient = MongoClient(
                    *     host=“11.22.33.44",
                    *     port=27017,
                    *     username=“usr",
                    *     password=“pwd"
                    * )
                * 或者是用Mongo URI，比如：
                  * `mongodb://usr:pwd@11.22.33.44:27017/dbName`
* Authorization=授权=判断用户能干嘛：针对哪个数据库，有哪些操作权限
    * 就像进了一间屋子，到底能进哪间房，且每间房里只能允许能干什么事
        * 不能进别的房间，进了允许进的房间后，也不能干不允许干的事
