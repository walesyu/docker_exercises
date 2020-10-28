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