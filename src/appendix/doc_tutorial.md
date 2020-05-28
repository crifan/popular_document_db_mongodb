# 教程和文档

此处整理一些关于MongoDB的官方和非官网的各种有用资料，供需要时查询和参考。

## MongoDB官网资料

官方文档入口：

[The MongoDB 4.0 Manual — MongoDB Manual](https://docs.mongodb.com/manual/)

官网还有个系列教程：

* [MongoDB University](https://university.mongodb.com)

部分细节内容：

* 更新数据
  * [db.collection.update() — MongoDB Manual](https://docs.mongodb.com/manual/reference/method/db.collection.update/)
* 查询
  * [Query Documents — MongoDB Manual](https://docs.mongodb.com/manual/tutorial/query-documents/)
  * [Query on Embedded/Nested Documents — MongoDB Manual](https://docs.mongodb.com/manual/tutorial/query-embedded-documents/)
  * [Query an Array — MongoDB Manual](https://docs.mongodb.com/manual/tutorial/query-arrays/)
  * [Query an Array of Embedded Documents — MongoDB Manual](https://docs.mongodb.com/manual/tutorial/query-array-of-documents/)
* 查询期间条件组合
  * [$or — MongoDB Manual](https://docs.mongodb.com/manual/reference/operator/query/or/)
  * [Read Data using Operators and Compound Queries](https://docs.mongodb.com/guides/server/read_operators/#write-an-or-query)
* 正则搜索
  * [$regex](https://docs.mongodb.com/manual/reference/operator/query/regex/#op._S_regex)
* 列表查询
  * [Array Query Operators — MongoDB Manual](https://docs.mongodb.com/manual/reference/operator/query-array/)
* 聚合
  * [Aggregation — MongoDB Manual 3.4](https://docs.mongodb.com/manual/aggregation/)
* Driver的
  * [MongoDB Drivers and Client Libraries — MongoDB Manual 3.6](https://docs.mongodb.com/manual/applications/drivers/)
* 用户和权限认证
  * Authentication
    * [Authentication — MongoDB Manual 3.6](https://docs.mongodb.com/manual/core/authentication/)
    * [authenticate — MongoDB Manual 3.6](https://docs.mongodb.com/manual/reference/command/authenticate/#dbcmd.authenticate)
  * Users
    * [Users — MongoDB Manual 3.6](https://docs.mongodb.com/manual/core/security-users/#user-authentication-database)
  * 权限
    * RBAC
      * [Role-Based Access Control — MongoDB Manual 3.6](https://docs.mongodb.com/manual/core/authorization/)
    * 角色
      * [Built-In Roles — MongoDB Manual 3.6](https://docs.mongodb.com/manual/reference/built-in-roles/#built-in-roles)
      * [User-Defined Roles — MongoDB Manual 3.6](https://docs.mongodb.com/manual/core/security-user-defined-roles/#user-defined-roles)
      * [grantRolesToUser — MongoDB Manual 3.6](https://docs.mongodb.com/manual/reference/command/grantRolesToUser/#dbcmd.grantRolesToUser)
  * Resource
    * [Resource Document — MongoDB Manual 3.6](https://docs.mongodb.com/manual/reference/resource-document/)
  * 新建用户
    * [createUser — MongoDB Manual 3.6](https://docs.mongodb.com/manual/reference/command/createUser/#dbcmd.createUser)

## 第三方资料

官网的（部分完成的）中文翻译：

* mongoing.com
  * MongoDB 4.2 手册
    * [Documentation | MongoDB中文社区](https://mongoing.com/docs4.2)
  * MongoDB 3.4 手册
    * [安装MongoDB — MongoDB Manual 3.4](https://mongoing.com/docs/)

* 极客学院
  * [mongodb 数据库 (1) - 《从零开始学 Python》(第二版) - 极客学院Wiki](http://wiki.jikexueyuan.com/project/start-learning-python/232.html)

## Mongo Shell资料

Mongo Shell的资料：
* 英文
  * [mongo Shell Quick Reference — MongoDB Manual 3.6](https://docs.mongodb.com/manual/reference/mongo-shell/)
* 中文
  * [mongo shell — MongoDB Manual 3.4](http://www.mongoing.com/docs/mongo.html)
    * 注：翻译未必是完整的，且不一定是最新版本
