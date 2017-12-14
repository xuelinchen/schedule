virtualbox
==========

install
----------

| 1、编辑source.list添加如下内容deb http://download.virtualbox.org/virtualbox/debian trusty contrib
| 2、wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
| 3、wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
| 4、apt-get update
| 5、apt-get install virtualbox-5.1
| 6、wget http://download.virtualbox.org/virtualbox/5.1.0/Oracle_VM_VirtualBox_Extension_Pack-5.1.0-108711.vbox-extpack 下载扩展
| 7、vboxmanage extpack install Oracle_VM_VirtualBox_Extension_Pack-5.1.0-108711.vbox-extpack 安装扩展 
| 8、vboxmanage list ostypes 查看支持的虚拟机类型
| 9、vboxmanage list vms 查看已存在的虚拟机

example
---------

* create vm ::

    vboxmanage createvm --name "ubuntu1204-base" --ostype "Ubuntu_64" --basefolder "/home/cxl/virtualbox/vm/" --register 创建虚拟机
    vboxmanage createhd --filename /home/cxl/virtualbox/vm/ubuntu1204-base/ubuntu1204-base --size 8000 创建虚拟硬盘
    vboxmanage storagectl "ubuntu1204-base" --add ide  --name "IDE Controller" --bootable on  创建ide接口
    vboxmanage storageattach "ubuntu1204-base" --storagectl "IDE Controller" --port 0 --device 0 --type hdd --medium "/home/cxl/virtualbox/vm/ubuntu1204-base/ubuntu1204-base.vdi" 虚拟机关联硬盘
    vboxmanage storageattach "ubuntu1204-base" --storagectl "IDE Controller" --port 1 --device 0 --type dvddrive --medium "/home/cxl/virtualbox/iso/ubuntu-12.04.1-server-amd64.iso" 虚拟机关联光驱，加入iso安装文件
    vboxmanage modifyvm "ubuntu1204-base" --vrde on --vrdeport 5001
    vboxmanage startvm "buildserver" --type headless
    
* delete vm ::

    vboxmanage unregistervm ubuntu1204-base --delete 删除虚拟机

* clone vm ::

    vboxmanage clonevm "ubuntu1204-base" --name "buildserver" --register --basefolder "/home/cxl/virtualbox/vm-root/" 
    vboxmanage startvm "buildserver" --type headless