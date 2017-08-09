# チュートリアル

## DB関連とModel

https://laravel.com/docs/5.4/database
https://laravel.com/docs/5.4/eloquent

###　DB作成

mysql上でblogデータベースを作成し
config/database.phpを

```
'mysql' => [
    'driver' => 'mysql',
    'host' => env('DB_HOST', '127.0.0.1'),
    'port' => env('DB_PORT', '3306'),
    'database' => env('DB_DATABASE', 'blog'),
    'username' => env('DB_USERNAME', 'root'),
    'password' => env('DB_PASSWORD', ''),
    'unix_socket' => env('DB_SOCKET', ''),
    'charset' => 'utf8mb4',
    'collation' => 'utf8mb4_unicode_ci',
    'prefix' => '',
    'strict' => true,
    'engine' => null,
],
```

とする。

### モデル作成

例えば、

```
$ php artisan make:model User -m
```

(すでにUserモデルはあるので、エラーになる)

### マイグレーションのみ

マイグレーションファイルと、テーブル名を指定

```
php artisan make:migration create_users_table --create=users
```

### マイグレーションの実行

```
php artisan migrate
```
