使用docker來執行命令與交談式互動
---

## 目的 
了解如何使用docker來執行工作

## 指令說明 

### docker run
docker run是用來執行並啟動container的指令，我們也可以利用一些參數來與container互動

Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

#### 常用參數
- -v 將本地的目錄分享給container，用法為: -v <<本地目錄>>:<<container目錄>>
- -p 指定container要暴露的port，用法為: -p <<本地埠號>>:<<container埠號>>，以http port 80為例:
  - -p 80: 如果直接帶數字會將container曝露的埠號直接對外，使用 http://localhost 就可以存取container的服務，
  - -p 8080:80: 如果想要有不同的對應則使用冒號隔開外部與內部的埠號，網址就要改成 http://localhost:8080 才能存取
- --rm 當container結束後自動刪除container
- -ti 這個參數是由-i -t組成的，可以提供一個tty讓使用者可以和container互動，輸入即時指令
- -d 在背景執行container
- 執行
```docker
docker run -it --rm -p 8888:8080 -v D:\projects\jsp_sample:/usr/local/tomcat/webapps/hello -d tomcat  
```
- 顯示結果
```console
ccd96c8f77304139fa65aade2ed2a81bbe6013140241e05e905421ad192a79d5
```
docker回傳這個container的SHA Id

### docker exec
當container已經在執行的時候，利用這個指令可以跟container進行互動

Usage:  docker exec [OPTIONS] CONTAINER COMMAND [ARG...]
#### 常用參數
- -ti 這個參數是由-i -t組成的，可以提供一個tty讓使用者可以和container互動，輸入即時指令
- -e 設定環境變數

- 執行
```docker
docker exec -ti ccd96c8f77304139fa65aade2ed2a81bbe6013140241e05e905421ad192a79d5 /bin/bash
```
- 顯示結果
```console
root@ccd96c8f7730:/usr/local/tomcat#
```
這樣就會進入container的bash，並可以進行操作