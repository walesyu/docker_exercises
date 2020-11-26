關於docker container的基礎指令
---

## 目的 
了解docker container的基本操作

##docker container的特性
 - docker container是每個docker image執行時的個體，啟動時會執行docker image中設定的啟動指令
 - container關閉後不會自動刪除(除非另外指定--rm)，跟virtualbox關閉後不會刪除客層一樣
 - 在container裡執行的各種活動都不會影響啟動時使用的docker image，但可以利用docker container commit建立新的image

## 常用指令 
### 查看本地的docker container
- 執行
```docker
docker container ls
```
- 顯示結果
```console
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
```
如果已經被stop的container不會顯示在這個畫面，必須加上-a的參數
- 執行
```docker
docker container ls -a
```
- 顯示結果
```console
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
adda35cae1b5        busybox             "sh"                15 seconds ago      Exited (0) 4 seconds ago                       optimistic_goldstine
```
- 欄位說明
  - CONTAINER ID: container的sha id
  - IMAGE: 這個container使用的image名稱
  - COMMAND: 啟動container時使用的指令
  - CREATED: 該image建立的時間
  - STATUS: 目前container的狀態
  - PORTS: 該container暴露的埠號與對應
  - NAMES: docker隨機產生的container名稱
### 建立一個本地端的container
以alpine為例，這是一個非常精簡版的linux核心
- 執行alpine並以互動模式登入
```docker
docker run -ti alpine
```
- 如果本地端沒有這個image，docker會自動下載
```console
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
188c0c94c7c5: Pull complete
Digest: sha256:c0e9560cda118f9ec63ddefb4a173a2b2a0347082d7dff7dc14272e7841a5b5a
Status: Downloaded newer image for alpine:latest
/ #
```

### 關閉docker container
以alpine來說，由於該image的啟動命令是[/bin/sh]，所以只要打exit就可以關閉這個container，但一般的操作方式應該是用

docker container stop << CONTAINER ID >>

或是

docker container stop << CONTAINER NAME >>
```
docker container stop fcf4ffe1a045
```

### 將container中的操作變化重新commit為一個新的docker image
通常我們在container會做一些操作或變動檔案，利用這個方法可以將變更重新打包成一個新的image
- 執行
```docker
docker container commit fcf4ffe1a045 alpine:mine
```
再用image ls觀看結果，可以發現會多一個相同REPOSITORY但不同tag的image
```console
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
alpine              mine                e5135053d2c7        2 hours ago         5.57MB
alpine              latest              d6e46aa2470d        5 weeks ago         5.57MB
```

### 刪除docker container
用法為

docker container rm << CONTAINER ID >>

或是

docker container rm << CONTAINER NAME >>

- 執行
```docker
docker container rm fcf4ffe1a045
```