# 总览

* 运行在内存中，所以非常快
* 用`key:value`形式存储

# 命令

## 普通值

* set
* get
* del
* exists
* keys 查找匹配的key
* flushall  删除所有
* ttl key 查看key对应的过期时间
* expire key time 设置key的过期时间time，单位s
* setex key time value 设置key，值为value，过期时间time

## Array相关

* lpush/rpush arrayName value
* lpop/rpop arrayName value
* lrange arrayName 0 -1 代表查看arrayName 中的所有值
* get 没法使用

## set

* sadd setName value
* smembers setName
* srem setName value

## hash

* hset hashName key value
* hget hashName key
* hgetall hashName 
* hdel hashName key
* hexists hashName key