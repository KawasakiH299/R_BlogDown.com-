---
title: linux 简单实用的操作
author: Xin Lu
date: '2023-05-04'
slug: []
categories: []
tags: []
---

实例

设置字体大小

```
②进入到所有字体的目录
命令：cd /lib/kbd/consolefonts
setfont LatGrkCyr-12x22.psfu.gz

网卡配置
/etc/sysconfig/network-scripts/ifcfg-en
```



```
crontab -e
crontab -l
crontab -r
```



```
at 5pm + 5days
\\ctrl + d  两次结束
at> /bin/ls /home
```



```
at now + 2 minutes
at rm 1
```



```
[root@localhost var]# lsblk
NAME            MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda               8:0    0   50G  0 disk
├─sda1            8:1    0    1G  0 part /boot
└─sda2            8:2    0   49G  0 part
  ├─centos-root 253:0    0   44G  0 lvm  /
  └─centos-swap 253:1    0    5G  0 lvm  [SWAP]
sr0              11:0    1  9.5G  0 rom

```



```
分区
fdisk /dev/sdb

分区格式化
mkfs -t ext4 /dev/sdb1

挂载
monut /dev/sdb1 /var/newdisk/

卸载
unmount /dev/sdb1

挂载的关系时临时的
```



```
自动（永久挂载）
修改/etc/fstab实现永久挂载，修改完成后mount -a即刻生效


```



```

[root@localhost var]# df -h
文件系统                 容量  已用  可用 已用% 挂载点
devtmpfs                 3.8G     0  3.8G    0% /dev
tmpfs                    3.9G     0  3.9G    0% /dev/shm
tmpfs                    3.9G   12M  3.8G    1% /run
tmpfs                    3.9G     0  3.9G    0% /sys/fs/cgroup
/dev/mapper/centos-root   44G  5.5G   39G   13% /
/dev/sda1               1014M  151M  864M   15% /boot
tmpfs                    781M     0  781M    0% /run/user/0

```



```
查看文件存储空间
[root@localhost var]# du -h --max-depth=1
0       ./tmp
1.7G    ./lib
11M     ./log
0       ./adm
394M    ./cache
8.0K    ./db
0       ./empty
0       ./games
0       ./gopher
0       ./local
0       ./nis
0       ./opt
0       ./preserve
20K     ./spool
0       ./yp
0       ./kerberos
0       ./crash
2.1G    .

```



```
top
```



```
ps -ef
#ppid 父进程
ps -aux | grep more


[root@localhost ~]# ps -aux
USER        PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root          1  0.0  0.0 193580  6692 ?        Ss   20:40   0:01 /usr/lib/systemd/systemd --switched-root
root          2  0.0  0.0      0     0 ?        S    20:40   0:00 [kthreadd]
root          4  0.0  0.0      0     0 ?        S<   20:40   0:00 [kworker/0:0H]
root          5  0.0  0.0      0     0 ?        S    20:40   0:00 [kworker/u256:0]



[root@localhost ~]# ps -aux | grep sshd
root       1148  0.0  0.0 112900  4308 ?        Ss   20:41   0:00 /usr/sbin/sshd -D
root       1688  0.0  0.0 159224  6292 ?        Ss   20:43   0:00 sshd: root@pts/0
root       1692  0.0  0.0 158896  5828 ?        Ss   20:43   0:00 sshd: root@notty
root       2021  0.0  0.0 112824   984 pts/0    S+   21:57   0:00 grep --color=auto sshd




[root@localhost ~]# ps -aux | grep bash
root       1671  0.0  0.0 115540  2028 tty1     Ss+  20:43   0:00 -bash
root       1703  0.0  0.0 115544  2048 pts/0    Ss   20:43   0:00 -bash
root       2039  0.0  0.0 112824   988 pts/0    S+   22:07   0:00 grep --color=auto bash

```



```
pstree
 -p  pid
 -u  user
  yum -y install psmisc
```



```
kill 
killall
```



```
[root@localhost ~]# ls -l /etc/init.d/
总用量 40
-rw-r--r--. 1 root root 18281 5月  22 2020 functions
-rwxr-xr-x. 1 root root  4569 5月  22 2020 netconsole
-rwxr-xr-x. 1 root root  7928 5月  22 2020 network
-rw-r--r--. 1 root root  1160 10月  2 2020 README


使用service 启动
7.0后许多都不使用service  而是systemctl
```



```
setup


　　#安装setuptool

　　yum install setuptool

　　#可以发现执行setup后不全，再安装一个用于系统服务管理

　　yum install ntsysv

　　#安装setup中配套的防火墙设置

　　yum install system-config-securitylevel-tui

　　#安装setup中配套的网络设置

　　yum install system-config-network-tui

　　#安装setup中配套的键盘设置

　　yum install system-config-keyboard
```





#### 服务管理

```
systemctl get-default


[root@localhost ~]# systemctl get-default
multi-user.target
多用户运行级别

systemctl set-default graphical-target
```





```
[root@localhost scrapyDemon01]# systemctl list-unit-files | grep firewalld

firewalld.service                             enabled

enable 开机自启动


[root@localhost scrapyDemon01]# systemctl is-enabled sshd
enabled
```



#### dhcp重新获取ip

```
Linux renew ip command
$ sudo dhclient -r //release ip 释放IP
$ sudo dhclient //获取IP
```

---

#### 网卡信息与配置

