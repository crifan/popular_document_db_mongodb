# 心得和总结

TODO:

* [【已解决】mongo命令行中如何删除文件](http://www.crifan.com/mongo_command_how_delete_file)
* [【已解决】把本地的音频字幕等数据存储到远程服务器的MongoDB数据库中](http://www.crifan.com/local_audio_subtitle_file_store_remote_server_mongodb_database)
* [【已解决】mongo中给普通数据库gridfs创建root的角色失败：Error couldn't add user No role named root@gridfs](http://www.crifan.com/mongodb_create_normal_gridfs_root_user_fail_error_couldnt_add_user_no_role_named_root_gridfs)
* [【已解决】本地mongo shell中连接远程加了权限控制的mongoDB](http://www.crifan.com/local_mongodb_shell_connect_remote_added_authority_mongodb)
* [【已解决】阿里云ECS服务器中已有的MongoDB的用户名密码和端口](http://www.crifan.com/aliyun_ecs_server_existed_mongodb_username_password_port)
* [【未解决】尝试用Mongo Management Studio去实现导入文件到Mongo的gridfs且带metadata信息](http://www.crifan.com/trial_mongo_management_studio_import_file_to_gridfs_with_metadata_info)
* [【已解决】确认服务器中MongoDB数据库是否有或已开启记录登录的日志](http://www.crifan.com/check_whether_mongodb_database_enabled_login_logging)
* [【已解决】确认服务器中MongoDB数据库是否有或已开启记录登录的日志](http://www.crifan.com/check_whether_mongodb_database_enabled_login_logging)
* [【已解决】MongoDB开启访问控制后currentOp出错：not authorized on admin to execute command](http://www.crifan.com/mongodb_enable_access_control_currentop_not_authorized_on_admin_to_execute_command)
* 【已解决】给MongoDB数据库新建用户和权限
* 【已解决】修改MongoDB的默认端口号27017为别的端口
* [【已解决】mongo的shell中find返回多个有限个数的结果](http://www.crifan.com/mongodb_mongo_shell_find_limit_return_number)
* [【已解决】公司Wi-Fi更换运营商导致IP变化导致远程Mongo连不上](http://www.crifan.com/company_wifi_ip_change_cause_remote_mongodb_connect_fail)
* [【已解决】连接远程mongoDB失败：Failed to connect to after 5000ms milliseconds giving up](http://www.crifan.com/connect_remote_mongodb_failed_to_connect_to_after_5000ms_milliseconds_giving_up)
* [【已解决】pymongo中用MongoClient去连接远程加了权限控制的mongoDB](http://www.crifan.com/pymongo_use_mongoclient_connect_remote_added_authorization_mongodb)
* [【已解决】用PyCharm的MongoDB插件连接远程MongoDB数据库](http://www.crifan.com/pycharm_mongodb_plugin_connect_remote_mongodb_database)
* [【已解决】MongoDB的用户的密码中包含@如何写URI](http://www.crifan.com/mongodb_username_password_contain_at_how_write_uri)
* [【已解决】给MongoDB限制IP访问](http://www.crifan.com/mongodb_add_restrict_ip_access)
* 【已解决】远程MongoDB新增dialog数据库并新增对应用户和权限
* [【已解决】PyCharm连接远程添加security的authorization的MongoDB出错：com.mongodb.MongoCommandExceptions: Command failed with error 13](http://www.crifan.com/pycharm_connect_remote_security_authorization_mongodb_error_com_mongodb_mongocommandexceptions_command_failed_with_error_13)
* [【已解决】Flask-PyMongo出错：RuntimeError Working outside of application context](http://www.crifan.com/flask_pymongo_runtimeerror_working_outside_of_application_context)
* [【已解决】pymongo的count()出错：pymongo.errors.ServerSelectionTimeoutError timed out](http://www.crifan.com/pymongo_count_pymongo_errors_serverselectiontimeouterror_timed_out)
* [【记录】通过阿里云ECS服务器安全组限制访问mongo的IP和端口](http://www.crifan.com/aliyun_ecs_security_group_limit_access_mongodb_ip_and_port)
* [【已解决】用PyCharm写Python的MongoDB代码并调试](http://www.crifan.com/pycharm_write_python_mongodb_code_and_debug)
* [【已解决】配置mongod以允许内网其他服务器访问mongo服务](http://www.crifan.com/config_mongod_allow_internal_network_other_server_access_mongo_service)
* [【已解决】PyCharm中安装MongoDB的插件：mongo4idea](http://www.crifan.com/pycharm_install_mongo_plugin_mongo4idea)

------

下面总结一些在MongoDB使用期间的心得和注意事项等内容。

先列出一些小的心得

## 导入数据之前，确保ID不能重复，否则会由于ID重复而无法覆盖

之前某次去恢复数据，故意没有删除本地之前已有（同样但是旧的）数据：

![mongodb_compass_existing_data](../assets/img/mongodb_compass_existing_data.png)

看看导入能否直接覆盖，结果由于ID重复而报错，覆盖失败：

```bash
  - E11000 duplicate key error collection: storybook.main index: _id_ dup key: { : ObjectId('5bd7be33bfaa44fe2c73bda2') }

^C2018-12-06T11:02:12.531+0800    signal 'interrupt' received; attempting to shut down
2018-12-06T11:02:12.560+0800    error: multiple errors in bulk operation:
  - E11000 duplicate key error collection: storybook.scholastic index: _id_ dup key: { : ObjectId('5bc71849bfaa4425b7ea8082') }
  - E11000 duplicate key error collection: storybook.scholastic index: _id_ dup key: { : ObjectId('5bc7184dbfaa4425b7ea8083') }
  - E11000 duplicate key error collection: storybook.scholastic index: _id_ dup key: { : ObjectId('5bc7184dbfaa4425b7ea8084') }
```
