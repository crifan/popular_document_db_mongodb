# 备份和恢复

MongoDB数据库，支持导出数据到文件，也支持从数据库文件导入，对应着备份和恢复。

与之对应，MongoDB提供了两个成对的配套的工具：
* `mongodump`和`mongorestore`
* `mongoexport`和`mongoimport`

下面详细介绍一下区别和具体用法。

## mongoimport/mongoexport和mongodump/mongorestore的区别

* 背景知识
  * JSON vs BSON
    * MongoDB内部数据保存用BSON
      * 原因：JSON是BSON的子集
        * -> 部分数据类型无法用JSON保存
          * -> 所以如果导出为JSON格式，可能会丢失部分复杂的数据类型的数据

|         | mongoimport/mongoexport | mongodump/mongorestore |
| ------- | ----------------------- | ---------------------- |
| 导出格式 | JSON | BSON |
| 主要用途 | 小规模的或部分的Mongo的数据的，测试期间的数据备份/恢复 | 简单且高效的 小型的MongoDB的数据库的备份/恢复 |
| 额外说明 | 导出数据时使用严格模式（[strict mode representation](https://docs.mongodb.com/manual/reference/mongodb-extended-json/)=[MongoDB Extended JSON](https://docs.mongodb.com/manual/reference/mongodb-extended-json/)）仅支持UTF-8编码的数据 | 不适合备份/恢复 大型MongoDB数据库<br/>默认是不拷贝local这个（特殊的）数据库 |
| 经验和结论 | 不支持普通导出单个db的所有的collection | 支持普通导出单个db的所有的collection<br/>建议：普通的，简单的，数据的备份和恢复，都还是用mongodump/mongorestore这套工具 |

* 其他相关
  * 如果是在线云平台部署的Mongo，备份/恢复可以使用
    * [MongoDB Atlas](https://www.mongodb.com/cloud/atlas?jmp=docs&_ga=2.206293584.238159457.1530236193-1039911943.1512195291)
      * Fully Managed MongoDB, hosted on AWS, Azure, and GCP | MongoDB
  * 如果是`replica sets`，备份/恢复可以使用：
    * [MongoDB Cloud Manager](https://docs.mongodb.com/manual/core/backups/#backup-with-mms)
    * 或
    * [Ops Manager](https://docs.mongodb.com/manual/core/backups/#backup-with-mms-onprem)
