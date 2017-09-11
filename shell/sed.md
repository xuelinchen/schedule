# sed --help
	Usage: sed [OPTION]... {script-only-if-no-other-script} [input-file]...
	
	  -n, --quiet, --silent
	                 suppress automatic printing of pattern space
	  -e script, --expression=script
	                 add the script to the commands to be executed
	  -f script-file, --file=script-file
	                 add the contents of script-file to the commands to be executed
	  --follow-symlinks
	                 follow symlinks when processing in place
	  -i[SUFFIX], --in-place[=SUFFIX]
	                 edit files in place (makes backup if SUFFIX supplied)
	  -l N, --line-length=N
	                 specify the desired line-wrap length for the `l' command
	  --posix
	                 disable all GNU extensions.
	  -r, --regexp-extended
	                 use extended regular expressions in the script.
	  -s, --separate
	                 consider files as separate rather than as a single continuous
	                 long stream.
	  -u, --unbuffered
	                 load minimal amounts of data from the input files and flush
	                 the output buffers more often
	  -z, --null-data
	                 separate lines by NUL characters
	      --help     display this help and exit
	      --version  output version information and exit
	
	If no -e, --expression, -f, or --file option is given, then the first
	non-option argument is taken as the sed script to interpret.  All
	remaining arguments are names of input files; if no input files are
	specified, then the standard input is read.
	
	GNU sed home page: <http://www.gnu.org/software/sed/>.
	General help using GNU software: <http://www.gnu.org/gethelp/>.
	E-mail bug reports to: <bug-sed@gnu.org>.
	Be sure to include the word ``sed'' somewhere in the ``Subject:'' field.

# example
	1、替换字符
		echo "this ReplaceWord success" | sed "s/ReplaceWord/is/"
		this is success
	2、替换文件
		echo "this ReplaceWord success" > test.txt
		cat test.txt
		sed -i "s/ReplaceWord/is/" test.txt
		cat test.txt
	3、使用正则
		echo "this 1234 success" | sed -r "s/[0-9]+/is/"
		this is success
	4、-g表示所有匹配的都执行
		echo "this 1234 success 1234" | sed -r "s/[0-9]+/is/g"
		this is success is