- [Tarea 2](#tarea-2)
  - [Paso 1: Preparación del Entorno](#paso-1-preparación-del-entorno)
  - [Paso 2: Descargar la Imagen de Tomcat](#paso-2-descargar-la-imagen-de-tomcat)
  - [Paso 3: Ejecutar el Contenedor de Tomcat](#paso-3-ejecutar-el-contenedor-de-tomcat)
  - [Paso 4: Probar la Configuración](#paso-4-probar-la-configuración)
  - [Paso 5: Detener y Eliminar el Contenedor](#paso-5-detener-y-eliminar-el-contenedor)

## Tarea 2
### Paso 1: Preparación del Entorno
> [!TIP]
> Comprobar instalacion de docker

Comando:
```bash
docker --version
```
Salida:
```bash
Docker version 24.0.7, build 24.0.7-0ubuntu2~20.04.1
```
### Paso 2: Descargar la Imagen de Tomcat
> [!TIP]
> Descargar la imagen oficial de tomcat

Comando:
```bash
docker pull tomcat
```
Salida:
```bash
Using default tag: latest
latest: Pulling from library/tomcat
afad30e59d72: Pull complete 
918d361e6529: Pull complete 
cf4dd2a7e40b: Pull complete 
d152af7a0148: Pull complete 
a5d7958ebd69: Pull complete 
409b41a58ed4: Pull complete 
4f4fb700ef54: Pull complete 
9eabaa92f491: Pull complete 
Digest: sha256:2ade2b0a424a446601688adc36c4dc568dfe5198f75c99c93352c412186ba3c9
Status: Downloaded newer image for tomcat:latest
docker.io/library/tomcat:latest
```
> [!TIP]
> Confirmar que se descargo la imagen

Comando:
```bash
docker images
```
Salida:
```bash
jonaykb/plantas-image                   latest    8412397cd30d   2 minutes ago   1.43GB
<none>                                  <none>    02524777fdb6   5 minutes ago   1.43GB
<none>                                  <none>    64f9b95d9500   6 minutes ago   1.43GB
jonaykb/plantas-image                   <none>    64aa572b17b9   3 hours ago     1.4GB
<none>                                  <none>    c52a85a2f468   3 hours ago     1.31GB
<none>                                  <none>    f14d316046e0   3 hours ago     1.31GB
jonaykb/plantas-nginx-webserver-image   latest    84a41403bd42   21 hours ago    236MB
php                                     8.1-fpm   903aebaf073b   6 days ago      492MB
composer                                latest    9e3f4c1ff4e1   9 days ago      202MB
tomcat                                  latest    f77539e7e45f   2 weeks ago     467MB
mysql                                   8.3.0     6f343283ab56   8 months ago    632MB
hello-world                             latest    d2c94e258dcb   19 months ago   13.3kB
```

### Paso 3: Ejecutar el Contenedor de Tomcat
> [!TIP]
> Ejecutar la imagen de tomcat

Comando:
```bash
  docker run -d -p 9090:8080 --name tomcat-server tomcat
```
Salida:
```bash
6b4f6846c0533b6929be0eff5f320f4cbbc0b87369b06f17fb1eb8d135fb770d
```

> [!TIP]
> Comprobar su ejecucion

Comando:
```bash
docker ps
```

Resultado:
```bash
CONTAINER ID   IMAGE     COMMAND             CREATED          STATUS          PORTS                                       NAMES
6b4f6846c053   tomcat    "catalina.sh run"   33 minutes ago   Up 33 minutes   0.0.0.0:9090->8080/tcp, :::9090->8080/tcp   tomcat-server
```

### Paso 4: Probar la Configuración
Acceder a http://localhost:9090

Y efectivamente nos da el error 404 

> [!TIP]
> Mirar logs

Comando:
```bash
docker logs tomcat-server
```

Resultado:
```bash
27-Nov-2024 21:39:21.786 INFO [main] org.apache.catalina.startup.Catalina.start Server startup in [189] milliseconds
```

> [!TIP]
> Ver si el puerto esta ocupado

Comando:
```bash
lsof -i :9090
```

Resultado:
```bash

```
### Paso 5: Detener y Eliminar el Contenedor
> [!TIP]
> Detener contenedor

Comando:
```bash
docker stop tomcat-server
```

Resultado:
```bash
tomcat-server
```
Esto signifca que se ha parado correctamente
> [!TIP]
> Eliminar el contenedor

Comando:
```bash
docker stop tomcat-server
```

Resultado:
```bash
tomcat-server
```
Esto signifca que se ha eliminado
 correctamente
