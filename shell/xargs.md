# refer
	http://www.jb51.net/article/44720.htm
# xargs --help
	Usage: xargs [OPTION]... COMMAND [INITIAL-ARGS]...
	Run COMMAND with arguments INITIAL-ARGS and more arguments read from input.
	
	Mandatory and optional arguments to long options are also
	mandatory or optional for the corresponding short option.
	  -0, --null                   items are separated by a null, not whitespace;
	                                 disables quote and backslash processing and
	                                 logical EOF processing
	  -a, --arg-file=FILE          read arguments from FILE, not standard input
	  -d, --delimiter=CHARACTER    items in input stream are separated by CHARACTER,
	                                 not by whitespace; disables quote and backslash
	                                 processing and logical EOF processing
	  -E END                       set logical EOF string; if END occurs as a line
	                                 of input, the rest of the input is ignored
	                                 (ignored if -0 or -d was specified)
	  -e, --eof[=END]              equivalent to -E END if END is specified;
	                                 otherwise, there is no end-of-file string
	  -I R                         same as --replace=R
	  -i, --replace[=R]            replace R in INITIAL-ARGS with names read
	                                 from standard input; if R is unspecified,
	                                 assume {}
	  -L, --max-lines=MAX-LINES    use at most MAX-LINES non-blank input lines per
	                                 command line
	  -l[MAX-LINES]                similar to -L but defaults to at most one non-
	                                 blank input line if MAX-LINES is not specified
	  -n, --max-args=MAX-ARGS      use at most MAX-ARGS arguments per command line
	  -P, --max-procs=MAX-PROCS    run at most MAX-PROCS processes at a time
	  -p, --interactive            prompt before running commands
	      --process-slot-var=VAR   set environment variable VAR in child processes
	  -r, --no-run-if-empty        if there are no arguments, then do not run COMMAND;
	                                 if this option is not given, COMMAND will be
	                                 run at least once
	  -s, --max-chars=MAX-CHARS    limit length of command line to MAX-CHARS
	      --show-limits            show limits on command-line length
	  -t, --verbose                print commands before executing them
	  -x, --exit                   exit if the size (see -s) is exceeded
	      --help                   display this help and exit
	      --version                output version information and exit

# example
	1. 当你尝试用rm 删除太多的文件，你可能得到一个错误信息：/bin/rm Argument list too long. 用xargs 去避免这个问题
		find ~ -name ‘*.log' -print0 | xargs -0 rm -f 
	2. 获得/etc/ 下所有*.conf 结尾的文件列表，有几种不同的方法能得到相同的结果，下面的例子仅仅是示范怎么实用xargs ，在这个例子中实用 xargs将find 命令的输出传递给ls -l
		find /etc -name "*.conf" | xargs ls –l
	3. 假如你有一个文件包含了很多你希望下载的URL, 你能够使用xargs 下载所有链接
		cat url-list.txt | xargs wget –c
	4. 查找所有的jpg 文件，并且压缩它
		find / -name *.jpg -type f -print | xargs tar -cvzf images.tar.gz
	5. 拷贝所有的图片文件到一个外部的硬盘驱动 
		ls *.jpg | xargs -n1 -i cp {} /external-hard-drive/directory
	6. 查找另一个目录同名文件，-n1表示每行一个参数 -i表示用{}表示输出的每行记录
		ls /home/cxl/git-svn/spi/spi-php/bin/res/supervisor | xargs -n1 -i echo {}
		