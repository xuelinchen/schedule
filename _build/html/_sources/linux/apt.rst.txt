apt
====

refer
-------

none refer

command example
----------------

base method
^^^^^^^^^^^^
    * install package :: 
    
       	$ apt install package_name  -y
    
    * remove package  :: 
    
        $ apt autoremove --purge package_name -y
        $ apt remove --purge package_name -y
    
    * check package ::
    
        $ dpkg -l | grep package_name
  
install&remove Nginx
^^^^^^^^^^^^^^^^^^^^^
    * install nginx ::
    
        apt install nginx -y
        find /etc -name "*nginx*"
            /etc/logrotate.d/nginx
            /etc/rc1.d/K01nginx
            /etc/rc5.d/S02nginx
            /etc/nginx
            /etc/nginx/nginx.conf
            /etc/init.d/nginx
            /etc/rc3.d/S02nginx
            /etc/ufw/applications.d/nginx
            /etc/rc2.d/S02nginx
            /etc/rc0.d/K01nginx
            /etc/init/nginx.conf
            /etc/default/nginx
            /etc/systemd/system/multi-user.target.wants/nginx.service
            /etc/rc4.d/S02nginx
            /etc/rc6.d/K01nginx
        find /usr -name "*nginx*"
            /usr/sbin/nginx
            /usr/share/doc/nginx
            /usr/share/doc/nginx-common
            /usr/share/doc/nginx-core
            /usr/share/nginx
            /usr/share/vim/registry/nginx.yaml
            /usr/share/vim/addons/indent/nginx.vim
            /usr/share/vim/addons/syntax/nginx.vim
            /usr/share/vim/addons/ftdetect/nginx.vim
            /usr/share/lintian/overrides/nginx-common
            /usr/share/lintian/overrides/nginx-core
            /usr/share/apport/package-hooks/source_nginx.py
        find /lib -name "*nginx*"
            /lib/systemd/system/nginx.service
        dpkg -l | grep nginx
            ii  nginx           1.10.3-0ubuntu0.16.04.2     all          small, powerful, scalable web/proxy server
            ii  nginx-common    1.10.3-0ubuntu0.16.04.2     all          small, powerful, scalable web/proxy server - common files
            ii  nginx-core      1.10.3-0ubuntu0.16.04.2     amd64        nginx web/proxy server (core version)
    
    * remove nginx ::
       
        apt autoremove --purge nginx-common -y 直接删除nginx-common
        
    会自动卸载依赖nginx及配置文件，执行以上命令都为空
    
    
