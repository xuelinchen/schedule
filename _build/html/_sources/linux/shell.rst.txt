shell
======

shell语法
-----------

* 空函数 ::

    init(){ :; } 
    
* case ::

    case "$optname" in
       "a")
           # apache 发布端口
          apache_publish_port=$OPTARG
           ;;
        *)
               exit
               ;;
    esac

shell参数处理
---------------

* refer

    http://www.jb51.net/article/48686.htm

* 处理方式

    例如：./test.sh -f config.conf -v --prefix=/home

    * 手工处理 ::
  
        * $0 ： ./test.sh,即命令本身，相当于c/c++中的argv[0]
        * $1 ： -f,第一个参数.
        * $2 ： config.conf
        * $3, $4 ... ：类推。
        * $#  参数的个数，不包括命令本身，上例中$#为4.
        * $@ ：参数本身的列表，也不包括命令本身，如上例为 -f config.conf -v --prefix=/home
        * $* ：和$@相同，但"$*" 和 "$@"(加引号)并不同，"$*"将所有的参数解释成一个字符串，而"$@"是一个参数数组。
        #!/bin/bash
        for arg in "$*"
        do
          echo $arg
        done
        for arg in "$@"
        do
         echo $arg
        done
    
    * getopts ::
  
        不支持长选项
        #!/bin/bash
        while getopts "a:bc" arg #选项后面的冒号表示该选项需要参数
        do
                case $arg in
                     a)
                        echo "a's arg:$optarg" #参数存在$optarg中
        
                     b)
                        echo "b"
        
                     c)
                        echo "c"
        
                     ?)  #当有不认识的选项的时候arg为?
                    echo "unkonw argument"
                exit 1
        
                esac
        done
        
    * getopt ::
    
        要点:
        1. getopt 用法
        语法：getopt [options] [--] optstring parameters
        例如：getopt ab:cd -a -b he free cat 
        输出：-a -b he -- free cat
                    getopt 根据 ab:cd 将选项和参数 -a -b he free cat  解析为如下格式：
                    -a -b he -- free cat
                     其中 -- 将选项与非选项参数分开 free 和 cat 就时非选项参数
        2. set -- 
        -- Do not change any of the flags; useful in setting $1 to -.
        set --  主要是影响特殊变量$1 $2 等，其实在上面的脚本中就是将$1 $2 等参数变量重新组合
        例如：
        set -- a b c 
        shell中的特殊位置变量$1 为a $2 为 b $3 为 c
        3.如上脚本为build.sh 用法如下：
        ./build.sh -a -c -d -e dog
        ./build.sh -acde  dog
        上面两个命令执行结果相同。

awk
---------

example
^^^^^^^^^^^

* 遍历文件相加 ::

    echo -e "1\n2\n3\n4" > test.txt
    awk '{ sum += $1 }; END { print sum }' test.txt
    10
        
* 按：分割，打印所有用户名 ::

    awk -F: '{ print $1 }' /etc/passwd
    
* 读取配置文件,并输出到变量里 ::

    echo -e "DB_PWD=123456\nDB_USER=root" > test.txt
    cat test.txt |sed "s#//# #g" | sed "s/=/ /g" | awk  '{if(NF>1){printf("%s=\"%s\";",$1,$2)}}'
    DB_PWD="123456";DB_USER="root";
    eval $(cat test.txt |sed "s#//# #g" | sed "s/=/ /g" | awk  '{if(NF>1){printf("%s=\"%s\";",$1,$2)}}')
    echo $DB_PWD
    123456
        
* 分析url ::

    param=`echo "$redirectUrl" | awk -F '?' '{print $2}'`;
    echo "$param" | awk -F '&' '{i=1;while(i<=NF){n=split($i,array,"=");if(array[1]=="code"){print array[2];break;};i++;}}'

* 分析php配置文件，找出session节host配置项 ::

    awk -F '=>' '{if($0~/\047session\047/){find=1;fl=0;fr=0}if(find){if($0~/\[/){fl++;};if($0~/\]/){fr++;};if($1~/\047host\047/){print $2;exit 0;}if(fl==fr){exit 99}}}' ../application/config.php | awk -F '\047' '{print $2,exit 0}'
    '127.0.0.1',
    
curl
---------

usage
^^^^^^^^
* 静默方式-s，-k不检查证实 -c 创建cookie文件 ::

    result=`curl -s -k -c cxl_cookie https://10.0.0.42:1066`
     echo $result
    {"status":0,"info":"调用接口成功","data":"home"}
        
* 通过使用 -v 和 -trace获取更多的链接信息 ::

    curl  -v  -k -c "" -d "" -H "" https://10.0.0.42:1066

* 打印返回的header（-i） ::

    curl  -i  -k -c "" -d "" -H "" https://10.0.0.42:1066

cut
----------

usage
^^^^^^^^

* 按字节剪切 ::

    echo "test" | cut --b 2-4
    est
    
* 按字符剪切 ::

    echo "test" | cut -c 2-4
    est
    
