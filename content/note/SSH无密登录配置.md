---
title: SSH无密登录配置
author: Xin Lu
date: '2023-08-04'
slug: []
categories: []
tags: []
---

- 生成公钥和私钥 

[atguigu@hadoop102 .ssh]$ pwd 

/home/atguigu/.ssh 

[atguigu@hadoop102 .ssh]$ ssh-keygen -t rsa 



然后敲（三个回车），就会生成两个文件 id_rsa（私钥）、id_rsa.pub（公钥） 



- 将公钥拷贝到要免密登录的目标机器上 

[atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop102 

- 需输入密码

```
[root@hadoop2102 .ssh]# ssh-copy-id hadoop2103
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
The authenticity of host 'hadoop2103 (192.168.121.147)' can't be established.
ECDSA key fingerprint is SHA256:puxPIj2IoBCaUJjtytH4E+jhYTjj7eg59VoHSLUDSKw.
ECDSA key fingerprint is MD5:93:02:9b:c7:4d:e1:60:5b:b5:e0:d1:2e:11:04:15:12.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@hadoop2103's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'hadoop2103'"
and check to make sure that only the key(s) you wanted were added.

[root@hadoop2102 .ssh]# ssh-copy-id hadoop2104
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/root/.ssh/id_rsa.pub"
The authenticity of host 'hadoop2104 (192.168.121.148)' can't be established.
ECDSA key fingerprint is SHA256:puxPIj2IoBCaUJjtytH4E+jhYTjj7eg59VoHSLUDSKw.
ECDSA key fingerprint is MD5:93:02:9b:c7:4d:e1:60:5b:b5:e0:d1:2e:11:04:15:12.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@hadoop102's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'hadoop2104'"
and check to make sure that only the key(s) you wanted were added.

```



[atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop103 

[atguigu@hadoop102 .ssh]$ ssh-copy-id hadoop104 



【注】：其他节点也需要交换公钥