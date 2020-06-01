FROM amazonlinux:2

COPY php.ini /usr/local/etc/php/
COPY www.conf /etc/php-fpm.d/www.conf

RUN yum -y update

# install nginx
#RUN amazon-linux-extras install nginx1.12
RUN amazon-linux-extras install php7.2 -y

RUN yum install -y php-cli php-common php-devel php-fpm php-gd php-mysqlnd php-mbstring php-pdo php-xml
RUN yum install -y mysql
RUN yum install -y git
RUN yum install -y sudo
RUN yum install -y unzip

#Composer install
COPY --from=composer /usr/bin/composer /usr/bin/composer

ENV COMPOSER_ALLOW_SUPERUSER 1

ENV COMPOSER_HOME /composer

ENV PATH $PATH:/composer/vendor/bin

WORKDIR /usr/share/nginx/dawn

RUN composer require "laravel/installer"
RUN composer require "laravel/cashier":"~7.0"
RUN composer require "stripe/stripe-php":"^5.0"
RUN composer require "doctrine/dbal"
RUN composer install

EXPOSE 9000
ENTRYPOINT /usr/sbin/php-fpm -F
