### 安装mysql5.7
```bash
sudo apt-cache search mysql-server
sudo apt-get install mysql-server-5.7
#未提示输入密码，查找mysql默认密码
cd /etc/mysql
cat debian.conf
mysql -udebian-sys-maint -pyUr10lPmIQd1iKqK
```
### 修改密码
```mysql
use mysql;
update user set authentication_string=PASSWORD("自定义密码") where User='root';
update user set plugin="mysql_native_password";
flush privileges;
exit
```
### 重启mysql，并用新root密码登录
```bash
service mysql restart
mysql -uroot -p
```