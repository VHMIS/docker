FROM centos:7

# prepare
RUN export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib \
    && rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
    && rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

# install default packages
RUN yum -y update
RUN yum -y install httpd wget supervisor
RUN yum -y install php70w php70w-cli php70w-common php70w-devel php70w-gd php70w-mbstring \
                   php70w-mcrypt php70w-mysqlnd php70w-pdo
RUN yum -y install mariadb-server mariadb-client

# install icu package
RUN cd ~ \
    && wget http://download.icu-project.org/files/icu4c/56.1/icu4c-56_1-RHEL6-x64.tgz \
    && tar -zxvf icu4c-56_1-RHEL6-x64.tgz \
    && cp -r usr / \
    && rm -rf usr \
    && rm -rf icu4c-56_1-RHEL6-x64.tgz

# install intl modules for php7
COPY intl.so /usr/lib64/php/modules/
COPY intl.ini /etc/php.d/

# copy configs
COPY host.conf /etc/httpd/conf.d/
COPY supervisord.conf /etc/

# copy bash scripts to start services
COPY httpd_start /usr/local/bin/
COPY mariadb_start /usr/local/bin/
RUN chmod +x /usr/local/bin/httpd_start \
    && chmod +x /usr/local/bin/mariadb_start

# Volumes
RUN mkdir /vhmis && mkdir /vhmis/Framework && mkdir /vhmis/VhmisSystem \
    && mkdir /vhmis/Libs && mkdir /vhmis/WebRoot \
    && mkdir /data
VOLUME /vhmis/Framework /vhmis/VhmisSystem /vhmis/Libs /vhmis/WebRoot /data

# Ports
EXPOSE 80 3306

# Default command to start all services
CMD ["/usr/bin/supervisord"]
