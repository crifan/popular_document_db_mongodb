# Cursor not found

用pymongo期间可能会报错：

`pymongo.errors.CursorNotFound: Cursor not found`

原因：

此处的：

```python
for eachDialog in dialogCollection.find():
```

find会返回多个数据，而这些数据的处理时间，超过了默认最长时间**10分钟**，所以超时报错了。

解决办法：

去掉超时时间的设置，加上参数`no_cursor_timeout=True`

代码改为：

```python
# for eachDialog in dialogCollection.find():
cursor = dialogCollection.find(no_cursor_timeout=True)
for eachDialog in cursor:
    yield eachDialog
cursor.close()
```

即可。
