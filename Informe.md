# dhcpgrupo4

Lo primero que hicimos para crear este laboratorio fue instalar la imagen de dhcp en kathara siguiendo esta guia
https://github.com/KatharaFramework/Docker-Images

Con el protocolo dhcp instalado procedimos a crear la infra estructura del laboratorio siguiendo la topologia dada
Para esto, creamos las carpetas que corresponderan a cada elemento del laboratorio con el comando

mkdir pc1 pc2 pc3 pc4 r1 sv1

con el comando touch crearemos sus .startups y el archivo lab.conf en donde configuraremos las conexiones de cada pc

en los startups de cada pc configuramos para que se ejecutamos un reinicio del servicio de network, una ruta por defecto y que se realiza una llamada a la direccion
10.0.0.2 www.google.com

Dentro de los directorios de cada pc, creamos la carpeta /etc/ y dentro de ella creamos /network/, dentro de esta ultima carpeta creamos y configuramos el archivo interfaces
en donde colocamos los comandos:

auto eth0 
iface eth0 inet dhcp

Estos realizaran la configuracion de la ip de la pc gracias al protocolo dhcp

Por el otro lado dentro del startup del router realizamos las configuraciones de ip y iniciamos el protocolo dhcp con el comando
service isc-dhcp-server start

seguimos con configurar el archivo isc-dhcp-server dentro de la carpeta /r1/etc/default/, dentro de este escribiremos los comandos
INTERFACESv4="eth0"
INTERFACESv6=""
estos causan que cuando se inicie el protocolo dhcp dentro del laboratorio, enlaze las interfaces ipv4 a los puertos eth0

Tambien configuramos el archivo dhcp.conf dentro del directorio /r1/etc/dhcp/dhcpd.conf, en este configuraremos los rangos de las ips que otorga el protocolo al laboratorio
