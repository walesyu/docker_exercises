關於docker image的基礎指令
---

## 目的 
了解docker image的基本操作

## docker image的特性
 - 我們可以試著將docker image當作是用來開機的live cd，每個docker image都會預先安裝好一些可以執行的軟體讓我們直接使用。
 - 使用者還可以利用某個image為基礎，使用Dockerfile這個檔案建立屬於自己的image。
   例如我們可以使用ubuntu的image為基礎，自由地加上nginx, mysql等軟體，並編譯出一個符合自己需求的影像檔。
 - 編譯好的docker image是唯讀的
 
Usage:  docker image COMMAND

## 常用指令 

### 查看本地的docker images
- 執行
```docker
docker image ls
```
- 顯示結果
```console
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
hello-world         latest              bf756fb1ae65        9 months ago        13.3kB
```
- 欄位說明
  - REPOSITORY: 這個image在repo上的名稱，預設我們會把docker hub當作repo的位置，所以當我們輸入https://hub.docker.com/_/hello-world 就可以看到這個image的詳細資料
  - TAG: 用來標示不同的版本的記號
  - IMAGE ID: image建立後自動產生的號碼，可以明確標示本地image的惟一值
  - CREATED: 該image建立的時間
  - SIZE: 檔案大小
  
### 從遠端repo拉取image
以openjdk為例，我們先瀏覽https://hub.docker.com/_/openjdk?tab=tags 看看有那些版本可以使用，例如我們要jdk11版
- 執行
```docker
docker pull openjdk:11.0.8-jre
```
- 下載中
```console
11.0.8-jre: Pulling from library/openjdk
e4c3d3e4f7b0: Downloading [===========>                                       ]  11.76MB/50.4MB
101c41d0463b: Download complete
8275efcd805f: Downloading [====================================>              ]  7.248MB/9.996MB
556bd89391a7: Downloading [================>                                  ]  1.862MB/5.529MB
91f5d9af427a: Waiting
2f8c930462b0: Waiting
```
- 下載完成
```
11.0.8-jre: Pulling from library/openjdk
e4c3d3e4f7b0: Pull complete
101c41d0463b: Pull complete
8275efcd805f: Pull complete
556bd89391a7: Pull complete
91f5d9af427a: Pull complete
2f8c930462b0: Pull complete
Digest: sha256:be26422ad6972c49b65242b66defa0d1e3690c52f3fb9d1f90500668c1e464de
Status: Downloaded newer image for openjdk:11.0.8-jre
docker.io/library/openjdk:11.0.8-jre
```
- 確認一下本地的images
```docker
docker image ls
```
```console
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
openjdk             11.0.8-jre          270be31528bf        8 days ago          285MB
hello-world         latest              bf756fb1ae65        9 months ago        13.3kB
```

### 刪除docker images
用法為 docker image rm << REPOSITORY >>:<< Tag >>

或是

docker image rm << IMAGE ID >>

- 執行
```docker
docker image rm openjdk:11.0.8-jre
docker image rm 270be31528bf
```
- 顯示結果
```console
Untagged: openjdk:11.0.8-jre
Untagged: openjdk@sha256:be26422ad6972c49b65242b66defa0d1e3690c52f3fb9d1f90500668c1e464de
Deleted: sha256:270be31528bf42b60705dc219c2f800a773baeb33dcb71f47992fa01a1520b73
Deleted: sha256:df794dfc45b3fd060d34514a27035a5d84db3e608f02dfd67e19d79fef5c2247
Deleted: sha256:23eb8fb9a110719c3c90da42d271f1d2f203a59099ffdda5bae2c5c5d12593f1
Deleted: sha256:5174d08097f02c081d00a5e0351bda2d2ced823e1447775300c77d0b5d45762e
Deleted: sha256:4bb57adf9037e4da45f2dbc0f84a7e9d8da6847bef3e63d09c8a9d8465f4d2c6
Deleted: sha256:5173011923d00f0fe606ecceda93ea88f17dc77e0b026df802c9aeb31bc1eac6
Deleted: sha256:9780f6d83e45878749497a6297ed9906c19ee0cc48cc88dc63827564bb8768fd```
