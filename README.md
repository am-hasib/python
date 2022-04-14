# For CentOS 7
rpm -ivh http://rpms.litespeedtech.com/centos/litespeed-repo-1.1-1.el7.noarch.rpm

yum install epel-release

yum install openlitespeed

yum install lsphp74 lsphp74-json lsphp74-xmlrpc lsphp74-xml lsphp74-tidy lsphp74-soap lsphp74-snmp lsphp74-pspell lsphp74-process lsphp74-pgsql lsphp74-pear lsphp74-pdo lsphp74-opcache lsphp74-odbc lsphp74-mysqlnd lsphp74-mcrypt lsphp74-mbstring lsphp74-ldap lsphp74-intl lsphp74-imap lsphp74-gmp lsphp74-gd lsphp74-enchant lsphp74-dba lsphp74-common lsphp74-bcmath lsphp74-memcached lsphp74-redis

# For Ubuntu
wget -O - http://rpms.litespeedtech.com/debian/enable_lst_debian_repo.sh | bash

apt install openlitespeed

apt install lsphp74 lsphp74-common lsphp74-curl lsphp74-dev lsphp74-imap lsphp74-intl lsphp74-json lsphp74-ldap lsphp74-mysql lsphp74-opcache lsphp74-pspell lsphp74-memcached lsphp74-redis lsphp74-sqlite3 lsphp74-tidy

## For eveyone

groupadd group-name

useradd -M -g group-name user-name

mkdir /home/domain.com

mkdir /home/domain.com/public_html

chown user-name:group-name /home/domain.com

chmod 711 /home/domain.com

chown user-name:nobody /home/domain.com/public_html

chmod 750 /home/domain.com/public_html

touch /home/domain.com/public_html/.htaccess
chown -R user-name:group-name /home/domain.com/public_html/.htaccess 

#create .htaccess for later use, this is optional

echo "<?php phpinfo();" > /home/domain.com/public_html/info.php

#create a phpinfo page to test

echo "hello world" > /home/domain.com/public_html/index.html 

#create a static HTML page to test

chown -R user-name:group-name /home/domain.com/public_html/*

# replace "user-name", "group-name" and "domain.com" to your actual value 
# user-name and group-name can use any name you wish , but suggest to use domain name for easier management.


# it is VERY important that you run that chown -R command to correctly set ownership for files after you migrate/upload files via SFTP or any other method.
# it is VERY important that you run that chown -R command to correctly set ownership for files after you migrate/upload files via SFTP or any other method.
# it is VERY important that you run that chown -R command to correctly set ownership for files after you migrate/upload files via SFTP or any other method.
# if ownership is not correctly set , you may encounter permission denied error. 


systemctl start lsws 

#start up OpenLiteSpeed

/usr/local/lsws/admin/misc/admpass.sh

# to set/reset the webadmin console login info.

https://your_server_ip:7080

# login to webadmin console , if you can not access it , make sure your firewall is NOT blocking it.
# you can run "curl -I -XGET -k https://server_public_ip:7080" and "curl -I -XGET -k https://127.0.0.1:7080" to verify.
# if 127 IP gives 301/302 response and public IP doesn't , that means 7080 port is not opened.

Address: uds://tmp/lshttpd/domain.sock

Max Connections: 10
Environment: PHP_LSAPI_CHILDREN=10
# this means maximum 10 PHP processes ,  change it to a high number GRADUALLY if your site requires lots PHP processes to process.

Command: /usr/local/lsws/lsphp74/bin/lsphp

Run As User: user-name

Run As Group: group-name
#this will force PHP script to run as site user , for security concern.

# external app settings


curl https://get.acme.sh | sh

# install acme.sh for let's encrypt certificate.

domain="domain.com" ; /root/.acme.sh/acme.sh --issue -d "$domain" -d www."$domain" -w /home/"$domain"/public_html

# replace "doamin.com" at first part of line to your actual domain  , and remove  -d www."$domain"    part if you don't use www domain.

# this is optional , you can use other tools like certbot , or just upload your own cert/key somehwhere and set path in webadmin console.

RewriteEngine On
#RewriteCond %{HTTP_HOST} !domain\.com [NC,OR]
RewriteCond %{HTTPS}  !=on
RewriteRule ^/?(.*) https://%{SERVER_NAME}/$1 [R=301,L]

# rewriterule to force HTTPS, add it into previously created .htaccess file
# change %{SERVER_NAME} to domain.com and remove # in second line, if you want to redirection http(s)://SERVER_IP to https://domain.com

# it is VERY important that you restart OpenLiteSpeed to load new .htaccess rules , otherwise it will not work.
# it is VERY important that you restart OpenLiteSpeed to load new .htaccess rules , otherwise it will not work.
# it is VERY important that you restart OpenLiteSpeed to load new .htaccess rules , otherwise it will not work.
