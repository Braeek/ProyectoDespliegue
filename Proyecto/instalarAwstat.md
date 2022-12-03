# Despliegue de aplicaciones web
## AWSTAT
### Para empezar, vamos a intarlar el paquete awstast
#### sudo apt-get install awstats
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/7%20-%20Instalar%20awstat/Captura%20de%20pantalla%20(113).png)

### Habilitamos modulo CGI de Apache teniendo asi que reinciar apache para guardar los cambios
#### sudo a2enmod cgi
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/7%20-%20Instalar%20awstat/Captura%20de%20pantalla%20(136).png)


### Luego, creamos el archivo de configuracion para nuestro dominio y asi poder ver las estadisticas
#### sudo cp /etc/awstats/awstats.conf /etc/awstats/awstats.centro.intranet.conf

### Ahora modificaremos el archivo de configuracion para establecer el nombre del dominio
#### sudo nano /etc/awstats/awstats.centro.intranet.conf
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/7%20-%20Instalar%20awstat/Captura%20de%20pantalla%20(115).png)

### Ponemos en 1 este parametro para ver las estadisticas y guardamos
#### AllowToUpdateStatsFromBrowser=1
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/7%20-%20Instalar%20awstat/Captura%20de%20pantalla%20(116).png)

### Generamos las estadisticas inciales con el comando:
#### sudo /usr/lib/cgi-bin/awstats.pl -config=centro.intranet -update
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/7%20-%20Instalar%20awstat/Captura%20de%20pantalla%20(117).png)


### Vemos las estadisticas
#### ![Image](https://github.com/Braeek/ProyectoDespliegue/blob/main/Proyecto/Proyecto/7%20-%20Instalar%20awstat/Captura%20de%20pantalla%20(118).png)
