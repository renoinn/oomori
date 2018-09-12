---
title: "Laradockで開発環境をセットアップ"
date: 2018-09-12T16:49:39+09:00
draft: true
---

Laradockを使ってLaravelの開発環境を作ったので、備忘録。

まずは適当にディレクトリを作って、laradockをgithubからcloneする。

```
$ mkdir sample_project
$ cd sample_project
$ git clone https://github.com/LaraDock/laradock.git
$ cd laradock
$ cp env-example .env
```

laradockの設定は.envで行うので、サンプルをコピーして.envファイルを作成する。ほぼそのまま使えるお手軽さ。
.envを作ったら必要なコンテナを起動する。

```
$ docker-compose up -d nginx mysql redis workspace
```

これでdocker環境はOKなので、次にworkspaceにlaravelプロジェクトを作成する。

```
$ docker-compose exec workspace bash
# composer create-project laravel/laravel app
# exit
```

laradockと同じディレクトリにappディレクトリができてるはずなので、appディレクトリがマウントされるようにlaradockの.envを修正する。

```
$ docker-compose stop
$ vim .env

APP_CODE_PATH_HOST=../app/ <-- APP_CODE_PATH_HOSTの値を.envから見たappディレクトリの相対パスに修正する
```

修正したらコンテナ再起動。

```
$ docker-compose up -d nginx mysql redis workspace
```

[http://localhost/](http://localhost/)にアクセスしたらLaravelのトップページが表示される。
