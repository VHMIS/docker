FROM centos:7

COPY mariadb.repo /etc/yum.repos.d/

RUN export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib \
    && groupadd -r mysql && useradd -r -g mysql mysql \
    && rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm \
    && yum -y install wget \
                      php70w php70w-cli php70w-common php70w-devel php70w-gd php70w-mbstring \
                      php70w-mcrypt php70w-mysqlnd php70w-pdo \
                      httpd supervisor \
                      MariaDB-server MariaDB-client \
    && cd ~ \
    && wget http://download.icu-project.org/files/icu4c/56.1/icu4c-56_1-RHEL6-x64.tgz \
    && tar -zxvf icu4c-56_1-RHEL6-x64.tgz \
    && cp -r usr / \
    && rm -rf usr \
    && rm -rf icu4c-56_1-RHEL6-x64.tgz

COPY intl.so /usr/lib64/php/modules/
COPY intl.ini /etc/php.d/
COPY httpd_start /usr/local/bin/
COPY mariadb_start /usr/local/bin/
COPY host.conf /etc/httpd/conf.d/
COPY supervisord.conf /etc/

RUN chmod +x /usr/local/bin/httpd_start \
    && chmod +x /usr/local/bin/mariadb_start \
    && mkdir /vhmis && mkdir /vhmis/Framework && mkdir /vhmis/VhmisSystem \
    && mkdir /vhmis/Libs && mkdir /vhmis/WebRoot \
    && mkdir /data

VOLUME /vhmis/Framework /vhmis/VhmisSystem /vhmis/Libs /vhmis/WebRoot /data

EXPOSE 80 3306

CMD ["/usr/bin/supervisord"]
