# GridFS存储文件

MongoDB针对于文件，尤其是大文件，专门设计了一套接口，叫做：GridFS

此处总结一下GridFS的使用心得。

TODO：

* 如何基于Flask搭建一个文件下载服务，甚至可以支持断点续传功能。把之前相关代码贴过来。
* 把更多帖子内容整理至此
  * GridFS
    * [【已解决】GridFS保存文件时如何得到文件的id或_id](http://www.crifan.com/gridfs_save_file_how_get_file_id)
    * [【已解决】用Python去连接本地mongoDB去用GridFS保存文件](http://www.crifan.com/python_connect_local_mongodb_use_gridfs_save_file)
    * [【已解决】MongoDB的GridFS中基于文件名或id去下载文件](http://www.crifan.com/mongodb_gridfs_download_file_via_filename_or_id)
    * 【已解决】MongoDB的GridFS中只返回file的chunks的个数而不返回chunks.data
    * [【基本解决】Python中把wma、wav等格式音频转换为mp3](http://www.crifan.com/python_convert_wma_wav_audio_to_mp3_format)
    * [【未解决】Mongo中更新gridfs中的mp3文件的metadata信息且尽量保持id不变](http://www.crifan.com/mongo_update_gridfs_mp3_file_metadata_info_retain_id_not_change)
    * [【已解决】远程的mongoDB中GridFS报错：AttributeError GridFS object has no attribute totalSize](http://www.crifan.com/remote_mongodb_gridfs_attributeerror_gridfs_object_has_no_attribute_totalsize)
    * 【规避解决】Flask-PyMongo中如何查询gridfs中的文件
    * [【已解决】如何用PyMongo中的GridFS的put去保存添加文件](http://www.crifan.com/how_use_pymongo_gridfs_put_to_save_add_file)
    * [【已解决】PyMongo中GridFS的exists始终检测不到文件已存在](http://www.crifan.com/pymongo_use_gridfs_exists_check_always_can_not_file_already_existed)
    * [【已解决】Flask中Mongo的GridFS数据如何保存为绝对路径的下载文件地址](http://www.crifan.com/flask_mongo_gridfs_file_data_save_to_absolute_http_url_for_download)
    * [【已解决】MongoDB通过GridFS的API的put保存文件时添加额外信息](http://www.crifan.com/mongodb_via_gridfs_api_put_save_file_add_extra_info)
    * [【已解决】PyMongo的GridFS中使用fs的collection去put出错：TypeError Collection object is not callable](http://www.crifan.com/pymongo_gridfs_use_fs_collection_put_typeerror_collection_object_is_not_callable)
    * [【已解决】把本地mp3文件存入在线Mongo中且填写meta信息](http://www.crifan.com/local_mp3_file_save_into_online_mongodb_and_with_metadata_info)
    * [【已解决】Flask中连接远程MongoDB数据库的gridfs并返回查询到的文件数据](http://www.crifan.com/flask_connect_remote_mongodb_database_gridfs_return_query_file_data)
  * 和其中mongofiles相关的：
    * [【已解决】用mongofiles去删除GridFS中的文件](http://www.crifan.com/use_mongofiles_delete_gridfs_file)
    * [【无法也无须解决】用mongofiles给GridFS中添加文件时添加额外参数属性字段](http://www.crifan.com/use_mongofiles_add_extra_more_field_property_for_gridfs_file)
    * [【已解决】mongofiles中put保存和get下载获取时指定文件名](http://www.crifan.com/mongofiles_put_save_file_get_via_filename)

一些供参考的资料：

* GirdFS官网文档
  * [GridFS — MongoDB Manual 3.6](https://docs.mongodb.com/manual/core/gridfs/)
* Pymongo
  * GridFS的例子
    * [GridFS Example — PyMongo 3.6.1 documentation](http://api.mongodb.com/python/current/examples/gridfs.html)
  * GridFS的API
    * [gridfs – Tools for working with GridFS — PyMongo 3.6.1 documentation](http://api.mongodb.com/python/current/api/gridfs/index.html#gridfs.GridFS.put)
  * 相关的grid_file
    * [grid_file – Tools for representing files stored in GridFS — PyMongo 3.6.1 documentation](http://api.mongodb.com/python/current/api/gridfs/grid_file.html#gridfs.grid_file.GridOut)


## 一些GirdFS的心得

### 通过id查找gridfs中file文件

注意不是：

```bash
> db.fs.files.find({"id": "5b556ee47f4d38ba6a189222"})
> db.fs.files.find({"_id": "5b556ee47f4d38ba6a189222"})
```

而是`ObjectId("5b556ee47f4d38ba6a189222")`：

```bash
> db.fs.files.find({"_id": ObjectId("5b556ee47f4d38ba6a189222")})
{ "_id" : ObjectId("5b556ee47f4d38ba6a189222"), "contentType" : "audio/mpeg", "chunkSize" : 261120, "metadata" : { "song" : { "singers" : [ "ChuChu TV" ] }, "series" : { "number" : 0, "name" : "" }, "topics" : [ ], "storybook" : { "publisher" : "", "isFiction" : "未知", "lexileIndex" : "", "awards" : "", "authors" : [ ], "foreignCountry" : "" }, "keywords" : { "fromName" : [ "Finger", "Family" ], "other" : [ ], "fromContent" : [ "Daddy Finger" ] }, "name" : "Finger Family", "resourceType" : "song", "mainActors" : [ ], "contentAbstract" : "", "isSeries" : false, "fitAgeStart" : 3, "fitAgeEnd" : 6, "fileInfo" : { "isAudio" : true, "contentType" : "audio/mpeg", "name" : "Finger Family.mp3", "suffix" : "mp3" } }, "filename" : "Finger Family.mp3", "length" : 2604280, "uploadDate" : ISODate("2018-07-23T06:00:04.925Z"), "md5" : "946564effc4c0a835c55564377e7d819" }
>
```

### 删除文件

举例：

```bash
> db.fs.files.deleteOne({"_id": ObjectId("5b556ee47f4d38ba6a189222")})
{ "acknowledged" : true, "deletedCount" : 1 }
```

### 格式化带缩进美观的输出结果

后面加上：`.pretty()`

```bash
> db.fs.files.find({"_id": ObjectId("5b556ee47f4d38ba6a189222")}).pretty()
{
    "_id" : ObjectId("5b556ee47f4d38ba6a189222"),
    "contentType" : "audio/mpeg",
    "chunkSize" : 261120,
    "metadata" : {
        "song" : {
            "singers" : [
                "ChuChu TV"
            ]
        },
        "series" : {
            "number" : 0,
            "name" : ""
        },
        "topics" : [ ],
        "storybook" : {
            "publisher" : "",
            "isFiction" : "未知",
            "lexileIndex" : "",
            "awards" : "",
            "authors" : [ ],
            "foreignCountry" : ""
        },
        "keywords" : {
            "fromName" : [
                "Finger",
                "Family"
            ],
            "other" : [ ],
            "fromContent" : [
                "Daddy Finger"
            ]
        },
        "name" : "Finger Family",
        "resourceType" : "song",
        "mainActors" : [ ],
        "contentAbstract" : "",
        "isSeries" : false,
        "fitAgeStart" : 3,
        "fitAgeEnd" : 6,
        "fileInfo" : {
            "isAudio" : true,
            "contentType" : "audio/mpeg",
            "name" : "Finger Family.mp3",
            "suffix" : "mp3"
        }
    },
    "filename" : "Finger Family.mp3",
    "length" : 2604280,
    "uploadDate" : ISODate("2018-07-23T06:00:04.925Z"),
    "md5" : "946564effc4c0a835c55564377e7d819"
}
>
```

