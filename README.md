# Yum Repositories

## PHP

```bash
if [[ `uname -a | grep el6` ]]; then
    # CentOS 6
    yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-6.noarch.rpm
    yum install -y http://rpms.remirepo.net/enterprise/remi-release-6.rpm
else
    # CentOS 7
    yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
    yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm
fi

yum install -y yum-utils
yum-config-manager --enable remi-php56 #php 5.6
yum-config-manager --enable remi-php70 #php 7.0
yum-config-manager --enable remi-php71 #php 7.1
yum-config-manager --enable remi-php72 #php 7.2
yum-config-manager --enable remi-php73 #php 7.3
yum info php | grep -i version
```

## MySQL

```bash
if [[ `uname -a | grep el6` ]]; then
    # CentOS 6
    yum install -y https://dev.mysql.com/get/mysql80-community-release-el6-3.noarch.rpm
else
    # CentOS 7
    yum install -y https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
fi

# list all versions
yum repolist all | grep mysql

# disable all versions
yum-config-manager --disable mysql55-community #MySQL 5.5
yum-config-manager --disable mysql56-community #MySQL 5.6
yum-config-manager --disable mysql57-community #MySQL 5.7
yum-config-manager --disable mysql80-community #MySQL 8.0

# enable the version you want
yum-config-manager --enable mysql?-community

# install
yum install mysql-community-server

```

## Nginx

```bash
yum install yum-utils

echo "[nginx-stable]
name=nginx stable repo
baseurl=http://nginx.org/packages/centos/\$releasever/\$basearch/
gpgcheck=1
enabled=1
gpgkey=https://nginx.org/keys/nginx_signing.key" > /etc/yum.repos.d/nginx.repo

yum install nginx
```



## Docker

```bash
# To install Docker CE, you need a maintained version of CentOS 7. Archived versions aren’t supported or tested.
yum install yum-utils device-mapper-persistent-data lvm2
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install docker-ce docker-ce-cli containerd.io

```

## Top 5 YUM Repositories

1. EPEL (Extra Packages for Enterprise Linux)

```bash
yum install epel-release
```

2. REMI

```bash
# CentOS 7  
yum install https://rpms.remirepo.net/enterprise/remi-release-7.rpm

# CentOS 6
yum install https://rpms.remirepo.net/enterprise/remi-release-6.rpm
```

3. RPMFusion

```bash
# CentOS 7
yum localinstall --nogpgcheck https://download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm 
yum localinstall --nogpgcheck https://download1.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-7.noarch.rpm

# CentOS 6
yum localinstall --nogpgcheck https://download1.rpmfusion.org/free/el/rpmfusion-free-release-6.noarch.rpm
yum localinstall --nogpgcheck https://download1.rpmfusion.org/nonfree/el/rpmfusion-nonfree-release-6.noarch.rpm
```

4. ELRepo

```bash
# CentOS 7
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm

# CentOS 6
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm -Uvh  http://www.elrepo.org/elrepo-release-6-8.el6.elrepo.noarch.rpm
```

5. Webtatic

```bash
# CentOS 7
sudo yum localinstall --nogpgcheck http://repo.webtatic.com/yum/el7/webtatic-release.rpm

# CentOS 6
sudo yum localinstall --nogpgcheck http://repo.webtatic.com/yum/el6/latest.rpm
```

## 参考

- [Download MySQL Yum Repository](https://dev.mysql.com/downloads/repo/yum/)
- [A Quick Guide to Using the MySQL Yum Repository](https://dev.mysql.com/doc/mysql-yum-repo-quick-guide/en/)
- [Get Docker CE for CentOS](https://docs.docker.com/install/linux/docker-ce/centos/)
- [nginx: Linux packages](https://nginx.org/en/linux_packages.html#RHEL-CentOS)
- [Top 5 Yum Repositories](https://tecadmin.net/top-5-yum-repositories-for-centos-rhel-systems/)
- [Top 8 Yum Repositories](https://www.tecmint.com/yum-thirdparty-repositories-for-centos-rhel/)
