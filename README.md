# SistemasDistribuidos_P2

#### Nombre Estudiante: Jaime Vélez Escandón
#### Código Estudiante: A00268524
#### Repositorio: https://github.com/jaimevlz7/sd-parcial2-2017a

### Descripción
Aprovisionamiento	de	un	ambiente	compuesto	por	los	siguientes	elementos:	un servidor	encargado de	realizar balanceo de	carga,	tres	servidores	web	con páginas estáticas. Se	debe probar	el	funcionamiento	del balanceador	realizando peticiones y mostrando servidores distintos atendiendo las peticiones.

<p align="center">
  <img src="images/01_diagrama_despliegue.png" width="650"/>
</p>

### Actividades
En un documento en formato PDF cuyo nombre de
archivo debe ser examen2_codigoestudiante.pdf debe incluir lo siguiente:

1. Documento en formato PDF:  
  * Formato PDF (5%)
  * Nombre y código de los integrantes del grupo (5%)
  * Ortografía y redacción (5%)
2. Consigne los comandos de linux necesarios para el aprovisionamiento de los servicios solicitados. En este punto no debe incluir archivos tipo Dockerfile solo se requiere que usted identifique los comandos o acciones que debe automatizar (15%)
3. Escriba los archivos Dockerfile para cada uno de los servicios solicitados junto con los archivos fuente necesarios. Tenga en cuenta consultar buenas prácticas para la elaboración de archivos Dockerfile. (20%)
4. Escriba el archivo docker-compose.yml necesario para el despliegue de la infraestructura (10%)
5. Publicar en un repositorio de github los archivos para el aprovisionamiento junto con un archivo de extensión .md donde explique brevemente como realizar el aprovisionamiento (15%)
6. Incluya evidencias que muestran el funcionamiento de lo solicitado (15%)
7. Documente algunos de los problemas encontrados y las acciones efectuadas para su solución al aprovisionar la infraestructura y aplicaciones (10%)


### Desarrollo

Inicialmente para el desarrollo del parcial:

1. Configuración de las imagenes.

Se instalaron las imagenes extraidas de docker hub, httpd y nginx (Imagenes ya preconfiguradas y modificadas para funcionar correctamente) teniendo en cuenta que con estas imagenes se podia cumplir el objetivo del parcial.

2. Configuración de la aplicación web.

Primero se define un formato para la pagina web que se va a desplegar, en este caso la misma pagina web (cambiando solo el ID de web a WEB 1, WEB 2 o WEB 3, según sea el caso) para cada web de la solución (web1, web2 y web3) de la siguiente manera:
```
<!DOCTYPE html>
<html >
<head> 
Prueba de balanceador de carga Nginx
</head>
<body>
<h1>Prueba de balanceador de carga Nginx</h1>			
<p>WEB 1</p>  
</body>
</html>
```
Y su correspondiente Dockerfile:
```
FROM httpd
ADD index.html /usr/local/apache2/htdocs/index.html
```
Dockerfile en el que se especifica la imagen y el archivo a guardar en la dirección de apache para desplegar el "index.html"

3. Configuración del nginx.


4. Configuración de Docker Compose.
```
version: '2'
 
services:
  app1:
    build:
      context:  ./app1
      dockerfile: Dockerfile
    expose:
      - "5000"
    volumes:
      - data_web:/data_web

  app2:
    build:
      context:  ./app2
      dockerfile: Dockerfile
    expose:
      - "5000"
    volumes:
      - data_web:/data_web

  app3:
    build:
      context:  ./app3
      dockerfile: Dockerfile
    expose:
      - "5000"
    volumes:
      - data_web:/data_web
  
  proxy:
    build:
      context:  ./nginx
      dockerfile: Dockerfile
    ports:
      - "8080:80"
    links:
      - app1
      - app2
      - app3
    volumes:
      - data_nginx:/data_nginx
volumes:
   data_web:
   data_nginx:
   ```
   


