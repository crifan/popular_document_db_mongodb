# 不要在admin中创建普通用户

创建用户时注意不要在admin数据库中创建：

如果不小心是在最开始的`admin`中去用`db.createUser`新建的普通用户，则实际上新建的用户只是属于`admin`数据库的。

可以用admin账号登录后，通过如下命令看到：

```bash
> use admin
switched to db admin
> show users
{
        "_id" : "admin.root",
        "user" : "root",
        "db" : "admin",
        "roles" : [
                {
                        "role" : "root",
                        "db" : "admin"
                }
        ]
}
{
        "_id" : "admin.log",
        "user" : "log",
        "db" : "admin",
        "roles" : [
                {
                        "role" : "dbOwner",
                        "db" : "log"
                }
        ]
}
```

所以要切换到对应新数据库中，再去创建才可以。

否则就会导致后续没有权限操作其下数据。
