title: mongodb4.0安装配置PHP测试
author: linjin101
tags:
  - mongodb
  - php_mongodb.dll
  - php
categories:
  - 架构
date: 2018-11-19 16:34:00
---
##### 1.安装环境  
CentOS release 6.8 (Final)  
Linux version 2.6.32-642.15.1.el6.x86_64  

##### 2.mongodb 4.0官方安装方法  
安装文档
https://docs.mongodb.com/manual/tutorial/install-mongodb-on-red-hat/


###### （1）配置包管理系统(yum)  
创建一个/etc/yum.repos.d/mongodb-org-4.0.repo文件，以便您可以使用以下方法直接安装MongoDByum:  
```
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.0.asc
```

###### (2)安装MongoDB包  
要安装MongoDB的最新稳定版本，发出以下命令：  
```
sudo yum install -y mongodb-org
```

###### (3)要安装MongoDB的特定版本，请分别指定每个组件包，并将版本号附加到包名中，如下面的示例所示：

```
sudo yum install -y mongodb-org-4.0.4 mongodb-org-server-4.0.4 mongodb-org-shell-4.0.4 mongodb-org-mongos-4.0.4 mongodb-org-tools-4.0.4
```

###### (4)安装MongoDB包和相关工具  
要安装MongoDB的最新稳定版本，发出以下命令：  
```
sudo yum install -y mongodb-org
```


###### (5)启动MongoDB  
您可以启动单神通过发出以下命令来处理：  

```
sudo service mongod start
```

###### (6)验证MongoDB是否已成功启动
您可以验证单神通过检查日志文件的内容，进程已成功启动。/var/log/mongoDB/mongod.log行读数  

```
[initandlisten] waiting for connections on port <port>
```
哪里<port>中配置的端口吗？/etc/mongod.conf, 27017默认情况下。
还可以通过发出以下命令，确保MongoDB将在系统重新启动之后启动：  

```
sudo chkconfig mongod on
```

###### (7)停止mongodb  
根据需要，您可以停止单神通过发出以下命令来处理：  


```
sudo service mongod stop
```


##### 3.解决 libc.so.6: version GLIBC_2.14  not found 问题  
试图运行程序，提示 ibc.so.6: version GLIBC_2.14  not found ,
原因是系统的glibc版本太低，软件编译时使用了较高版本的glibc引起的：
问题Centos 自动更新glibc-2.14

###### 1.查看系统glibc支持的版本：  

```
strings /lib64/libc.so.6 |grep GLIBC_
rpm -qa |grep glibc 
```

可以看到最高只支持2.12版本，所以考虑编译解决这个问题
到http://www.gnu.org/software/libc/的目录http://ftp.gnu.org/gnu/glibc/glibc-2.14.tar.xz下载最新版本，我这里下载了glibc-2.14.tar.xz 这个版本
注意：解压的目录和安装的目录放在一起，这样会冲突  

###### 2.glibc-2.14安装  


```
wget http://ftp.gnu.org/gnu/glibc/glibc-2.14.tar.xz
tar -zxvf glibc-2.14.tar.gz 
cd glibc-2.14
mkdir build
cd build
../configure --prefix=/usr/local/glibc-2.14
make -j4
make install
问题：/root/glibc-2.14/build/elf/ldconfig: Can't open configuration file /usr/local/glibc-2.14/etc/ld.so.conf: No such file or directory
解决：
cp  /etc/ld.so.c* /usr/local/glibc-2.14/etc/
```

###### 3、创建软链接  

1、删除原来软链  
```
rm -rf /lib64/libc.so.6 
```

2、解决补救问题  

```
LD_PRELOAD=/usr/local/glibc-2.14/lib/libc-2.14.so ln -s /usr/local/glibc-2.14/lib/libc-2.14.so /lib64/libc.so.6
```

因为操作删除软链接后系统无法操作任何命令，我们需要复制上命令操作后才可以。
3、创建新软链接  

```
ln -s /usr/local/glibc-2.14/lib/libc-2.14.so /lib64/libc.so.6
```

第四、查看当前新的glibc版本库  
```
strings /lib64/libc.so.6 |grep GLIBC_
```

##### 4.Mongodb配置  

设置IP：0.0.0.0 否则内网访问不了，测试用直接打开。  

```
vi /etc/mongod.conf

network interfaces
net:
port: 27017
bindIp: 0.0.0.0 #127.0.0.1  # Enter 0.0.0.0,:: to bind to all IPv4 and IPv6 addresses or, alternatively, use the ne        t.bindIpAll setting.

开启mongodb
service mongod start
关闭mongodb
service mongod stop
重启mongodb
service mongod restart

mongodb client访问命令：
mongo mongodb://192.168.3.12:27017
root@gym-virtual-machine:~# mongo 192.168.3.12:27017
MongoDB shell version: 2.6.10
connecting to: 192.168.3.12:27017/test


```

##### 5.PHP配置  
引用：[https://blog.csdn.net/weixin_36185028/article/details/76144859](https://blog.csdn.net/weixin_36185028/article/details/76144859)  
  
1. 打开phpinfo 查看 nts（非线程） 还是 ts （线程），然后查看操作位数  
2. 下载对应的版本的php_mongodb.dll 文件  
下载链接:https://pecl.php.net/package/mongodb/1.2.9/windows  
注: 下载需要翻墙  
3. 把文件解压出来 php_mongodb.dll 文件复制到php安装目录下的 ext 目录下(列子: phpStudy\php\php-7.0.12-nts\ext)  
4. 打开php.ini 配置文件增加行 ： extension=php_mongodb.dll  
5. 重启，再打开phpinfo() 查看是否有mongodb扩展，出现下图则安装成功


##### 5.PHP连接测试  
```
<?php
 
$manager = new MongoDB\Driver\Manager("mongodb://192.168.3.12:27017");
print_r($manager);

```

输出连接信息：
```
stdClass Object
(
    [_id] => MongoDB\BSON\ObjectID Object
        (
            [oid] => 5bf26d1a54902e5e6c007b92
        )

    [name] => Ceres
    [size] => 946
    [distance] => 2.766
)
stdClass Object
(
    [_id] => MongoDB\BSON\ObjectID Object
        (
            [oid] => 5bf26d1a54902e5e6c007b93
        )

    [name] => Vesta
    [size] => 525
    [distance] => 2.362
)
stdClass Object
(
    [_id] => MongoDB\BSON\ObjectID Object
        (
            [oid] => 5bf26d3954902e5e6c007b94
        )

    [name] => Ceres
    [size] => 946
    [distance] => 2.766
)
stdClass Object
(
    [_id] => MongoDB\BSON\ObjectID Object
        (
            [oid] => 5bf26d3954902e5e6c007b95
        )

    [name] => Vesta
    [size] => 525
    [distance] => 2.362

```

##### 6.Mongodb客户端  
GUI界面的免费客户端Robo 3T下载  
https://robomongo.org/download