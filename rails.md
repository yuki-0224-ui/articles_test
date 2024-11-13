## はじめに
どうも、yukiです。

この記事では既存のRailsプロジェクトをDocker化する手順をまとめてみました。

### Dockerfileの作成
今回は既存のイメージを使わないので、まずはプロジェクトに合わせたDockerfileを作成していきます。
私のプロジェクトの例だと以下のようになります。

**環境**
- Ruby: 3.2.2
- Rails: 7.0.6
- Postgres: 12

```Dockerfile
FROM ruby:3.2.2

RUN apt-get update && apt-get install -y build-essential \
    libpq-dev \
    nodejs \
    postgresql-client

WORKDIR /myapp

COPY Gemfile Gemfile.lock /myapp/

RUN bundle install
```
RailsはGemfileを見てバージョンを決定するので、Dockerfileにコピーしておきます。
Postgresのクライアントもインストールしておきます。


### docker-compose.ymlの作成

```docker-compose.yml
volumes:
  db-data:

services:
  web:
    build: .
    platform: linux/amd64
    command: >
      bash -c "rm -f tmp/pids/server.pid &&
               bundle exec rails server -b '0.0.0.0'"

    ports:
      - '3000:3000'
    environment:
      - 'DATABASE_PASSWORD=postgres'
    volumes:
      - .:/myapp
    tty: true
    stdin_open: true
    depends_on:
      - db
    links:
      - db
  db:
    image: postgres:12
    platform: linux/amd64
    volumes:
      - 'db-data:/var/lib/postgresql/data'
    environment:
      - 'POSTGRES_PASSWORD=postgres'
      - 'POSTGRES_USER=postgres'
```

mac m1チップ環境ではplatform: linux/amd64を指定しないとエラーが出ると聞きましたので、明示的に指定しました。

これを指定すると動作が重くなってしまうという話も耳に入りましたが、今回は目を瞑ります。

### start.shの作成
```bash
#!/bin/bash

docker compose build

docker-compose run --rm web rails db:prepare

docker-compose up
```
