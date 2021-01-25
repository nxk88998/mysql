Mysql5.7 离线安装

安装前准备工作

1、环境配置

关闭内置防火墙以及selinux
```
systemctl stop firewalld  && systemctl disable firewalld
```
关闭selinux服务
```
sed -i s/SELINUX\=enforcing/SELINUX\=disabled/g /etc/selinux/config
setenforce 0
```
安装mysql5.7

1、将安装包mysql5.7.28-install.tar.gz导入系统后

解压离线安装包(自动解压到当前目录)
```
tar -xf mysql5.7.28-install.tar.gz
```
2、进入目录
```
cd mysql5.7.28-install
```
3、运行mysql安装脚本
```
bash  mysql.sh
```
5、替换本机数据库配置文件并覆盖
```
cp my.cnf /etc/my.cnf
```
6、初始化数据库

记住初始化后的密码
```
mysqld  --initialize  --user=mysql
```
注意！保存下这个密码，等下会用到！

7、安装完成，完毕后会提示找不到自定义的日志文件，手动生成一下。
```
mkdir /data/mysql/logs/
touch /data/mysql/logs/remotejob-02-slow.log
```
8、重新赋予目录权限
```
chmod -R 755 /data
chown -R mysql. /data
```
9、启动数据库
```
systemctl  restart  mysqld
```
10、登入数据库
```
mysql -u root -p 初始化的密码
```
11、更改root用户权限和密码
```
alter user 'root'@'localhost' identified by '123456';
```
12、退出重新登入
```
exit
```
13、重新登入
```
mysql -u root -p 
```
14、赋予远程登入权限
```
grant all on *.* to 'root'@'%' identified by '123456';
```
至此mysql安装介绍完成

离线文件下载
链接：https://pan.baidu.com/s/1zcjQ7UB5gy4s-MDYxg0AjA 
提取码：vku7 
