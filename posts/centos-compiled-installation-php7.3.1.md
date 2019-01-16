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
```bash
cd ~/php-7.3.1
cp -R ./php.ini-development ./php.ini-production /usr/local/php7/etc
cp /usr/local/php7/etc/php.ini-development /usr/local/php7/etc/php.ini
cp /usr/local/php7/etc/php-fpm.conf.default /usr/local/php7/etc/php-fpm.conf
cp /usr/local/php7/etc/php-fpm.d/www.conf.default /usr/local/php7/etc/php-fpm.d/www.conf
```

### 建立软链
```bash
ln -s /usr/local/php7/etc/php.ini /usr/local/etc/php7.ini
ln -s /usr/local/php7/etc/php-fpm.conf /usr/local/etc/php7-fpm.conf
ln -s /usr/local/php7/etc/php-fpm.d/www.conf /usr/local/etc/php7-fpm.d/www.conf
```

### 配置环境变量，加入全局命令
```bash
vim /etc/profile

PATH=$PATH:/usr/local/php7/bin
export PATH

source /etc/profile
```

### 启动php-fpm 服务
```bash
/usr/local/sbin/php7-fpm
```

### 查看是否启动
```bash
netstat -lnt | grep 9000
```

### 杀死 php-fpm
```bash
killall php-fpm
# 或者
netstat -tunlp |grep php
kill -USR2 4081
```

### 安装完成 php7 路径备忘
```bash
Installing shared extensions:     /usr/local/php7/lib/php/extensions/no-debug-zts-20180731/
Installing PHP CLI binary:        /usr/local/php7/bin/
Installing PHP CLI man page:      /usr/local/php7/php/man/man1/
Installing PHP FPM binary:        /usr/local/php7/sbin/
Installing PHP FPM defconfig:     /usr/local/php7/etc/
Installing PHP FPM man page:      /usr/local/php7/php/man/man8/
Installing PHP FPM status page:   /usr/local/php7/php/php/fpm/
Installing phpdbg binary:         /usr/local/php7/bin/
Installing phpdbg man page:       /usr/local/php7/php/man/man1/
Installing PHP CGI binary:        /usr/local/php7/bin/
Installing PHP CGI man page:      /usr/local/php7/php/man/man1/
Installing build environment:     /usr/local/php7/lib/php/build/
Installing header files:          /usr/local/php7/include/php/
Installing helper programs:       /usr/local/php7/bin/
  program: phpize
  program: php-config
Installing man pages:             /usr/local/php7/php/man/man1/
  page: phpize.1
  page: php-config.1
Installing PEAR environment:      /usr/local/php7/lib/php/
[PEAR] Archive_Tar    - installed: 1.4.4
[PEAR] Console_Getopt - installed: 1.4.1
[PEAR] Structures_Graph- installed: 1.1.1
[PEAR] XML_Util       - installed: 1.4.3
[PEAR] PEAR           - installed: 1.10.7
Warning! a PEAR user config file already exists from a previous PEAR installation at '/root/.pearrc'. You may probably want to remove it.
Wrote PEAR system config file at: /usr/local/php7/etc/pear.conf
You may want to add: /usr/local/php7/lib/php to your php.ini include_path
/root/php-7.3.1/build/shtool install -c ext/phar/phar.phar /usr/local/php7/bin
ln -s -f phar.phar /usr/local/php7/bin/phar
Installing PDO headers:           /usr/local/php7/include/php/ext/pdo/
```

> 参考链接 ： [https://segmentfault.com/a/1190000015433237?utm_source=tag-newest](https://segmentfault.com/a/1190000015433237?utm_source=tag-newest)
