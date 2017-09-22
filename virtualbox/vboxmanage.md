# install
	1、编辑source.list添加如下内容deb http://download.virtualbox.org/virtualbox/debian trusty contrib
	2、wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
	3、wget -q https://www.virtualbox.org/download/oracle_vbox.asc -O- | sudo apt-key add -
	4、apt-get update
	5、apt-get install virtualbox-5.1
	6、wget http://download.virtualbox.org/virtualbox/5.1.0/Oracle_VM_VirtualBox_Extension_Pack-5.1.0-108711.vbox-extpack 下载扩展
	7、vboxmanage extpack install Oracle_VM_VirtualBox_Extension_Pack-5.1.0-108711.vbox-extpack 安装扩展 
	8、vboxmanage list ostypes 查看支持的虚拟机类型
	9、vboxmanage list vms 查看已存在的虚拟机
	
# vboxmanage --help
	Oracle VM VirtualBox Command Line Management Interface Version 4.3.36_Ubuntu
	(C) 2005-2016 Oracle Corporation
	All rights reserved.
	
	Usage:
	
	  VBoxManage [<general option>] <command>
	 
	 
	General Options:
	 
	  [-v|--version]            print version number and exit
	  [-q|--nologo]             suppress the logo
	  [--settingspw <pw>]       provide the settings password
	  [--settingspwfile <file>] provide a file containing the settings password
	 
	 
	Commands:
	 
	  list [--long|-l]          vms|runningvms|ostypes|hostdvds|hostfloppies|
	                            intnets|bridgedifs|hostonlyifs|natnets|dhcpservers|
	                            hostinfo|hostcpuids|hddbackends|hdds|dvds|floppies|
	                            usbhost|usbfilters|systemproperties|extpacks|
	                            groups|webcams
	
	  showvminfo                <uuid|vmname> [--details]
	                            [--machinereadable]
	  showvminfo                <uuid|vmname> --log <idx>
	
	  registervm                <filename>
	
	  unregistervm              <uuid|vmname> [--delete]
	
	  createvm                  --name <name>
	                            [--groups <group>, ...]
	                            [--ostype <ostype>]
	                            [--register]
	                            [--basefolder <path>]
	                            [--uuid <uuid>]
	
	  modifyvm                  <uuid|vmname>
	                            [--name <name>]
	                            [--groups <group>, ...]
	                            [--description <desc>]
	                            [--ostype <ostype>]
	                            [--iconfile <filename>]
	                            [--memory <memorysize in MB>]
	                            [--pagefusion on|off]
	                            [--vram <vramsize in MB>]
	                            [--acpi on|off]
	                            [--pciattach 03:04.0]
	                            [--pciattach 03:04.0@02:01.0]
	                            [--pcidetach 03:04.0]
	                            [--ioapic on|off]
	                            [--hpet on|off]
	                            [--triplefaultreset on|off]
	                            [--hwvirtex on|off]
	                            [--nestedpaging on|off]
	                            [--largepages on|off]
	                            [--vtxvpid on|off]
	                            [--vtxux on|off]
	                            [--pae on|off]
	                            [--longmode on|off]
	                            [--synthcpu on|off]
	                            [--cpuidset <leaf> <eax> <ebx> <ecx> <edx>]
	                            [--cpuidremove <leaf>]
	                            [--cpuidremoveall]
	                            [--hardwareuuid <uuid>]
	                            [--cpus <number>]
	                            [--cpuhotplug on|off]
	                            [--plugcpu <id>]
	                            [--unplugcpu <id>]
	                            [--cpuexecutioncap <1-100>]
	                            [--rtcuseutc on|off]
	                            [--graphicscontroller none|vboxvga|vmsvga]
	                            [--monitorcount <number>]
	                            [--accelerate3d on|off]
	                            [--accelerate2dvideo on|off]
	                            [--firmware bios|efi|efi32|efi64]
	                            [--chipset ich9|piix3]
	                            [--bioslogofadein on|off]
	                            [--bioslogofadeout on|off]
	                            [--bioslogodisplaytime <msec>]
	                            [--bioslogoimagepath <imagepath>]
	                            [--biosbootmenu disabled|menuonly|messageandmenu]
	                            [--biossystemtimeoffset <msec>]
	                            [--biospxedebug on|off]
	                            [--boot<1-4> none|floppy|dvd|disk|net>]
	                            [--nic<1-N> none|null|nat|bridged|intnet|hostonly|
	                                        generic|natnetwork]
	                            [--nictype<1-N> Am79C970A|Am79C973|
	                                            82540EM|82543GC|82545EM|
	                                            virtio]
	                            [--cableconnected<1-N> on|off]
	                            [--nictrace<1-N> on|off]
	                            [--nictracefile<1-N> <filename>]
	                            [--nicproperty<1-N> name=[value]]
	                            [--nicspeed<1-N> <kbps>]
	                            [--nicbootprio<1-N> <priority>]
	                            [--nicpromisc<1-N> deny|allow-vms|allow-all]
	                            [--nicbandwidthgroup<1-N> none|<name>]
	                            [--bridgeadapter<1-N> none|<devicename>]
	                            [--hostonlyadapter<1-N> none|<devicename>]
	                            [--intnet<1-N> <network name>]
	                            [--nat-network<1-N> <network name>]
	                            [--nicgenericdrv<1-N> <driver>
	                            [--natnet<1-N> <network>|default]
	                            [--natsettings<1-N> [<mtu>],[<socksnd>],
	                                                [<sockrcv>],[<tcpsnd>],
	                                                [<tcprcv>]]
	                            [--natpf<1-N> [<rulename>],tcp|udp,[<hostip>],
	                                          <hostport>,[<guestip>],<guestport>]
	                            [--natpf<1-N> delete <rulename>]
	                            [--nattftpprefix<1-N> <prefix>]
	                            [--nattftpfile<1-N> <file>]
	                            [--nattftpserver<1-N> <ip>]
	                            [--natbindip<1-N> <ip>
	                            [--natdnspassdomain<1-N> on|off]
	                            [--natdnsproxy<1-N> on|off]
	                            [--natdnshostresolver<1-N> on|off]
	                            [--nataliasmode<1-N> default|[log],[proxyonly],
	                                                         [sameports]]
	                            [--macaddress<1-N> auto|<mac>]
	                            [--mouse ps2|usb|usbtablet|usbmultitouch]
	                            [--keyboard ps2|usb
	                            [--uart<1-N> off|<I/O base> <IRQ>]
	                            [--uartmode<1-N> disconnected|
	                                             server <pipe>|
	                                             client <pipe>|
	                                             file <file>|
	                                             <devicename>]
	                            [--lpt<1-N> off|<I/O base> <IRQ>]
	                            [--lptmode<1-N> <devicename>]
	                            [--guestmemoryballoon <balloonsize in MB>]
	                            [--audio none|null|oss|alsa|pulse]
	                            [--audiocontroller ac97|hda|sb16]
	                            [--clipboard disabled|hosttoguest|guesttohost|
	                                         bidirectional]
	                            [--draganddrop disabled|hosttoguest
	                            [--vrde on|off]
	                            [--vrdeextpack default|<name>
	                            [--vrdeproperty <name=[value]>]
	                            [--vrdeport <hostport>]
	                            [--vrdeaddress <hostip>]
	                            [--vrdeauthtype null|external|guest]
	                            [--vrdeauthlibrary default|<name>
	                            [--vrdemulticon on|off]
	                            [--vrdereusecon on|off]
	                            [--vrdevideochannel on|off]
	                            [--vrdevideochannelquality <percent>]
	                            [--usb on|off]
	                            [--usbehci on|off]
	                            [--snapshotfolder default|<path>]
	                            [--teleporter on|off]
	                            [--teleporterport <port>]
	                            [--teleporteraddress <address|empty>
	                            [--teleporterpassword <password>]
	                            [--teleporterpasswordfile <file>|stdin]
	                            [--tracing-enabled on|off]
	                            [--tracing-config <config-string>]
	                            [--tracing-allow-vm-access on|off]
	                            [--usbcardreader on|off]
	                            [--autostart-enabled on|off]
	                            [--autostart-delay <seconds>]
	                            [--vcpenabled on|off]
	                            [--vcpscreens [<display>],...
	                            [--vcpfile <filename>]
	                            [--vcpwidth <width>]
	                            [--vcpheight <height>]
	                            [--vcprate <rate>]
	                            [--vcpfps <fps>]
	                            [--defaultfrontend default|<name>]
	
	  clonevm                   <uuid|vmname>
	                            [--snapshot <uuid>|<name>]
	                            [--mode machine|machineandchildren|all]
	                            [--options link|keepallmacs|keepnatmacs|
	                                       keepdisknames]
	                            [--name <name>]
	                            [--groups <group>, ...]
	                            [--basefolder <basefolder>]
	                            [--uuid <uuid>]
	                            [--register]
	
	  import                    <ovfname/ovaname>
	                            [--dry-run|-n]
	                            [--options keepallmacs|keepnatmacs]
	                            [more options]
	                            (run with -n to have options displayed
	                             for a particular OVF)
	
	  export                    <machines> --output|-o <name>.<ovf/ova>
	                            [--legacy09|--ovf09|--ovf10|--ovf20]
	                            [--manifest]
	                            [--iso]
	                            [--options manifest|iso|nomacs|nomacsbutnat]
	                            [--vsys <number of virtual system>]
	                                    [--product <product name>]
	                                    [--producturl <product url>]
	                                    [--vendor <vendor name>]
	                                    [--vendorurl <vendor url>]
	                                    [--version <version info>]
	                                    [--description <description info>]
	                                    [--eula <license text>]
	                                    [--eulafile <filename>]
	
	  startvm                   <uuid|vmname>...
	                            [--type gui|sdl|headless]
	
	  controlvm                 <uuid|vmname>
	                            pause|resume|reset|poweroff|savestate|
	                            acpipowerbutton|acpisleepbutton|
	                            keyboardputscancode <hex> [<hex> ...]|
	                            setlinkstate<1-N> on|off |
	                            nic<1-N> null|nat|bridged|intnet|hostonly|generic|
	                                     natnetwork [<devicename>] |
	                            nictrace<1-N> on|off |
	                            nictracefile<1-N> <filename> |
	                            nicproperty<1-N> name=[value] |
	                            nicpromisc<1-N> deny|allow-vms|allow-all |
	                            natpf<1-N> [<rulename>],tcp|udp,[<hostip>],
	                                        <hostport>,[<guestip>],<guestport> |
	                            natpf<1-N> delete <rulename> |
	                            guestmemoryballoon <balloonsize in MB> |
	                            usbattach <uuid>|<address> |
	                            usbdetach <uuid>|<address> |
	                            clipboard disabled|hosttoguest|guesttohost|
	                                      bidirectional |
	                            draganddrop disabled|hosttoguest |
	                            vrde on|off |
	                            vrdeport <port> |
	                            vrdeproperty <name=[value]> |
	                            vrdevideochannelquality <percent> |
	                            setvideomodehint <xres> <yres> <bpp>
	                                            [[<display>] [<enabled:yes|no> |
	                                              [<xorigin> <yorigin>]]] |
	                            screenshotpng <file> [display] |
	                            vcpenabled on|off |
	                            vcpscreens all|none|<screen>,[<screen>...] |
	                            setcredentials <username>
	                                           --passwordfile <file> | <password>
	                                           <domain>
	                                           [--allowlocallogon <yes|no>] |
	                            teleport --host <name> --port <port>
	                                     [--maxdowntime <msec>]
	                                     [--passwordfile <file> |
	                                      --password <password>] |
	                            plugcpu <id> |
	                            unplugcpu <id> |
	                            cpuexecutioncap <1-100>
	                            webcam <attach [path [settings]]> | <detach [path]> | <list>
	
	  discardstate              <uuid|vmname>
	
	  adoptstate                <uuid|vmname> <state_file>
	
	  snapshot                  <uuid|vmname>
	                            take <name> [--description <desc>] [--live] |
	                            delete <uuid|snapname> |
	                            restore <uuid|snapname> |
	                            restorecurrent |
	                            edit <uuid|snapname>|--current
	                                 [--name <name>]
	                                 [--description <desc>] |
	                            list [--details|--machinereadable]
	                            showvminfo <uuid|snapname>
	
	  closemedium               disk|dvd|floppy <uuid|filename>
	                            [--delete]
	
	  storageattach             <uuid|vmname>
	                            --storagectl <name>
	                            [--port <number>]
	                            [--device <number>]
	                            [--type dvddrive|hdd|fdd]
	                            [--medium none|emptydrive|additions|
	                                      <uuid|filename>|host:<drive>|iscsi]
	                            [--mtype normal|writethrough|immutable|shareable|
	                                     readonly|multiattach]
	                            [--comment <text>]
	                            [--setuuid <uuid>]
	                            [--setparentuuid <uuid>]
	                            [--passthrough on|off]
	                            [--tempeject on|off]
	                            [--nonrotational on|off]
	                            [--discard on|off]
	                            [--bandwidthgroup <name>]
	                            [--forceunmount]
	                            [--server <name>|<ip>]
	                            [--target <target>]
	                            [--tport <port>]
	                            [--lun <lun>]
	                            [--encodedlun <lun>]
	                            [--username <username>]
	                            [--password <password>]
	                            [--initiator <initiator>]
	                            [--intnet]
	
	  storagectl                <uuid|vmname>
	                            --name <name>
	                            [--add ide|sata|scsi|floppy|sas]
	                            [--controller LSILogic|LSILogicSAS|BusLogic|
	                                          IntelAHCI|PIIX3|PIIX4|ICH6|I82078]
	                            [--portcount <1-30>]
	                            [--hostiocache on|off]
	                            [--bootable on|off]
	                            [--remove]
	
	  bandwidthctl              <uuid|vmname>
	                            add <name> --type disk|network
	                                --limit <megabytes per second>[k|m|g|K|M|G] |
	                            set <name>
	                                --limit <megabytes per second>[k|m|g|K|M|G] |
	                            remove <name> |
	                            list [--machinereadable]
	                            (limit units: k=kilobit, m=megabit, g=gigabit,
	                                          K=kilobyte, M=megabyte, G=gigabyte)
	
	  showhdinfo                <uuid|filename>
	
	  createhd                  --filename <filename>
	                            [--size <megabytes>|--sizebyte <bytes>]
	                            [--diffparent <uuid>|<filename>
	                            [--format VDI|VMDK|VHD] (default: VDI)
	                            [--variant Standard,Fixed,Split2G,Stream,ESX]
	
	  modifyhd                  <uuid|filename>
	                            [--type normal|writethrough|immutable|shareable|
	                                    readonly|multiattach]
	                            [--autoreset on|off]
	                            [--property <name=[value]>]
	                            [--compact]
	                            [--resize <megabytes>|--resizebyte <bytes>]
	
	  clonehd                   <uuid|inputfile> <uuid|outputfile>
	                            [--format VDI|VMDK|VHD|RAW|<other>]
	                            [--variant Standard,Fixed,Split2G,Stream,ESX]
	                            [--existing]
	
	  convertfromraw            <filename> <outputfile>
	                            [--format VDI|VMDK|VHD]
	                            [--variant Standard,Fixed,Split2G,Stream,ESX]
	                            [--uuid <uuid>]
	  convertfromraw            stdin <outputfile> <bytes>
	                            [--format VDI|VMDK|VHD]
	                            [--variant Standard,Fixed,Split2G,Stream,ESX]
	                            [--uuid <uuid>]
	
	  getextradata              global|<uuid|vmname>
	                            <key>|enumerate
	
	  setextradata              global|<uuid|vmname>
	                            <key>
	                            [<value>] (no value deletes key)
	
	  setproperty               machinefolder default|<folder> |
	                            hwvirtexclusive on|off |
	                            vrdeauthlibrary default|<library> |
	                            websrvauthlibrary default|null|<library> |
	                            vrdeextpack null|<library> |
	                            autostartdbpath null|<folder> |
	                            loghistorycount <value>
	                            defaultfrontend default|<name>
	                            logginglevel <log setting>
	
	  usbfilter                 add <index,0-N>
	                            --target <uuid|vmname>|global
	                            --name <string>
	                            --action ignore|hold (global filters only)
	                            [--active yes|no] (yes)
	                            [--vendorid <XXXX>] (null)
	                            [--productid <XXXX>] (null)
	                            [--revision <IIFF>] (null)
	                            [--manufacturer <string>] (null)
	                            [--product <string>] (null)
	                            [--remote yes|no] (null, VM filters only)
	                            [--serialnumber <string>] (null)
	                            [--maskedinterfaces <XXXXXXXX>]
	
	  usbfilter                 modify <index,0-N>
	                            --target <uuid|vmname>|global
	                            [--name <string>]
	                            [--action ignore|hold] (global filters only)
	                            [--active yes|no]
	                            [--vendorid <XXXX>|""]
	                            [--productid <XXXX>|""]
	                            [--revision <IIFF>|""]
	                            [--manufacturer <string>|""]
	                            [--product <string>|""]
	                            [--remote yes|no] (null, VM filters only)
	                            [--serialnumber <string>|""]
	                            [--maskedinterfaces <XXXXXXXX>]
	
	  usbfilter                 remove <index,0-N>
	                            --target <uuid|vmname>|global
	
	  sharedfolder              add <uuid|vmname>
	                            --name <name> --hostpath <hostpath>
	                            [--transient] [--readonly] [--automount]
	
	  sharedfolder              remove <uuid|vmname>
	                            --name <name> [--transient]
	
	  guestproperty             get <uuid|vmname>
	                            <property> [--verbose]
	
	  guestproperty             set <uuid|vmname>
	                            <property> [<value> [--flags <flags>]]
	
	  guestproperty             delete|unset <uuid|vmname>
	                            <property>
	
	  guestproperty             enumerate <uuid|vmname>
	                            [--patterns <patterns>]
	
	  guestproperty             wait <uuid|vmname> <patterns>
	                            [--timeout <msec>] [--fail-on-timeout]
	
	  guestcontrol              <uuid|vmname>
	
	                              exec[ute]
	                              --image <path to program> --username <name>
	                              [--passwordfile <file> | --password <password>]
	                              [--domain <domain>] [--verbose] [--timeout <msec>]
	                              [--environment "<NAME>=<VALUE> [<NAME>=<VALUE>]"]
	                              [--wait-exit] [--wait-stdout] [--wait-stderr]
	                              [--dos2unix] [--unquoted-args] [--unix2dos]
	                              [-- [<argument1>] ... [<argumentN>]]
	
	                              copyfrom
	                              <guest source> <host dest> --username <name>
	                              [--passwordfile <file> | --password <password>]
	                              [--domain <domain>] [--verbose]
	                              [--dryrun] [--follow] [--recursive]
	
	                              copyto|cp
	                              <host source> <guest dest> --username <name>
	                              [--passwordfile <file> | --password <password>]
	                              [--domain <domain>] [--verbose]
	                              [--dryrun] [--follow] [--recursive]
	
	                              createdir[ectory]|mkdir|md
	                              <guest directory>... --username <name>
	                              [--passwordfile <file> | --password <password>]
	                              [--domain <domain>] [--verbose]
	                              [--parents] [--mode <mode>]
	
	                              removedir[ectory]|rmdir
	                              <guest directory>... --username <name>
	                              [--passwordfile <file> | --password <password>]
	                              [--domain <domain>] [--verbose]
	                              [--recursive|-R|-r]
	
	                              removefile|rm
	                              <guest file>... --username <name>
	                              [--passwordfile <file> | --password <password>]
	                              [--domain <domain>] [--verbose]
	
	                              ren[ame]|mv
	                              <source>... <dest> --username <name>
	                              [--passwordfile <file> | --password <password>]
	                              [--domain <domain>] [--verbose]
	
	                              createtemp[orary]|mktemp
	                              <template> --username <name>
	                              [--passwordfile <file> | --password <password>]
	                              [--directory] [--secure] [--tmpdir <directory>]
	                              [--domain <domain>] [--mode <mode>] [--verbose]
	
	                              list <all|sessions|processes|files> [--verbose]
	
	                              process kill --session-id <ID>
	                                           | --session-name <name or pattern>
	                                           [--verbose]
	                                           <PID> ... <PID n>
	
	                              [p[s]]kill --session-id <ID>
	                                         | --session-name <name or pattern>
	                                         [--verbose]
	                                         <PID> ... <PID n>
	
	                              session close  --session-id <ID>
	                                           | --session-name <name or pattern>
	                                           | --all
	                                           [--verbose]
	
	                              stat
	                              <file>... --username <name>
	                              [--passwordfile <file> | --password <password>]
	                              [--domain <domain>] [--verbose]
	
	                              updateadditions
	                              [--source <guest additions .ISO>] [--verbose]
	                              [--wait-start]
	                              [-- [<argument1>] ... [<argumentN>]]
	
	                              watch [--verbose]
	
	  debugvm                   <uuid|vmname>
	                            dumpguestcore --filename <name> |
	                            info <item> [args] |
	                            injectnmi |
	                            log [--release|--debug] <settings> ...|
	                            logdest [--release|--debug] <settings> ...|
	                            logflags [--release|--debug] <settings> ...|
	                            osdetect |
	                            osinfo |
	                            getregisters [--cpu <id>] <reg>|all ... |
	                            setregisters [--cpu <id>] <reg>=<value> ... |
	                            show [--human-readable|--sh-export|--sh-eval|
	                                  --cmd-set] 
	                                <logdbg-settings|logrel-settings>
	                                [[opt] what ...] |
	                            statistics [--reset] [--pattern <pattern>]
	                            [--descriptions]
	
	  metrics                   list [*|host|<vmname> [<metric_list>]]
	                                                 (comma-separated)
	
	  metrics                   setup
	                            [--period <seconds>] (default: 1)
	                            [--samples <count>] (default: 1)
	                            [--list]
	                            [*|host|<vmname> [<metric_list>]]
	
	  metrics                   query [*|host|<vmname> [<metric_list>]]
	
	  metrics                   enable
	                            [--list]
	                            [*|host|<vmname> [<metric_list>]]
	
	  metrics                   disable
	                            [--list]
	                            [*|host|<vmname> [<metric_list>]]
	
	  metrics                   collect
	                            [--period <seconds>] (default: 1)
	                            [--samples <count>] (default: 1)
	                            [--list]
	                            [--detach]
	                            [*|host|<vmname> [<metric_list>]]
	
	  natnetwork                add --netname <name>
	                            --network <network>
	                            [--enable|--disable]
	                            [--dhcp on|off]
	                            [--port-forward-4 <rule>]
	                            [--loopback-4 <rule>]
	                            [--ipv6 on|off]
	                            [--port-forward-6 <rule>]
	                            [--loopback-6 <rule>]
	
	  natnetwork                remove --netname <name>
	
	  natnetwork                modify --netname <name>
	                            [--network <network>]
	                            [--enable|--disable]
	                            [--dhcp on|off]
	                            [--port-forward-4 <rule>]
	                            [--loopback-4 <rule>]
	                            [--ipv6 on|off]
	                            [--port-forward-6 <rule>]
	                            [--loopback-6 <rule>]
	
	  natnetwork                start --netname <name>
	
	  natnetwork                stop --netname <name>
	
	  hostonlyif                ipconfig <name>
	                            [--dhcp |
	                            --ip<ipv4> [--netmask<ipv4> (def: 255.255.255.0)] |
	                            --ipv6<ipv6> [--netmasklengthv6<length> (def: 64)]]
	                            create |
	                            remove <name>
	
	  dhcpserver                add|modify --netname <network_name> |
	                                       --ifname <hostonly_if_name>
	                            [--ip <ip_address>
	                            --netmask <network_mask>
	                            --lowerip <lower_ip>
	                            --upperip <upper_ip>]
	                            [--enable | --disable]
	
	  dhcpserver                remove --netname <network_name> |
	                                   --ifname <hostonly_if_name>
	
	  extpack                   install [--replace] <tarball> |
	                            uninstall [--force] <name> |
                            		cleanup

# example
	1. create vm
		vboxmanage createvm --name "ubuntu1204-base" --ostype "Ubuntu_64" --basefolder "/home/cxl/virtualbox/vm/" --register 创建虚拟机
		vboxmanage createhd --filename /home/cxl/virtualbox/vm/ubuntu1204-base/ubuntu1204-base --size 8000 创建虚拟硬盘
		vboxmanage storagectl "ubuntu1204-base" --add ide  --name "IDE Controller" --bootable on  创建ide接口
		vboxmanage storageattach "ubuntu1204-base" --storagectl "IDE Controller" --port 0 --device 0 --type hdd --medium "/home/cxl/virtualbox/vm/ubuntu1204-base/ubuntu1204-base.vdi" 虚拟机关联硬盘
		vboxmanage storageattach "ubuntu1204-base" --storagectl "IDE Controller" --port 1 --device 0 --type dvddrive --medium "/home/cxl/virtualbox/iso/ubuntu-12.04.1-server-amd64.iso" 虚拟机关联光驱，加入iso安装文件
		vboxmanage modifyvm "ubuntu1204-base" --vrde on --vrdeport 5001
		vboxmanage startvm "buildserver" --type headless
		
	2. delete vm
		vboxmanage unregistervm ubuntu1204-base --delete 删除虚拟机
	
	3. clone vm 
		vboxmanage clonevm "ubuntu1204-base" --name "buildserver" --register --basefolder "/home/cxl/virtualbox/vm-root/" 
		vboxmanage startvm "buildserver" --type headless