* 多个分段用逗号分开 ::

    echo "test test"|cut -b 3-5,8
    st s
    
* 从文件获取 ::

    echo -e "星期一\n星期二\n星期三" > test.txt
    cut -b 1-3 test.txt
    星
    星
    星
    
* 中文 ::

    echo "星期四 星期三" | cut -c 1-3
    星
    
* 按特殊字符分割 ::

    echo "root:test:ok" | cut -d : -f 1
    root
    
* 综合应用 ::

    echo "root:test:ok" | cut -d : -f 3 | cut -c 1
    o

find
----------

grep
----------

usage
^^^^^^^^^^^^
* 去不命中的行 ::

    crontab -l | grep -v "php "
    
* 添加crontab ::

    (crontab -l 2>/dev/null | grep -v "php.*cleanAccesstoken";echo "* 1 * * * php /home/cxl/git-svn/spi-php/think cleanAccesstoken") | crontab -

jq
--------------
install
^^^^^^^^
apt install jq -y

usage
^^^^^^^^^^^^
* get value ::

    echo '{"status":0,"info":"we are success","data":{"client":{"client_id":"123456","client_secret":"567890"}}}' | jq ".status"
    0
    echo '{"status":0,"info":"we are success","data":{"client":{"client_id":"123456","client_secret":"567890"}}}' | jq ".info" | sed 's/"//g'
    we are success
    echo '{"status":0,"info":"we are success","data":{"client":{"client_id":"123456","client_secret":"567890"}}}' | jq ".data.client.client_id" | sed 's/"//g'
    123456
    
* filter data ::

    echo '{"status":0,"info":"we are success","data":{"client":{"client_id":"123456","client_secret":"567890"}}}' | jq '.data|.client'
    {
      "client_id": "123456",
      "client_secret": "567890"
    }
    

mktemp
----------------
usage
^^^^^^^^^^^^

* 生成随机文件 ::

    mktemp ttXXXX.tmp
    
* 生成随机目录 ::
    
    mktemp -d tempXXXXXX
        
nano
--------------
usage
^^^^^^^^^^^^
sed
---------------
usage
^^^^^^^^^^^^

* 替换字符 ::

    echo "this ReplaceWord success" | sed "s/ReplaceWord/is/"
    this is success
    
* 替换文件 ::

    echo "this ReplaceWord success" > test.txt
    cat test.txt
    sed -i "s/ReplaceWord/is/" test.txt
    cat test.txt
        
* 使用正则 ::

    echo "this 1234 success" | sed -r "s/[0-9]+/is/"
    this is success
    
* -g表示所有匹配的都执行 ::

    echo "this 1234 success 1234" | sed -r "s/[0-9]+/is/g"
    this is success is
    
* 按行号删除文件内容 ::

    sed -i '1,50000d' "$cxl_log_file" # 删除50000万行
    sed -i '1d' a.txt删首行
    sed -i '$d' b.txt删尾行
    sed -i 's/[ ]*//g' c.txt删空格
    sed -i '/^$/d' d.txt删空行
    sed -i ‘/^[0-9]*$/d' a.txt删包含数字的行
    sed -i ‘1,2d’a.txt删2行
    sed -i ‘/love/d’ a.txt删包含string的行
    
* 修改制定行内容

    sed -r  's/( *'host' *).*/\1"test"/'  ../application/config.php 

service
---------------
usage
^^^^^^^^^^^^
* service --status-all
* service supervisor status

tr
-----------------
usage
^^^^^^^^^^^^
* 转换为大写 ::

    echo "hello world" | tr [:lower:] [:upper:]      
    HELLO WORLD
    
* 删除空格、数字和-号 ::

    echo "hello-123-world  empty" | tr -d '[:blank:][:digit:]-'
    helloworldempty
    
* 删除补级以外的字符，和上一例子正相反 ::

    echo "hello - 123-world  empty" | tr -d -c '[:blank:][:digit:]-'
    - 123-  
    
* 去掉连续重复字符 ::

    echo "helloooo oooo    isssso ookk" | tr -s " os"  
    hello o iso okk
    
* 删除window文件造成^M字符 ::

    cat file | tr -s "\r" "\n" > new_file
    cat file | tr -d "\r" > new_file
    
    
uname
-------------
usage
^^^^^^^^^^^^
* 打印全部 ::

    uname -a
    Linux 1604developer 4.4.0-89-generic #112-Ubuntu SMP Mon Jul 31 19:38:41 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux

* 打印kernel-name ::

    uname -s
    Linux
        
* 打印机器网络名 ::

    uname -n
    1604developer
    
* 打印kernel-release ::

    uname -r
    4.4.0-89-generic
    
* 打印kernel-version ::

    uname -v
    #112-Ubuntu SMP Mon Jul 31 19:38:41 UTC 2017
    
* 打印机器硬件名称 ::

    uname -m
    x86_64
    
* 打印处理器类型 ::

    uname -p
    x86_64
    
* 打印硬件平台 ::

    uname -i
    x86_64
    
