svn
====

refer
------

install
--------

* 安装1.8 ::

    sudo sh -c 'echo "deb http://opensource.wandisco.com/ubuntu precise svn18" >> /etc/apt/sources.list.d/subversion18.list'
    sudo wget -q http://opensource.wandisco.com/wandisco-debian.gpg -O- | sudo apt-key add -
    sudo apt-get update
    sudo apt-cache show subversion | grep '^Version:'
    sudo apt-get install subversion
    
usage
--------

* 创建项目目录 ::

    mkdir svn
    
* 创建仓库 ::

    svnadmin create /home/svn/project
    chmod 777 -R /home/svn/project
    
* 查看svn服务器是否支持 cyrus sasl 方式认证 ::

    svnserve --version
    是否存在 Cyrus SASL authentication is available.
    
* 配置权限 ::

    1、vi /home/svn/project/conf/svnserve.conf
    打开 auth-access = write 授权用户可写
    password-db = passwd 
    2、vi /home/svn/project/conf/passwd
    添加用户
    [users]
    # harry = harryssecret
    # sally = sallyssecret
    cxl = xuelin
    wqx = qinxue
    3、vi /home/svn/project/conf/authz 
    admin = cxl
    @admin = rw
    * = 
    admin=cxl，cxl用户属于admin权限组，@admin=rw，admin权限组可以read，其他用户不能读取
    
* 守护进程方式启动svn ::
    
    svnserve -d -r /home/svn
      
* svnsync 同步测试

    1、在源地址创建项目svn://192.168.1.66/namtso/branch/web_code/svnsynctest
    2、vi /home/svn/svnsynctest/hooks/pre_revprop-change.bat
    添加一行exit 0
    3、配置权限，同上
    4、初始化：
    svnsync init  --source-username chenxl --source-password xuelin --sync-username chenxl  --sync-password xuelin svn://10.0.0.21/svnsynctest svn://192.168.1.66/namtso/branch/web_code/svnsynctest
    5、同步版本
    svnsync sync --source-username chenxl --source-password xuelin --sync-username chenxl  --sync-password xuelin svn://10.0.0.21/svnsynctest
        