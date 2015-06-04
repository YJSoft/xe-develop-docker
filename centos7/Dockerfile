# "ported" by Adam Miller <maxamillion@fedoraproject.org> from
#   https://github.com/fedora-cloud/Fedora-Dockerfiles
# Modify to support XE(XpressEngine) by YJSoft
#
# Originally written for Fedora-Dockerfiles by
#   scollier <scollier@redhat.com>

FROM centos:centos7
MAINTAINER YJSoft <yjsoft@yjsoft.pe.kr>

RUN yum -y update; yum clean all
RUN yum -y install epel-release; yum clean all
RUN yum -y install httpd php php-mysql php-gd pwgen supervisor bash-completion openssh-server psmisc tar unzip; yum clean all
ADD ./start.sh /start.sh
ADD ./foreground.sh /etc/apache2/foreground.sh
ADD ./supervisord.conf /etc/supervisord.conf
RUN echo %sudo	ALL=NOPASSWD: ALL >> /etc/sudoers
ADD https://github.com/xpressengine/xe-core/archive/develop.zip /develop.zip
RUN unzip /develop.zip
RUN mv /xe-core-develop/* /xe-core-develop/.htaccess /var/www/html/
RUN chown -R apache:apache /var/www/
RUN chmod 755 /start.sh
RUN chmod 755 /etc/apache2/foreground.sh
RUN mkdir /var/run/sshd

EXPOSE 80
EXPOSE 22

CMD ["/bin/bash", "/start.sh"]
