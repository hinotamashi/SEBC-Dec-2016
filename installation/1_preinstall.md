[hinotamashi94@instance-2 ~]$ sudo cat /proc/sys/vm/swappiness
30
[hinotamashi94@instance-2 ~]$ sudo sysctl vm.swappiness=10
vm.swappiness = 10
[hinotamashi94@instance-2 ~]$ sudo yum install nano
Loaded plugins: fastestmirror
base                                                                                     | 3.6 kB  00:00:00     
extras                                                                                   | 3.4 kB  00:00:00     
google-cloud-compute/signature                                                           |  454 B  00:00:00     
google-cloud-compute/signature                                                           | 1.4 kB  00:00:00 !!! 
google-cloud-sdk/signature                                                               |  454 B  00:00:00     
google-cloud-sdk/signature                                                               | 1.4 kB  00:00:00 !!! 
updates                                                                                  | 3.4 kB  00:00:00     
(1/6): base/7/x86_64/group_gz                                                            | 155 kB  00:00:00     
(2/6): google-cloud-compute/primary                                                      | 1.9 kB  00:00:00     
(3/6): google-cloud-sdk/primary                                                          | 2.8 kB  00:00:00     
(4/6): extras/7/x86_64/primary_db                                                        | 166 kB  00:00:00     
(5/6): updates/7/x86_64/primary_db                                                       | 9.1 MB  00:00:00     
(6/6): base/7/x86_64/primary_db                                                          | 5.3 MB  00:00:01     
Determining fastest mirrors
 * base: mirrors.umflint.edu
 * extras: repos.forethought.net
 * updates: mirrors.gigenet.com
google-cloud-compute                                                                                        4/4
google-cloud-sdk                                                                                            7/7
Resolving Dependencies
--> Running transaction check
---> Package nano.x86_64 0:2.3.1-10.el7 will be installed
--> Finished Dependency Resolution
Dependencies Resolved
================================================================================================================
 Package                Arch                     Version                           Repository              Size
================================================================================================================
Installing:
 nano                   x86_64                   2.3.1-10.el7                      base                   440 k
Transaction Summary
================================================================================================================
Install  1 Package
Total download size: 440 k
Installed size: 1.6 M
Is this ok [y/d/N]: y
Downloading packages:
nano-2.3.1-10.el7.x86_64.rpm                                                             | 440 kB  00:00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : nano-2.3.1-10.el7.x86_64                                                                     1/1 
  Verifying  : nano-2.3.1-10.el7.x86_64                                                                     1/1 
Installed:
  nano.x86_64 0:2.3.1-10.el7                                                                                    
Complete!
[hinotamashi94@instance-2 ~]$ sudo nano /etc/sysctl.conf
[hinotamashi94@instance-2 ~]$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G  1.4G   29G   5% /
devtmpfs        6.4G     0  6.4G   0% /dev
tmpfs           6.4G     0  6.4G   0% /dev/shm
tmpfs           6.4G  8.2M  6.4G   1% /run
tmpfs           6.4G     0  6.4G   0% /sys/fs/cgroup
tmpfs           1.3G     0  1.3G   0% /run/user/1000
[hinotamashi94@instance-2 ~]$ sudo fdisk -l
Disk /dev/sda: 32.2 GB, 32212254720 bytes, 62914560 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 4096 bytes
I/O size (minimum/optimal): 4096 bytes / 4096 bytes
Disk label type: dos
Disk identifier: 0x00091e3d
   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048    62910539    31454246   83  Linux
[hinotamashi94@instance-2 ~]$ sudo sysctl -a |grep hugepages
vm.hugepages_treat_as_movable = 0
vm.nr_hugepages = 0
vm.nr_hugepages_mempolicy = 0
vm.nr_overcommit_hugepages = 0
[root@instance-2 hinotamashi94]#  echo never > /sys/kernel/mm/transparent_hugepage/enabled
[root@instance-2 hinotamashi94]# echo never > /sys/kernel/mm/transparent_hugepage/defrag
[root@instance-2 hinotamashi94]# sysctl -a |grep hugepages
vm.hugepages_treat_as_movable = 0
vm.nr_hugepages = 0
vm.nr_hugepages_mempolicy = 0
vm.nr_overcommit_hugepages = 0
[hinotamashi94@instance-2 ~]$ sudo su
[root@instance-2 hinotamashi94]# cat /sys/kernel/mm/transparent_hugepage/enabled
always madvise [never]
[root@instance-2 hinotamashi94]# cat /sys/kernel/mm/transparent_hugepage/defrag
always madvise [never]
[root@instance-2 hinotamashi94]# nano /etc/rc.local
[root@instance-2 hinotamashi94]# ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN 
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1460 qdisc mq state UP qlen 1000
    link/ether 42:01:0a:80:00:02 brd ff:ff:ff:ff:ff:ff
    inet 10.128.0.2/32 brd 10.128.0.2 scope global dynamic eth0
       valid_lft 83934sec preferred_lft 83934sec
