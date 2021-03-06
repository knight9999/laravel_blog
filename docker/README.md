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
$ docker run --privileged -p 8022:22 -p 8080:80 -v `pwd`/..:/home/laravel/work/blog -it ubuntu_with_laravel_blog
```

laravelユーザーが自動的に作られます。
またローカルの親ディレクトリ(..)が、Dockerのlaravelユーザーのworkディレクトリにマウントされます。

git管理などは、ローカルのworkから行うことにします。

### Remark

curlでcomposerがうまくインストールできていない場合があるので、その時は、

```
# curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
```

を手動で実行します。

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

1. ホストPCから、workディレクトリに、Laravel Projectをcloneします(本プロジェクトは、すでにcloneしているので不要)
1. 次に、ゲストPCでlaravelユーザーになり、`$ composer install`を実行します。
1. Apacheの000-default.confの設定で、Document Rootの設定を適時修正します。
1. .env.exampleをコピーして、.envにします。そして、API_KEYに値を設定します。
  API_KEYの値は

  ```
    $ php artisan key:generate
  ```

  で生成した値を使います。


### Restart

次のコマンドを実行します。

```
# service apache2 restart
```




### Other Reference

http://blog.yucchiy.com/2015/01/16/dockerized-laravel5/
