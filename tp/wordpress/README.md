# WordPress
In order to deploy a *wordpress* application, we should:
- create 1 network
- create 2 volumes
  - 1 for mysql
  - 1 for wordpress
- launch the *mysql* container
- launch the *wordpress* container


## Docker Deployment
### Network Creation
- `docker network create wordpress`
- `docker network list`

### Volume Creation
- `docker volume create mysql`
- `docker volume create wordpress`
- `docker volume list`

### WordPress Image Download
- `docker image pull wordpress`
- `docker image inspect wordpress:latest`

### MySql Image Download
- `docker image pull mysql`
- `docker image inspect mysql:5.7`

### Launch the Container MySql
- `docker run --name wordpressdb -d --rm \
--net wordpress \
-v mysql:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=P@ssw0rd \
-e MYSQL_DATABASE=wordpress \
mysql:5.7`

### Launch the Container Wordpress
- `docker run --name wordpress -d --rm \
--net wordpress -p 8090:80 --link wordpressdb:mysql \
-e WORDPRESS_DB_PASSWORD=P@ssw0rd \
wordpress:4.9.6`

### Check
- `http://localhost:8090` through a browser


## docker-compose Deployment
- `docker-compose up`