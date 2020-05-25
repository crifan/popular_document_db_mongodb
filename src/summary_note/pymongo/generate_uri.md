# 生成URI

在开发期间，可能会涉及到，从配置中生成MongoDB的URI

下面代码供参考使用

```python
def generateMongoUri(host=None,
                port=None,
                isUseAuth=False,
                username=None,
                password=None,
                authSource=None,
                authMechanism=None):
    """"generate mongodb uri"""
    mongodbUri = ""

    if not host:
        # host = "127.0.0.0"
        host = "localhost"

    if not port:
        port = 27017

    mongodbUri = "mongodb://%s:%s" % (
        host, \
        port
    )
    # 'mongodb://localhost:27017'
    # 'mongodb://ip:27017'

    if isUseAuth:
        mongodbUri = "mongodb://%s:%s@%s:%s" % (
            quote_plus(username), \
            quote_plus(password), \
            host, \
            port \
        )
        print(mongodbUri)

        if authSource:
            mongodbUri = mongodbUri + ("/%s" % authSource)
            print("mongodbUri=%s" % mongodbUri)

        if authMechanism:
            mongodbUri = mongodbUri + ("?authMechanism=%s" % authMechanism)
            print("mongodbUri=%s" % mongodbUri)

    print("return mongodbUri=%s" % mongodbUri)
    #mongodb://username:quoted_password@host:port/authSource?authMechanism=authMechanism
    #mongodb://localhost:27017

    return mongodbUri
```

调用举例：

```python
from pymongo import MongoClient

mongoUri = generateMongoUri(
    host=MONGODB_HOST,
    port=int(MONGODB_PORT),
    username=MONGODB_USERNAME,
    password=MONGODB_PASSWORD,
    authSource=MONGODB_AUTH_SOURCE,
    authMechanism=MONGODB_AUTH_MECHANISM,
)
mongoClient = MongoClient(mongoUri)
```
