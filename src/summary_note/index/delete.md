# 删除索引

## mongo shell

```bash
db.gameShortLink.dropIndex({gameShortLink:1})
```

举例：

![mongo_drop_index](../../assets/img/mongo_drop_index.png)

## MongoDB Compass

MongoDB Compass：

点击索引右边的 垃圾箱的按钮

![compass_index_trash_icon](../../assets/img/compass_index_trash_icon.png)

> #### Note:: 默认`_id`的index无法删除
> 
> `Indexes`中，默认有个`_id`的`index`，是系统自带的，无法删除 -> 所以后面没有垃圾桶按钮 -> 是正常现象。

举例：

一共5个索引：

去删除2个：

![compass_drop_index_first](../../assets/img/compass_drop_index_first.png)

![compass_drop_index_2nd](../../assets/img/compass_drop_index_2nd.png)

还剩3个：

![compass_remain_three_index](../../assets/img/compass_remain_three_index.png)
