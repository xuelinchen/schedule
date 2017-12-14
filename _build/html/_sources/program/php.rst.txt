php
====

php7功能点
-------------

#. 花括号 {} ::

    1. 表示{}里面的是一个变量  ,执行时按照变量来处理    
    2. 在字符串中引用变量使用的特殊包括方式，这样就可以不使用.运算符，从而减少代码的输入量了。
    $s = "Di, "; 
    echo ("${s}omething");  == echo $s."omething";
    //Output: Di, omething 
    
    PHP 变量后面加上一个大括号{}，里面填上数字，就是指 PHP 变量相应序号的字符。
    例如：
    $str = 'hello';
    echo $str{0}; // 输出为 h
    echo $str{1}; // 输出为 e
    如果要检查某个字符串是否满足多少长度，可以考虑用这种大括号（花括号）加 isset 的方式替代 strlen 函数，因为 isset 是语言结构，strlen 是函数，所以使用 isset 比使用 strlen 效率更高。
    比如判断一个字符串的长度是否小于 5：
    if ( !isset ( $str{5} ) ) 就比 if ( strlen ( $str ) < 5 ) 好。

#. call_user_func & call_user_func_array ::

    区别 调用方式不同
        call_user_func(array($class,$method),param1,param2);
        call_user_func_array(array($class,$method),array(param1,param2));
    注意如果上面$class为字符串,$method为非静态方法，则必须要先实例化，比如 $class = new \app\class;
    
#. method_exists & is_callable ::

    调用方式不同，is_callable 
        if ( is_callable( array( $obj, $method ) ) ) 
        { 
        /*要操作的代码段*/
        } 
        method_exists($obj,$method) 
        $result = is_callable(['\app\sms\model\NoDisturbNumber','clearData']);
        dump($result);
        $result = method_exists('appsms\model\NoDisturbNumber', "clearData");
        dump($result);
    其他
        php函数method_exists()与is_callable()的区别在于在php5中，一个方法存在并不意味着它就可以被调用。对于 private，protected和public类型的方法，method_exits()会返回true，但是is_callable()会检查存在其是否可以访问，如果是private，protected类型的，它会返回false。
        
#. trait ::

    属性：如果 trait 定义了一个属性，那类将不能定义同样名称的属性，否则会产生一个错误。 
    如果类的定义是兼容的（同样的可见性和初始值）则错误的级别是 E_STRICT，否则是一个致命错误。

#. php7新功能 ::

    1、运算符（NULL 合并运算符）
        $a = $_GET['a'] ?? 1; 相当于 $a = isset($_GET['a']) ? $_GET['a'] : 1;
    2、函数返回值类型声明
      # declare(strict_types=1); 
        function foo($a):int{
            return $a
        }
        foo(1.0); foo 函数返回 int 1，没有任何错误
        去掉上面代码的注释，采用严格模式，则会出发一个 TypeError 的 Fatal error。
    3、标量类型声明
        function sumOfints(int ...$ints){
            return array_sum($ints)
        }
        var_dump(sumOfInts(2, '3', 4.1)); 
    4、use 批量声明
        use some/namespace/{ClassA, ClassB, ClassC as C}; 
        use function some/namespace/{fn_a, fn_b, fn_c}; 
        use const some/namespace/{ConstA, ConstB, ConstC}; 
    5、spaceship（<=>）操作符
        用来比较两个表达式，左边小于、等于、大于右边时分别返回-1,0,1
    6、常量array可以使用define定义
        define('ANIMALS', [
    'dog',
    'cat',
    'bird'
        ]);
        echo ANIMALS[1]; // outputs "cat"
    7、匿名类
        interface Logger {
    public function log(string $msg);
        }
        class Application {
            private $logger;
        
            public function getLogger(): Logger {
                 return $this->logger;
            }
        
            public function setLogger(Logger $logger) {
                 $this->logger = $logger;
            }
        }       
        $app = new Application;
        $app->setLogger(new class implements Logger {
            public function log(string $msg) {
                echo $msg;
            }
        });     
        var_dump($app->getLogger());
        The above example will output:
        object(class@anonymous)#2 (0) {
        }
    8、闭包（ Closure）增加了一个 call 方法
        class A {private $x = 1;}
        // Pre PHP 7 code
        $getX = function() {return $this->x;};
        $getXCB = $getX->bindTo(new A, 'A'); // intermediate closure
        echo $getXCB();
        
        // PHP 7+ code
        $getX = function() {return $this->x;};
        echo $getX->call(new A);
        
 
tp5
----------

queue
^^^^^^^^^^^
* refer ::
    
    https://github.com/coolseven/notes/blob/master/thinkphp-queue/README.md
    
* install ::

    composer require topthink/think-queue
    
