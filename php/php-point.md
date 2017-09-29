# 花括号 {}
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

# call_user_func & call_user_func_array
	* 区别 调用方式不同
		call_user_func(array($class,$method),param1,param2);
		call_user_func_array(array($class,$method),array(param1,param2));
	* 注意如果上面$class为字符串,$method为非静态方法，则必须要先实例化，比如 $class = new \app\class;
	
# method_exists & is_callable
	* 调用方式不同，is_callable 
		if ( is_callable( array( $obj, $method ) ) ) 
		{ 
		/*要操作的代码段*/
		} 
		method_exists($obj,$method) 
		$result = is_callable(['\app\sms\model\NoDisturbNumber','clearData']);
		dump($result);
		$result = method_exists('appsms\model\NoDisturbNumber', "clearData");
		dump($result);
	* 其他
		php函数method_exists()与is_callable()的区别在于在php5中，一个方法存在并不意味着它就可以被调用。对于 private，protected和public类型的方法，method_exits()会返回true，但是is_callable()会检查存在其是否可以访问，如果是private，protected类型的，它会返回false。
		
# trait
	属性：如果 trait 定义了一个属性，那类将不能定义同样名称的属性，否则会产生一个错误。 如果类的定义是兼容的（同样的可见性和初始值）则错误的级别是 E_STRICT，否则是一个致命错误。
	
	