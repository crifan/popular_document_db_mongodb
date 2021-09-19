# 索引

如果（MongoDB）数据库中的数据量很大，普通的查询，就会很（非常）耗时

而通过给数据库（的字段）建立索引，可以（极大地）提高查询速度

## 举例

建索引前后的效果（查询速度）对比：

* `shortLink.gameShortLink`：数据量：**270多万**
  * 要查询的字段：shortLink
  * 查询代码：
    * `existedDuplicatedItem = mongoCollectionShortlink.find_one({"shortLink": curShortLink})`
* 没有索引：查询耗时 **10秒**左右
* 建索引：
  * `db.gameShortLink.createIndex({shortLink: 1})`
* 建索引后：查询耗时 不到**0.01秒**
