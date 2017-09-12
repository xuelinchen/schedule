 
# uname --help

	Usage: uname [OPTION]...
	Print certain system information.  With no OPTION, same as -s.
	
	  -a, --all                print all information, in the following order,
	                             except omit -p and -i if unknown:
	  -s, --kernel-name        print the kernel name
	  -n, --nodename           print the network node hostname
	  -r, --kernel-release     print the kernel release
	  -v, --kernel-version     print the kernel version
	  -m, --machine            print the machine hardware name
	  -p, --processor          print the processor type (non-portable)
	  -i, --hardware-platform  print the hardware platform (non-portable)
	  -o, --operating-system   print the operating system
	      --help     display this help and exit
	      --version  output version information and exit
	
	GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
	Full documentation at: <http://www.gnu.org/software/coreutils/uname>
	or available locally via: info '(coreutils) uname invocation'

# example
	1、打印全部
		uname -a
		Linux 1604developer 4.4.0-89-generic #112-Ubuntu SMP Mon Jul 31 19:38:41 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
	2、打印kernel-name
		uname -s
		Linux
	3、打印机器网络名
		uname -n
		1604developer
	4、打印kernel-release
		uname -r
		4.4.0-89-generic
	5、打印kernel-version
		uname -v
		#112-Ubuntu SMP Mon Jul 31 19:38:41 UTC 2017
	6、打印机器硬件名称
		uname -m
		x86_64
	7、打印处理器类型
		uname -p
		x86_64
	8、打印硬件平台
		uname -i
		x86_64
	9、打印操作系统
		uname -o
		GNU/Linux