install&remove mysql
^^^^^^^^^^^^^^^^^^^^^
    * install mysql ::
    
        apt install mysql-server -y
        find /etc -name "*mysql*"
            /etc/logrotate.d/mysql-server
            /etc/logcheck/ignore.d.server/mysql-server-5_7
            /etc/logcheck/ignore.d.workstation/mysql-server-5_7
            /etc/logcheck/ignore.d.paranoid/mysql-server-5_7
            /etc/rc1.d/K02mysql
            /etc/rc5.d/S02mysql
            /etc/init.d/mysql
            /etc/rc3.d/S02mysql
            /etc/rc2.d/S02mysql
            /etc/rc0.d/K02mysql
            /etc/init/mysql.conf
            /etc/apparmor.d/usr.sbin.mysqld
            /etc/apparmor.d/local/usr.sbin.mysqld
            /etc/systemd/system/multi-user.target.wants/mysql.service
            /etc/mysql
            /etc/mysql/conf.d/mysql.cnf
            /etc/mysql/conf.d/mysqldump.cnf
            /etc/mysql/mysql.cnf
            /etc/mysql/mysql.conf.d
            /etc/mysql/mysql.conf.d/mysqld_safe_syslog.cnf
            /etc/mysql/mysql.conf.d/mysqld.cnf
            /etc/rc4.d/S02mysql
            /etc/rc6.d/K02mysql
        find /usr -name "*mysql*"
            /usr/lib/mysql
            /usr/lib/mysql/plugin/mysql_no_login.so
            /usr/sbin/mysqld
            /usr/bin/mysql_upgrade
            /usr/bin/mysql_embedded
            /usr/bin/mysqlpump
            /usr/bin/mysqldumpslow
            /usr/bin/mysql_secure_installation
            /usr/bin/mysqladmin
            /usr/bin/mysql_config_editor
            /usr/bin/mysqlcheck
            /usr/bin/mysqld_multi
            /usr/bin/mysqldump
            /usr/bin/mysqloptimize
            /usr/bin/mysql_tzinfo_to_sql
            /usr/bin/mysqlshow
            /usr/bin/mysqlimport
            /usr/bin/mysqlrepair
            /usr/bin/mysql_plugin
            /usr/bin/mysqlslap
            /usr/bin/mysqlreport
            /usr/bin/mysqld_safe
            /usr/bin/mysql
            /usr/bin/mysqlanalyze
            /usr/bin/mysqlbinlog
            /usr/bin/mysql_install_db
            /usr/bin/mysql_ssl_rsa_setup
            /usr/share/doc/mysql-server-5.7
            /usr/share/doc/mysql-server-5.7/mysqld.sym.gz
            /usr/share/doc/mysql-server
            /usr/share/doc/mysql-server-core-5.7
            /usr/share/doc/mysql-client-5.7
            /usr/share/doc/kamailio/examples/icscf/icscf.mysql.sql.gz
            /usr/share/doc/kamailio/examples/kamailio/acc-mysql.cfg.gz
            /usr/share/doc/mysql-common
            /usr/share/doc/mysql-client-core-5.7
            /usr/share/vim/vim74/syntax/mysql.vim
            /usr/share/mysql
            /usr/share/mysql/mysql-log-rotate
            /usr/share/mysql/mysql_security_commands.sql
            /usr/share/mysql/mysql_sys_schema.sql
            /usr/share/mysql/mysql_test_data_timezone.sql
            /usr/share/mysql/mysql-systemd-start
            /usr/share/mysql/mysqld_multi.server
            /usr/share/mysql/mysql_system_tables.sql
            /usr/share/mysql/mysql_system_tables_data.sql
            /usr/share/lintian/overrides/mysql-server-5.7
            /usr/share/lintian/overrides/mysql-client-5.7
            /usr/share/lintian/overrides/mysql-common
            /usr/share/man/man1/mysqldumpslow.1.gz
            /usr/share/man/man1/mysqloptimize.1.gz
            /usr/share/man/man1/mysqlpump.1.gz
            /usr/share/man/man1/mysqlshow.1.gz
            /usr/share/man/man1/mysql_upgrade.1.gz
            /usr/share/man/man1/mysql_config_editor.1.gz
            /usr/share/man/man1/mysqlbinlog.1.gz
            /usr/share/man/man1/mysqld_safe.1.gz
            /usr/share/man/man1/mysqlrepair.1.gz
            /usr/share/man/man1/mysqldump.1.gz
            /usr/share/man/man1/mysqlanalyze.1.gz
            /usr/share/man/man1/mysqlslap.1.gz
            /usr/share/man/man1/mysqld_multi.1.gz
            /usr/share/man/man1/mysql_secure_installation.1.gz
            /usr/share/man/man1/mysqlreport.1.gz
            /usr/share/man/man1/mysqlimport.1.gz
            /usr/share/man/man1/mysqlcheck.1.gz
            /usr/share/man/man1/mysql_plugin.1.gz
            /usr/share/man/man1/mysqladmin.1.gz
            /usr/share/man/man1/mysql.1.gz
            /usr/share/man/man1/mysql_embedded.1.gz
            /usr/share/man/man1/mysql_install_db.1.gz
            /usr/share/man/man1/mysql_ssl_rsa_setup.1.gz
            /usr/share/man/man1/mysqlman.1.gz
            /usr/share/man/man1/mysql_tzinfo_to_sql.1.gz
            /usr/share/man/man8/mysqld.8.gz
            /usr/share/sosreport/sos/plugins/mysql.py
            /usr/share/sosreport/sos/plugins/__pycache__/mysql.cpython-35.pyc
            /usr/share/apport/package-hooks/source_mysql-5.7.py
            /usr/share/bash-completion/completions/mysqladmin
            /usr/share/bash-completion/completions/mysql
            /usr/share/mysql-common
        find /lib -name "*mysql*"
            /lib/systemd/system/mysql.service
        dpkg -l | grep mysql
            ii  mysql-client-5.7                   5.7.19-0ubuntu0.16.04.1                    amd64        MySQL database client binaries
            ii  mysql-client-core-5.7              5.7.19-0ubuntu0.16.04.1                    amd64        MySQL database core client binaries
            ii  mysql-common                       5.7.19-0ubuntu0.16.04.1                    all          MySQL database common files, e.g. /etc/mysql/my.cnf
            ii  mysql-server                       5.7.19-0ubuntu0.16.04.1                    all          MySQL database server (metapackage depending on the latest version)
            ii  mysql-server-5.7                   5.7.19-0ubuntu0.16.04.1                    amd64        MySQL database server binaries and system database setup
            ii  mysql-server-core-5.7              5.7.19-0ubuntu0.16.04.1                    amd64        MySQL database server binaries
    
    * remove mysql ::
    
        apt autoremove --purge mysql-common -y 
        find /etc -name "*mysql*"
            /etc/mysql
        find /usr -name "*mysql*"
            /usr/share/doc/kamailio/examples/icscf/icscf.mysql.sql.gz
            /usr/share/doc/kamailio/examples/kamailio/acc-mysql.cfg.gz
            /usr/share/vim/vim74/syntax/mysql.vim
            /usr/share/sosreport/sos/plugins/mysql.py
            /usr/share/sosreport/sos/plugins/__pycache__/mysql.cpython-35.pyc
            /usr/share/bash-completion/completions/mysqladmin
            /usr/share/bash-completion/completions/mysql   
        这个配置目录没有删除，手动删除 
        rm /etc/mysql -rf 
        rm /var/lib/mysql -rf
    
