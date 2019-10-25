# ( 转载 ) CentOS 7 yum 安装 PHP7.3

2018-12-06号，php7.3.0正式发布，PHP 7.3 也带了性能提升，相比早期的 PHP 7.0 有了近 22% 的性能提升。同时 PHP 5.6 和 7.0 都即将失去 PHP 社区官方的支持，所以也是建议大家能尽快的升级到最新版本。

### PHP 7.3 的主要更新内容：

> 灵活的 Heredoc 和 Nowdoc 语法
从 PCRE 迁移至 PCRE2
Multiple MBString Improvements
LDAP 控件支持
改善 FPM 日志
改善 Windows 文件删除
弃用相关就平台

···bash
yum install epel-release
yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm  
yum install yum-utils
yum install -y php73-php-fpm php73-php-cli php73-php-bcmath php73-php-gd php73-php-json php73-php-mbstring php73-php-mcrypt php73-php-mysqlnd php73-php-opcache php73-php-pdo php73-php-pecl-crypto php73-php-pecl-mcrypt php73-php-pecl-geoip php73-php-recode php73-php-snmp php73-php-soap php73-php-xmll
···

安装完成后最好重启一下计算机，不然有可能无法启动php

### 设置开机启动、运行服务：
···bash
systemctl enable php73-php-fpm
systemctl start php73-php-fpm
···

### 设置 PHP

查找php.ini位置：
···bash
find /etc/opt/remi/php73 -name php.ini
# 编辑/etc/opt/remi/php73/php.ini替换换 ;cgi.fix_pathinfo=1 为 cgi.fix_pathinfo=0 快捷命令：
# sed -i 's/;cgi.fix_pathinfo=1/cgi.fix_pathinfo=0/' /etc/opt/remi/php73/php.ini
# 重启php73-php-fpm
systemctl restart php73-php-fpm
# 更多操作：
systemctl restart php73-php-fpm #重启
systemctl start php73-php-fpm #启动
systemctl stop php73-php-fpm #关闭
systemctl status php73-php-fpm #检查状态
···

原文链接 (https://blog.csdn.net/laohe08/article/details/93166590)