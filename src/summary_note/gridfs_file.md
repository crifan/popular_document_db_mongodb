# GridFS存储文件

MongoDB针对于文件，尤其是大文件，专门设计了一套接口，叫做：GridFS

此处总结一下GridFS的使用心得。

TODO：

如何基于Flask搭建一个文件下载服务，甚至可以支持断点续传功能。把之前相关代码贴过来。


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

