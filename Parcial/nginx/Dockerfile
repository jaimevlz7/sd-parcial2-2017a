#Se usa el contenedor con nginx pre instalado
FROM nginx

#Se elimina el archivo de configuración default y su carpeta

RUN rm /etc/nginx/conf.d/default.conf && rm -r /etc/nginx/conf.d

#Se agrega el archivo de configuracion de nginx

ADD nginx.conf /etc/nginx/nginx.conf

#Se agrega esta linea para que el contenedor no termine su ejecucion.

RUN echo "daemon off;" >> /etc/nginx/nginx.conf

CMD service nginx start
