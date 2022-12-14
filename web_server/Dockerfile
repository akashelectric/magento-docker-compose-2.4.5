FROM ubuntu:20.04
ENV DEBIAN_FRONTEND=noninteractive
LABEL maintainer="Akash <akashkumarverma@cedcommerce.com>"

RUN apt-get update \
    && apt-get -y install apache2 nano mysql-client \
    && a2enmod rewrite \
    && a2enmod headers \
    && export LANG=en_US.UTF-8 \
    && apt-get update \
    && apt-get install -y software-properties-common \
    && apt-get install -y language-pack-en-base \
    && LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php \
    && apt-get update \
    && apt-get -y install php8.1 php8.1-curl php8.1-bcmath php8.1-soap php8.1-mysql php8.1-intl php8.1-gd php8.1-dom php8.1-mcrypt php8.1-iconv php8.1-xsl php8.1-mbstring php8.1-ctype   php8.1-zip php8.1-pdo php8.1-xml php8.1-bz2 \
    && sed -i -e"s/^memory_limit\s*=\s*128M/memory_limit = 512M/" /etc/php/8.1/apache2/php.ini \
    && rm /var/www/html/* \
    && sed -i "s/None/all/g" /etc/apache2/apache2.conf \
    && chmod 777 /usr/local/bin/ \
    && apt-get install curl \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=2.2.10 \
    && apt-get install composer -y \
##install supervisor and setup supervisord.conf file
    && apt-get install -y supervisor \
    && mkdir -p /var/log/supervisor
RUN apt-get update && apt-get install wget build-essential gcc make -y

RUN apt-get install default-jdk -y
RUN wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.17.0-amd64.deb
RUN dpkg -i elasticsearch-7.17.0-amd64.deb

env APACHE_RUN_USER    www-data
env APACHE_RUN_GROUP   www-data
env APACHE_PID_FILE    /var/run/apache2.pid
env APACHE_RUN_DIR     /var/run/apache2
env APACHE_LOCK_DIR    /var/lock/apache2
env APACHE_LOG_DIR     /var/log/apache2
env LANG               C

WORKDIR /var/www/html

CMD ["/usr/bin/supervisord"]
