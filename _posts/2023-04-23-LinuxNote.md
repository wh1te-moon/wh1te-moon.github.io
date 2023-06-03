---
layout: page
title: Linux,sql学习笔记
tags: linux, sql
categories: study
---
# 非常有用的
`ls` 查看目录文件,-a显示隐藏文件,-l以列表显示,-h人性化显示文件大小,-R递归显示子目录

`pwd` 查看当前位置

`cd` .当前目录,cd ..,cd ~家目录,cd -上一次工作目录

`kill` PID.杀进程 

`nohup <command> &` 后台执行命令<command>
例如:`nohup python -u launch.py >>log.txt &`后台执行`python -u launch.py >>log.txt`的命令

`ps` 查看进程
推荐用法:ps|grep <正则> 输出符合正则表达式的进程
例如:`ps |grep xhm_log.txt` 查看输出到xhm_log.txt的进程,配合nohup使用很方便 


## 也许有用的
`touch` name1 name2

`mkdir` -p递归创建

`rm` -r递归删除(文件夹必用),-f强制删除

`mv` -f覆盖前不询问,-i覆盖前询问,-n不覆盖,mv在一个文件夹下移动,即重命名

`cp` -i覆盖前提示,-r递归复制

`cat` -n输出行编号-s不输出多行空格-b对非空行进行编号

`more` 分页查看文件内容

history

useradd -d指定账户的主目录,-g指定用户的所属组,-G指定用户附加组,-s指定用户登录shell

,-m自动创建家目录

userdel -r删除用户的同时删除家目录

usermod修改用户账号属性 -u用户id,-g所属组id,-a -G?,-d -m将家目录移到新位置,-s用户

账号的新登录,-l新的登录名称

groupadd

groupdel

groupmod -g Gid

chmod u文件所有者/g文件所有组/o其他用户 +/-/=rwx 文件名|目录名

chmod ??? 文件名|目录名 7rwx,6rw-,5r-x,4r--,3-wx,2-w-,1--x,0---(r4w2x1)

ifconfig

ping 网址 -c指定ping数目,-i指定发送间隔,-s指定发送大小,-t设置TTL大小,ctrl+c退出

service sshd status查看是否开启ssh服务

windows ssh用xshell或putty

ssh -p 端口 主机(-p端口默认22)

scp将远程的文件复制过来,scp 用户(root)@ip:/本地路径,将本地的文件复制到远程,scp 本地路
径 用户@ip:/远程路径,复制文件夹scp -r 当前路径文件夹 用户@ip 远程目录

date查看系统当前时间

df -TH查看磁盘分区以及挂载情况

du -sh [目录名]查看目录大小

du -h[文件名]察看文件大小

uname -a查看内核,系统,cpu,-i查看硬件平台,-m查看cpu,-n节点名称,-o操作系统,-v内核版本,-r发行版本号

top查看进程实时情况 q退出 PID进程id,USER进程所有者,PR进程优先级,NInice值,VIRT使用虚拟
内存量,RES使用物理内存量,SHR共享内存量,S进程状态(D不可中断的睡眠状态,R运行,S睡眠,T跟踪/停止,Z
僵尸进程),%CPU上次更新到现在cpu时间占用百分比,%MEM占物理内存百分比,TIME+使用cpu时间总计,COMM
AND进程名称

ps -ajx查看所有进程状态 D不可中断系统进程,R运行中,S中断sleep状态,T停止,Z僵尸进程
kill -9 [进程号]强制结束进程 kill -15 [进程号]结束进程
whereis(选项)(参数) -b只查找二进制文件,-B<目录>在范围内查找二进制文件,-f不显示文件路径,-m
只查找说明文件,-M<目录>在范围内查找说明文件,-s只查找原始代码文件,-S<目录>...,-u查找不包含指定类
型的文件
which 命令查找命令所在路径
sudo apt-get install mysql-server安装mysql服务器,sudo server mysql start启动服务
ps ajx|grep mysql或sudo server mysql status查看服务是否启动,sudo server mysql stop停
止服务,sudo service mysql restart重启服务

