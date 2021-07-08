FROM mysql:lastest #tên baseimage

## danh sách các biến môi trường
ENV MYSQL_ROOT_PASSWORD root
## tên database
ENV MYSQL_DATABASE huuvuot 
ENV MYSQL_USER huuvuot
ENV MYSQL_PASSWORD huuvuot
...........

# thêm file sql vào thư mục init của mysql
ADD path_to_file.sql /docker-entrypoint-initdb.d

## set port truy cập
EXPOSE 3307

## run script build
docker build -t name_image .
docker run --name name_container -p 3307:3307 -d name_image

![tham khảo](https://viblo.asia/p/tim-hieu-ve-dockerfile-va-tao-docker-image-V3m5WWag5O7)

```Dockerfile
FROM mysql:latest
ENV MYSQL_ROOT_PASSWORD root
# tên database
ENV MYSQL_DATABASE huuvuot 
ENV MYSQL_USER huuvuot
ENV MYSQL_PASSWORD huuvuot
# thêm file sql vào cơ sở dữ liệu
ADD animal.sql /docker-entrypoint-initdb.d
#set port cho cổng truy cập
EXPOSE 3307
```
