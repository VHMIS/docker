# VHMIS DOCKER

## Inside

* CentOS 7.
* Default httpd, mariadb (ship with Centos7).
* php7 from webstatic repo.
* Lastest icu library from ICU project.
* Custom php7-intl module.

## Install

    docker build -t vhmis .

## Run

    docker run -d -P --name vhmis_server \
               -v /vhmis/Framework:/vhmis/Framework \
               -v /vhmis/VhmisSystem:/vhmis/VhmisSystem \
               -v /vhmis/WebRoot:/vhmis/WebRoot \
               -v /vhmis/Data:/vhmis/Data \
               -v /vhmis/Libs:/vhmis/Libs \
               -v /vhmis/MysqlData:/var/lib/mysql \
               vhmis

For linux host, use your correct HOST_USER_ID and HOST_USER_GID to allow container has write permission.

    # get folder's user and group id on host
    id -u username
    id -g groupname

    # run container with ids
    docker run -d -P --name vhmis_server \
               -v /vhmis/Framework:/vhmis/Framework \
               -v /vhmis/VhmisSystem:/vhmis/VhmisSystem \
               -v /vhmis/WebRoot:/vhmis/WebRoot \
               -v /vhmis/Data:/vhmis/Data \
               -v /vhmis/Libs:/vhmis/Libs \
               -v /vhmis/MysqlData:/var/lib/mysql \
               -e HOST_USER_ID='uid' \
               -e HOST_USER_GID='gid' \
               vhmis

## Set mysql root password

In the first time running, execute follow command to set mysql root password

    docker exec [container_name] mysqladmin -u root -S /var/run/mariadb/mysql.sock password 'newpassword'

## My command

Ubuntu at work

    docker run -d -P --name vhmis_server \
           -v /vhmis/Framework:/vhmis/Framework \
           -v /vhmis/VhmisSystem:/vhmis/VhmisSystem \
           -v /vhmis/WebRoot:/vhmis/WebRoot \
           -v /vhmis/Data:/vhmis/Data \
           -v /vhmis/Libs:/vhmis/Libs \
           -v /vhmis/MysqlData:/var/lib/mysql \
           -e HOST_USER_ID='1000' \
           -e HOST_USER_GID='1000' \
           vhmis

Mac

    docker run -d -p 80:80 -p 3306:3306 --name vhmis_server \
           -v /vhmis/Framework:/vhmis/Framework \
           -v /vhmis/VhmisSystem:/vhmis/VhmisSystem \
           -v /vhmis/WebRoot:/vhmis/WebRoot \
           -v /vhmis/Data:/vhmis/Data \
           -v /vhmis/Libs:/vhmis/Libs \
           -v /vhmis/MysqlData:/var/lib/mysql \
           vhmis

SQL 123456

    docker exec [container_name] mysqladmin -u root -S /var/run/mariadb/mysql.sock password '123456'
