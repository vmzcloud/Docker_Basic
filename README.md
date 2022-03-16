# Docker Basic

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