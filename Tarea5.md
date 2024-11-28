- [Tarea 5](#tarea-5)
  - [Redes disponibles](#redes-disponibles)
  - [Crear una red y levantar los servidores](#crear-una-red-y-levantar-los-servidores)
  - [Fichero de configuracion del Balanceador y su arranque](#fichero-de-configuracion-del-balanceador-y-su-arranque)

## Tarea 5
### Redes disponibles
> [!TIP] 
> Ver las redes disponibles

Comando:
```bash
docker network ls
```

Resultado:
```bash
NETWORK ID     NAME                             DRIVER    SCOPE
5562f073bd75   bridge                           bridge    local
3da72d9b2271   cuidadoplantas_plantas-network   bridge    local
6cdf8f23cc17   host                             host      local
0053e6430ab4   none                             null      local
```

### Crear una red y levantar los servidores
Comandos:
```bash
docker network create tomcat-network
docker run -d --name tomcat1 --network tomcat-network -p 8081:8080 tomcat:latest
docker run -d --name tomcat2 --network tomcat-network -p 8081:8080 tomcat:latest
```

Salida:
```bash
9b9b996a7d7ff5b0e1b00fd001a9b812ee5f9d5630ba13c9d72ee8f28af109ac

aaf116137e14ad065f081bb516868eb66676d26058240d50b5116b1e2b84b4a8

4f4d49662cc273af4b9cd3086f02c6d196e28e8139502898c48350f0c43bb9ff
```

> [!TIP]
> Ver los contenedores activos

Comando:
```bash
docker ps
```

Resultado:
```bash
CONTAINER ID   IMAGE           COMMAND             CREATED              STATUS              PORTS                                       NAMES
4f4d49662cc2   tomcat:latest   "catalina.sh run"   About a minute ago   Up About a minute   0.0.0.0:8082->8080/tcp, :::8082->8080/tcp   tomcat2
aaf116137e14   tomcat:latest   "catalina.sh run"   About a minute ago   Up About a minute   0.0.0.0:8081->8080/tcp, :::8081->8080/tcp   tomcat1
```

### Fichero de configuracion del Balanceador y su arranque
Fichero:
```bash
events {}

http {
    upstream tomcat_backend {
        server tomcat1:8080;
        server tomcat2:8080;
    }

    server {
        listen 80;

        location / {
            proxy_pass http://tomcat_backend;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }
    }
}
```
> [!TIP]
> Ejecuta el balenceador
Comando:
```bash
docker run -d --name nginx --network tomcat-network -p 81:80 -v $(pwd)/nginx.conf:/etc/nginx/nginx.conf nginx:latest
```

Respuesta:
```bash
53b1f228dabf174d1d618d28229afb344cdc534280a74ba1520e51e4771da532
```

> [!TIP]
> Explicacion:
> 
Si entramos a http://localhost:8081:
Iremos diractamente a ese tomcat

Si entramos a http://localhost:8082:
Iremos diractamente a ese tomcat

Si entramos a http://localhost:81:
Nginx eligira a que tomcat mandar la solicitud