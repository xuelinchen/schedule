redis
==========

refer
-------

    http://doc.redisfans.com/
    http://www.redis.net.cn/tutorial/3501.html
    http://www.cnblogs.com/liuconglin/p/5847568.html
    这是一篇讲各种数据类型的应用场景的文章，可做参考：http://blog.csdn.net/gaogaoshan/article/details/41039581/
    redislive 是一款redis使用状态的软件 具体可参考：http://blog.csdn.net/hz_blog/article/details/41822825
    这篇文章讲了此工具如何安装 具体不做说明 地址：http://www.cnblogs.com/hepingqingfeng/p/6107809.html

install&research
-----------------

安装
^^^^^^^^
| $ wget http://download.redis.io/releases/redis-3.2.6.tar.gz
| $ tar xzf redis-3.2.6.tar.gz
| $ cd redis-3.2.6
| $ make
| $ src/redis-server 运行redis服务
| $ src/redis-cli
| redis> set foo bar
| OK
| redis> get foo
| "bar"

配置
^^^^^^^^^^^

* redis配置 ::

    vi redis.conf
    bind 10.0.0.23
    daemonize yes
    logfile "/var/pbx/tmp/Logs/redis/redis_6379.log"
    dbfilename dump_6379.rdb
    //生产环境
    rename-command FLUSHALL ""
    rename-command FLUSHDB ""
    rename-command KEYS ""
    rename-command CONFIG ""
    maxmemory 2gb //占用的最大内存 <span style='color:green;font-weight:bold;'><一般推荐Redis设置内存为最大物理内存的四分之三,设置最大内存后一般需设置过期策略></span>
    appendonly yes
    appendfilename "appendonly_6379.aof"
    requirepass "prettydogKnockTheDoor" //需要密码才能访问
    将redis加入到系统自启动的脚本中
    
    Redis使用超过设置的最大值
    打开debug模式下的页面，提示错误：OOM command not allowed when used memory > ‘maxmemory’.
    设置了maxmemory的选项，redis内存使用达到上限。可以通过设置LRU算法来删除部分key，释放空间。默认是按照过期时间的,如果set时候没有加上过期时间就会导致数据写满maxmemory。
    如果不设置maxmemory或者设置为0，64位系统不限制内存，32位系统最多使用3GB内存。
    
    LRU是Least Recently Used 近期最少使用算法。
    volatile-lru -> 根据LRU算法生成的过期时间来删除。
    allkeys-lru -> 根据LRU算法删除任何key。
    volatile-random -> 根据过期设置来随机删除key。
    allkeys->random -> 无差别随机删。
    volatile-ttl -> 根据最近过期时间来删除（辅以TTL）
    noeviction -> 谁也不删，直接在写操作时返回错误。

.. note::
    详细配置可参考文章：`这篇文章主要讲的是配置的含义和优化 <http://www.tuicool.com/articles/MvMBf2>` 

* iptable配置 ::

    考虑到安全，不允许外网用户访问redis
    
    10.0.0.0/24 表示C类地址 24掩码前面的0
    iptables -A INPUT ! -s 10.0.0.0/24 -p tcp --dport 6379 -j DROP //拒绝所有非本网段的机器访问redis
    iptables -A INPUT ! -s 10.0.0.0/24 -p udp --dport 6379 -j DROP
    保存iptables规则下次启动时自动启动规则
    iptables-save > /etc/iptables.up.rules //保存规则
    vi /etc/network/interfaces
    pre-up iptables-restore < /etc/iptables.up.rules  //恢复规则
    iptables -F
    重启网络
    /etc/init.d/networking restart
    iptables -L -v
    重启机器
    iptables -L -v
    可以看到刚刚配置的规则都在

测试
^^^^^^^^

