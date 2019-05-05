### PHP
```
yum install autoconf
yum install gc
yum install gc-c++
yum install automake
yum install libtool

git clone https://github.com/skvadrik/re2c/tree/0.15.3/re2c 
cd re2c
./configure --prefix=/usr/local/re2c
make && make install

yum install bison

yum -y install zlib zlib-devel openssl openssl--devel pcre pcre-devel

```
#### 安装nginx
```
> wget https://nginx.org/download/nginx-1.11.3.tar.gz
> tar xf nginx-1.11.3.tar.gz
> cd nginx-1.11.3
> ./configure prefix=/usr/local/nginx
> vi /etc/init.d/nginx
#!/bin/bash
#chkconfig: - 85 15
PATH=/usr/local/nginx
DESC="nginx daemon"
NAME=nginx
DAEMON=$PATH/sbin/$NAME
CONFIGFILE=$PATH/conf/$NAME.conf
PIDFILE=$PATH/logs/$NAME.pid
SCRIPTNAME=/etc/init.d/$NAME
set -e
[ -x "$DAEMON" ] || exit 0
    do_start() {
    $DAEMON -c $CONFIGFILE || echo -n "nginx already running"
}
do_stop() {
    $DAEMON -s stop || echo -n "nginx not running"
}
do_reload() {
    $DAEMON -s reload || echo -n "nginx can't reload"
}
case "$1" in
start)
    echo -n "Starting $DESC: $NAME"
    do_start
    echo "."
;;
stop)
    echo -n "Stopping $DESC: $NAME"
    do_stop
echo "."
;;
reload|graceful)
    echo -n "Reloading $DESC configuration..."
    do_reload
    echo "."
;;
restart)
    echo -n "Restarting $DESC: $NAME"
    do_stop
    do_start
    echo "."
;;
*)
echo "Usage: $SCRIPTNAME {start|stop|reload|restart}" >&2
exit 3
;;
esac
exit 0
>service nginx start
>service nginx restart
>service nginx stop
```
#### 针对centos7 systemctl 操作
```
> vi /lib/systemd/system/nginx.service
[Unit]
Description=nginx
After=network.target
  
[Service]
Type=forking
ExecStart=/usr/local/nginx/sbin/nginx
ExecReload=/usr/local/nginx/sbin/nginx -s reload
ExecStop=/usr/local/nginx/sbin/nginx -s quit
PrivateTmp=true
  
[Install]
WantedBy=multi-user.target


[Unit]:服务的说明
Description:描述服务
After:描述服务类别
[Service]服务运行参数的设置
Type=forking是后台运行的形式
ExecStart为服务的具体运行命令
ExecReload为重启命令
ExecStop为停止命令
PrivateTmp=True表示给服务分配独立的临时空间
注意：[Service]的启动、重启、停止命令全部要求使用绝对路径
[Install]运行级别下服务安装的相关设置，可设置为多用户，即系统运行级别为3

保存退出。

> systemctl enable nginx.service
> systemctl start nginx.service
> systemctl stop nginx.service
> systemctl list-units --type=service #查看service

```
#### PHP安装
```
解决依赖包
> yum install libxml2-dev
> yum install openssl openssl-devel
> ln -s /usr/lib64/libssl.so /usr/lib/
> yum -y install curl-devel
> yum -y install libjpeg-devel
> yum install libpng libpng-devel -y
> yum install freetype-devel
> yum -y install libxslt libxslt-devel
> yum install libzip-devel
> yum install libpng libpng-devel -y
> yum install libpng libpng-devel -y
> yum install libpng libpng-devel -y
> yum install libpng libpng-devel -y
> yum install libpng libpng-devel -y
> yum install libpng libpng-devel -y
> yum install libpng libpng-devel -y
> yum install libpng libpng-devel -y
> yum install libpng libpng-devel -y
> yum install libpng libpng-devel -y
> yum install libpng libpng-devel -y


> tar xf php-7.3.4
> cd php-7.3.4
> ./configure --prefix=/usr/local/php7
--exec-prefix=/usr/local/php7 \
--bindir=/usr/local/php7/bin \
--sbindir=/usr/local/php7/sbin \
--includedir=/usr/local/php7/include \
--libdir=/usr/local/php7/lib/php \
--mandir=/usr/local/php7/php/man \
--with-config-file-path=/usr/local/php7/etc \
--with-mysql-sock=/var/lib/mysql/mysql.sock \
--with-mcrypt=/usr/include \
--with-mhash \
--with-openssl \
--with-mysql=shared,mysqlnd \
--with-mysqli=shared,mysqlnd \
--with-pdo-mysql=shared,mysqlnd \
--with-gd \
--with-iconv \
--with-zlib \
--enable-zip \
--enable-inline-optimization \
--disable-debug \
--disable-rpath \
--enable-shared \
--enable-xml \
--enable-bcmath \
--enable-shmop \
--enable-sysvsem \
--enable-mbregex \
--enable-mbstring \
--enable-ftp \
--enable-gd-native-ttf \
--enable-pcntl \
--enable-sockets \
--with-xmlrpc \
--enable-soap \
--without-pear \
--with-gettext \
--enable-session \
--with-curl \
--with-jpeg-dir \
--with-freetype-dir \
--enable-opcache \
--enable-redis \
--enable-fpm \
--enable-fastcgi \
--with-fpm-user=www \
--with-fpm-group=www \
--without-gdbm \
--disable-fileinfo

> make && make install
> cp php.ini.default /usr/local/php7/php.ini  #复制配置文件到php路径
> cp /usr/local/etc/php-fpm.d/www.conf.default /usr/local/etc/php-fpm.d/www.conf #复制fpm配置文件
> cp sapi/fpm/php-fpm /usr/local/bin/ #复制执行文件到bin
> vim /usr/local/php7/php.ini => cgi.fix_pathinfo=0
> vim /usr/local/etc/php-fpm.d/www.conf
user = www-data
group = www-data
> /usr/local/bin/php-fpm  #开启fpm

> vim /usr/local/nginx/conf/nginx.conf
location / {
    root   html;
    index  index.php index.html index.htm;
}
location ~* \.php$ {
    fastcgi_index   index.php;
    fastcgi_pass    127.0.0.1:9000;
    include         fastcgi_params;
    fastcgi_param   SCRIPT_FILENAME    $document_root$fastcgi_script_name;
    fastcgi_param   SCRIPT_NAME        $fastcgi_script_name;
}
> service nginx start 或  /usr/local/nginx/sbin/nginx -s start

测试phpinfo();
> echo "<?php phpinfo(); ?>" >> /usr/local/nginx/html/index.php

```
### Swoole
```
sss
```