* 例子 

    * 配置 ::
    
        application/extra/queue.php
        return [
                'connector'  => 'Redis',         // Redis 驱动
                'expire'     => 60,             // 任务的过期时间，默认为60秒; 若要禁用，则设置为 null
                'default'    => 'default',      // 默认的队列名称
                'host'       => '127.0.0.1',        // redis 主机ip
                'port'       => 6379,           // redis 端口
                'password'   => '',             // redis 密码
                'select'     => 2,                  // 使用哪一个 db，默认为 db1
                'timeout'    => 0,              // redis连接的超时时间
                'persistent' => false,          // 是否是长连接
        ];
    
    * 建立生产者 ::
    
        public function test(){
            // 1.当前任务将由哪个类来负责处理。
            //   当轮到该任务时，系统将生成一个该类的实例，并调用其 fire 方法
            $jobHandlerClassName  = 'app\job\Import';
            // 2.当前任务归属的队列名称，如果为新队列，会自动创建
            $jobQueueName     = "importQueue";
            // 3.当前任务所需的业务数据 . 不能为 resource 类型，其他类型最终将转化为json形式的字符串
            //   ( jobData 为对象时，需要在先在此处手动序列化，否则只存储其public属性的键值对)
            $jobData          = [ 'ts' => time(), 'bizId' => uniqid() , 'a' => 1 ] ;
            // 4.将该任务推送到消息队列，等待对应的消费者去执行
            $isPushed = Queue::push( $jobHandlerClassName , $jobData , $jobQueueName );
            // database 驱动时，返回值为 1|false  ;   redis 驱动时，返回值为 随机字符串|false
            if( $isPushed !== false ){
                echo date('Y-m-d H:i:s') . " a new Hello Job is Pushed to the MQ [$isPushed]"."<br>";
            }else{
                echo 'Oops, something went wrong.';
            }
        }
        
    * 查看queue ::
    
        llen "queues:helloJobQueue" 长度
        lpop "queues:helloJobQueue" 出栈
        lrange "queues:helloJobQueue" 0 -1 查询队列内容
    
    * 建立消费者 ::
    
        namespace app\job;
        use think\queue\Job;
        use think\Log;
        
        class Import{
            
            /**
             * fire方法是消息队列默认调用的方法
             * @param Job            $job      当前的任务对象
             * @param array|mixed    $data     发布任务时自定义的数据
             */
            public function fire(Job $job,$data){
                $isJobDone = $this->doHelloJob($data);
                
                if ($isJobDone) {
                    //如果任务执行成功， 记得删除任务
                    $job->delete();
                    print("<info>Hello Job has been done and deleted"."</info>\n");
                }else{
                    if ($job->attempts() > 3) {
                        //通过这个方法可以检查这个任务已经重试了几次了
                        print("<warn>Hello Job has been retried more than 3 times!"."</warn>\n");
                        $job->delete();
                        // 也可以重新发布这个任务
                        //print("<info>Hello Job will be availabe again after 2s."."</info>\n");
                        //$job->release(2); //$delay为延迟时间，表示该任务延迟2秒后再执行
                    }
                }
            }
            
            /**
             * 根据消息中的数据进行实际的业务处理
             * @param array|mixed    $data     发布任务时自定义的数据
             * @return boolean                 任务执行的结果
             */
            private function doHelloJob($data) {
                // 根据消息中的数据进行实际的业务处理...
                print("<info>Hello Job Started. job Data is: ".var_export($data,true)."</info> \n");
                print("<info>Hello Job is Fired at " . date('Y-m-d H:i:s') ."</info> \n");
                print("<info>Hello Job is Done!"."</info> \n");
                return true;
            }
            
            public function failed($data){
                
                // ...任务达到最大重试次数后，失败了
                print("<info>Hello Job is failed!"."</info> \n");
                Log::write("has fail in import:");
            }   
        }
        
    * 全局错误类 ::
    
        1. tags.php 标签配置
        // 任务失败统一回调,有四种定义方式
        'queue_failed'=> [
                    ['app\\common\\behavior\\MyQueueFailedLogger', 'logAllFailedQueues']
                ],
        2. fail方法
            namespace app\common\behavior;
            use think\Log;
            class MyQueueFailedLogger{
                const should_run_hook_callback = true;
                
                /**
                 * @param $jobObject   \think\queue\Job   //任务对象，保存了该任务的执行情况和业务数据
                 * @return bool     true                  //是否需要删除任务并触发其failed() 方法
                 */
                public function logAllFailedQueues(&$jobObject){
                    
                    /* $failedJobLog = [
                            'jobHandlerClassName'   => $jobObject->getName(), // 'application\index\job\Hello'
                            'queueName' => $jobObject->getQueue(),             // 'helloJobQueue'
                            'jobData'   => $jobObject->getRawBody()['data'],  // '{'a': 1 }'
                            'attempts'  => $jobObject->attempts(),            // 3
                    ];
                    var_export(json_encode($failedJobLog,true)); */
                    Log::write("i am in failed method");
                    //Log::write("failed in ".json_encode($failedJobLog,true));
                    // $jobObject->release();     //重发任务
                    //$jobObject->delete();         //删除任务
                    //$jobObject->failed();   //通知消费者类任务执行失败
                    
                    return self::should_run_hook_callback;
                }
            } 
              
    * 测试 ::
    
        1. https://10.0.0.42:1066/home/index/test
            2017-09-23 10:04:18 a new Hello Job is Pushed to the MQ [A25ZVpTcRIDUMyUgwSiRy76ebkLPuck8]
        2. php think queue:work --queue="importQueue" --daemon
    
    * 使用supervisor管理进程 ::
    
        [program:import]
        directory=/home/cxl/git-svn/spi/spi-php
        command=php think queue:work --queue="importQueue" --tries=1 --daemon
        process_name=import_%(process_num)s
        numprocs=2
        numprocs_start=1
        autostart=true
        startsecs=5
        autorestart=true
        startretries=3
        user=www-data
        ;redirect_stderr=true
        ;stdout_logfile_maxbytes = 20MB
        ;stdout_logfile_backups = 20
        ;stdout_logfile = /data/logs/usercenter_stdout.log
        ;environment=PYTHONPATH=$PYTHONPATH:/path/to/somewhere
        导入队列，使用两个进程处理，循环处理
        kill一个进程会自动重启   
    