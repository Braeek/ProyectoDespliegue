# Despliegue de aplicaciones web
## Servidor
### El servidor que he decidido usar para tenemos como 2 servidor fue Nginx, asi que primero lo instalaremos
### Introducimos:
#### sudo apt install nginx
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/8%20-%202%20serv/Captura%20de%20pantalla%20(122).png)

### Descargamos y extraemos phpMyAdmin e instalamos los paquetes de php necesarios
#### sudo wget https://files.phpmyadmin.net/phpMyAdmin/5.2.0/phpMyAdmin-5.2.0-all-languages.tar.gz
sudo tar -zxvf phpMyAdmin-5.2.0-all-languages.tar.gz
#### sudo apt install -y php-fpm php-mysql php-json php-mbstring php-xml
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/8%20-%202%20serv/Captura%20de%20pantalla%20(123).png)

### Lo movemos hasta la carpeta que necesitamos
#### sudo mv phpMyAdmin-5.2.0-all-languages /var/www/phpmyadmin

### Tambien movemos la plantilla de configuracion cambiandole tambien el nombre
#### sudo mv /var/www/phpmyadmin/config.sample.inc.php /var/www/phpmyadmin/config.inc.php


### Ahora generaremos un codigo con "sudo pwgen -s 32 1" y lo copiaremos para pegarlo en la siguiente direccion:
#### sudo nano /var/www/phpmyadmin/config.inc.php
### Ademas del codigo, tambien insertamos otras lineas de codigo importantes
#### $cfg['Servers'][$i]['controlhost'] = 'localhost';
$cfg['Servers'][$i]['controlport'] = '';
$cfg['Servers'][$i]['controluser'] = 'pmauser';
$cfg['Servers'][$i]['controlpass'] = 'mypmapass';
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/8%20-%202%20serv/Captura%20de%20pantalla%20(137).png)

### Tras haber guardado cambios, tenemos que relacionar MySQL con phpMyAdmin de la siguiente forma:
#### sudo mysql < /var/www/phpmyadmin/sql/create_tables.sql -u root -p

### Acto seguido, creamos la configuracion de servidor para phpMyAdmin en Nginx insertando estas lineas de codigo:
#### sudo nano /etc/nginx/sites-available/phpmyadmin.conf
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/8%20-%202%20serv/Captura%20de%20pantalla%20(138).png)


### Al guardar cambios, crearemos una carpeta temporal para phpMyAdmin y cambiaremos los permisos
#### sudo mkdir /var/www/phpmyadmin/tmp
#### sudo chmod 777 /var/www/phpmyadmin/tmp

### Establecemos la propiedad del directorio agregando a su vez el dominio
#### sudo chown -R www-data:www-data /var/www/phpmyadmin
#### sudo nano /etc/hosts
### Insertamos tambien 127.0.0.1 servidor2.centro.intranet
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/8%20-%202%20serv/Captura%20de%20pantalla%20(139).png)

### Finalmente, reiniciamos Nginx junto a php
#### sudo systemctl restart nginx php8.1-fpm