install&remove redis
^^^^^^^^^^^^^^^^^^^^^
    * install redis ::
        
        apt install redis-server -y
        find /etc -name "*redis*"
            /etc/logrotate.d/redis-server
            /etc/rc1.d/K01redis-server
            /etc/rc5.d/S02redis-server
            /etc/redis
            /etc/redis/redis.conf
            /etc/redis/redis-server.pre-up.d
            /etc/redis/redis-server.post-down.d
            /etc/redis/redis-server.post-up.d
            /etc/redis/redis-server.pre-down.d
            /etc/init.d/redis-server
            /etc/rc3.d/S02redis-server
            /etc/rc2.d/S02redis-server
            /etc/rc0.d/K01redis-server
            /etc/default/redis-server
            /etc/systemd/system/multi-user.target.wants/redis-server.service
            /etc/systemd/system/redis.service
            /etc/rc4.d/S02redis-server
            /etc/rc6.d/K01redis-server
        find /usr -name "*redis*"
            /usr/lib/tmpfiles.d/redis-server.conf
            /usr/bin/redis-check-dump
            /usr/bin/redis-benchmark
            /usr/bin/redis-server
            /usr/bin/redis-cli
            /usr/bin/redis-check-aof
            /usr/share/doc/redis-server
            /usr/share/doc/redis-tools
            /usr/share/doc/redis-tools/examples/redis-trib.rb
            /usr/share/man/man1/redis-server.1.gz
            /usr/share/man/man1/redis-benchmark.1.gz
            /usr/share/man/man1/redis-cli.1.gz
            /usr/share/bash-completion/completions/bash_completion.d/redis-cli
        find /lib -name "*redis*"
            /lib/systemd/system/redis-server.service
        dpkg -l | grep redis
            ii  redis-server  2:3.0.6-1      amd64        Persistent key-value database with network interface
            ii  redis-tools   2:3.0.6-1      amd64        Persistent key-value database with network interface (client)
        
    * remove redis ::
    
        所有内容都返回空
        apt autoremove --purge redis-server -y 
    
