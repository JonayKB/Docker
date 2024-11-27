# Docker PGL
- [Docker PGL](#docker-pgl)
  - [Tarea 1](#tarea-1)
    - [Paso 1: Trabajar con imágenes de Docker](#paso-1-trabajar-con-imágenes-de-docker)
    - [Paso 2: Administrar contenedores de Docker](#paso-2-administrar-contenedores-de-docker)

## Tarea 1
### Paso 1: Trabajar con imágenes de Docker
>[!TIP]
> Activar la imagen hello-world
Comando:
```bash
  sudo docker run hello-world
```
Resultado:
```bash
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
### Paso 2: Administrar contenedores de Docker
>[!TIP]
> Obtener activos
Comando:
```bash
sudo docker ps
```
Resultado:
```bash
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```
>[!TIP]
> Obtener todos
Comando:
```bash
docker ps -a
```
Resultado:
```bash
CONTAINER ID   IMAGE                                   COMMAND                  CREATED          STATUS                       PORTS     NAMES
a0e91e763726   hello-world                             "/hello"                 3 minutes ago    Exited (0) 3 minutes ago               silly_bouman
51d1db520893   jonaykb/plantas-nginx-webserver-image   "/docker-entrypoint.…"   11 minutes ago   Exited (0) 7 minutes ago               plantas-nginx-webserver
ef64aa3eaf08   jonaykb/plantas-image                   "docker-php-entrypoi…"   2 hours ago      Exited (137) 6 minutes ago             plantas-container
e5ad15e80766   c52a85a2f468                            "/bin/sh -c 'php /va…"   2 hours ago      Exited (1) 2 hours ago                 sad_bouman
d2ec5bd2d12c   f14d316046e0                            "/bin/sh -c 'php /va…"   2 hours ago      Exited (1) 2 hours ago                 compassionate_noyce
39a6ae6d54e7   mysql:8.3.0                             "docker-entrypoint.s…"   2 hours ago      Exited (0) 6 minutes ago               plantas-mysql-container
```
>[!TIP]
> Obtener ultimo creado
Comando:
```bash
sudo docker ps -l
```
Resultado:
```bash
CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
a0e91e763726   hello-world   "/hello"   8 minutes ago   Exited (0) 8 minutes ago             silly_bouman
```

>[!TIP]
> Obtener imagenes
Comando:
```bash
sudo docker images
```
Resultado:
```bash
REPOSITORY                              TAG       IMAGE ID       CREATED         SIZE
jonaykb/plantas-image                   latest    64aa572b17b9   2 hours ago     1.4GB
<none>                                  <none>    c52a85a2f468   2 hours ago     1.31GB
<none>                                  <none>    f14d316046e0   2 hours ago     1.31GB
jonaykb/plantas-nginx-webserver-image   latest    84a41403bd42   20 hours ago    236MB
php                                     8.1-fpm   903aebaf073b   6 days ago      492MB
composer                                latest    9e3f4c1ff4e1   9 days ago      202MB
mysql                                   8.3.0     6f343283ab56   8 months ago    632MB
hello-world                             latest    d2c94e258dcb   19 months ago   13.3kB
```