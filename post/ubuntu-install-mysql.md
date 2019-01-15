```bash
sudo apt-cache search mysql-server
sudo apt-get install mysql-server-5.7
cd /etc/mysql
cat debian.conf
mysql -udebian-sys-maint -pyUr10lPmIQd1iKqK
```
```mysql
use mysql;
update user set authentication_string=PASSWORD("自定义密码") where User='root';
update user set plugin="mysql_native_password";
flush privileges;
exit
```
```bash
service mysql restart
mysql -uroot -p
```