#sample_Rails_new  

#version  
Ruby 2.7.0   
Rails 6.0.2.1  
MySQL 8.0  　

#手順

1.　5つのファイルをローカルの作業ディレクトリにコピーし、ターミナルで作業ディレクトリまで移動する  

2.　コマンドを実行　→　docker-compose run web bundle exec rails new . --force --database=mysql  

3.　コマンドを実行　→　docker-compose build  

4.　config/database.yml のhostの部分を localhost　から　db　に書き換える  

5.　コマンドを実行　→　docker-compose build  

6.　mysqlの認証方式を変更する  

7.　コマンドを実行　→　docker-compose exec db bash  

8.　コマンドを実行　→　mysql -u root  

9.　コマンドを実行　→　select User,Host,plugin from mysql.user;  

+------------------+-----------+-----------------------+  
| User             | Host      | plugin                |  
+------------------+-----------+-----------------------+  
| root             | %         | caching_sha2_password |　←ここを変更する  
| mysql.infoschema | localhost | caching_sha2_password |  
| mysql.session    | localhost | caching_sha2_password |  
| mysql.sys        | localhost | caching_sha2_password |  
| root             | localhost | caching_sha2_password |  
+------------------+-----------+-----------------------+  

10.　コマンドを実行　→　ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '';  

11.　コマンドを実行　→　select User,Host,plugin from mysql.user;  

+------------------+-----------+-----------------------+  
| User             | Host      | plugin                |  
+------------------+-----------+-----------------------+  
| root             | %         | mysql_native_password |　←ここが変更されていることを変更する  
| mysql.infoschema | localhost | caching_sha2_password |  
| mysql.session    | localhost | caching_sha2_password |  
| mysql.sys        | localhost | caching_sha2_password |  
| root             | localhost | caching_sha2_password |  
+------------------+-----------+-----------------------+  

12.　control + p + q でSQLコマンドを抜ける  

13.　コマンドを実行　→　docker-compose exec web bundle exec rails db:prepare  

14.  コマンドを実行　→　docker-compose up -d  

15.　ブラウザでlocalhost:3000と入力し、Yay! You’re on Rails!の画面が表示される  
