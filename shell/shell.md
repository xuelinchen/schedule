# 空函数
	init(){ :; } 
	
# case
	 case "$optname" in
		"a")
		    # apache 发布端口
		   apache_publish_port=$OPTARG
		    ;;
		 *)
		 		exit
		 		;;
	 esac