# tr --help
	Usage: tr [OPTION]... SET1 [SET2]
	Translate, squeeze, and/or delete characters from standard input,
	writing to standard output.
	
	  -c, -C, --complement    use the complement of SET1
	  -d, --delete            delete characters in SET1, do not translate
	  -s, --squeeze-repeats   replace each sequence of a repeated character
	                            that is listed in the last specified SET,
	                            with a single occurrence of that character
	  -t, --truncate-set1     first truncate SET1 to length of SET2
	      --help     display this help and exit
	      --version  output version information and exit
	
	SETs are specified as strings of characters.  Most represent themselves.
	Interpreted sequences are:
	
	  \NNN            character with octal value NNN (1 to 3 octal digits)
	  \\              backslash
	  \a              audible BEL
	  \b              backspace
	  \f              form feed
	  \n              new line
	  \r              return
	  \t              horizontal tab
	  \v              vertical tab
	  CHAR1-CHAR2     all characters from CHAR1 to CHAR2 in ascending order
	  [CHAR*]         in SET2, copies of CHAR until length of SET1
	  [CHAR*REPEAT]   REPEAT copies of CHAR, REPEAT octal if starting with 0
	  [:alnum:]       all letters and digits
	  [:alpha:]       all letters
	  [:blank:]       all horizontal whitespace
	  [:cntrl:]       all control characters
	  [:digit:]       all digits
	  [:graph:]       all printable characters, not including space
	  [:lower:]       all lower case letters
	  [:print:]       all printable characters, including space
	  [:punct:]       all punctuation characters
	  [:space:]       all horizontal or vertical whitespace
	  [:upper:]       all upper case letters
	  [:xdigit:]      all hexadecimal digits
	  [=CHAR=]        all characters which are equivalent to CHAR
	
	Translation occurs if -d is not given and both SET1 and SET2 appear.
	-t may be used only when translating.  SET2 is extended to length of
	SET1 by repeating its last character as necessary.  Excess characters
	of SET2 are ignored.  Only [:lower:] and [:upper:] are guaranteed to
	expand in ascending order; used in SET2 while translating, they may
	only be used in pairs to specify case conversion.  -s uses the last
	specified SET, and occurs after translation or deletion.
	
	GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
	Full documentation at: <http://www.gnu.org/software/coreutils/tr>
	or available locally via: info '(coreutils) tr invocation'
	
	来自: http://man.linuxde.net/tr
	
	从标准输入中翻译、压缩和/或删除字符

# example
	1、 转换为大写
			echo "hello world" | tr [:lower:] [:upper:]      
			HELLO WORLD
	2、 删除空格、数字和-号
			echo "hello-123-world  empty" | tr -d '[:blank:][:digit:]-'
			helloworldempty
	3、 删除补级以外的字符，和上一例子正相反
			echo "hello - 123-world  empty" | tr -d -c '[:blank:][:digit:]-'
			- 123-  
	4、 去掉连续重复字符
			echo "helloooo oooo    isssso ookk" | tr -s " os"  
			hello o iso okk
	5、 删除window文件造成^M字符
			cat file | tr -s "\r" "\n" > new_file
			cat file | tr -d "\r" > new_file