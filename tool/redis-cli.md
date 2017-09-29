# refer
	http://doc.redisfans.com/
	
# redis usage

## key
	1、help set
	  SET key value [EX seconds] [PX milliseconds] [NX|XX]
	  summary: Set the string value of a key
	  since: 1.0.0
	  group: string
	  
	  set test 10
	  set test 10 EX 60 60秒过期
	  

## list
	1. 查询list
		lrange queues:importQueue 0 -1
	2. 从队列头pop元素，在队列里删除该元素
		lpop queues:importQueue
	3. 清空队列
		ltrim queues:importQueue 1 0
		
## set
## zset（sorted set）操作相关
	1. 查询
		zrange queues:importQueue:reserved 0 -1
	2. 删除所有元素
		zrem queues:importQueue:reserved 0 -1
## hash
	1. 查看hash中的值和value
		hgetall job_result
		1) "importQueue_p0yzx4AQEcVefgUnvZ9nLLiUprwP6ff5"
		2) "{\"job_status\":1}"
	2. 删除值
		hDel job_result importQueue_p0yzx4AQEcVefgUnvZ9nLLiUprwP6ff5
		(integer) 1