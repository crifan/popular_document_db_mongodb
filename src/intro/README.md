# MongoDB简介

下面针对MongoDB做一下简要介绍：

* MongoDB
  * Logo
    * ![mongodb_logo](../assets/img/mongodb_logo.jpg)
  * 一句话描述：**一种主流的文档数据库**
    * 一种：还有其他的
      * 其他文档型数据库：`CouchDB`、`Amazon DynamoDB`、`Couchbase`、`MarkLogic`
    * 文档数据库：
      * = `面向文档的数据库` = `Document-Oriented Datdabase`
      * 范畴：属于非关系型数据库
        * 常称为：`NoSQL`
      * 与之对应：
        * (传统的)关系型数据库：`MySQL`
        * 其他的NoSQL
          * 键值对(K/V)数据库：`redis`、`Cassandra`、`LevelDB`
          * 图数椐库：`Neo4j`
          * 时序数据库：`InfluxDB`
          * （全文）搜索（数据库）引擎：`ElasticSearch`、`Solr`
          * 列式数据库：`HBase`
      * 数据格式
        * 主要：`JSON`
          * 引申：`BSON`
          * 其他：`XML`
      * 优势
          * 修改数据和结构很方便
            * 直接修改JSON数据本身
            * 对比：传统MySQL需要改表结构
            * 引申出：容易兼容历史数据
              * 字段不存在只是空值不会报错
          * 复杂JSON可以描述复杂（嵌套）的数据结构
      * 适用场景
        * 数据量很大或者未来会变得很大
        * 表结构不明确，且字段在不断增加
      * 不适用场景
        * 在不同的文档上需要添加事务支持
          * 文档数据库不支持文档间的事务
        * 多个文档直接需要复杂查询
          * 例如join
  * 起源
    * 移动互联网兴起
      * 不仅：数据量大（高并发），架构复杂
      * 还要：快速响应
    * 结论：传统MySQL类关系型数据库无法满足
    * 出现：关系型数据库
      * 其中最流行：`MongoDB`
        * 胜出关键：易用、架构良好、功能丰富
  * 概述
    * 底层实现：`C++`
    * 支持平台：`Windows`、`Mac`、`Linux`、`Solaris`等
    * 编程接口API：常见语言都支持
      * `C`、`C++`、`C#`、`Go`、`Java`、`Node.js`、`Perl`、`PHP`、`Python`、`Ruby`、`Rust`、`Scala`、`Swift`
  * 优势
    * 高性能
    * 富查询语言（支持 CRUD、数据聚合、文本搜索和地理空间查询）
    * 高可靠性
    * 自动伸缩架构
    * 支持多存储引擎
