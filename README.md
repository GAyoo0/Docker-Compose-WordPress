# Docker-Compose-WordPress

## 设置WordPress

在主文件夹中创建一个新的目录my_wordpress，并使用cd进入：

```
mkdir ~/my_wordpress/
cd ~/my_wordpress/
```


在此文件夹中创建名为docker-compose.yml的文件并添加以下内容
在WORDPRESS_DB_PASSWORD、MYSQL_ROOT_PASSWORD和MYSQL_PASSWORD环境选择设置您自己的密码
WORDPRESS_DB_PASSWORD和MYSQL_PASSWORD的密码应该是相同的

docker-compose.yml

```
version: '3.3'
​
services:
wordpress:
  depends_on:
 - db
  image: wordpress:latest
  volumes:
 - wordpress_files:/var/www/html
  ports:
 - "80:80"
  restart: always
  environment:
 WORDPRESS_DB_HOST: db:3306
 WORDPRESS_DB_USER: wordpress
 WORDPRESS_DB_PASSWORD: my_wordpress_db_password
​
db:
  image: mysql:5.7
  volumes:
 - db_data:/var/lib/mysql
  restart: always
  environment:
 MYSQL_ROOT_PASSWORD: my_db_root_password
 MYSQL_DATABASE: wordpress
 MYSQL_USER: wordpress
 MYSQL_PASSWORD: my_wordpress_db_password
volumes:
 wordpress_files:
 db_data:
```

从my_wordpress目录中启动Docker容器：

```
docker-compose up -d
```

