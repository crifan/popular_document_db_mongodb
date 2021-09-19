# 搜索查询

## 查询：子字段，嵌套字段

子字段，嵌套字段，用`parentField.childField`

### pymongo代码

#### find_one：搜索特定嵌套值

查询：`parsedGame.realGameName`是某个值，且字段`parsedGame.gameTheme`存在

```python
queryDict = {
  "parsedGame.realGameName": realGameName,
  "parsedGame.gameTheme": {"$exists": True},
}
parsedGameThemeItem = mongoCollectionShortlink.find_one(queryDict)
```

## find+sort：设置时间范围等查询条件

代码：

```python
import pymongo
import datetime

curTime = datetime.datetime.now()
# timeKeyName = "start_time"
timeKeyName = "finish_time"
earliestTime = curTime - datetime.timedelta(days = 180)
userEvaluations = evalCollection.find({
    "user_id": userId,
    timeKeyName: {
        "$gte": earliestTime,
        "$lte": curTime
    }
}).sort(timeKeyName, pymongo.DESCENDING).limit(20)
userEvaluationList = list(userEvaluations)
userEvaluationList.reverse()
historyList = []
for eachEvaluation in userEvaluationList:
    if "overall_level" in eachEvaluation:
        curTimeLevelDict = {
            "time": eachEvaluation[timeKeyName],
            "overall_level": eachEvaluation["overall_level"]
        }
        historyList.append(curTimeLevelDict)
log.debug("historyList=%s", historyList)
```

实现了期望的逻辑：

* 去mongodb查询
  * 最早半年前，最晚当前时间
  * 结果中再去根据时间倒序
  * 然后再去取最多20个
    * 从而实现：最近半年，最多20个，只不过顺序是反的而已
* 对于时间倒序后的结果，再调换顺序

即可得到需要的：最近半年的，最多20个，按照时间升序排列

然后输出希望的结果：

![postman output mongo search result](../../../assets/img/postman_mongodb_search_result.png)

## find用法举例

### 查看集合gameShortLink_2010816现在一共有多少条数据

`Mongo shell`中：

```bash
db.gameShortLink_2010816.find().count()
```

效果：

![mongo_shell_find_count](../../../assets/img/mongo_shell_find_count.png)

### 查询：特定条件的数据有多少

`Mongo shell`中：

```bash
db.gameShortLink_2010816.find("parsedGame.realGameName":"天龙八部").count()
```

![mongo_shell_find_specifc_1](../../../assets/img/mongo_shell_find_specifc_1.png)

![mongo_shell_find_specifc_2](../../../assets/img/mongo_shell_find_specifc_2.png)

后续其他例子：

```bash
db.gameShortLink.find({"input.generateDate":"20210816"}).count()
```

![mongo_shell_find_specifc_3](../../../assets/img/mongo_shell_find_specifc_3.png)

### 查询单条数据详情

```bash
db.gameShortLink_2010816.find({"shortLink":"http://xuz0.cn/9tzScdKT?0ef6"}).pretty()
```

![mongo_shell_find_single_1](../../../assets/img/mongo_shell_find_single_1.png)

![mongo_shell_find_single_2](../../../assets/img/mongo_shell_find_single_2.png)
