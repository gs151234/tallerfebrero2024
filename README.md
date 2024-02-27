# Obligatorio Taller de Servidores Linux 2024

Trabajo obligatorio para la materia de taller de Linux 2024.

Este proyecto abarca la utilización de la herramienta Ansible para la actualización de paquetes del sistema operativo e instalación y configuración de aplicaciones web y servicios de proxy para distribuciones de las familias RedHat y Debian. 

## Requisitos previos

*Servidor como Bastión donde instalar Ansible y ejecutar los playbooks.

*Instalar Ansible [core 2.15.3e] 

*Instalar git [en este caso utilizamos la versión 2.39.3]
para clonar el repositorio.

## Ansible-Playbooks

Aclaración: el archivo "/inventories/hosts" contiene el listado de hosts con los que se van a trabajar, esto está sujeto a cambios según cada empresa/usuario. Es importante ingresar y editar el archivo con los los hosts de su propia red.

Playbooks:

-	initial_config.yml

o	Copiar la clave para conectarse por SSH y deshabilitar el acceso por ssh de Root y quitar login por password.

o	Se realiza la creación del usuario Ansible, se copia la clave y se deja con permisos SUDO sin password.

-	hosts_updates.yml

o	Se conecta con el usuario Ansible y ejecuta las actualizaciones de los SO con reinicio al final de la tarea.

-	web_ servers.yml

o	instala las aplicaciones OpenJDK11 y Apache-tomcat-8.5.73 con las configuraciones correspondientes. Se utiliza un template que crea el servicio tomcat.service para iniciar el servicio. Se habilita en el firewall el puerto 8080/tcp para la conexión con el proxy.

-	reverse_proxy.yml

o	Instala Apache2, habilita los módulos proxy y proxy_http. Utiliza desde templates el archivo para ka configuración del virtualhost. Activa el sitio. Activa y configura el firewall, en este caso UFW, habilitando los puertos 22, 80 y 443.





## USO

Instalar Ansible

En este caso se realizó desde una distribución con Rocky Linux
```
$ sudo dnf install ansible
```
Clonar el repositorio desde GitHub y validamos accediendo a la carpeta.

```
$ git clone git@github.com:gs151234/tallerfebrero2024.git
```
Validamos accediendo y listando los archivos
```
$ cd /tallerfebrero2024

$ ll
```
Nos debería devolver el siguiente listado
```

[sysadmin@bastion tallerfebrero2024]$ ll
total 56
-rw-rw-r--. 1 sysadmin sysadmin   514 Feb 26 20:21 hosts_updates.yml
-rw-rw-r--. 1 sysadmin sysadmin  1367 Feb 26 19:51 initial_config.yml
drwxrwxr-x. 2 sysadmin sysadmin    19 Feb 25 20:15 inventories
-rw-rw-r--. 1 sysadmin sysadmin 35149 Feb 25 19:50 LICENSE
-rw-rw-r--. 1 sysadmin sysadmin    55 Feb 25 19:50 README.md
-rw-rw-r--. 1 sysadmin sysadmin  1336 Feb 25 20:10 reverse_proxy.yml
drwxrwxr-x. 2 sysadmin sysadmin    58 Feb 25 20:20 templates
-rw-rw-r--. 1 sysadmin sysadmin  1848 Feb 25 20:09 web_servers.yml

```

Comenzamos con la ejecución de Playbooks con la configuración inicial

```
$ ansible-playbook -i inventories/hosts initial_config.yml
```

Seguimos por las updates
```
$ ansible-playbook -i inventories/hosts hosts_updates.yml
```
En este punto no hay orden definido. 

En este caso ejecutamos la instalación y configuración del web server
```
$ ansible-playbook -i inventories/hosts web_sever.yml
```
Finalizamos con el proxy
```
$ ansible-playbook -i inventories/hosts reverse_proxy.yml
```
## Documentación de la implementación



## Autores

Nombres: 

  - Diego Vazquez 

  - Giovanni Storti

Universidad ORT 
