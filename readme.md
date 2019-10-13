Laradocを使ったEC Site 作成

作業ディレクトリ設定

```
 git clone https://github.com/Laradock/laradock.git
 cd laradoc
 cp env-example .env

 vim .env
- APP_CODE_PATH_HOST=../
+ APP_CODE_PATH_HOST=../ecsite

```

mysql認証方式の変更

認証方式の確認
```
show variables like 'default_authentication%';

```

laradoc のmysql→my.conf に以下の設定を書き加える 
```
[mysqld]
default_authentication_plugin=mysql_native_password
```

Laravel プロジェクトの作成

$ docker-compose exec workspace bash
$ composer create-project laravel/laravel .


MigrateFileの作成

$ php artisan make:migration “マイグレーションファイル名”

作成したmigratefileは以下の場所に保存される

$ database/migrations/

migratefileの例

```
 public function up()
    {
        Schema::create('cart_items', function (Blueprint $table) {
            $table->bigIncrements('id');
            $table->integer('user_id');
            $table->integer('item_id');
            $table->integer('quantity');
            $table->timestamps();
        });
    }
```

※ upファンクションの中身が実行される




migrateの実行

$ php artisan migrate 


※ artisan コマンド一覧

https://qiita.com/haxpig/items/4ae3ed9092d338c9666e




認証画面の作成

6.0系から、「php artisan make:auth」が使えなくなった。

larval 6系で詳しく書いてそうな本（まだ読んでない）

https://www.amazon.co.jp/dp/B07XZNJT6D


代わりのコマンドがこちら

$ composer require laravel/ui
$ php artisan migrate
$ php artisan ui vue  --auth
$ nom run dev (開発サーバの起動）


ログインとかも問題なく動作、あっけないくらいかんたん

gmailで開発用のメールアカウントを取得して、以下の情報を設定する

.env にgmailで取得したアプリパスワードを記載する

MAIL_DRIVER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=xxxxx@gmail.com
MAIL_PASSWORD=xxxxxxxxx
MAIL_ENCRYPTION=tls