### mysql
sudo apt install mysql -client安装命令行客户端
mysql -u 用户 -p连接数据库
select version();查看数据库版本
select now();查看当前时间
show databases;
create database 数据库名 charset=utf8;
use 数据库名
select database();查看正在使用哪个数据库
drop database 数据库名
show tables;
create table 表名(
id int auto_increment primary key not null comment '主键',
name varchar(??) not null comment '姓名',
is_delete bit(1) not null default 0 comment '巴拉巴拉'
);
show create table 表名;查看创建表的sql语句
alter table 表名 add/drop 字段名字 (类型);
alter table 表名 modify 字段名字 类型及约束;
alter table 表名 change 原名 新名 类型及约束;
drop table 表名;
select * from 表名;
insert into 表名 (字段1,字段2,,,) values(1值1,1值2,,,)(2值1,2值2,,,)(3),,,;
update 表名 set 字段=xxx where xxx;
delete from 表名 where xxx;
mysqldump -u root -p 数据库名 > 备份文件名.sql,备份数据库
mysql -u root -p 新数据库名 < 备份文件名.sql,恢复数据库
模糊查询like,%表示任意多个字符,_表示一个字符,rlike 匹配正则,in 包含在内的,%%匹配%
sth is null
desc降序,asc升序
聚合函数 count,max,min,sum,avg,round,substr修改字符串,left(str,len),right(str,len),
MOD(N,M)%取N/M的模,FLOOR(N)向下取整,CEILING(N)向上取整,CURDATA()当前日期,CURTIME()当前时间
group by 字段
as
having在group by后面过滤条件
limit(x,y)x开始位置,y显示数据数
连接select * from 表1 inner/left/right join 表2 on 表1.字段=表2.字段
insert into 表名 (字段1,字段2,,,); 子查询
union (all)(完全)合并
select user,host from user;查看mysql用户信息
create user'用户名'@'ip地址';
grant 权限(create/alter/drop/select/insert/update/delete/all privileges等) on 数据
库 to '用户名'@'ip地址'; 给予权限
show grants for 用户名;
revoke 权限 on '数据库'(*.*代指所有数据库) from '用户'@'ip';
在终端修改密码 MySQLadmin -u用户名 -p 密码 新密码
root账号修改普通用户的密码 修改MySQL.user表,更新权限 update MySQL.user authentication_string=新
密码 where user='用户名'; flush privileges;
drop '用户'@'ip'/delete from user where user='用户';
事务 begin,commit,rollback,set auto_commit=0/1 隐式提交create,alter,drop,truncate,rename 隐
式回滚 客户端强制退出,连接异常中断,系统崩溃
视图 创建视图create view 名称 as select语句;,查看视图show tables;/show TABLE status; 删除视图drop
view 名称; 调用视图select * from 名称;
索引 主键索引alter table 表名 add primary key (字段名);唯一索引alter table 表名 add unique (字段名);
普通索引alter table 表名 add index 索引名称 (字段名);全文索引alter table 表名 fulltext (字段名);组合索引
alter table add index 索引名称(字段1,字段2,,,);查看索引show index from 表名;drop index 索引名 on 表名;
查询速度测试工具set profiling=1;查看执行时间show profiles;
存储过程 创建存储过程
    delimiter //
    create procedure 名称(参数列表)
    begin
    sql语句(DECLARE 变量名 datatype 变量数据类型 DEFAULT 默认值;)
    end
    //
    delimiter ;
存储过程和函数都在mysql.proc表中 name名称,type类型(存储过程还是函数),body正文脚本,db属于的数据库
调用存储过程call 存储过程名称(参数); 删除存储过程drop procedure 名称;
变量 set,select into
IF语句
    IF 条件 THEN
        sql语句;
    ELSEIF 条件 THEN
        sql语句;
    ...
    ELSE
        sql语句;
    END IF;
WHILE语句
    WHILE 条件 DO
        sql语句;
    END WHILE;
