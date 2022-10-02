# PostgreSQL環境構築

## 概要

dockerを使って環境構築をします

## Dockerfileの準備

```Dockerfile
FROM postgres:latest

ENV POSTGRES_PASSWORD postgres

RUN apt-get update && \
    apt-get clean language-pack-ja  && \
    rm -fr /var/lib/apt/lists/*

# Time Zone
ENV TZ Asia/Tokyo

# Language
RUN localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG="ja_JP.UTF-8" \
    LANGUAGE="ja_JP:ja" \
    LC_ALL="ja_JP.UTF-8"
```

## docker-compose.ymlの用意

```yml
version: '3'
services:
  pgsql:
    build:
      context: .
      dockerfile: Dockerfile
    container_name: pgsql
    tty: true
    volumes:
      - ./db:/var/lib/postgresql/data
    ports:
      - '25432:5432'
```

## ビルド

```docker-compose build```

## コンテナの起動

```docker-compose up -d```

## コンテナに入る

```docker exec -u postgres -it pgsql bash```

## クライアントの起動

```psql```

## 参考

[【PostgreSQLをインストール】Dockerを使って15分以内に作成する！ | Study Infra](https://study-infra.com/postgresql-install-docker/)