* 打印操作系统 ::

    uname -o
    GNU/Linux
    
update-rc.d
----------------
usage
^^^^^^^^^^^^
* 添加启动项 ::

    sudo update-rc.d   apache2 defaults  
    sudo update-rc.d   nginx defaults  
    sudo update-rc.d   redis_6379 defaults  
    
* 删除启动项 ::

    sudo update-rc.d -f apache2 remove  
    sudo update-rc.d -f nginx remove  
    sudo update-rc.d -f redis_6379 remove  
    
vi
--------------
usage
^^^^^^^^^^^^
* 翻下页ctrl+f
* 翻上页ctrl+b
* 设置行号 set nu

xargs
----------------
usage
^^^^^^^^^^^^
1. 当你尝试用rm 删除太多的文件，你可能得到一个错误信息：/bin/rm Argument list too long. 用xargs 去避免这个问题 ::

    find ~ -name ‘*.log' -print0 | xargs -0 rm -f 
    
2. 获得/etc/ 下所有*.conf 结尾的文件列表，有几种不同的方法能得到相同的结果，下面的例子仅仅是示范怎么实用xargs ，在这个例子中实用 xargs将find 命令的输出传递给ls -l ::
    
    find /etc -name "*.conf" | xargs ls –l
    
3. 假如你有一个文件包含了很多你希望下载的URL, 你能够使用xargs 下载所有链接 ::
    
    cat url-list.txt | xargs wget –c
    
4. 查找所有的jpg 文件，并且压缩它 ::
    
    find / -name *.jpg -type f -print | xargs tar -cvzf images.tar.gz
    
5. 拷贝所有的图片文件到一个外部的硬盘驱动 ::

    ls *.jpg | xargs -n1 -i cp {} /external-hard-drive/directory
    
6. 查找另一个目录同名文件，-n1表示每行一个参数 -i表示用{}表示输出的每行记录 ::

    ls /home/cxl/git-svn/spi/spi-php/bin/res/supervisor | xargs -n1 -i echo {}

环境变量
------------

refer
^^^^^^^^^^
http://www.cnblogs.com/zhaofeng555/p/4895517.html

usage
^^^^^^^^^^^
先将export LANG=zh_CN加入/etc/profile ,退出系统重新登录，登录提示显示英文。将/etc/profile 中的export LANG=zh_CN删除，将LNAG=zh_CN加入/etc/environment，退出系统重新登录，登录提示显示中文。用户环境建立的过程中总是先执行/etc/profile然后在读取/etc/environment。为什么会有如上所叙的不同呢?
 
应该是先执行/etc/environment，后执行/etc/profile。
/etc/environment是设置整个系统的环境，而/etc/profile是设置所有用户的环境，前者与登录用户无关，后者与登录用户有关。  www.2cto.com  
系统应用程序的执行与用户环境可以是无关的，但与系统环境是相关的，所以当你登录时，你看到的提示信息，象日期、时间信息的显示格式与系统环境的LANG是相关的，缺省LANG=en_US，如果系统环境LANG=zh_CN，则提示信息是中文的，否则是英文的。

对于用户的SHELL初始化而言是先执行/etc/profile,再读取文件/etc/environment.对整个系统而言是先执行/etc/environment。这样理解正确吗?
/etc/enviroment --> /etc/profile --> $HOME/.profile   -->$HOME/.env (如果存在)

/etc/profile 是所有用户的环境变量
/etc/enviroment是系统的环境变量
登陆系统时shell读取的顺序应该是   www.2cto.com  
     /etc/profile ->/etc/enviroment -->$HOME/.profile   -->$HOME/.env

原因应该是jtw所说的用户环境和系统环境的区别了
如果同一个变量在用户环境(/etc/profile)和系统环境(/etc/environment)有不同的值那应该是以用户环境为准了。
 
（1）/etc/profile： 此文件为系统的每个用户设置环境信息,当用户第一次登录时,该文件被执行. 并从/etc/profile.d目录的配置文件中搜集shell的设置。

（2）/etc/bashrc: 为每一个运行bash shell的用户执行此文件.当bash shell被打开时,该文件被读取。  www.2cto.com  

（3）~/.bash_profile: 每个用户都可使用该文件输入专用于自己使用的shell信息,当用户登录时,该文件仅仅执行一次!默认情况下,他设置一些环境变量,执行用户的.bashrc文件。

（4）~/.bashrc: 该文件包含专用于你的bash shell的bash信息,当登录时以及每次打开新的shell时,该该文件被读取。
 
（5） ~/.bash_logout:当每次退出系统(退出bash shell)时,执行该文件. 另外,/etc/profile中设定的变量(全局)的可以作用于任何用户,而~/.bashrc等中设定的变量(局部)只能继承 /etc/profile中的变量,他们是"父子"关系。

（6）~/.bash_profile 是交互式、login 方式进入 bash 运行的~/.bashrc 是交互式 non-login 方式进入 bash 运行的通常二者设置大致相同，所以通常前者会调用后者。