# 基本用法

安装好了MongoDB后，接下来去搞清楚如何操作MongoDB。

操作和使用MongoDB的基本逻辑都是：

* 启动MongoDB的服务端
* 用某种Client去操作MongoDB
  * 根据类型分，常见Client有3种方式
    * 命令行
      * MongoDB自带：`mongo shell`
        * 提供了一个最基础的操作数据库的方式
    * GUI图形界面工具
      * 通过图形界面工具去查看和操作数据会更加直观和方便
        * 如`MongoDB Compass`、`Robot 3T`等
    * API
      * 用各种语言的代码，通过API操作数据库
        * 如`Python`、`Java`等

接下来分别去介绍MongoDB的服务器和客户端。

## 基本概念

MongoDB中的一些概念和术语的含义，可以通过和SQL对比去理解：

| SQL术语和概念 | MongoDB术语概念 | 解释和说明 |
| ----------- | -------------- | -------- |
| database    | database | 数据库 |
| table       | collection | 数据库表 / 集合 |
| row         | document | 数据记录行 / 文档 |
| column      | field    | 数据字段 / 域 |
| index       | index    | 索引 |
| table joins |          | 表连接，MongoDB不支持 |
| primary key | primary key | 主键，MongoDB自动将`_id`作为主键 |
