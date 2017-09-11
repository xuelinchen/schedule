# awk --help
	Usage: awk [POSIX or GNU style options] -f progfile [--] file ...
	Usage: awk [POSIX or GNU style options] [--] 'program' file ...
	POSIX options:          GNU long options: (standard)
	        -f progfile             --file=progfile
	        -F fs                   --field-separator=fs
	        -v var=val              --assign=var=val
	Short options:          GNU long options: (extensions)
	        -b                      --characters-as-bytes
	        -c                      --traditional
	        -C                      --copyright
	        -d[file]                --dump-variables[=file]
	        -D[file]                --debug[=file]
	        -e 'program-text'       --source='program-text'
	        -E file                 --exec=file
	        -g                      --gen-pot
	        -h                      --help
	        -i includefile          --include=includefile
	        -l library              --load=library
	        -L[fatal|invalid]       --lint[=fatal|invalid]
	        -M                      --bignum
	        -N                      --use-lc-numeric
	        -n                      --non-decimal-data
	        -o[file]                --pretty-print[=file]
	        -O                      --optimize
	        -p[file]                --profile[=file]
	        -P                      --posix
	        -r                      --re-interval
	        -S                      --sandbox
	        -t                      --lint-old
	        -V                      --version
	
	To report bugs, see node `Bugs' in `gawk.info', which is
	section `Reporting Problems and Bugs' in the printed version.
	
	gawk is a pattern scanning and processing language.
	By default it reads standard input and writes standard output.
	
	Examples:
	        gawk '{ sum += $1 }; END { print sum }' file
	        gawk -F: '{ print $1 }' /etc/passwd

# example
	1、遍历文件相加
		echo -e "1\n2\n3\n4" > test.txt
		awk '{ sum += $1 }; END { print sum }' test.txt
		10
	2、按：分割，打印所有用户名
		awk -F: '{ print $1 }' /etc/passwd
	3、读取配置文件,并输出到变量里
		echo -e "DB_PWD=123456\nDB_USER=root" > test.txt
		cat test.txt |sed "s#//# #g" | sed "s/=/ /g" | awk  '{if(NF>1){printf("%s=\"%s\";",$1,$2)}}'
		DB_PWD="123456";DB_USER="root";
		eval $(cat test.txt |sed "s#//# #g" | sed "s/=/ /g" | awk  '{if(NF>1){printf("%s=\"%s\";",$1,$2)}}')
		echo $DB_PWD
		123456