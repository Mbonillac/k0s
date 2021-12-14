# Preparación del servidor

Para poner en funcionamiento k0s, se va a montar un servidor web con una página web bastante simple, que solamente consta de un título. Esta página web ha sido modificada desde dentro del propio pod.


## Preparando el servidor

<center>

![servido-k0s](https://github.com/Mbonillac/k0s/blob/main/imagenes/Winscp-40.png?raw=true)

</center>


 ## Preparando el Pod  

Para lanzar un pod es necesario un archivo yaml que lo configure, este archivo deb erá ser cargado dentro del servidor para poder ser lanzado y ejecutado por kubectl.  
Para ello se ha utilizado la herramienta Winscp, tambien puede ser usado scp.  

<center>

![WinSCP-yaml](https://github.com/Mbonillac/k0s/blob/main/imagenes/Winscp-40.png?raw=true)

</center>


 ## Preparando el Archivo Yaml  

Para lanzar este pod se ha utilizado este archivo yaml, en el que se ha indicado que servidor web utilizar.   
Para saber el nombre de la imagen que el pod va a utilizar, hay que buscar en [dockerhub](https://hub.docker.com/search?type=image); que en este caso __Apache2__ es nombrado como **httpd**.  
Este archivo tiene como nombre apache2.yaml

 ~~~
 apiVersion: v1
kind: Pod
metadata:
 name: pod-apache2
 labels:
   app: apache2
   service: web
   autor: Manuel
spec:
 containers:
   - image: httpd
     name: contenedor-apache2
     imagePullPolicy: Always
 ~~~