install&remove apache
^^^^^^^^^^^^^^^^^^^^^^^
    * install apache ::
    
        apt install apache2 -y
        find /etc -name "*apache*"
            /etc/logrotate.d/apache2
            /etc/rc1.d/K01apache-htcacheclean
            /etc/rc1.d/K01apache2
            /etc/rc5.d/K01apache-htcacheclean
            /etc/rc5.d/S02apache2
            /etc/init.d/apache2
            /etc/init.d/apache-htcacheclean
            /etc/rc3.d/K01apache-htcacheclean
            /etc/rc3.d/S02apache2
            /etc/ufw/applications.d/apache2
            /etc/ufw/applications.d/apache2-utils.ufw.profile
            /etc/apache2
            /etc/apache2/apache2.conf
            /etc/rc2.d/K01apache-htcacheclean
            /etc/rc2.d/S02apache2
            /etc/rc0.d/K01apache-htcacheclean
            /etc/rc0.d/K01apache2
            /etc/default/apache-htcacheclean
            /etc/cron.daily/apache2
            /etc/rc4.d/K01apache-htcacheclean
            /etc/rc4.d/S02apache2
            /etc/rc6.d/K01apache-htcacheclean
            /etc/rc6.d/K01apache2
        find /usr -name "*apache*"
            /usr/lib/apache2
            /usr/sbin/apachectl
            /usr/sbin/apache2ctl
            /usr/sbin/apache2
            /usr/share/doc/apache2-bin
            /usr/share/doc/apache2
            /usr/share/doc/apache2/examples/apache2.monit
            /usr/share/doc/apache2-data
            /usr/share/doc/apache2-utils
            /usr/share/apache2
            /usr/share/apache2/apache2-maintscript-helper
            /usr/share/apache2/icons/apache_pb.png
            /usr/share/apache2/icons/apache_pb.gif
            /usr/share/apache2/icons/apache_pb.svg
            /usr/share/apache2/icons/apache_pb2.gif
            /usr/share/apache2/icons/apache_pb2.png
            /usr/share/vim/vim74/syntax/apachestyle.vim
            /usr/share/vim/vim74/syntax/apache.vim
            /usr/share/bug/apache2-bin
            /usr/share/bug/apache2
            /usr/share/lintian/overrides/apache2-bin
            /usr/share/lintian/overrides/apache2
            /usr/share/lintian/overrides/apache2-data
            /usr/share/man/man8/apache2.8.gz
            /usr/share/man/man8/apachectl.8.gz
            /usr/share/man/man8/apache2ctl.8.gz
            /usr/share/sosreport/sos/plugins/__pycache__/apache.cpython-35.pyc
            /usr/share/sosreport/sos/plugins/apache.py
            /usr/share/apport/package-hooks/apache2.py
            /usr/share/bash-completion/completions/apache2ctl
        find /lib -name "*apache*"
            /lib/systemd/system/apache2.service.d
            /lib/systemd/system/apache2.service.d/apache2-systemd.conf
        dpkg -l | grep apache
            ii  apache2          2.4.18-2ubuntu3.4    amd64        Apache HTTP Server
            ii  apache2-bin      2.4.18-2ubuntu3.4    amd64        Apache HTTP Server (modules and other binary files)
            ii  apache2-data     2.4.18-2ubuntu3.4    all          Apache HTTP Server (common files)
            ii  apache2-utils    2.4.18-2ubuntu3.4    amd64        Apache HTTP Server (utility programs for web servers)
        
    * remove apache ::
    
        apt autoremove --purge apache2 -y 满足需求

