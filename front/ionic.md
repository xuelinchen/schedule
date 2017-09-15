# install oracle java
	apt install python-software-properties
	add-apt-repository ppa:webupd8team/java
	apt install oracle-java8-installer
	update-alternatives --config java
		There is 1 choice for the alternative java (providing /usr/bin/java).
		
		  Selection    Path                                     Priority   Status
		------------------------------------------------------------
		  0            /usr/lib/jvm/java-8-oracle/jre/bin/java   1081      auto mode
		* 1            /usr/lib/jvm/java-8-oracle/jre/bin/java   1081      manual mode
	