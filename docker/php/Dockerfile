FROM phpdockerio/php74-fpm:latest
ENV WORKDIR /home/codeblog.pro/www

WORKDIR ${WORKDIR}

RUN groupadd -g 1000 ubuntu
RUN useradd -d /home/ubuntu -s /bin/bash -u 1000 -g 1000 ubuntu
# Create home directory
RUN mkdir /home/ubuntu
# User and group own home directory
RUN chown -R ubuntu:ubuntu /home/ubuntu

# Install selected extensions and other stuff
RUN apt-get update \
    && apt-get -y --no-install-recommends install  php7.4-mysql php-redis php-xdebug php7.4-bcmath php7.4-bz2 php7.4-gd php-mongodb php7.4-xsl \
    && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Install git && net-tools && vim
RUN apt-get update && apt-get install net-tools -y && apt-get install vim -y && apt-get install git -y

# Install postfix for smtp and mailutils
RUN apt-get install postfix -y && apt-get install mailutils -y && service postfix start

# Install Composer
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer