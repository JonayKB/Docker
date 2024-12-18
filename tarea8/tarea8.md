## Tarea 8

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

#### Crear Docker-Compose

```yml
version: '3.3'
services:
  mariadb:
    image: mariadb:11.1.2
    container_name: mariadb
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: exampledb
    volumes:
      - mariadb_data:/var/lib/mysql
    ports:
      - "3307:3306"
    networks:
      - newNetwork
  mongodb:
    image: mongo:8.0.4
    container_name: mongodb
    volumes:
      - mongodb_data:/data/db
    ports:
      - "27017:27017"
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: root
    networks:
      - newNetwork

  tomcat:
    image: tomcat:10.1.9-jdk17
    container_name: tomcat
    ports:
      - "8090:8080"
    volumes:
      - ./sample.war:/usr/local/tomcat/webapps/sample.war
    depends_on:
      - mariadb
    networks:
      - newNetwork
  tomcat2:
    image: tomcat:10.1.9-jdk17
    container_name: tomcat2
    ports:
      - "8091:8081"
    volumes:
      - ./sample.war:/usr/local/tomcat/webapps/sample.war
    depends_on:
      - mariadb
    networks:
      - newNetwork

  cloudbeaver:
    image: dbeaver/cloudbeaver:latest
    container_name: cloudbeaver
    environment:
      DB_HOST: mariadb
      DB_PORT: 3307
      DB_USER: root
      DB_PASSWORD: root
      DB_NAME: exampledb
    ports:
      - "8978:8978"
    networks:
      - newNetwork
  mongo-express:
    image: mongo-express
    restart: always
    ports:
      - 8081:8081
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: admin123
      ME_CONFIG_MONGODB_URL: mongodb://root:root@mongodb:27017/
    depends_on:
      - mongodb
    networks:
      - newNetwork

volumes:
  mariadb_data:
  mongodb_data:
networks:
  newNetwork:
```
#### Prueba de que funciona
![MongoExpress](image.png)
![MariaDB](image-1.png)
