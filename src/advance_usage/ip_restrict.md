# IP限制

有时候为了安全，需要限定只有某个或某些IP才可以访问自己的（远端）MongoDB数据库。

这时候，就可以用上IP限制的功能了。

举例：

编辑配置文件`vi /etc/mongod.conf`，改为：

```bash
bindIp: 127.0.0.1,112.4.64.141 # Listen to specific IP
```

即可允许除了本机外的别的固定IP的访问。

## 添加了IP限制的mongod重启出错：Job for mongod.service failed because the control process exited with error code

不过，可能会遇到，添加了IP限制后，mongod启动出错：

`Job for mongod.service failed because the control process exited with error code`

的原因是：

其实有多种多样，具体的情况，需要根据实际情况去找原因，再去解决。

其中，辅助的办法是：

参考提提示的：

`Job for mongod.service failed because the control process exited with error code. See "systemctl status mongod.service" and "journalctl -xe" for details.`

去运行：

```bash
journalctl -xe
```

去看看具体的错误。

比如此处的：

```bash
Unregistered Authentication Agent for unix-process:4637:8872553
```

但是后来证明，无法根据此现象找到根本原因。

只是看起来像是：

端口权限方面的问题，有些人是SELINUX限制了端口导致的，而我此处没有开启SELINU，所以不是这方面的问题。

而真正解决问题的办法是：

此处主要是去看log文件

-> 从中（先后多次）找到真正的具体的错误信息

-> 然后才能知道错误原因

-> 然后才得以解决：

(1) 错误：listen(): bind() failed errno:98 Address already in use for socket: 127.0.0.1:32018

办法：停止掉mongo后再重新启动：

* 如果和我一样，没有root用户密码，则：reboot重启服务器
* 有root密码：以mongod用户去停止mongo
  * sudo -u mongod systemctl stop mongod

(2) 错误：getaddrinfo("112.4.64.141") failed: Name or service not known

办法：确保bindIp中多个IP中间逗号分隔时，没有空格：

```bash
bindIp: 127.0.0.1,112.4.64.141
```

(3) 错误：WiredTiger (13) [1523341777:968015][1095:0x7fa3cf097dc0], file:WiredTiger.wt, connection: /var/lib/mongo/WiredTiger.turtle: handle-open: open: Permission denied

办法：确认

/var/lib/mongo

其下的所有的文件，包括此处的WiredTiger.turtle，对于此处的mongod用户，要有权限

-> 可以考虑把所有文件的owner所有者，改为此处mongo 服务对应的所属用户：mongod:mongod

-> 以及后续还有另外一个相关的：

```bash
/var/lib/mongo/journal/
```

(4) 错误：Failed to unlink socket file /tmp/mongodb-32018.sock errno:1 Operation not permitted

办法：

删除这个sock文件：

```bash
sudo rm /tmp/mongodb-32018.sock
```

后，重启mongod服务，或直接重启服务器-》启动服务器会去启动mongod服务的
