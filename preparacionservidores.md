# Preparación del servidor

## Preparando el directorio

Para poner en funcionamiento k0s, se va a montar un servidor web con una página web bastante simple, que solamente consta de varios enlaces a otras páginas webs creadas por mí y a las webs oficiales de k0s y clounding.  

Para ello se va a proceder a instalar el servidor apache (temporalmente) y cargaremos en su directorio nuestra página web. Podemos cargar los archivos directamente a través del comando scp o para mayor comodidad, ya que contamos con un entorno gráfico y son varios los archvivos que tenemos que mover, a través de un programa de transferencia de archvivos; en este caso WinSCP.  

<center>

![WinSCP](https://github.com/Mbonillac/k0s/blob/main/imagenes/Winscp-40.png?raw=true)

</center>

Una vez que tenemos cargada la pagina web, pasaremos a deshabilitar el servidor apached de la sigueiente manera:  

* Paramos el servicio.
~~~
root@debian209-1:~# systemctl stop apache2.service
~~~

* Deshabilitamos el arranque en el inicio del sistema.
~~~
root@debian209-1:~# systemctl disable apache2.service
Synchronizing state of apache2.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install disable apache2
~~~

* Comprobamos que el servicio se encuentra parado y deshabilitado.
~~~
root@debian209-1:~# systemctl status apache2.service
● apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; disabled; vendor preset: enabled)
     Active: inactive (dead) since Tue 2021-12-07 14:05:22 CET; 10s ago
       Docs: https://httpd.apache.org/docs/2.4/
   Main PID: 121601 (code=exited, status=0/SUCCESS)
        CPU: 520ms

Dec 07 10:48:06 debian209-1 systemd[1]: Starting The Apache HTTP Server...
Dec 07 10:48:06 debian209-1 apachectl[121600]: AH00557: apache2: apr_sockaddr_info_get() failed for debian209-1
Dec 07 10:48:06 debian209-1 apachectl[121600]: AH00558: apache2: Could not reliably determine the server's fully qualif>Dec 07 10:48:06 debian209-1 systemd[1]: Started The Apache HTTP Server.
Dec 07 14:05:22 debian209-1 systemd[1]: Stopping The Apache HTTP Server...
Dec 07 14:05:22 debian209-1 apachectl[122471]: AH00557: apache2: apr_sockaddr_info_get() failed for debian209-1
Dec 07 14:05:22 debian209-1 apachectl[122471]: AH00558: apache2: Could not reliably determine the server's fully qualif>Dec 07 14:05:22 debian209-1 systemd[1]: apache2.service: Succeeded.
Dec 07 14:05:22 debian209-1 systemd[1]: Stopped The Apache HTTP Server.
lines 1-16/16 (END)
~~~  

Ya está el servidor preparado para poder instalar k0s.