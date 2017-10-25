#  update-rc.d 
	update-rc.d: error: not enough arguments
	usage: update-rc.d [-n] [-f] <basename> remove
	       update-rc.d [-n] <basename> disable|enable [S|2|3|4|5]
	                -n: not really
	                -f: force	
	The disable|enable API is not stable and might change in the future.
	
# example
## 添加启动项
	sudo update-rc.d   apache2 defaults  
	sudo update-rc.d   nginx defaults  
	sudo update-rc.d   redis_6379 defaults  
## 删除启动项
	sudo update-rc.d -f apache2 remove  
	sudo update-rc.d -f nginx remove  
	sudo update-rc.d -f redis_6379 remove  