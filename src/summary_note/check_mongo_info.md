# 查看当前MongoDB信息

想要查看当前MongoDB信息，即如何得知mongod的 启动文件、 配置文件、log日志文件、数据文件路径等等是什么

经过研究，可以用如下方法：

可以通过：

```bash
systemctl status mongod
```

中看到启动文件，比如：

```bash
[root@xxx-general-01 ~]# systemctl status mongod
[0m mongod.service - SYSV: Mongo is a scalable, document-oriented database.
   Loaded: loaded (/etc/rc.d/init.d/mongod; bad; vendor preset: disabled)
   Active: active (running) since Tue 2018-04-10 15:37:29 CST; 20h ago
     Docs: man:systemd-sysv-generator(8)
   CGroup: /system.slice/mongod.service
           1096 /usr/bin/mongod -f /etc/mongod.conf

Apr 10 15:37:28 xxx-general-01 systemd[1]: Starting SYSV: Mongo is a scalable, document-oriented database....
Apr 10 15:37:28 xxx-general-01 runuser[1077]: pam_unix(runuser:session): session opened for user mongod by (uid=0)
Apr 10 15:37:29 xxx-general-01 runuser[1077]: pam_unix(runuser:session): session closed for user mongod
Apr 10 15:37:29 xxx-general-01 mongod[1058]: Starting mongod: [  OK  ]
Apr 10 15:37:29 xxx-general-01 systemd[1]: Started SYSV: Mongo is a scalable, document-oriented database..
```

中的：

`/etc/rc.d/init.d/mongod`

是启动脚本

然后再去查看此启动脚本的内容，可以找到配置文件：

```bash
[root@xxx-general-01 ~]# cat /etc/rc.d/init.d/mongod 
#!/bin/bash

# mongod - Startup script for mongod

# chkconfig: 35 85 15
# description: Mongo is a scalable, document-oriented database.
# processname: mongod
# config: /etc/mongod.conf

. /etc/rc.d/init.d/functions

# NOTE: if you change any OPTIONS here, you get what you pay for:
# this script assumes all options are in the config file.
CONFIGFILE="/etc/mongod.conf"
OPTIONS=" -f $CONFIGFILE"

mongod=${MONGOD-/usr/bin/mongod}

MONGO_USER=mongod
MONGO_GROUP=mongod
...
```

中的：

`/etc/mongod.conf`

然后再从配置文件中看到，对应的log日志，数据文件等信息：

```bash
[root@xxx-general-01 ~]# cat /etc/mongod.conf 
# mongod.conf

# for documentation of all options, see:
#   http://docs.mongodb.org/manual/reference/configuration-options/

# where to write logging data.
systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

# Where and how to store data.
storage:
  dbPath: /var/lib/mongo
  journal:
    enabled: true
#  engine:
#  mmapv1:
#  wiredTiger:

# how the process runs
processManagement:
  fork: true  # fork and run in background
  pidFilePath: /var/run/mongodb/mongod.pid  # location of pidfile

# network interfaces
net:
  port: 32018
  bindIp: 127.0.0.1,172.16.141.197 # Listen to specific IP
#  bindIp: 127.0.0.1  # Listen to local interface only, comment to listen on all interfaces.
#  bindIp: 0.0.0.0  # Listen to all interfaces
#  port: 27017

security:
  authorization: 'enabled'

#operationProfiling:

#replication:

#sharding:

## Enterprise-Only Options

#auditLog:

#snmp:
```

中，找到：

* 日志文件：`/var/log/mongodb/mongod.log`
* 数据文件（路径）：`/var/lib/mongo`
