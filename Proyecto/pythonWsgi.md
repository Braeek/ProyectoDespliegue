# Despliegue de aplicaciones web
## WSGI
### Ahora activaremos el módulo “wsgi”
### Primero hacemos la descarga:
#### sudo apt install libapache2-mod-wsgi-py3
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/4%20-%20activar%20wsgi/Captura%20de%20pantalla%20(108).png)

### Tras esto, creamos el archivo y le introducimos el codigo python
#### sudo nano /var/www/html/archivo.py
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/4%20-%20activar%20wsgi/Captura%20de%20pantalla%20(109).png)


### Establecemos los permisos al archivo que hemos creado anteriormente
#### sudo chown www-data:www-data /var/www/html/archivo.py
#### sudo chmod 775 /var/www/html/archivo.py
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/4%20-%20activar%20wsgi/Captura%20de%20pantalla%20(110).png)

### Finalmente, vinculamos el dominio con el directorio entrado en:

#### sudo nano /etc/apache2/sites-available/000-default.conf
### y añadimos esta linea de codigo
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/4%20-%20activar%20wsgi/Captura%20de%20pantalla%20(121).png)
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/4%20-%20activar%20wsgi/Captura%20de%20pantalla%20(121).png)
