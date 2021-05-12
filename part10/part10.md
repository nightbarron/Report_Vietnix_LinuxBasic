# Report_Vietnix_LinuxBasic

# *~~ MENU FOR PART 10 Create Repo in Cent OS ~~*


## In server site

```
yum install createrepo

yum install yum-utils

sudo mkdir –p /var/www/html/repos/{base,centosplus,extras,updates}

sudo reposync -g -l -d -m --repoid=base --newest-only --download-metadata --download_path=/var/www/html/repos/

sudo reposync -g -l -d -m --repoid=centosplus --newest-only --download-metadata --download_path=/var/www/html/repos/

sudo reposync -g -l -d -m --repoid=extras --newest-only --download-metadata --download_path=/var/www/html/repos/

sudo reposync -g -l -d -m --repoid=updates --newest-only --download-metadata --download_path=/var/www/html/repos/   

sudo createrepo /var/www/html

service httpd start

# DONE
```

## In client side

```
# Create vietnix.repo file 
nano /etc/yum.repo.d/vietnix.repo

# Content as below:

[Vietnix.vn]
name=mirror.vietnix.vn
baseurl=http://mirror.vietnix.vn
enabled=1
gpgcheck=0

```
# HAPPY ENDDING!

<a href='../README.md'>Coming back!</a>