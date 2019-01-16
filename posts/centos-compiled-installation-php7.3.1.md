### 安装依赖
```bash
yum -y install wget vim pcre pcre-devel openssl openssl-devel libicu-devel gcc gcc-c++ autoconf libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel libxml2 libxml2-devel zlib zlib-devel glibc glibc-devel glib2 glib2-devel ncurses ncurses-devel curl curl-devel krb5-devel libidn libidn-devel openldap openldap-devel nss_ldap jemalloc-devel cmake boost-devel bison automake libevent libevent-devel gd gd-devel libtool* libmcrypt libmcrypt-devel mcrypt mhash libxslt libxslt-devel readline readline-devel gmp gmp-devel libcurl libcurl-devel openjpeg-devel
```

### 下载解压安装包
```bash
http://cn2.php.net/get/php-7.3.1.tar.gz
tar -zxvf php-7.3.1.tar.gz
```

### 编译安装
```bash
cd php-7.3.1
./configure --prefix=/usr/local/php7 \
--with-config-file-path=/usr/local/php/etc7 \
--enable-fpm \
--with-fpm-user=www \
--with-fpm-group=www \
--enable-mysqlnd \
--with-mysqli=mysqlnd \
--enable-mysqlnd-compression-support \
--with-iconv-dir \
--with-freetype-dir \
--with-jpeg-dir \
--with-png-dir \
--with-zlib \
--with-libxml-dir \
--enable-xml \
--disable-rpath \
--enable-bcmath \
--enable-shmop \
--enable-sysvsem \
--enable-inline-optimization \
--with-curl \
--enable-mbregex \
--enable-intl \
--enable-ftp \
--with-gd \
--enable-gd-jis-conv \
--with-mhash \
--enable-pcntl \
--enable-sockets \
--with-xmlrpc \
--enable-zip \
--enable-soap \
--with-gettext \
--disable-fileinfo \
--with-pear \
--enable-maintainer-zts \
--with-ldap=shared \
--without-gdbm \
--enable-opcache \
--enable-tokenizer \
--enable-ctype \
--enable-json \
--enable-mbstring \
--with-openssl \
--with-pdo-mysql=mysqlnd
#如果报错如下 ext/gd/libgd/.libs/gdkanji.o: In function `do_convert’:
# vi Makefile
# 找到下面这行：
# EXTRA_LIBS = -lcrypt ...
# 在最后添加 -liconv
如果报错 编译 zip.h:59:21: 致命错误：zipconf.h：没有那个文件或目录
cp /usr/local/lib/libzip/include/zipconf.h /usr/local/include/zipconf.h
make && make install
```
### 建立软链
```bash
ln -s /usr/local/php7/ /usr/local/php7
ln -s /usr/local/php7/bin/php /usr/local/bin/php7
ln -s /usr/local/php7/sbin/php-fpm /usr/local/sbin/php7-fpm
```

### 对 php-fpm 运行用户进行设置
cd ~/php-7.3.1
cp -R ./php.ini-development ./php.ini-production /usr/local/php7/etc
cp /usr/local/php7/etc/php.ini-development /usr/local/php7/etc/php.ini
cp /usr/local/php7/etc/php-fpm.conf.default /usr/local/php7/etc/php-fpm.conf
cp /usr/local/php7/etc/php-fpm.d/www.conf.default /usr/local/php7/etc/php-fpm.d/www.conf
### 建立软链
ln -s /usr/local/php7/etc/php.ini /usr/local/etc/php7.ini
ln -s /usr/local/php7/etc/php-fpm.conf /usr/local/etc/php7-fpm.conf
ln -s /usr/local/php7/etc/php-fpm.d/www.conf /usr/local/etc/php7-fpm.d/www.conf
### 配置环境变量，加入全局命令
vim /etc/profile

PATH=$PATH:/usr/local/php7/bin
export PATH

source /etc/profile

### 启动php-fpm 服务
/usr/local/sbin/php7-fpm

### 查看是否启动
netstat -lnt | grep 9000

### 杀死 php-fpm
killall php-fpm
# 或者
netstat -tunlp |grep php
kill -USR2 4081

> 参考链接 ： [https://segmentfault.com/a/1190000015433237?utm_source=tag-newest](https://segmentfault.com/a/1190000015433237?utm_source=tag-newest)
