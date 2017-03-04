FROM php:7

RUN sed -i 's/deb\.debian\.org/mirrors.aliyun.com/' /etc/apt/sources.list && sed -i 's/security\.debian\.org/mirrors.aliyun.com\/debian-security/' /etc/apt/sources.list

RUN apt-get update && apt-get install -y \ 
	--no-install-recommends \
	software-properties-common \
	apt-transport-https \
	ca-certificates \
	git \
	curl \
    libfreetype6-dev \
    vim \
    wget \
    sudo 

ARG GIT_NAME=git_name
ARG GIT_EMAIL=git_email

RUN git config --global user.name "${GIT_NAME}" \
 && git config --global user.email "${GIT_EMAIL}"

#RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
# && php -r "if (hash_file('SHA384', 'composer-setup.php') === '55d6ead61b29c7bdee5cccfb50076874187bd9f21f65d8991d46ec5cc90518f447387fb9f76ebae1fbbacf329e583e30') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
# && php composer-setup.php \
# && php -r "unlink('composer-setup.php');" \
# && mv composer.phar /usr/local/bin/composer

COPY composer /usr/local/bin/


RUN echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bashrc \
 && . ~/.bashrc \
 && composer config -g repo.packagist composer https://packagist.phpcomposer.com
 

# redis
ENV REDIS_VERSION 3.2.8
ENV REDIS_DOWNLOAD_URL http://download.redis.io/releases/redis-$REDIS_VERSION.tar.gz

RUN wget -O redis.tar.gz "$REDIS_DOWNLOAD_URL" \
 && mkdir -p /usr/src/redis \
 && tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1 \
 && rm redis.tar.gz \
 && make -C /usr/src/redis \
 && make -C /usr/src/redis install \
 && rm -r /usr/src/redis \
 && echo 'alias redis-cli="redis-cli -h redis"' >> ~/.bashrc \
 && . ~/.bashrc


#RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
# && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
# && apt-get update \
# && apt-get install -y \ 
#	--no-install-recommends \
#	yarn \
# && yarn config set registry 'https://registry.npm.taobao.org' 

RUN usermod -u 1000 -s /bin/bash -G sudo,www-data -d /home/www-data www-data \
 && mkdir /home/www-data \
 && chown -R www-data:www-data /home/www-data

USER www-data

RUN echo 'alias redis-cli="redis-cli -h redis"' >> ~/.bashrc \
 && . ~/.bashrc \
 && git config --global user.name "${GIT_NAME}" \
 && git config --global user.email "${GIT_EMAIL}"

WORKDIR /var/www/
