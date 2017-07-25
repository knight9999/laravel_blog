# docker_ubuntu_with_laravel_blog

## Usage

### Create image

git cloneして、そのディレクトリに移動してから、以下を実行して、Dockerイメージを作成します。

```
$ docker build -t ubuntu_with_laravel_blog .
```

### Run Containter

以下のコマンドで、Dockerコンテナを起動します。

```
$ docker run --privileged -p 8022:22 -p 8080:80 -v `pwd`/..:/home/laravel/work/ -it ubuntu_with_laravel_blog
```

laravelユーザーが自動的に作られます。
またローカルのworkディレクトリが、Dockerのlaravelユーザーのworkディレクトリにマウントされます。

git管理などは、ローカルのworkから行うことにします。

### Laravel

Dockerコンテナにログインしたら、以下でlaravelユーザーになります。(アプリは、すべてlaravelユーザーのworkディレクトリ以下に作成してゆきます)

```
$ su - laravel
```

### First Time

#### Install laravel installer & Create Laravel Project


1. インストーラのインストール
    ```
    $ composer global require "laravel/installer"
    ```
1. Laravel Installerがインストールできたら、laravelコマンドでプロジェクトを作成します。
    ```
    $ cd work
    $ laravel new blog
    ```
1. storageディレクトリとbootstrap/cacheディレクトリに、読み書き権限を与えます。

1. Apacheの000-default.confの設定で、Document Rootの設定を適時修正します。


### Second Time

1. ホストPCから、workディレクトリに、Laravel Projectをclonseします
1. 次に、ゲストPCでlaravelユーザーになり、`$ composer install`を実行します。
1. Apacheの000-default.confの設定で、Document Rootの設定を適時修正します。
1. .env.exampleをコピーして、.envにします。そして、API_KEYに値を設定します。
  API_KEYの値は

  ```
    $ php artisan key:generate
  ```

  で生成した値を使います。




### Other Reference

http://blog.yucchiy.com/2015/01/16/dockerized-laravel5/
