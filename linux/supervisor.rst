supervisor
==========

refer
-------

    http://supervisord.org/
    http://www.ttlsa.com/linux/using-supervisor-control-program/

install 
--------------

    Supervisor: A Process Control System
    apt install supervisor -y
    
usage          
-------------

* example ::

    cd /etc/supervisor/conf.d
    echo_supervisord_conf > /etc/supervisord.conf
    [unix_http_server]
    file=/tmp/supervisor.sock   ; UNIX socket 文件，supervisorctl 会使用
    ;chmod=0700                 ; socket 文件的 mode，默认是 0700
    ;chown=nobody:nogroup       ; socket 文件的 owner，格式： uid:gid    
    ;[inet_http_server]         ; HTTP 服务器，提供 web 管理界面
    ;port=127.0.0.1:9001        ; Web 管理后台运行的 IP 和端口，如果开放到公网，需要注意安全性
    ;username=user              ; 登录管理后台的用户名
    ;password=123               ; 登录管理后台的密码
     
    [supervisord]
    logfile=/tmp/supervisord.log ; 日志文件，默认是 $CWD/supervisord.log
    logfile_maxbytes=50MB        ; 日志文件大小，超出会 rotate，默认 50MB
    logfile_backups=10           ; 日志文件保留备份数量默认 10
    loglevel=info                ; 日志级别，默认 info，其它: debug,warn,trace
    pidfile=/tmp/supervisord.pid ; pid 文件
    nodaemon=false               ; 是否在前台启动，默认是 false，即以 daemon 的方式启动
    minfds=1024                  ; 可以打开的文件描述符的最小值，默认 1024
    minprocs=200                 ; 可以打开的进程数的最小值，默认 200
     
    ; the below section must remain in the config file for RPC
    ; (supervisorctl/web interface) to work, additional interfaces may be
    ; added by defining them in separate rpcinterface: sections
    [rpcinterface:supervisor]
    supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface
     
    [supervisorctl]
    serverurl=unix:///tmp/supervisor.sock ; 通过 UNIX socket 连接 supervisord，路径与 unix_http_server 部分的 file 一致
    ;serverurl=http://127.0.0.1:9001 ; 通过 HTTP 的方式连接 supervisord
     
    ; 包含其他的配置文件
    [include]
    files = relative/directory/*.ini    ; 可以是 *.conf 或 *.ini
    
    增加一个管理进程
    [program:usercenter]
    directory = /home/leon/projects/usercenter ; 程序的启动目录
    command = gunicorn -c gunicorn.py wsgi:app  ; 启动命令，可以看出与手动在命令行启动的命令是一样的
    autostart = true     ; 在 supervisord 启动的时候也自动启动
    startsecs = 5        ; 启动 5 秒后没有异常退出，就当作已经正常启动了
    autorestart = true   ; 程序异常退出后自动重启
    startretries = 3     ; 启动失败自动重试次数，默认是 3
    user = leon          ; 用哪个用户启动
    redirect_stderr = true  ; 把 stderr 重定向到 stdout，默认 false
    stdout_logfile_maxbytes = 20MB  ; stdout 日志文件大小，默认 50MB
    stdout_logfile_backups = 20     ; stdout 日志文件备份数
    ; stdout 日志文件，需要注意当指定目录不存在时无法正常启动，所以需要手动创建目录（supervisord 会自动创建日志文件）
    stdout_logfile = /data/logs/usercenter_stdout.log
     
    ; 可以通过 environment 来添加需要的环境变量，一种常见的用法是修改 PYTHONPATH
    ; environment=PYTHONPATH=$PYTHONPATH:/path/to/somewhere
    
    [program:cat]
    command=/bin/cat
    process_name=%(program_name)s
    numprocs=1
    directory=/tmp
    umask=022
    priority=999
    autostart=true
    autorestart=true
    startsecs=10
    startretries=3
    exitcodes=0,2
    stopsignal=TERM
    stopwaitsecs=10
    user=chrism
    redirect_stderr=false
    stdout_logfile=/a/path
    stdout_logfile_maxbytes=1MB
    stdout_logfile_backups=10
    stdout_capture_maxbytes=1MB
    stderr_logfile=/a/path
    stderr_logfile_maxbytes=1MB
    stderr_logfile_backups=10
    stderr_capture_maxbytes=1MB
    environment=A="1",B="2"
    serverurl=AUTO
    
    ;*为必须填写项
    ;*[program:应用名称]
    [program:cat]
    
    ;*命令路径,如果使用python启动的程序应该为 python /home/test.py, 
    ;不建议放入/home/user/, 对于非user用户一般情况下是不能访问
    command=/bin/cat
    
    ;当numprocs为1时,process_name=%(program_name)s
    ;当numprocs>=2时,%(program_name)s_%(process_num)02d
    process_name=%(program_name)s
    
    ;进程数量
    numprocs=1
    
    ;执行目录,若有/home/supervisor_test/test1.py
    ;将directory设置成/home/supervisor_test
    ;则command只需设置成python test1.py
    ;否则command必须设置成绝对执行目录
    directory=/tmp
    
    ;掩码:--- -w- -w-, 转换后rwx r-x w-x
    umask=022
    
    ;优先级,值越高,最后启动,最先被关闭,默认值999
    priority=999
    
    ;如果是true,当supervisor启动时,程序将会自动启动
    autostart=true
    
    ;*自动重启
    autorestart=true
    
    ;启动延时执行,默认1秒
    startsecs=10
    
    ;启动尝试次数,默认3次
    startretries=3
    
    ;当退出码是0,2时,执行重启,默认值0,2
    exitcodes=0,2
    
    ;停止信号,默认TERM
    ;中断:INT(类似于Ctrl+C)(kill -INT pid),退出后会将写文件或日志(推荐)
    ;终止:TERM(kill -TERM pid)
    ;挂起:HUP(kill -HUP pid),注意与Ctrl+Z/kill -stop pid不同
    ;从容停止:QUIT(kill -QUIT pid)
    ;KILL, USR1, USR2其他见命令(kill -l),说明1
    stopsignal=TERM
    
    stopwaitsecs=10
    
    ;*以root用户执行
    user=root
    
    ;重定向
    redirect_stderr=false
    
    stdout_logfile=/a/path
    stdout_logfile_maxbytes=1MB
    stdout_logfile_backups=10
    stdout_capture_maxbytes=1MB
    stderr_logfile=/a/path
    stderr_logfile_maxbytes=1MB
    stderr_logfile_backups=10
    stderr_capture_maxbytes=1MB
    
    ;环境变量设置
    environment=A="1",B="2"
    
    serverurl=AUTO
    
    command：启动程序使用的命令，可以是绝对路径或者相对路径
    process_name：一个python字符串表达式，用来表示supervisor进程启动的这个的名称，默认值是%(program_name)s
    numprocs：Supervisor启动这个程序的多个实例，如果numprocs>1，则process_name的表达式必须包含%(process_num)s，默认是1
    numprocs_start：一个int偏移值，当启动实例的时候用来计算numprocs的值
    priority：权重，可以控制程序启动和关闭时的顺序，权重越低：越早启动，越晚关闭。默认值是999
    autostart：如果设置为true，当supervisord启动的时候，进程会自动重启。
    autorestart：值可以是false、true、unexpected。false：进程不会自动重启，unexpected：当程序退出时的退出码不是exitcodes中定义的时，进程会重启，true：进程会无条件重启当退出的时候。
    startsecs：程序启动后等待多长时间后才认为程序启动成功
    startretries：supervisord尝试启动一个程序时尝试的次数。默认是3
    exitcodes：一个预期的退出返回码，默认是0,2。
    stopsignal：当收到stop请求的时候，发送信号给程序，默认是TERM信号，也可以是 HUP, INT, QUIT, KILL, USR1, or USR2。
    stopwaitsecs：在操作系统给supervisord发送SIGCHILD信号时等待的时间
    stopasgroup：如果设置为true，则会使supervisor发送停止信号到整个进程组
    killasgroup：如果设置为true，则在给程序发送SIGKILL信号的时候，会发送到整个进程组，它的子进程也会受到影响。
    user：如果supervisord以root运行，则会使用这个设置用户启动子程序
    redirect_stderr：如果设置为true，进程则会把标准错误输出到supervisord后台的标准输出文件描述符。
    stdout_logfile：把进程的标准输出写入文件中，如果stdout_logfile没有设置或者设置为AUTO，则supervisor会自动选择一个文件位置。
    stdout_logfile_maxbytes：标准输出log文件达到多少后自动进行轮转，单位是KB、MB、GB。如果设置为0则表示不限制日志文件大小
    stdout_logfile_backups：标准输出日志轮转备份的数量，默认是10，如果设置为0，则不备份
    stdout_capture_maxbytes：当进程处于stderr capture mode模式的时候，写入FIFO队列的最大bytes值，单位可以是KB、MB、GB
    stdout_events_enabled：如果设置为true，当进程在写它的stderr到文件描述符的时候，PROCESS_LOG_STDERR事件会被触发
    stderr_logfile：把进程的错误日志输出一个文件中，除非redirect_stderr参数被设置为true
    stderr_logfile_maxbytes：错误log文件达到多少后自动进行轮转，单位是KB、MB、GB。如果设置为0则表示不限制日志文件大小
    stderr_logfile_backups：错误日志轮转备份的数量，默认是10，如果设置为0，则不备份
    stderr_capture_maxbytes：当进程处于stderr capture mode模式的时候，写入FIFO队列的最大bytes值，单位可以是KB、MB、GB
    stderr_events_enabled：如果设置为true，当进程在写它的stderr到文件描述符的时候，PROCESS_LOG_STDERR事件会被触发
    environment：一个k/v对的list列表
    directory：supervisord在生成子进程的时候会切换到该目录
    umask：设置进程的umask
    serverurl：是否允许子进程和内部的HTTP服务通讯，如果设置为AUTO，supervisor会自动的构造一个url    
    eg：
    
    
    [program:import]
    directory=/home/cxl/git-svn/spi/spi-php
    command=php think queue:work --queue="importQueue" --tries=1 --daemon
    process_name=import_%(process_num)s
    numprocs=2
    numprocs_start=1
    autostart=true
    startsecs=5
    autorestart=true
    startretries=3
    user=www-data
    ;redirect_stderr=true
    ;stdout_logfile_maxbytes = 20MB
    ;stdout_logfile_backups = 20
    ;stdout_logfile = /data/logs/usercenter_stdout.log
    ;environment=PYTHONPATH=$PYTHONPATH:/path/to/somewhere
    导入队列，使用两个进程处理，循环处理