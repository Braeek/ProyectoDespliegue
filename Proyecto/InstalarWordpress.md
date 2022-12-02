# Despliegue de aplicaciones web
## Wordpress
### Para comenzar, iniciamos sesión en la cuenta root de MySQ y creamos la base de datos para WordPress:
### Introducimos:
#### mysql -u root -p
#### CREATE DATABASE wordpress DEFAULT CHARACTER SET utf8 COLLATE utf8_unicode_ci;
### Creamos un usuario con una contraseña: CREATE USER 'wordpressuser'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/3%20-%20Instalar%20wordpress/Captura%20de%20pantalla%20(100).png)

### Instalación de extensiones de PHP adicionales:
#### apt update
#### sudo apt install php-curl php-gd php-mbstring php-xml php-xmlrpc php-soap php-intl php-zip
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/3%20-%20Instalar%20wordpress/Captura%20de%20pantalla%20(101).png)


### Descargamos Wordpress en nuestra maquina virtual con:
#### cd /tmp
#### curl -O https://wordpress.org/latest.tar.gz
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/3%20-%20Instalar%20wordpress/Captura%20de%20pantalla%20(102).png)

### Descomprimimos el archivo:
#### tar xzvf latest.tar.gz
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/3%20-%20Instalar%20wordpress/Captura%20de%20pantalla%20(129).png)

### Moveremos estos archivos a nuestro root de documentos por ahora. Antes de hacerlo, podemos añadir un archivo ficticio .htaccess de modo que esté disponible para que WordPress lo use más adelante.
#### touch /tmp/wordpress/.htaccess
#### cp /tmp/wordpress/wp-config-sample.php /tmp/wordpress/wp-config.php
#### sudo cp -a /tmp/wordpress/. /var/www/wordpress
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/3%20-%20Instalar%20wordpress/Captura%20de%20pantalla%20(130).png)


### Mas adelante actualizamos la propiedad con el comando chown que nos permite modificar la propiedad del archivo
#### sudo chown -R www-data:www-data /var/www/wordpress
### Ejecutaremos dos comandos find:
#### sudo find /var/www/wordpress/ -type d -exec chmod 750 {} \;
#### sudo find /var/www/wordpress/ -type f -exec chmod 640 {} \;
### Tras esto, obtenemos los valores seguros del generador de claves secretas de WordPress:
#### curl -s https://api.wordpress.org/secret-key/1.1/salt/
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/3%20-%20Instalar%20wordpress/Captura%20de%20pantalla%20(131).png)


### A continuación, abra el archivo de configuración de WordPress:
#### sudo nano /var/www/wordpress/wp-config.php
### Estando aqui, copiamos las lineas de codigo que sacamos anteriormente con:
#### curl -s https://api.wordpress.org/secret-key/1.1/salt/ y las pegamos sustituyendolas por las que ya estan. Ademas, de añadir otros cambios que se muestran en la imagen como "define('FS_METHOD', 'direct');"
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/3%20-%20Instalar%20wordpress/Captura%20de%20pantalla%20(132).png)

### Finalmente, asignamos el dominio al directorio de instalación de Worpress 
#### nano /etc/apache2/sites-available/000-default.conf
### dentro del directorio, pegamos:
<VirtualHost*:80>
  ServerName centro.intranet
  ServerAlias www.centro.intranet
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/wordpress
  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/3%20-%20Instalar%20wordpress/Captura%20de%20pantalla%20(107).png)
