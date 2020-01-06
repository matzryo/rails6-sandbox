FROM mariadb:10.2 as base

# mysqlクライアントで日本語を入力/表示可能にする
RUN apt-get update && \
    apt-get install -y locales && \
    rm -rf /var/lib/apt/lists/* && \
    echo "ja_JP.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen ja_JP.UTF-8
ENV LC_ALL ja_JP.UTF-8
COPY ./charset.cnf /etc/mysql/conf.d/
# タイムゾーンを設定
RUN echo "Asia/Tokyo" > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

FROM base as dev
# サンプルデータ
# https://hub.docker.com/_/mariadb#initializing-a-fresh-instance
# COPY ./schema.sql /docker-entrypoint-initdb.d/schema.sql