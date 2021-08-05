MYSQLで何度やってもできなかったのでMariaDBでやりました。

https://www.petitmonte.com/ruby/mariadb_rails.html の通りに実行しました

localhost:3000にアクセスしてブロックされていたのですが　エラー画面に行くようにはなりました


sudo /etc/init.d/start mysql #MariaDB起動

sudo apt update && sudo apt upgrade openssl

sudo apt update && sudo apt upgrade opens

---------------------------------------------------------------

mysql -u root -p
 
// ユーザーの作成
CREATE USER 'ユーザー名' IDENTIFIED BY 'パスワード';
 
// データベースの作成
CREATE DATABASE MyApp_development;
 
// ユーザーにデータベース(MyApp_development)の権限を付与する
GRANT ALL PRIVILEGES ON MyApp_development.* TO 'ユーザー名';
 
 
// --- 関連するコマンド
// データベースの一覧
SHOW DATABASES;
// テーブルの一覧
SHOW TABLES;
// ユーザーの一覧を表示する
SELECT host, user, password FROM mysql.user;
// ユーザーの削除
DROP USER ユーザー名;
// データベースの削除
DROP DATABASE データベース名; 

-----------------------------------------------------------------

// カレントディレクトリの移動
cd /mnt/d/任意のディレクトリ
※Cドライブは/mnt/c、Dドライブは/mnt/d
 
// プロジェクトの生成
rails new MyApp -d mysql
 
// MyApp/config/database.ymlの編集
// ---
development:
  <<: *default
  database: MyApp_development
  username: ユーザー名
  password: パスワード
// ---
 
cd /mnt/d/任意のディレクトリ/MyApp
 
// モデルの作成(モデル/マイグレーションファイルの生成)
bin/rails g model Task name:string description:text
 
// マイグレーションの実行(テーブルの生成)
bin/rails db:migrate
 
// コントローラーの作成(コントローラー/ビューの生成)
bin/rails g controller tasks index show new edit
 
// Pumaサーバの起動
bin/rails s
