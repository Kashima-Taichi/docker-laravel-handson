# FROM命令は、以降の命令で使用するベースイメージの設定　必須
FROM php:7.3-fpm-alpine

# LABEL命令はイメージにメタデータを追加。キーとバリューのペア。
LABEL maintainer "Taichi-Kashima"

# 構築時に作業者がdocker buildで使う変数、フラグを定義
ARG TZ

# ENVは環境変数キーとバリューのセット
# 1を設定するとrootでのインストールを許可できる
ENV COMPOSER_ALLOW_SUPERUSER 1
ENV COMPOSER_HOME /composer

RUN set -eux && \
    apk add --update-cache --no-cache --virtual=.build-dependencies tzdata && \
    cp /usr/share/zoneinfo/${TZ} /etc/localtime && \
    apk del .build-dependencies && \
    docker-php-ext-install bcmath pdo_mysql && \
    curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer && \
    composer config -g repos.packagist composer https://packagist.jp && \
    composer global require hirak/prestissimo