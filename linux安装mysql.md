本次安装的是源码安装方式，版本为MySQL5.7.26

1 首先下载MySQL server 的tar包,下载地址https://downloads.mysql.com/archives/community/

 ![](C:\Users\liuyouyun\Pictures\1.png)                                          

2 通过xftp工具上传，然后解压到指定目录

```shell
tar -zxvf mysql-5.7.26-el7-x86_64.tar.gz -C /home/myinstall/mysql
```

3 创建 mysql 用户组和用户并修改权限：

```shell
groupadd mysql
useradd -r -g mysql mysql
```

  创建数据目录并赋予权限

```shell
mkdir -p  /data/mysql              #创建目录
chown mysql:mysql -R /data/mysql   #赋予权限
```

4 配置 my.cnf

```shell
vim /etc/my.cnf
```

内容如下

```shell
[mysqld]
bindaddress=0.0.0.0
port=3306
user=mysql
basedir=/home/myinstall/mysql
datadir=/data/mysql
socket=/tmp/mysql.sock
log-error=/data/mysql/mysql.err
pid-file=/data/mysql/mysql.pid
#character config
character_set_server=utf8mb4
symbolic-links=0
explicit_defaults_for_timestamp=true`
```

5 初始化数据库

进入mysql的bin目录

```shell
cd /home/myinstall/mysql/bin/
```

初始化

```shell
./mysqld --defaults-file=/etc/my.cnf --basedir=/home/myinstall/mysql/ --datadir=/data/mysql/ --user=mysql --initialize
```

查看密码：

```shell
cat /data/mysql/mysql.err #可以看到一个随机初始密码
```

启动

```shell
service mysql start
ps -ef|grep mysql #查看是否正在运行
```

6 登录

```shell
./mysql -u root -p
```

使用刚才的随机密码登录会被拒绝

7 更改用户密码

1)vi /etc/my.cnf  

2)在[mysqld]下边的某个位置增加： skip-grant-tables  ,然后 :wq 保存退出

3)在 /home/myinstall/mysql/bin目录下执行命令：  ./mysql -u root -p   ，然后回车两次，进入到mysql

4）执行命令：

use mysql

SET SQL_SAFE_UPDATES = 0

5)update mysql.user set authentication_string=password('root') where User='root';

6)flush privileges ; 

7)执行命令：SET SQL_SAFE_UPDATES = 1

8）vi /etc/my.cnf  ，删除skip-grant-tables 行

9）service mysql restart

10) 在/home/myinstall/mysql/bin目录下执行命令：

  ./mysql -u root -p   然后输入新建的密码：root即可进入mysql

好了，上面一系列操作之后，还是发现用密码登录会被拒绝

此时先不用密码登录  进入mysql命令模式，然后执行

```shell
set password for ‘root’@‘localhost’=password(‘root’);
```

好了本地，算是可以登录了，但远程还不能访问

8 远程可以访问

本次mysql安装在阿里云服务器，首先要配置安全规则 开启3306端口

登入mysql后，更改 mysql 数据库里的 "user" 表里的 "host" 项，将"localhost"改称"%"

```sql
Update user set host = ‘%’ where user = ‘root’
```

然后执行 flush previleges;

参考博客

<https://www.cnblogs.com/lianym/p/14662120.html>

<https://www.cnblogs.com/acer097/p/12539668.html>

https://www.cnblogs.com/xuanbjut/p/10406980.html

 