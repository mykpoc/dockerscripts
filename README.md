# dockerscripts
Sample scripts used for deployment of docker containers

For Projectsend

**Main container**
docker create \
  --name=projectsend \
  -e TZ=Kuala_Lumpur \
  -e MAX_UPLOAD=5000 \
  -p 80:80 \
  -v /var/lib/projectsend/config:/config \
  -v /var/lib/projectsend/data:/data \
  --restart unless-stopped \
  linuxserver/projectsend
  
  
**Database container**  
  docker create \
  --name=mariadb \
  -e MYSQL_ROOT_PASSWORD=P@ssw0rd \
  -e TZ=Kuala_Lumpur\
  -e MYSQL_DATABASE=projectsend \
  -e MYSQL_USER=projectsenduser \
  -e MYSQL_PASSWORD=P@ssw0rd \
  -p 3306:3306 \
  -v /var/lib/mysql/config:/config \
  --restart unless-stopped \
  linuxserver/mariadb
  
If database container is created in same host, then use the internal docker network IP to connect. Additionally, go to the docker console of mariadb container and edit mysql.cnf and uncomment #binding of 127.0.0.1
(Hint: find the file location using find . -name mysql.cnf

During set up for projectsend at http://<your-ip>/install/make-config.php connect to mariadb docker network (i.e 172.17.0.3 etc.) and not localhost