* redis数据类型测试 ::

    设置值，获取值
    * set foo "bar"
    * get foo
    * expire foo 120
    * ttl foo 查询过期时间 返回-2值不存在 -1 值永不过期
    
    自增变量
    set connections 10
    incr connections
    del connections
    
    list 队列
    rpush friends "alice" 添加到队尾
    rpush friends "bob"
    lpush friends "sam" 添加到队首
    lrange friends 0 -1 获取全部队列
    lrange friends 0 1 获取0-1
    llen friends 队列长度
    lpop friends 弹出首个对象
    rpop friends 弹出队尾对象
    
    set 与list相似，但没有顺序且对象只能出现一次
    sadd superpowers "flight"   添加值
    sadd superpowers "x-ray vision"
    sadd superpowers "reflexes"  
    srem superpowers "reflexes"  删除值
    sismember superpowers "reflexes"  判断是否存在0不存在1存在
    smembers superpowers
    sadd birdpowers "flight"
    sadd birdpowers "pecking"
    sunion superpowers birdpowers 合并set
    
    sorted set 可排序set
    zadd hackers 1940 "alan key"
    zadd hackers 1980 "Grace hopper"
    zadd hackers 1945 "richard stallman"
    zadd hackers 1944 "macker"
    zrange hackers 0 -1
    
    hashes
    hset user:1000 name "john smith"
    hset user:1000 email "john.smith@example.com"
    hset user:1000 password "s3cret"
    hgetall user:1000 
    HMSET user:1001 name "Mary Jones" password "hidden" email "mjones@example.com"
    SET user:1000 visits 10
    HINCRBY user:1000 visits 1 加1
    hdel user:1000 visits 删除值

.. note::
    `测试参考文档 <http://www.cnblogs.com/silent2012/p/4514901.html>`

* 安全测试 

    * 只有使用密码才能访问 ::
    
        root@1604developer:/var# telnet 10.0.0.23 6379
        Trying 10.0.0.23...
        telnet: Unable to connect to remote host: Connection refused
        root@1604developer:/var# telnet 10.0.0.23 6379
        Trying 10.0.0.23...
        Connected to 10.0.0.23.
        Escape character is '^]'.
        auth prettydogKnockTheDoor
        +OK
        keys *
        *0   
    
    * 指定ip才能访问 ::
    
        iptables -L -v --line-num
        配置iptables只允许10.0.0.1-32的ip地址访问redis
        iptables -A INPUT ! -s 10.0.0.0/27 -p tcp --dport 6379 -j DROP
        iptables -A INPUT ! -s 10.0.0.0/27 -p udp --dport 6379 -j DROP
        在本机访问
        root@ubuntu1204base:/home/cxl/redis/redis-3.2.6# telnet 10.0.0.23 6379
        Trying 10.0.0.23...
        Connected to 10.0.0.23.
        Escape character is '^]'.
        auth prettydogKnockTheDoor
        +OK
        keys *
        *0
        在10.0.0.237机器访问
        root@php1 16:51:00:~# telnet 10.0.0.23 6379
        Trying 10.0.0.23...
        如果策略修改为
        iptables -A INPUT ! -s 10.0.0.0/27 -p tcp --dport 6379 -j REJECT
        iptables -A INPUT ! -s 10.0.0.0/27 -p udp --dport 6379 -j REJECT
        再次在10.0.0.237机器访问
        root@php1 16:53:23:~# telnet 10.0.0.23 6379
        Trying 10.0.0.23...
        telnet: Unable to connect to remote host: Connection refused

