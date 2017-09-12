# php7新特性
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
		