# Ubuntu16 安装 mysql5.7

### 安装 mysql5.7
```bash
sudo apt-cache search mysql-server
sudo apt-get install mysql-server-5.7
#未提示输入密码，查找mysql默认密码
cd /etc/mysql
cat debian.conf
mysql -udebian-sys-maint -p
```
### 修改密码
```mysql
use mysql;
update user set authentication_string=PASSWORD("newPassword") where User="root";
update user set plugin="mysql_native_password";
flush privileges;
exit
```
### 重启 mysql，并用新 root 密码登录
```bash
service mysql restart
mysql -uroot -p
```
