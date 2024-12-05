## Tarea 7

### Ejercio

#### Crear la red personalizada

Comando:
```bash
docker network create my_network
```

Respuesta:
```bash
b5c59e344c5470ca41f291dca152612692971e1f253ef70fe7460e62a639ae52
```

#### Crear volumen comun

Comando:
```bash
docker volume create my_db_volume
```

Respuesta:
```bash
my_db_volume
```

#### Crear el DockerFile

```docker
# Usar una imagen base de Ubuntu para las instalaciones adicionales
FROM ubuntu:20.04

# Instalar dependencias necesarias (como wget y curl)
RUN apt-get update -y && \
    apt-get install -y \
    wget \
    curl \
    unzip \
    mysql-client \
    && rm -rf /var/lib/apt/lists/*

# Configurar MariaDB usando la imagen oficial
FROM mariadb:10.5

# Configurar Tomcat usando la imagen oficial
FROM tomcat:9.0

# Descargar y configurar CloudBeaver utilizando la imagen oficial de CloudBeaver desde Docker Hub
FROM dbeaver/cloudbeaver:latest

# Exponer puertos
EXPOSE 8080 8081

# Volúmenes para MariaDB
VOLUME /var/lib/mysql

# Configuración de MariaDB: Establecer la contraseña root y crear la base de datos (esto es suficiente con las variables de entorno)
ENV MYSQL_ROOT_PASSWORD=root
ENV MYSQL_DATABASE=exampledb

# Iniciar los servicios de MariaDB, Tomcat y CloudBeaver
CMD service mysql start && \
    /opt/tomcat/bin/catalina.sh run & \
    /opt/cloudbeaver/cloudbeaver/bin/cloudbeaver & \
    wait
```

#### Consturir la imagen
Comando:
```bash
docker build -t tomcat-mariadb-cloudbeaver .
```

Respuesta:
```bash
DEPRECATED: The legacy builder is deprecated and will be removed in a future release.
            Install the buildx component to build images with BuildKit:
            https://docs.docker.com/go/buildx/

Sending build context to Docker daemon  4.608kB
Step 1/11 : FROM ubuntu:20.04
 ---> 6013ae1a63c2
Step 2/11 : RUN apt-get update -y &&     apt-get install -y     wget     curl     unzip     mysql-client     && rm -rf /var/lib/apt/lists/*
 ---> Using cache
 ---> f46bb6911cc6
Step 3/11 : FROM mariadb:10.5
 ---> 88680d56d3a9
Step 4/11 : EXPOSE 8081
 ---> Running in 717d95707472
Removing intermediate container 717d95707472
 ---> 032dfd3eff25
Step 5/11 : FROM tomcat:9.0
 ---> 22ad854e49dd
Step 6/11 : FROM dbeaver/cloudbeaver:latest
 ---> 9f27e55b1196
Step 7/11 : EXPOSE 8978
 ---> Running in 46340592e082
Removing intermediate container 46340592e082
 ---> d132767e41bc
Step 8/11 : VOLUME /var/lib/mysql
 ---> Running in 36e0623993e1
Removing intermediate container 36e0623993e1
 ---> 0b7f45ce10d2
Step 9/11 : ENV MYSQL_ROOT_PASSWORD=root
 ---> Running in 0a6822c79b0f
Removing intermediate container 0a6822c79b0f
 ---> b00dcb58aef4
Step 10/11 : ENV MYSQL_DATABASE=exampledb
 ---> Running in 9a6b02eeb1c0
Removing intermediate container 9a6b02eeb1c0
 ---> 776e2bf9aad7
Step 11/11 : CMD service mysql start &&     /opt/tomcat/bin/catalina.sh run &     /opt/cloudbeaver/cloudbeaver/bin/cloudbeaver &     wait
 ---> Running in 52f6122f566e
Removing intermediate container 52f6122f566e
 ---> a3e1424aad99
Successfully built a3e1424aad99
Successfully tagged tomcat-mariadb-cloudbeaver:latest
```

#### Ejecutar imagen

Comando:
```bash
docker run --name tarea7 -d -p 8978:8978 -p 8081:8081 tomcat-mariadb-cloudbeaver
```