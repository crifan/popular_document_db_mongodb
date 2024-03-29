# 主流文档型数据库：MongoDB

* [前言](README.md)
* [简介](intro/README.md)
* [安装](install/README.md)
  * [Mac中安装MongoDB](install/mac_install_mongodb.md)
* [基本用法](basic_usage/README.md)
  * [Server端](basic_usage/server.md)
  * [Client端](basic_usage/client/README.md)
    * [命令行shell](basic_usage/client/shell.md)
    * [GUI工具](basic_usage/client/gui/README.md)
      * [MongoDB Compass](basic_usage/client/gui/mongodb_compass.md)
    * [API](basic_usage/client/api/README.md)
      * [PyMongo](basic_usage/client/api/pymongo.md)
* [高级用法](advance_usage/README.md)
  * [IP限制](advance_usage/ip_restrict.md)
  * [用户和权限](advance_usage/user_permission.md)
* [心得和总结](summary_note/README.md)
  * [备份和恢复](summary_note/backup_restore/README.md)
    * [mongodump和mongorestore](summary_note/backup_restore/dump_restore.md)
    * [mongoexport和mongoimport](summary_note/backup_restore/export_import.md)
  * [查看当前MongoDB信息](summary_note/check_mongo_info.md)
  * [连接MongoDB](summary_note/connect_mongo/README.md)
    * [PyMongo生成URI](summary_note/connect_mongo/generate_uri.md)
    * [连接远程MongoDB](summary_note/connect_mongo/remote.md)
  * [数据库和集合](summary_note/db_collection/README.md)
    * [新建空数据库和集合](summary_note/db_collection/create_empty.md)
    * [操作集合](summary_note/db_collection/operate_collection.md)
  * [记录](summary_note/record/README.md)
    * [搜索查询](summary_note/record/find_query/README.md)
      * [高级搜索](summary_note/record/find_query/advanced.md)
    * [新建记录](summary_note/record/new_insert.md)
    * [更新记录](summary_note/record/update.md)
    * [删除记录](summary_note/record/delete.md)
  * [运行mongo命令](summary_note/run_mongo_cmd.md)
  * [GridFS存储文件](summary_note/gridfs_file.md)
  * [索引](summary_note/index/README.md)
    * [查看索引](summary_note/index/check.md)
    * [创建索引](summary_note/index/create.md)
    * [重建索引](summary_note/index/reindex.md)
    * [删除索引](summary_note/index/delete.md)
  * [MongoDB Compass心得](summary_note/mongodb_compass/README.md)
* [坑](pitfall/README.md)
  * [停止MongoDB](pitfall/stop_mongodb.md)
  * [Cursor not found](pitfall/cursor_not_found.md)
  * [参数_id是不是字符串](pitfall/para_is_objectid.md)
  * [不要在admin中创建普通用户](pitfall/not_create_user_in_admin.md)
* [附录](appendix/README.md)
  * [教程和文档](appendix/doc_tutorial.md)
  * [参考资料](appendix/reference.md)
