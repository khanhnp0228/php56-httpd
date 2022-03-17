FROM centos:centos6

RUN curl https://www.getpagespeed.com/files/centos6-eol.repo --output /etc/yum.repos.d/CentOS-Base.repo

RUN rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm
RUN rpm -Uvh http://ftp.pbone.net/mirror/vault.centos.org/6.10/extras/x86_64/Packages/epel-release-6-8.noarch.rpm
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-6.rpm

RUN yum clean all && yum update -y

RUN yum install -y php php-devel php-mysql php-mbstring php-mcrypt php-pdo php-xml php-bcmath php-cli php-common php-gd --enablerepo=remi,remi-php56

COPY ./docker-entrypoint.sh /docker-entrypoint.sh

RUN chmod +x /docker-entrypoint.sh

RUN sed -i 's/www.example.com:80/localhost/g' /etc/httpd/conf/httpd.conf
RUN sed -i 's/#ServerName/ServerName/g' /etc/httpd/conf/httpd.conf
RUN sed -i 's/#NameVirtualHost/NameVirtualHost/g' /etc/httpd/conf/httpd.conf

WORKDIR /var/www/html

EXPOSE 80

ENTRYPOINT ["/docker-entrypoint.sh"]