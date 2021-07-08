# file Dockerfile
### cùng thư mục với file sql và file sh
```Dockerfile
FROM mysql:latest
ADD myproj.sql /tmp/myproj.sql
ADD run.sh /tmp/run.sh
RUN /tmp/run.sh
```

# file sh
```sh
#!/bin/bash
/usr/bin/mysqld_safe --skip-grant-tables & sleep 5

mysql -u root -proot -e "CREATE DATABASE huuvuot"
mysql -u root -proot huuvuot < /tmp/myproj.sql
```