* 数据恢复测试 

    * kill redis 进程 ::
    
        root@ubuntu1204base:/home/cxl/redis/redis-3.2.6# src/redis-cli -h 10.0.0.23
        10.0.0.23:6379> auth prettydogKnockTheDoor
        OK
        10.0.0.23:6379> set "first Key" "first Value"
        OK
        10.0.0.23:6379> get "first Key"
        "first Value"
        10.0.0.23:6379> quit
        root@ubuntu1204base:/home/cxl/redis/redis-3.2.6# ps -aux |grep redis
        Warning: bad ps syntax, perhaps a bogus '-'? See http://procps.sf.net/faq.html
        root      4418  0.1  0.3  36124  1564 ?        Ssl  17:54   0:00 src/redis-server 10.0.0.23:6379
        root      4497  0.0  0.1   9380   936 pts/2    S+   17:57   0:00 grep --color=auto redis
        root@ubuntu1204base:/home/cxl/redis/redis-3.2.6# kill 4418
        root@ubuntu1204base:/home/cxl/redis/redis-3.2.6# src/redis-server redis.conf
        root@ubuntu1204base:/home/cxl/redis/redis-3.2.6# src/redis-cli -h 10.0.0.23
        10.0.0.23:6379> auth prettydogKnockTheDoor
        OK
        10.0.0.23:6379> get "first Key"
        "first Value"
        10.0.0.23:6379> quit
    
    * 重启redis进程，查看redis数据 ::
    
        root@ubuntu1204base:/home/cxl/redis/redis-3.2.6# reboot
        root@ubuntu1204base:/home/cxl/redis/redis-3.2.6# src/redis-server redis.conf
        root@ubuntu1204base:/home/cxl/redis/redis-3.2.6# src/redis-cli -h 10.0.0.23
        10.0.0.23:6379> auth prettydogKnockTheDoor
        OK
        10.0.0.23:6379> get "first Key"
        "first Value"
        10.0.0.23:6379> 

* 性能测试 

    * 内存占用测试 ::
    
        vi redis.conf
        maxmemory 1m //为了测试方便设置为1mb
        vi addKey.sh 
        # !/usr/bin/bash
        
        echo "AUTH prettydogKnockTheDoor"
        sleep 1
        
        outstr=""
        value10="1"
        j=700
        while [ $j -gt 690 ]
        do
        for i in {100..199}
        do
        outstr="${outstr}set key$j-$i ${value10}\r\n"
        done
        printf "$outstr"
        outstr=""
        j=`expr $j - 1`
        done  
        这个脚本往redis服务器加入1000个key，其中Key值10个字节，value值一个字节
        
        10.0.0.23:6379> flushall //清空redis
        10.0.0.23:6379> info
        # Memory
        used_memory:821552
        used_memory_human:803.70K
        看出来，redis初始状态就占用803.70k，所以设置1m最大内存，实际可用应该是200k左右
        运行脚本插入1000个键值
        
        >方式1
        ./addkey.sh | nc 10.0.0.23 6379
        
        >方式2
        ./addkey.sh | ../redis-3.2.6/src/redis-cli -h 10.0.0.23 -a prettydogKnockTheDoor --pipe
        All data transferred. Waiting for the last reply...
        Last reply received from server.
        errors: 0, replies: 100001
        
        
        10.0.0.23:6379> info
        # Memory
        used_memory:871184
        used_memory_human:850.77K
            
        占用内存47k，所以11字节的key+value大概占用47字节的内存空间
        修改一下脚本加入4000key
        -OOM command not allowed when used memory > 'maxmemory'.
        10.0.0.23:6379> dbsize
        (integer) 3109
        只加入了3109键值
        used_memory:980120
        used_memory_human:957.15K
    
    * 大并发测试 ::
    
        50个客户端发送100000请求每个请求3个字节，看起来redis很给力
        root@ubuntu1204base:/home/cxl/redis/redis-3.2.6# src/redis-benchmark -h 10.0.0.23 -q （<span style='color:red;font-weight:bold'>本机测试</span>） 
        PING_INLINE: 75131.48 requests per second
        PING_BULK: 74074.07 requests per second
        SET: 76277.65 requests per second
        GET: 74349.44 requests per second
        INCR: 75815.01 requests per second
        LPUSH: 74074.07 requests per second
        RPUSH: 73421.44 requests per second
        LPOP: 74794.31 requests per second
        RPOP: 74571.22 requests per second
        SADD: 74906.37 requests per second
        SPOP: 74794.31 requests per second
        LPUSH (needed to benchmark LRANGE): 73367.57 requests per second
        LRANGE_100 (first 100 elements): 72621.64 requests per second
        LRANGE_300 (first 300 elements): 74515.65 requests per second
        LRANGE_500 (first 450 elements): 74019.25 requests per second
        LRANGE_600 (first 600 elements): 76277.65 requests per second
        MSET (10 keys): 73746.31 requests per second
        
        <span style='color:red;font-weight:bold'>内网跨服务器测试</span>
        PING_INLINE: 13596.19 requests per second
        PING_BULK: 13696.75 requests per second
        SET: 13676.15 requests per second
        GET: 13738.15 requests per second
        INCR: 13738.15 requests per second
        LPUSH: 13664.94 requests per second
        RPUSH: 13585.11 requests per second
        LPOP: 13730.61 requests per second
        RPOP: 13719.30 requests per second
        SADD: 13702.38 requests per second
        SPOP: 13691.13 requests per second
        LPUSH (needed to benchmark LRANGE): 13655.61 requests per second
        LRANGE_100 (first 100 elements): 13650.01 requests per second
        LRANGE_300 (first 300 elements): 13648.15 requests per second
        LRANGE_500 (first 450 elements): 13550.14 requests per second
        LRANGE_600 (first 600 elements): 13674.28 requests per second
        MSET (10 keys): 13220.52 requests per second
 
