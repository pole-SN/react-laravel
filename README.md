# 概要
フロントエンドをReact、バックエンドをLaravelを用いたAPIサーバーで開発環境を構築するための基礎パッケージ。  

## 起動
本プロジェクトをクローン後、以下を実行してください。

```
# ビルド
docker-compose build または
docker-compose build --no-cache

# コンテナ起動
docker-compose up -d

# ビルドと起動を一気にやる場合
docker-compose up -d --build

# Laravelのvendorフォルダ生成
docker-compose exec laravel composer install

# コンテナ停止
docker-compose down
```

## アクセス
```
React - フロントページ
http://localhost

Laravel - バックページ
http://localhost/api/

Laravel - タスク一覧取得API
http://localhost/api/tasks
```

## データベースマイグレーション
```
1. モデルの作成（ここではTaskというサンプルモデルを指定）
php artisan make:model -a Task

2. カラムの追加などを行う。
/app-laravel-backend/database/migrations配下に作成されるcreate_tableファイルを編集

3. マイグレート
docker-compose exec laravel php artisan migrate
→localhost:1234でmyadmin等に入り、2までに追加したテーブルが作成されていることを確認

4. XxxFactory.phpでサンプルデータ定義
TaskFactory.phpなどを参考にする

5. XxxSeeder.phpでファクトリーを使って作成するデータを定義
TaskSeeder.phpなどを参考にする

6. docker-compose exec laravel php artisan db:seed
→localhost:1234でmyadmin等に入り、テーブルにデータがあることを確認
```

## メモ
```
# reactプロジェクトの作成（Typescript含む）
npx create-react-app app-react-frontend --template typescript

# Laravelプロジェクトの作成
composer create-project laravel/laravel app-laravel-backend
```
