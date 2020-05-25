# MongoDB的Server端


## 配置

典型的MongoDB的服务端文件是：

`/etc/rc.d/init.d/mongod`

而其中核心配置是：

```bash
CONFIGFILE="/etc/mongod.conf"
OPTIONS=" -f $CONFIGFILE"
mongod=${MONGOD-/usr/bin/mongod}
MONGO_USER=mongod
MONGO_GROUP=mongod
```

对应配置文件是：

`/etc/mongod.conf`

内部核心参数是：

```bash
# Where and how to store data.
storage:
  dbPath: /var/lib/mongo
```

表示数据库存放位置是：`/var/lib/mongo`

## 启动本地MongoDB服务

* 对于普通安装的MongoDB

直接在终端中运行：

```bash
mongod
```

* 对于安装的是mongodb-community

如果Mac中安装的MongoDB是`mongodb-community`，那么用：

```bash
brew services start mongodb-community
```

以及，关于MongoDB服务端的其他常见管理方式有：
* 启动：`brew services start mongodb-community`
* 停止：`brew services stop mongodb-community`
* 重启：`brew services restart mongodb-community`
* 查看状态：
    * `brew services list`
        * 如何确定已运行：看到`mongodb-community`是`started`
    * 用`ps`
        * `ps -ef | grep mongod`
        * `ps aux | grep mongod`
            * -》有输出`mongod`

## 启动远程服务器中的MongoDB服务

* 方案1：切换到mongo用户再去启动

如果是通过SSH连接的远程服务器中：

mongod的服务，是作为mongod的组和用户，去在开机时启动的，可以正常启动的话

那么自己用ssh作为root用户登录进来后，是root用户，是无法启动属于`mongod:mongod`的服务mongod

在当前登录用户root的情况下，换用mongd的用户去，启动mongod：

```bash
sudo -u mongod mongod -f /etc/mongod.conf
```

才可以。

* 方案2：用systemctl或service去管理mongod

如果本身已有服务可以管理mongod，则可以通过服务管理去启动：

```bash
systemctl restart mongod
```

等价于：

```bash
service mongod restart
```