.. note::
    结论：本机访问是内网跨服务器访问各类请求每秒执行数量五倍多


* 监控性能 ::
    
    >>top监控
     root@ubuntu1204base:/home/cxl/redis/redis-3.2.6#  top -b -p 16417 -n 2|egrep "16417|PID"|tail -2
     PID USER      PR  NI  VIRT  RES  SHR S %CPU %MEM    TIME+  COMMAND                                                                
     16417 root      20   0 42268 8980 1240 S  0.0  1.8   0:02.70 redis-server  
    
    >>redis-cli info监控
    
     root@ubuntu1204base:/home/cxl/redis/redis-3.2.6# src/redis-cli -h 10.0.0.23 -a prettydogKnockTheDoor info|grep used_memory
     used_memory:7470144
     used_memory_human:7.12M
     used_memory_rss:9023488
     used_memory_rss_human:8.61M
     used_memory_peak:7470144
     used_memory_peak_human:7.12M
     used_memory_lua:37888
     used_memory_lua_human:37.00K

代码示例
^^^^^^^^^^^^^

* predis ::

    好处是不需要安装php扩展，直接require就行了
    git clone git://github.com/nrk/predis.git
    wget https://github.com/nrk/predis/archive/v1.1.1.tar.gz
    拷贝到Thinkphp vendor目录下
    
    示例代码
    <pre>
           require_once VENDOR_PATH."predis/autoload.php";
           try {
               $redis = new Predis\Client("redis://127.0.0.1:6379/");
               $redis->set('library', 'predis1');
               $retval = $redis->get('library1');
               var_export($retval);
           } catch (Exception $e) {
               var_dump($e->getMessage());
           }
           
    </pre>
    
    predis函数集：http://www.open-open.com/lib/view/open1355830836135.html

    
usage
---------

* key ::

    1、help set
    SET key value [EX seconds] [PX milliseconds] [NX|XX]
    summary: Set the string value of a key
    since: 1.0.0
    group: string
    
    set test 10
    set test 10 EX 60 60秒过期
      

* list
    1. 查询list
        lrange queues:importQueue 0 -1
    2. 从队列头pop元素，在队列里删除该元素
        lpop queues:importQueue
    3. 清空队列
        ltrim queues:importQueue 1 0
        
* set
    * zset（sorted set）操作相关 ::
    
        1. 查询
            zrange queues:importQueue:reserved 0 -1
        2. 删除所有元素
            zrem queues:importQueue:reserved 0 -1
            
    * hash ::
    
        1. 查看hash中的值和value
            hgetall job_result
            1) "importQueue_p0yzx4AQEcVefgUnvZ9nLLiUprwP6ff5"
            2) "{\"job_status\":1}"
        2. 删除值
            hDel job_result importQueue_p0yzx4AQEcVefgUnvZ9nLLiUprwP6ff5
            (integer) 1