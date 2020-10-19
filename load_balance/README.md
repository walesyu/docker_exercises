利用docker實現load balancer
---
## 目的 
利用兩個以上的docker container交互使用，製作最基本的web load balancer服務
## 使用方式 
- build image
```docker
docker-compose build
```
- 啟動服務
```docker
docker-compose up -d
```
- 確認服務狀態
```docker
docker container ls -a
```

- 讀取docker啟動訊息
```docker
docker-compose logs
```
- 停止服務
```docker
docker-compose down
```
