# refer
# 配置
	1、vi /etc/network/interfaces
	2、配置
		# This file describes the network interfaces available on your system
		# and how to activate them. For more information, see interfaces(5).
		source /etc/network/interfaces.d/*
		# The loopback network interface
		auto lo
		iface lo inet loopback
		# The primary network interface
		auto enp0s3  # 网卡端口
		#iface enp0s3 inet dhcp  # dhcp自动获取ip
		iface enp0s3  inet static  # 静态ip
		address 10.0.0.42          # ip地址
		netmask 255.255.255.0      # 掩码
		gateway 10.0.0.254					# 网关
		dns-nameservers 202.106.0.20 8.8.8.8 # dns服务器地址
	3、重启network
		/etc/init.d/networking restart
~
~