[hinotamashi94@instance-2 ~]$ getent hosts
127.0.0.1       localhost localhost.localdomain localhost4 localhost4.localdomain4
127.0.0.1       localhost localhost.localdomain localhost6 localhost6.localdomain6
10.128.0.2      instance-2.c.soy-tower-151610.internal instance-2
169.254.169.254 metadata.google.internal
[hinotamashi94@instance-2 ~]$ nslookup hosts
-bash: nslookup: command not found
[hinotamashi94@instance-2 ~]$ sudo yum install bind-utils
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.umflint.edu
 * extras: repos.forethought.net
 * updates: mirrors.gigenet.com
Resolving Dependencies
--> Running transaction check
---> Package bind-utils.x86_64 32:9.9.4-29.el7_2.4 will be installed
--> Processing Dependency: bind-libs = 32:9.9.4-29.el7_2.4 for package: 32:bind-utils-9.9.4-29.el7_2.4.x86_64
--> Processing Dependency: liblwres.so.90()(64bit) for package: 32:bind-utils-9.9.4-29.el7_2.4.x86_64
--> Processing Dependency: libisccfg.so.90()(64bit) for package: 32:bind-utils-9.9.4-29.el7_2.4.x86_64
--> Processing Dependency: libisccc.so.90()(64bit) for package: 32:bind-utils-9.9.4-29.el7_2.4.x86_64
--> Processing Dependency: libisc.so.95()(64bit) for package: 32:bind-utils-9.9.4-29.el7_2.4.x86_64
--> Processing Dependency: libdns.so.100()(64bit) for package: 32:bind-utils-9.9.4-29.el7_2.4.x86_64
--> Processing Dependency: libbind9.so.90()(64bit) for package: 32:bind-utils-9.9.4-29.el7_2.4.x86_64
--> Running transaction check
---> Package bind-libs.x86_64 32:9.9.4-29.el7_2.4 will be installed
--> Finished Dependency Resolution
Dependencies Resolved
==========================================================================================================================
 Package                     Arch                    Version                               Repository                Size
==========================================================================================================================
Installing:
 bind-utils                  x86_64                  32:9.9.4-29.el7_2.4                   updates                  200 k
Installing for dependencies:
 bind-libs                   x86_64                  32:9.9.4-29.el7_2.4                   updates                  1.0 M
Transaction Summary
==========================================================================================================================
Install  1 Package (+1 Dependent package)
Total download size: 1.2 M
Installed size: 3.0 M
Is this ok [y/d/N]: y
Downloading packages:
(1/2): bind-utils-9.9.4-29.el7_2.4.x86_64.rpm                                                      | 200 kB  00:00:00     
(2/2): bind-libs-9.9.4-29.el7_2.4.x86_64.rpm                                                       | 1.0 MB  00:00:00     
--------------------------------------------------------------------------------------------------------------------------
Total                                                                                     2.7 MB/s | 1.2 MB  00:00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : 32:bind-libs-9.9.4-29.el7_2.4.x86_64                                                                   1/2 
  Installing : 32:bind-utils-9.9.4-29.el7_2.4.x86_64                                                                  2/2 
  Verifying  : 32:bind-libs-9.9.4-29.el7_2.4.x86_64                                                                   1/2 
  Verifying  : 32:bind-utils-9.9.4-29.el7_2.4.x86_64                                                                  2/2 
Installed:
  bind-utils.x86_64 32:9.9.4-29.el7_2.4                                                                                   
Dependency Installed:
  bind-libs.x86_64 32:9.9.4-29.el7_2.4                                                                                    
Complete!
[hinotamashi94@instance-2 ~]$ nslookup hosts
Server:         169.254.169.254
Address:        169.254.169.254#53
** server can't find hosts: NXDOMAIN
[hinotamashi94@instance-2 ~]$ nscd
-bash: nscd: command not found
[hinotamashi94@instance-2 ~]$ nano /ect/nscd.conf
[hinotamashi94@instance-2 ~]$ nano /etc/nscd.conf
[hinotamashi94@instance-2 ~]$ sudo yum install nscd
Loaded plugins: fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.umflint.edu
 * extras: repos.forethought.net
 * updates: mirrors.gigenet.com
Resolving Dependencies
--> Running transaction check
---> Package nscd.x86_64 0:2.17-106.el7_2.8 will be installed
--> Finished Dependency Resolution
Dependencies Resolved