install&remove php
^^^^^^^^^^^^^^^^^^^^^

    * install php ::
    
        apt install apache2 -y                  安装apache2
        apt install mysql-server -y             安装mysql
        apt install php7.0 -y
        find /etc -name "*php*"
            /etc/logrotate.d/php7.0-fpm
            /etc/rc1.d/K01php7.0-fpm
            /etc/rc5.d/S01php7.0-fpm
            /etc/alternatives/php.1.gz
            /etc/alternatives/php
            /etc/init.d/php7.0-fpm
            /etc/rc3.d/S01php7.0-fpm
            /etc/apache2/conf-available/php7.0-fpm.conf
            /etc/rc2.d/S01php7.0-fpm
            /etc/rc0.d/K01php7.0-fpm
            /etc/php
            /etc/php/7.0/fpm/php-fpm.conf
            /etc/php/7.0/fpm/php.ini
            /etc/php/7.0/cli/php.ini
            /etc/init/php7.0-fpm.conf
            /etc/apparmor.d/abstractions/php5
            /etc/systemd/system/multi-user.target.wants/php7.0-fpm.service
            /etc/rc4.d/S01php7.0-fpm
            /etc/cron.d/php
            /etc/rc6.d/K01php7.0-fpm
        find /usr -name "*php*"
            /usr/lib/tmpfiles.d/php7.0-fpm.conf
            /usr/lib/php
            /usr/lib/php/php7.0-fpm-reopenlogs
            /usr/lib/php/php-maintscript-helper
            /usr/lib/php/php7.0-fpm-checkconf
            /usr/lib/php/php-helper
            /usr/lib/php/7.0/php.ini-production
            /usr/lib/php/7.0/php.ini-production.cli
            /usr/lib/php/7.0/php.ini-development
            /usr/sbin/phpenmod
            /usr/sbin/phpdismod
            /usr/sbin/phpquery
            /usr/sbin/php-fpm7.0
            /usr/bin/php7.0
            /usr/bin/php
            /usr/share/doc/php7.0
            /usr/share/doc/php7.0-readline
            /usr/share/doc/php-common
            /usr/share/doc/php7.0-json
            /usr/share/doc/php7.0-cli
            /usr/share/doc/php7.0-fpm
            /usr/share/doc/php7.0-common
            /usr/share/doc/kamailio/examples/web_im/click_to_dial.php
            /usr/share/doc/kamailio/examples/web_im/send_im.php
            /usr/share/doc/kamailio/examples/kamailio/web_im/click_to_dial.php
            /usr/share/doc/kamailio/examples/kamailio/web_im/send_im.php
            /usr/share/doc/php7.0-opcache
            /usr/share/php7.0-readline
            /usr/share/vim/vim74/autoload/phpcomplete.vim
            /usr/share/vim/vim74/indent/php.vim
            /usr/share/vim/vim74/syntax/php.vim
            /usr/share/vim/vim74/ftplugin/php.vim
            /usr/share/vim/vim74/compiler/php.vim
            /usr/share/php7.0-json
            /usr/share/nano/php.nanorc
            /usr/share/bug/php7.0
            /usr/share/bug/php7.0-readline
            /usr/share/bug/php7.0-json
            /usr/share/bug/php7.0-cli
            /usr/share/bug/php7.0-fpm
            /usr/share/bug/php7.0-common
            /usr/share/bug/php7.0-opcache
            /usr/share/mime/application/x-php.xml
            /usr/share/php
            /usr/share/lintian/overrides/php7.0-readline
            /usr/share/lintian/overrides/php7.0-json
            /usr/share/lintian/overrides/php7.0-cli
            /usr/share/lintian/overrides/php7.0-fpm
            /usr/share/lintian/overrides/php7.0-common
            /usr/share/lintian/overrides/php7.0-opcache
            /usr/share/php7.0-common
            /usr/share/man/man1/php.1.gz
            /usr/share/man/man1/php7.0.1.gz
            /usr/share/man/man8/php-fpm7.0.8.gz
            /usr/share/php7.0-opcache
        find /lib -name "*php*"
            /lib/modules/4.4.0-92-generic/kernel/drivers/pci/hotplug/acpiphp_ibm.ko
            /lib/modules/4.4.0-91-generic/kernel/drivers/pci/hotplug/acpiphp_ibm.ko
            /lib/modules/4.4.0-93-generic/kernel/drivers/pci/hotplug/acpiphp_ibm.ko
            /lib/systemd/system/php7.0-fpm.service
        dpkg -l | grep php
            ii  php-common                         1:35ubuntu6                                all          Common files for PHP packages
            ii  php7.0                             7.0.22-0ubuntu0.16.04.1                    all          server-side, HTML-embedded scripting language (metapackage)
            ii  php7.0-cli                         7.0.22-0ubuntu0.16.04.1                    amd64        command-line interpreter for the PHP scripting language
            ii  php7.0-common                      7.0.22-0ubuntu0.16.04.1                    amd64        documentation, examples and common module for PHP
            ii  php7.0-fpm                         7.0.22-0ubuntu0.16.04.1                    amd64        server-side, HTML-embedded scripting language (FPM-CGI binary)
            ii  php7.0-json                        7.0.22-0ubuntu0.16.04.1                    amd64        JSON module for PHP
            ii  php7.0-opcache                     7.0.22-0ubuntu0.16.04.1                    amd64        Zend OpCache module for PHP
            ii  php7.0-readline                    7.0.22-0ubuntu0.16.04.1                    amd64        readline module for PHP
    
    * remove php ::
        
        apt autoremove --purge php-common -y 
        find /etc -name "*php*"
            /etc/php
            /etc/apparmor.d/abstractions/php5
        rm /etc/php -rf
    
