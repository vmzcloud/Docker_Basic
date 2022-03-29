# Docker 基本

![Blue Whale](blue_whale.png)

---

[找有用的映像檔](#找有用的映像檔)

[下載 docker image](#下載-docker-image)

[查看已經下載的 Docker Image](#查看已經下載的-docker-image)

[啟動一個 Docker Container](#啟動一個-docker-container)

[查看啟動過的 Container 清單](#查看啟動過的-container-清單)

[停用和啟動 Container](#停用和啟動-container)

[移除 Container](#移除-container)

[刪掉不用的 Docker Image](#刪掉不用的-docker-image)

[查看 Container 資訊](#查看-container-資訊)

[將檔案搬進 Container](#將檔案搬進-container)

- [把檔案複製到 Container 裡](#將檔案搬進-container)
- [把檔案從 Container 複製出來](#把檔案從-container-複製出來)

[外掛 Container 的儲存空間](#外掛-container-的儲存空間)

[直接執行 Container 內的程式或指令](#直接執行-container-內的程式或指令)

[讓 Container 在執行結束後自動移除](#讓-container-在執行結束後自動移除)

[Container 自動重新啟動](#container-自動重新啟動)

[進入 Container 操作命令列](#進入-container-操作命令列)

[Container 綁定指定 IP address](#container-綁定指定-ip-address)

---

## 找有用的映像檔

    docker serach [軟體名稱]

### Example

    docker search nginx

## 下載 docker image

    docker pull <Docker Image 名稱>

### Example

    docker pull nginx
    docker pull httpd

## 查看已經下載的 Docker Image

    docker images

## 啟動一個 Docker Container

    -d : Detach 背後執行

    docker run -p [對外的埠號]:[預設的埠號] -d <Docker Image 名稱>

### Example

    docker run -p 8080:80 -d nginx

## 查看啟動過的 Container 清單

    docker ps -a

## 停用和啟動 Container

    docker start <Container ID>

    docker stop <Container ID>

## 移除 Container

    docker rm <Container ID>

## 刪掉不用的 Docker Image

    docker rmi <Image 名稱或 ID>

## 查看 Container 資訊

    docker inspect <Container ID 或名稱>

## 將檔案搬進 Container

### 把檔案複製到 Container 裡

    docker cp <檔案來源 Container ID 或名稱>:<檔案名稱與完整路徑> <完整目的資料夾路徑>

### 把檔案從 Container 複製出來

    docker cp <檔案來源檔案名稱與完整路徑> <目的 Container ID 或名稱>:<完整目的資料夾路徑>

### Example

    docker cp index.html nginx-cp:/usr/share/nginx/html

## 外掛 Container 的儲存空間

    docker run -v <外部資料夾或檔案的完整路徑>:<Container 內部要被取代的資料夾完整路徑或檔案名稱> -p <對外的埠號>:<預設的埠號> -d <Docker Image 名稱>

### Example

將 container 內的 /usr/share/nginx/html 資料夾改以主機 /var/www 取代

*如果主機上沒有 /var/www 資料夾存在時，docker run 會自動新增主機資料夾

    docker run -v /var/www:/usr/sahre/nginx/html --name nginx01 -p 80:80 -d nginx

主機上 /home/vmzcloud/nginx.conf 取代預設的 nginx.conf

    docker run -v /home/vmzcloud/nginx.conf:/etc/nginx/nginx.conf -v /var/www:/usr/share/nginx/html --name nginx02 -p 80:80 -d nginx

## 直接執行 Container 內的程式或指令

    docker run <Docker Image 名稱> <指令>

### Example

    docker run ubuntu /bin/ls

把 Windows 上某個資料夾用 ls 顯示出來

    docker run -v C:\downloads:/home ubuntu /bin/ls -l /home

## 讓 Container 在執行結束後自動移除

    docker run --rm unbuntu /bin/ls -l /home

## Container 自動重新啟動

    docker run --restart=always nginx

只是需要 Container 自動重新啟動，而不需要在電腦開機自動啟動

    docker run --restart=unless-stopped nginx

Container 非正常退出時，才會重啟 Container

    docker run --restart=failure nginx

Container 非正常退出時重啟，最多重啟3次

    docker run --restart=on-failure:3 nginx

## 進入 Container 操作命令列

    docker run -it --rm -name testing-nginx nginx /bin/bash

## Container 綁定指定 IP address

    docker run -p 192.168.5.1:80:80 -d nginx