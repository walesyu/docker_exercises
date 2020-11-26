其他使用範例
---

## tomcat
- 啟動服務
```docker
docker run -it --rm --name tomcat -p 8888:8080 -v %cd%/jsp_sample:/usr/local/tomcat/webapps/hello -d tomcat  
```
- 確認服務狀態
```
http://localhost:8888/hello/index.jsp
```

## mariadb
- 開啟mariadb並設定密碼
```docker
docker run --name mariadb --rm -p 3306:3306 -e MYSQL_ROOT_PASSWORD=1234 -d mariadb
```
- 連進去mariadb
```docker
docker exec -it mariadb mysql -uroot -p1234
```