==========================================================================================================================
 Package                 Arch                      Version                               Repository                  Size
==========================================================================================================================
Installing:
 nscd                    x86_64                    2.17-106.el7_2.8                      updates                    261 k
Transaction Summary
==========================================================================================================================
Install  1 Package
Total download size: 261 k
Installed size: 179 k
Is this ok [y/d/N]: y
Downloading packages:
nscd-2.17-106.el7_2.8.x86_64.rpm                                                                   | 261 kB  00:00:00     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : nscd-2.17-106.el7_2.8.x86_64                                                                           1/1 
  Verifying  : nscd-2.17-106.el7_2.8.x86_64                                                                           1/1 
Installed:
  nscd.x86_64 0:2.17-106.el7_2.8                                                                                          
Complete!
[hinotamashi94@instance-2 ~]$ sudo service nscd start
Redirecting to /bin/systemctl start  nscd.service
[hinotamashi94@instance-2 ~]$ sudo service nscd status
Redirecting to /bin/systemctl status  nscd.service
● nscd.service - Name Service Cache Daemon
   Loaded: loaded (/usr/lib/systemd/system/nscd.service; disabled; vendor preset: disabled)
   Active: active (running) since Wed 2016-12-07 04:17:56 UTC; 5s ago
  Process: 1770 ExecStart=/usr/sbin/nscd $NSCD_OPTIONS (code=exited, status=0/SUCCESS)
 Main PID: 1771 (nscd)
   CGroup: /system.slice/nscd.service
           └─1771 /usr/sbin/nscd
Dec 07 04:17:55 instance-2 nscd[1771]: 1771 monitoring file `/etc/hosts` (4)
Dec 07 04:17:55 instance-2 nscd[1771]: 1771 monitoring directory `/etc` (2)
Dec 07 04:17:55 instance-2 nscd[1771]: 1771 monitoring file `/etc/resolv.conf` (5)
Dec 07 04:17:55 instance-2 nscd[1771]: 1771 monitoring directory `/etc` (2)
Dec 07 04:17:55 instance-2 nscd[1771]: 1771 monitoring file `/etc/services` (6)
Dec 07 04:17:55 instance-2 nscd[1771]: 1771 monitoring directory `/etc` (2)
Dec 07 04:17:55 instance-2 nscd[1771]: 1771 disabled inotify-based monitoring for file `/etc/netgroup': No such f...ectory
Dec 07 04:17:55 instance-2 nscd[1771]: 1771 stat failed for file `/etc/netgroup'; will try again later: No such f...ectory
Dec 07 04:17:56 instance-2 nscd[1771]: 1771 Access Vector Cache (AVC) started
Dec 07 04:17:56 instance-2 systemd[1]: Started Name Service Cache Daemon.
Hint: Some lines were ellipsized, use -l to show in full.
[hinotamashi94@instance-2 ~]$ sudo service ntpd status
Redirecting to /bin/systemctl status  ntpd.service
● ntpd.service - Network Time Service
   Loaded: loaded (/usr/lib/systemd/system/ntpd.service; enabled; vendor preset: disabled)
   Active: active (running) since Wed 2016-12-07 03:25:59 UTC; 53min ago
 Main PID: 1152 (ntpd)
   CGroup: /system.slice/ntpd.service
           └─1152 /usr/sbin/ntpd -u ntp:ntp -g
Dec 07 03:25:59 instance-2 ntpd[1152]: Listen and drop on 1 v6wildcard :: UDP 123
Dec 07 03:25:59 instance-2 ntpd[1152]: Listen normally on 2 lo 127.0.0.1 UDP 123
Dec 07 03:25:59 instance-2 ntpd[1152]: Listen normally on 3 eth0 10.128.0.2 UDP 123
Dec 07 03:25:59 instance-2 ntpd[1152]: Listening on routing socket on fd #20 for interface updates
Dec 07 03:25:59 instance-2 ntpd[1152]: 0.0.0.0 c016 06 restart
Dec 07 03:25:59 instance-2 ntpd[1152]: 0.0.0.0 c012 02 freq_set kernel 0.000 PPM
Dec 07 03:25:59 instance-2 ntpd[1152]: 0.0.0.0 c011 01 freq_not_set
Dec 07 03:26:00 instance-2 ntpd[1152]: 0.0.0.0 c614 04 freq_mode
Dec 07 03:46:13 instance-2 ntpd[1152]: 0.0.0.0 0612 02 freq_set kernel -0.710 PPM
Dec 07 03:46:13 instance-2 ntpd[1152]: 0.0.0.0 0615 05 clock_sync
