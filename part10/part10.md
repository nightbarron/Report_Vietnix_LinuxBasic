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



# Other PRO part

```

## Out of date
# wget --recursive --no-parent -nH --reject="index.html*, *.iso" http://mirror.centos.org/centos/.

# Cent OS
rsync -rv rsync://mirror.aktkn.sg/centos/ /var/www/html/centos

# Ubuntu

# Fedora
rsync -rv rsync://download.nus.edu.sg/epel/ /var/www/html/fedora

# Debian
rsync -rv rsync://ftp.hk.debian.org/debian/ /var/www/html/debian

# RSYNC everyday: `crontab -e`

0 */4 * * * rsync --aqzH --delete <src rsync> <dest> # Every 4 hours

# Optional --ignore-existing will ignore content's checking if file name existed!!!

```

At Client Side:

```
[base]
name=CentOS-$releasever - Base
#mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
baseurl=http://mirror.vietnix.vn/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
.....
.....

```

# HAPPY ENDDING!

<a href='../README.md'>Coming back!</a>