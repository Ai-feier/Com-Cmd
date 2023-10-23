常用数据结构（红黑树,b树等）：
```bash
go get github.com/emirpasic/gods
```

opentelemetry (可观测性)
```bash
go get go.opentelemetry.io/otel
```

## web 
### gin
```bash
# gin
go get github.com/gin-gonic/gin
# gin-session
go get github.com/gin-contrib/sessions
```

优质 session 结构体定义
```bash
go get github.com/gorilla/sessions
```

## 数据库
### sqlmock
```bash
go get github.com/DATA-DOG/go-sqlmock
```

## 测试相关
testify (assert/) 
```bash
go get github.com/stretchr/testify/assert
assert.Equal(t, expected, actual)  # 函数方法无法比较，只能使用反射获取值后比较

github.com/stretchr/testify/require
require.NoError(t, err)
```


## 缓存
go-redis
```bash
go get github.com/redis/go-redis/v9
```

优质缓存 go-cache
```bash
go get github.com/patrickmn/go-cache
```

lru
```bash
go get github.com/hashicorp/golang-lru
```

bytebufferpoll
```bash
go get github.com/valyala/bytebufferpool 
```
![Alt text](image.png)
![Alt text](image-2.png)
![Alt text](image-1.png)