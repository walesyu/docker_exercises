hello world
---
## 目的 
確認docker安裝成功的第一個使用範例
## 使用方式 
### 直接執行docker run指令
- 執行
```docker
docker run hello-world
```
- 顯示結果
```console
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
### 也可以先拉image再執行
- 執行
```docker
docker pull hello-world
```
- 確認image已經拉下來了
```docker
docker image ls
```
- 顯示結果
```console
hello-world         latest              bf756fb1ae65        9 months ago        13.3kB
```
## 確認container是否已結束 
- 執行
```docker
docker container ls -a
```
- 顯示結果
```console
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
78a2e0394484        hello-world         "/hello"            10 minutes ago      Exited (0) 10 minutes ago                       reverent_goldwasser
```
**當沒有指定container名稱時，docker會自動以兩個單字加上"_"組成一個字串來當作container的臨時名稱**

