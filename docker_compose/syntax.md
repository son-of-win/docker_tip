# file docker-compose.yml đc viết theo cú pháp của YMAL

version: "3"  # chọn viết phiên bản của docker file

services:   # khai báo các container nằm trong services

    mydb:  # dịch vụ thứ nhất
        image: "ubuntu:latest"  # tên image base của dịch vụ
        container_name: "huuvuot"  # tên container khi chạy
        build:  # sử dụng Dockerfile để build
            content: .
            dockerfile: path_to_dockerfile

        networks:
            - tên network driver
        ports:
            - "8080:80" # cổng 8080 trên host được ánh xạ vào cổng 80 trên container
        volumes: # ánh xạ các thư mục trên host vào container
            - /mycode/db:/var/lib/sql # ánh xạ thư mục "/mycode/db" vào thư mục "/var/lib/sql" trên container
            - dir-site:/home/sites/
        enviroment: # các biến môi trường cho container
            MYSQL_ROOT_PASSWORD: root
            .....


# build container bằng docker-compose
docker-compose up -d

# example
```yaml
version: '3.7'
services:
  mysql_01:
    image: mysql:5.7
    build : .
#    command: mysqld --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci --default-authentication-plugin=mysql_native_password
    restart: always

    env_file:
      - .env
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    volumes:
      - ./volumes/mysql:/var/lib/mysql
    ports:
      - '3307:3306'
```