# ���ü̳������Ǵ�����sshd����
FROM sshd:dockerfile

# ��������Ϣ
MAINTAINER binggou alibaba-inc.com

# ���û������������в������Ƿǽ���ʽ��
ENV DEBIAN_FRONTEND noninteractive

# ��װ
RUN apt-get -yq install apache2 && rm -rf /var/lib/apt/lists/*
RUN echo "Asia/Shanghai" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
# ע������Ҫ����ϵͳ��ʱ�����ã���Ϊ��WebӦ���о������õ��������ϵͳ������Ĭ�ϵ�Ubuntu�������Ӧ�ó���������˼���Ч��Ŷ

# �������ǵĽű���������Ȩ�ޣ���Ḳ��֮ǰ�������λ�õĽű�
ADD run.sh /run.sh
RUN chmod 755 /*.sh

# ����һ��ʾ����Webվ�㣬ɾ��Ĭ�ϰ�װ��Apache�ļ���������ļ��������������ӵ�ʾ��������������/var/www/htmlĿ¼����
RUN mkdir -p /var/lock/apache2 && mkdir -p /app && rm -rf /var/www/html && ln -s /app /var/www/html
COPY sample/ /app

# ����Apache��ص�һЩ������������������ʱ�����ʹ��-e�������
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_SERVERADMIN admin@localhost
ENV APACHE_SERVERNAME localhost
ENV APACHE_SERVERALIAS docker.localhost
ENV APACHE_DOCUMENTROOT /var/www

EXPOSE 80
WORKDIR /app
CMD ["/run.sh"]
