# 停止MongoDB

想要去停止MongoDB的服务端。

对于之前是正常安装方式

`brew install mongodb-community`

则去停止运行方式是

`brew services stop mongodb-community`

不过之前遇到过特殊情况，试了各种方式都无法直接关闭掉，经研究最后是用：

`sudo mongod -f /etc/mongod.conf --shutdown`

输出：

`killing process with pid: 30213`

才算真正的关闭了MongoDB。

详见：

【已解决】CentOS中如何彻底真正关闭mongod的服务
