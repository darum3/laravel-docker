# laravel-docker

## 説明
Docker環境でLaravelプロジェクトを動かすベースプロジェクト

なるべくそれぞれのコンテナを小さくすることを目標とした

## 各種バージョン
PHPのバージョンは任意に指定可能
* Laravel6
* nginx 1.15
* MySQL 5.8 (開発用)

## 使い方

### サーバ環境

リバースプロキシ用のnginxが、`proxy_ext_network`という名前でネットワークを作成している前提で、
webのコンテナに接続できるようにしている。

* `.env`を作る
    * `cp .env.example .env`
    * PHP_VERSION を使用したいバージョンに設定する
* `docker-compose build`
* Laravelのセットアップ
    * `docker-compose run --rm composer i`
    * Laravelの`.env`を作る
        ```
        cd laravel
        cp .env.example .env
        cd ..
        ```
    * `docker-compose run --rm artisan key:generate`
    * 起動の確認
        * `docker-compose up -d`
        * `docker-compose ps` で、web, laravelのコンテナがupになっている
* JSのビルド
    * `docker-compose run --rm npm i`
    * `docker-compose run --rm npm run dev`

### ローカル環境

開発用のMySQLも立ち上がります

* `.env`を作る
    * `cp .env.example .env`
    * PHP_VERSION を使用したいバージョンに設定する
    * WEB_PORT, MYSQL_PORT を任意に設定する
* `./dev.sh build`
    * `dev.sh`内で、`docker-compose-dev.yml`も利用する形になっている
* Laravelのセットアップ
    * `./dev.sh run --rm composer i`
    * Laravelの`.env`を作る
        ```
        cd laravel
        cp .env.example .env
        cd ..
        ```
    * データベース接続の設定を以下にする
        ```
        DB_HOST=dev_mysql
        DB_PORT=3306
        DB_DATABASE=dev
        DB_USERNAME=root
        DB_PASSWORD=zaq123
        ```
    * `./dev.sh run --rm artisan key:generate`
    * 起動の確認
        * `./dev.sh up -d`
        * `./dev.sh ps` で、web, laravel, dev_mysql(MySQL) のコンテナがupになっている
        * ブラウザで、http://localhost:8000/ (8000は、.envで設定した値) にアクセスすると、Laravelのデフォルトページが表示される
        * mysql コマンドでMySQLに接続できる
    * LaravelとMySQL接続確認
        ```
        $ ./dev.sh run --rm laravel ./artisan migrate:install
        Migration table created successfully.
        ```