字符串拼接CONCAT(str1,str2,,,'?')
函数select 函数() 内置函数 ascii(str),char(int) concat(str1,str2,,,'?') length(str) 截取字
符串left(str,len) right(str,len) substring(str,pos,len) 去除空格ltrim(str) rtrim(str) trim(
both/leading/trailing 'str' from str) space() replace(原str,被替换str,新str) lower(str) upper
(str) year/month(date) day/hour/minute/second(time) date_format(date,%Y/y/m/d/H/h/i/s(完整年份
/简写年份/月份/日期/24进制小时/12进制小时/分钟/秒)) current_date() current_time() now()
自定义函数
    delimiter $$
    create function 函数名称(参数列表) returns 返回类型
    begin
    sql语句
    end
    $$
    delimiter ;

#### mongodb(内容皆为字典)
配置路径/etc/mongodb.conf 数据保存路径/var/lib/mongodb systemLog系统日志 path=/var/lib/mongodb
/mongodb.log net网络配置 bind_ip绑定ip port端口号
mongo
show dbs/collections
use 数据库名
删除当前数据库db.dropDatabase()
db.createCollection('name',选项({capped:true,size:int})) 限定大小的集合不能remove内容
show collections
db.集合名称.drop/insert/update/save/remove/find()(.limit(int).skip(int) sort(字段) count())
insert({(_id:'int'),,,})
update({条件},{$set:{新内容},{multi:true(默认false)}})
save(文档)存在即修改,不存在就添加
remove({条件},{justOne:true(默认false)})
find条件,$lt(e)$gt(e)$ne $or $(n)in findOne()返回第一个 (.pretty())将结果格式化
备份和恢复 mongodump -h 数据库主机ip:端口 -d 数据库名 -o 路径,mongorestore -h ip:port(端口) -d 数据
库名 --dir 恢复数据位置
监控运行情况
1.mongostat mongotop
输出项解释
inserts/s 	每秒插入次数
query/s 	每秒查询次数
update/s	每秒更新次数
delete/s	每秒删除次数
getmore/s 	每秒执行getmore次数,查询时游标(cursor)的getmore操作
command/s	每秒的命令数，除了插入、查找、更新、删除操作，还统计了别的命令
dirty	脏数据字节的缓存百分比
used	正在使用中的缓存百分比
flushs/s	每秒执行fsync将数据写入硬盘的次数
vsize 	虚拟内存使用量，单位是MB
res 	物理内存使用量，单位是MB
qr	客户端等待从MongoDB实例读数据的队列长度
qw	客户端等待从MongoDB实例写入数据的队列长度
ar	执行读操作的活跃客户端数量
aw	执行写操作的活客户端数量
netIn	MongoDB实例的网络进流量
netOut	MongoDB实例的网络出流量
conn	当前连接数
time	时间戳
嵌入式关系(简单,耗性能) 字典中有一项key的value为列表(元素为内容组成的字典),查询{'key':true}
引用式关系 key的value为列表(元素为内容id组成的字典),查询需要先定义变量 var rest = db.user.findOne({"name":
"zhouxingchi"},{"address_ids":1})   db.address.find({"_id":{"$in":rest["address_ids"]}})
DBRefs{$ref:'集合名称',$id:'引用的id',$db:'数据库名称'}
全文索引 db.集合名.createIndex({content:'text'}) 查看索引 db.集合名.getIndex() 使用全文索引 db.集合名.
find($text:{$search:'搜索内容'}}).pretty() 删除索引 db.集合名.dropIndex('content text')
新开mongodb实例sudo mongod --port ? --dbpath=? __logpath=? --replSet 名称 --logappend --fork 登录
mongo port ? 初始化rs.initiate({_id:'复制集名称',members:[{_id:1,host='ip:port'}]}) 查看状态rs.status()
添加成员rs.add('ip:port') 设置仲裁节点rs.addAArb('id:port')(rs.slaveOK()修改从节点功能)
复制集常用方法 复制集初始化rs.initiate() 查看复制集状态rs.status() 查看复制情况db.printSlaveReplicationInfo()：
查看复制集配置rs.conf()/rs.config()
在当前连接让secondary可以提供读操作rs.slaveOk() rs.add() rs.remove() rs.addArb() 重新加载配置文件rs.reconfig()