install&remove other
^^^^^^^^^^^^^^^^^^^^^
    * install ::
        
        apt install php7.0-curl -y
        find /etc -name "*curl*"
            /etc/php/7.0/mods-available/curl.ini
            /etc/php/7.0/fpm/conf.d/20-curl.ini
            /etc/php/7.0/cli/conf.d/20-curl.ini
        find /usr -name "*php7.0-curl*"
            /usr/share/doc/php7.0-curl
            /usr/share/bug/php7.0-curl
            /usr/share/php7.0-curl
            /usr/share/lintian/overrides/php7.0-curl
        find /lib -name "*curl*"
        dpkg -l | grep php7.0-curl
            ii  php7.0-curl                        7.0.22-0ubuntu0.16.04.1                    amd64        CURL module for PHP
        
        apt install php7.0-mbstring -y
        find /etc -name "*mbstring*"
            /etc/php/7.0/mods-available/mbstring.ini
            /etc/php/7.0/fpm/conf.d/20-mbstring.ini
            /etc/php/7.0/cli/conf.d/20-mbstring.ini
        find /usr -name "*mbstring*"
            /usr/lib/php/20151012/mbstring.so
            /usr/share/doc/php7.0-mbstring
            /usr/share/php7.0-mbstring
            /usr/share/php7.0-mbstring/mbstring
            /usr/share/php7.0-mbstring/mbstring/mbstring.ini
            /usr/share/bug/php7.0-mbstring
            /usr/share/lintian/overrides/php7.0-mbstring
        find /lib -name "*mbstring*"
        dpkg -l | grep mbstring
            ii  php7.0-mbstring                    7.0.22-0ubuntu0.16.04.1                    amd64        MBSTRING module for PHP
        
        apt install libapache2-mod-php7.0 -y
        vi /etc/apache2/mods-enabled/php7.0.load
            LoadModule php7_module /usr/lib/apache2/modules/libphp7.0.so
        find /etc -name "*libapache2*"
        find /usr -name "*libapache2*"
        find /lib -name "*libapache2*"
        dpkg -l | grep libapache2
            ii  libapache2-mod-php7.0              7.0.22-0ubuntu0.16.04.1                    amd64        server-side, HTML-embedded scripting language (Apache 2 module)
            
        apt install php7.0-gd -y
        find /etc -name "*gd.ini"
            /etc/php/7.0/apache2/conf.d/20-gd.ini
            /etc/php/7.0/mods-available/gd.ini
            /etc/php/7.0/fpm/conf.d/20-gd.ini
            /etc/php/7.0/cli/conf.d/20-gd.ini
        find /usr -name "*gd"
            /usr/sbin/rsyslogd
            /usr/share/doc/php7.0-gd
            /usr/share/bug/php7.0-gd
            /usr/share/locale/gd
            /usr/share/lintian/overrides/php7.0-gd
            /usr/share/php7.0-gd
            /usr/share/php7.0-gd/gd
        ls /usr/lib/php/20151012/gd*
            /usr/lib/php/20151012/gd.so
        dpkg -l | grep php7.0-gd
            ii  php7.0-gd                          7.0.22-0ubuntu0.16.04.1                    amd64        GD module for PHP
        
        apt install php7.0-mysql -y
        ls /usr/lib/php/20151012/mysql*
            /usr/lib/php/20151012/mysqli.so  /usr/lib/php/20151012/mysqlnd.so
        find /etc -name "mysql*.ini"
            /etc/php/7.0/mods-available/mysqli.ini
            /etc/php/7.0/mods-available/mysqlnd.ini
        dpkg -l | grep php7.0-mysql
            ii  php7.0-mysql                       7.0.22-0ubuntu0.16.04.1                    amd64        MySQL module for PHP
        
        apt install php-redis -y
        ls /usr/lib/php/20151012/redis* 
            /usr/lib/php/20151012/redis.so
        find /etc -name "redis*.ini"
            /etc/php/7.0/mods-available/redis.ini
        dpkg -l | grep php-redis
            ii  php-redis                          2.2.7-389-g2887ad1+2.2.7-1                 amd64        PHP extension for interfacing with Redis
            
        apt install mcrypt -y
        apt install libmcrypt-dev -y
        
        apt install php-mcrypt -y
        ls /usr/lib/php/20151012/mcrypt*
            /usr/lib/php/20151012/mcrypt.so
        find /etc -name "mcrypt*.ini"
            /etc/php/7.0/mods-available/mcrypt.ini
        dpkg -l | grep mcrypt | grep "php"
            ii  php-mcrypt                         1:7.0+35ubuntu6                            all          libmcrypt module for PHP [default]
            ii  php7.0-mcrypt                      7.0.22-0ubuntu0.16.04.1                    amd64        libmcrypt module for PHP
        
    
    * remove  ::

        先删除依赖mysql，apache的包，mcrypt和libmcrypt-dev是系统包，不删除
        apt autoremove --purge libapache2-mod-php7.0 -y 
        ls /etc/apache2/mods-enabled/php*
        dpkg -l | grep libapache2
        ls /usr/lib/apache2/modules/libphp7.0.so
        执行命令均未发现残余
        apt autoremove --purge php7.0-mysql -y 
        执行命令均未发现残余
        删除php
        apt autoremove --purge php-common -y 
        ls /usr/lib/php
            ls: cannot access '/usr/lib/php': No such file or directory
        find /etc -name "*php*"
            /etc/php
            /etc/apparmor.d/abstractions/php5
        rm /etc/php -rf

   
.. attention::
   以上软件是基于SPI系统测试，运行在ubuntu16.04上!

