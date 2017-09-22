# refer
	http://blog.csdn.net/Lj_550566181/article/details/52005698
	https://www.digitalocean.com/community/tutorials/how-to-install-java-on-ubuntu-with-apt-get
	https://cordova.apache.org/docs/en/7.x/guide/platforms/android/#installing-the-requirements
	
# install oracle java
	
	1. apt install python-software-properties
	2. add-apt-repository ppa:webupd8team/java
	3. apt install oracle-java8-installer
	4. update-alternatives --config java
		There is 1 choice for the alternative java (providing /usr/bin/java).
		
		  Selection    Path                                     Priority   Status
		------------------------------------------------------------
		  0            /usr/lib/jvm/java-8-oracle/jre/bin/java   1081      auto mode
		* 1            /usr/lib/jvm/java-8-oracle/jre/bin/java   1081      manual mode
	5. sudo nano /etc/environment
	6. add line JAVA_HOME=”/usr/lib/jvm/java-8-oracle“
	7. source /etc/environment
	8. echo $JAVA_HOME
	
# install android SDK
	
	1. wget http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
	2. tar xvf android-sdk_r24.4.1-linux.tgz 
	3. mv android-sdk-linux/ /usr/local
	4. nano /etc/environment 
		Set the ANDROID_HOME environment variable to the location of your Android SDK installation
		It is also recommended that you add the Android SDK's tools, tools/bin, and platform-tools directories to your PATH
		ANDROID_HOME="/usr/local/android-sdk-linux"
	5. source /etc/environment 

# install Gradle
	Gradle是一个基于Apache Ant和Apache Maven概念的项目自动化构建工具。它使用一种基于Groovy的特定领域语言(DSL)来声明项目设置，抛弃了基于XML的各种繁琐配置。
	Gradle是一个基于JVM的构建工具，是一款通用灵活的构建工具，支持maven， Ivy仓库，支持传递性依赖管理，而不需要远程仓库或者是pom.xml和ivy.xml配置文件，基于Groovy，build脚本使用Groovy编写。
	如果提前没有安装gradle，在ionic build android里面也会自动加载，但是慢到崩溃还容易出错，所以最好提前下载完毕，并且apt install 来的版本才2.1，太老，所以最好还是去官网下载
	1. wget https://services.gradle.org/distributions/gradle-4.1-all.zip
	2. unzip gradle-4.1-all.zip
	3. mv gradle-4.1 /opt
	4. nano /etc/environment
		$GRADLE_HOME/bin to PATH
	5. source /etc/environment

# install ionic
	1. npm install -g cordova ionic (install fail)
	
# window

##  install android studio
	http://tools.android-studio.org/index.php
	在 Android Studio 安装目录 bin/idea.properties 文件最后追加一句
	disable.android.first.run=true

	