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
	
	