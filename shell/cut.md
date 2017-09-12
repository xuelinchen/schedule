# cut --help
	Usage: cut OPTION... [FILE]...
	Print selected parts of lines from each FILE to standard output.
	
	With no FILE, or when FILE is -, read standard input.
	
	Mandatory arguments to long options are mandatory for short options too.
	  -b, --bytes=LIST        select only these bytes
	  -c, --characters=LIST   select only these characters
	  -d, --delimiter=DELIM   use DELIM instead of TAB for field delimiter
	  -f, --fields=LIST       select only these fields;  also print any line
	                            that contains no delimiter character, unless
	                            the -s option is specified
	  -n                      (ignored)
	      --complement        complement the set of selected bytes, characters
	                            or fields
	  -s, --only-delimited    do not print lines not containing delimiters
	      --output-delimiter=STRING  use STRING as the output delimiter
	                            the default is to use the input delimiter
	  -z, --zero-terminated    line delimiter is NUL, not newline
	      --help     display this help and exit
	      --version  output version information and exit
	
	Use one, and only one of -b, -c or -f.  Each LIST is made up of one
	range, or many ranges separated by commas.  Selected input is written
	in the same order that it is read, and is written exactly once.
	Each range is one of:
	
	  N     N'th byte, character or field, counted from 1
	  N-    from N'th byte, character or field, to end of line
	  N-M   from N'th to M'th (included) byte, character or field
	  -M    from first to M'th (included) byte, character or field
	
	GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
	Full documentation at: <http://www.gnu.org/software/coreutils/cut>
	or available locally via: info '(coreutils) cut invocation'

# example
	1、按字节剪切
		echo "test" | cut --b 2-4
		est
	2、按字符剪切
		echo "test" | cut -c 2-4
		est
	3、多个分段用逗号分开
		echo "test test"|cut -b 3-5,8
		st s
	4、从文件获取
		echo -e "星期一\n星期二\n星期三" > test.txt
		cut -b 1-3 test.txt
		星
		星
		星
	5、 中文
		echo "星期四 星期三" | cut -c 1-3
		星
	6、按特殊字符分割
		echo "root:test:ok" | cut -d : -f 1
		root
	7、综合应用
		echo "root:test:ok" | cut -d : -f 3 | cut -c 1
		o