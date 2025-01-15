# Wordpress
Au debut j'ai commence par creer un space de travail ```Workspace, un dossier v1 et le fichier docker-compose.yml``` ensuite,
j'ai mis ce code dans le docker-compose.yml
```python
version: '2'
services:
  db:
    # We use a mariadb image which supports both amd64 & arm64 architecture
    image: mariadb:10.6.4-focal
    # If you really want to use MySQL, uncomment the following line
    # image: mysql:8.0.27
    command: '--default-authentication-plugin=mysql_native_password'
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=somewordpress
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=wordpress
    expose:
      - "3306"
      - "33060"
  wordpress:
    image: wordpress:latest
    volumes:
      - wp_data:/var/www/html
    ports:
      - "80:80"
    restart: always
    environment:
      - WORDPRESS_DB_HOST=db
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=wordpress
      - WORDPRESS_DB_NAME=wordpress
volumes:
  db_data:
  wp_data:
```

# requierment
docker
## docker
sudo apt update 
j'ai mis à jour les packets 

sudo apt upgrade 

Pour voir la version du docker installer 
```bash
sudo docker --version
```
Pour ajouter l'utilisateur au groupe Docker j'ai utilise la commande 
```bash
sudo usermod -aG docker $USER
```
Pour applique les changement j'ai reboot ma machine 
```bash
reboot
```
POur lancer docker 
```
docker-compose up -d
```