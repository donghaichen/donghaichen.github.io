```bash
sudo service mysql stop
sudo /usr/bin/mysqld_safe --skip-grant-tables --skip-networking
#新开shell
mysql -u root
```

```sql
use mysql;
update user set authentication_string=PASSWORD("123456") where User='root';
update user set plugin="mysql_native_password";
flush privileges;
quit;
```

sudo /etc/init.d/mysql start
mysql -u root -p123456