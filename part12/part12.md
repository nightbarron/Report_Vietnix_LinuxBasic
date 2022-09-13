# Report_Vietnix_LinuxBasic

# *~~ MENU FOR PART 12 Multi HOST Apache2 (Ubuntu Server 20.04) ~~*

# 1. Config some users with their own host

```
useradd -m webad01 webad02 webad03

# Then change password of user to ENABLE them
# Create public_html in their home dir

mkdir /home/webad01/public_html /home/webad02/public_html /home/webad03/public_html

```

# 2. Config VirtualHost

```
cd /etc/apache2

# Create dafault Vhost
nano default_vhost.conf 

# Content like below:

<VirtualHost *:80>
    ServerName defaultwebsite.com
    ServerAlias *
    DocumentRoot /var/www/html
</VirtualHost>

# Them create config for host

mkdir vhost.d && cd vhost.d

nano webad01.conf

# Create content as below:
                                    
<VirtualHost *:80>
    ServerAdmin webad01@localhost
    DocumentRoot /home/webad01/public_html
    ServerName webad01.info

    <Directory /home/webad01/public_html>
            Options Indexes FollowSymLinks
            AllowOverride All
            Require all granted
    </Directory>

</VirtualHost>

# NOTE: Because of using same port, Server will identify them by their SERVERNAME (Or SERVERALIAS)

# Same of other

# Then we must edit /etc/apache2/apache2.conf

nano /etc/apache2/apache2.conf

# Add some lines at the END as order below:

IncludeOptional vhost.d/*.conf
IncludeOptional default_vhost.conf

# NOTE: if you change this ORDER, Server may work unexpected!!!

service apache2 restart

# DONE
```

# 3. Config Mutil PHP for each VHOST

```
# We will run PHP 7.4 in webad01.info
# AND PHP 5.4 in webadmin02.info

# Please see from #part04 line 80, to know how to install FastCGI PHP Handler. 
# In this part, we will using both 'PHP7.4 Apache2Handler' and 'FastCGI' handler for each hosts

apt-get install gcc g++ make apache2-dev aprx php-cgi

a2emond fastcgi
a2dismod php7.4 cgi

# Install Multi PHP
apt install software-properties-common 
add-apt-repository ppa:ondrej/php

apt install -y php5.6 php5.6-cgi

apt-get install -y libapache2-mod-fcgid

 apt-get install -y apache2-suexec-custom
 # Change docroot

```