```
[root@mysql ~]# ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.0.111  netmask 255.255.255.0  broadcast 192.168.0.255
        inet6 fe80::8c18:4c0c:35b:f89c  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:bf:7a:4b  txqueuelen 1000  (Ethernet)
        RX packets 396  bytes 43132 (42.1 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 189  bytes 25028 (24.4 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
# eth0：网卡名称
# Link encap：网卡的接口类型，这里是以太网
# HWaddr：网卡的硬件地址，俗称的MAC地址
# inet addr：IPv4地址，如果是IPv6会写成inet6 addr
# Bcast：广播地址
# Mask：子网掩码
# UP：表示网卡是开启状态
# BROADCAST：表示网卡支持广播
# RUNNING：表示网卡的网线已经被接上
# MULTICAST：表示网卡支持组播
# MTU：网络最大传输单元
# Metric：到达网关的度量值，参考：http://m.chinabyte.com/network/191/12287691_gfh.shtml
# RX packets：网络从启动到现在为止接收的数据包大小，单位是字节，error 发生错误的数据包，dropped 被丢弃的数据包
# TX packets：网络从启动到现在为止发送的数据包大小，单位是字节，error 发生错误的数据包，dropped 被丢弃的数据包
# collisions：发生碰撞的数据包，如果发生太多次,表明网络状况不太好
# txqueuelen：传输数据的缓冲区的储存长度
# RX bytes：总接收字节总量
# TX bytes：总发送字节总量
# Memory：网卡硬件的内存地址



[root@mysql ~]# ifconfig -a             // 查看所有网卡的信息(包括down状态的网卡

[root@mysql ~]# ifconfig eth0 // 查看指定网卡的信息

[root@mysql ~]# ifconfig eth0 up        // 启用指定的网卡，等同于：ifup eth0

[root@mysql ~]# ifconfig eth0 down      // 关闭指定的网卡，等同于：ifdown eth0

[root@mysql ~]# ifconfig eth0 arp       // 开启网卡的ARP协议
[root@mysql ~]# ifconfig eth0 -arp      // 关闭网卡的ARP协议


[root@mysql ~]# ifconfig eth0 192.168.0.100                               // 设置/修改网卡的IP地址(临时生效)
[root@mysql ~]# ifconfig eth0 192.168.0.100/24                            // 设置/修改网卡的IP地址和子网掩码(临时生效)
[root@mysql ~]# ifconfig eth0 192.168.0.100 netmask 255.255.255.0         // 设置/修改网卡的IP地址和子网掩码(临时生效)
[root@mysql ~]# ifconfig eth0 192.168.0.100 hw ether 04:64:03:00:12:51    // 设置/修改网卡的IP地址和MAC地址(临时生效)，ether(以太网)表示网卡的接口类型
[root@mysql ~]# ifconfig eth0 mtu 1500                                      // 设置/修改网卡的最大传输单元(临时生效)

[root@mysql ~]# ifconfig eth0:0 192.168.0.50/24    // 给网卡配置虚拟接口，相当于给网卡再配置一个IP地址(临时生效)
[root@mysql ~]# ifconfig eth0:1 192.168.0.51/24    // 给网卡配置虚拟接口，相当于给网卡再配置一个IP地址(临时生效)
[root@mysql ~]# ifconfig eth0:2 192.168.0.52/24    // 给网卡配置虚拟接口，相当于给网卡再配置一个IP地址(临时生效
```



#### 二 DNS配置

```
在完成IP地址基本设置后虽然可以上网，但是输入网址却无法解析（即无法ping www.baidu.com），所以此时需要对DNS进行设置。
1.进入配置文件
**vi /etc/resolv.conf**

https://blog.csdn.net/cenjeal/article/details/107694525
```



#### 不同一网段（不同主机互通）

```
https://blog.csdn.net/feinifi/article/details/105893420
```

```
开机自启动
systemctl enable 服务
disable
is-enabled是否自启动
```

#### 开启防火墙并开启服务器监听端口

```
打开端口
firewall-cmd --permanent --add-port=111/tcp
必须重载防火墙
firewall-cmd --reload
查看端口是否开启
firewall-cmd --query-port=111/tcp
必须重载防火墙
firewall-cmd --reload

```

#### 动态监控

```
top
 -p
 -m
 -n
 
```



#### rsync 远程同步工具

- rsync 主要用于备份和镜像。具有速度快、避免复制相同内容和支持符号链接的优点。 

- rsync 和 scp 区别：用 rsync 做文件的复制要比 scp 的速度快，rsync 只对差异文件做更 新。scp 是把所有文件都复制过去。

```
rsync -av $pdir/$fname $user@$host:$pdir/$fname
命令 选项参数 要拷贝的文件路径/名称 目的地用户@主机:目的地路径/名称
[atguigu@hadoop102 ~]$ rsync -av hadoop-3.1.3/      atguigu@hadoop103:/opt/module/hadoop-3.1.3/

-a 归档拷贝
-v 显示处理信息
```



#### scp 可以实现服务器与服务器之间的数据拷贝。

#### （from server1 to server2） 

2）基本语法 

```
scp -r $pdir/$fname $user@$host:$pdir/$fname 
命令 递归 要拷贝的文件路径/名称 目的地用户@主机:目的地路径/名称 
[atguigu@hadoop102 ~]$ scp -r /opt/module/jdk1.8.0_212 
atguigu@hadoop103:/opt/module
```



#### chown [选项]... [所有者][:[组]] 文件...

##### 命令功能：通过chown改变文件的拥有者和群组

```
[atguigu@hadoop102 ~]$ sudo  chown atguigu:atguigu -R /opt/module

chown -R 处理指定目录以及其子目录下的所有文件
```

