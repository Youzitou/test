# 概念

| SQL术语/概念 | MongoDB术语/概念 | 解释/说明                           |
| :----------- | :--------------- | :---------------------------------- |
| database     | database         | 数据库                              |
| table        | collection       | 数据库表/集合                       |
| row          | document         | 数据记录行/文档                     |
| column       | field            | 数据字段/域                         |
| index        | index            | 索引                                |
| table joins  |                  | 表连接,MongoDB不支持                |
| primary key  | primary key      | 主键,MongoDB自动将_id字段设置为主键 |

如图实例

![mongdb概念](.\img\mongdb概念.png)

# mongodb下载

![1664208323950](.\img\mongodb下载.png)

# mongdb安装

```shell
tar -zxvf mongodb-linux-x86_64-rhel80-4.4.16.tgz  -C /home
cd /home/
cp mongodb-linux-x86_64-rhel80-4.4.16/ /usr/local/mongodb -rf
cd /usr/local/mongodb
mkdir -p data/db
mkdir log
cd log
touch mongodb.log

./mongod --dbpath /usr/local/mongodb/data/db/ --logpath /usr/local/mongodb/log/mongodb.log  --fork

cd /usr/local/mongodb
mkdir etc
cd etc/
# 配置方式启动
vim mongodb.conf
# 增加如下配置
dbpath=/usr/local/mongodb/data/db
logpath=/usr/local/mongodb/log/mongodb.log
port=27017
bind_ip=0.0.0.0
fork=true

 ./mongod --shutdown --dbpath /usr/local/mongodb/data/db
 ./mongod --config /usr/local/mongodb/etc/mongodb.conf 
# 配置环境变量
vim /etc/profile
source /etc/profile
mongod --help
 
 mongod --shutdwon --config /usr/local/mongodb/etc/mongodb.conf 
 # 启动客户端
 mongo
 use admin
```

权限以及创建用户

```shell
--创建用户
use admin
db.createUser({ "user" : "liuyouyun","pwd": "liuyouyun","roles" : [ {"role": "userAdminAnyDatabase","db": "admin"}]})
```

