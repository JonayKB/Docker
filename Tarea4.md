- [Tarea 4](#tarea-4)

## Tarea 4
### Descargar e iniciar un contenedor MariaDB
Comando:
```bash
docker run --name mariadb-container -e MYSQL_ROOT_PASSWORD=admin -e MYSQL_DATABASE=exampledb -p 3306:3306 -d mariadb:latest
```
Respuesta:
```bash
910e92fadf39e086482f72a4e6b5abd98ce5da6e0b9c6b9b16b93f7a8570cda3
```
### Descargar y ejecutar CloudBeaver en Docker
Comando:
```bash
docker run -d --name cloudbeaver -p 8978:8978 dbeaver/cloudbeaver:latest
```
Respuesta:
```bash
Digest: sha256:be0b0b8e16a5ba5abbeec3dc18e2bb18e1d2f6bb04135e32faace799a78b17c4
Status: Downloaded newer image for dbeaver/cloudbeaver:latest
6718b5fcb6123a35bb170dfff8ee87b68ec71bc82e63986fff4e93d883b66a17
```

Contenedores desplegados actualmente:
```bash
CONTAINER ID   IMAGE                        COMMAND                  CREATED          STATUS         PORTS                                       NAMES
6718b5fcb612   dbeaver/cloudbeaver:latest   "./run-server.sh"        10 seconds ago   Up 8 seconds   0.0.0.0:8978->8978/tcp, :::8978->8978/tcp   cloudbeaver
910e92fadf39   mariadb:latest               "docker-entrypoint.s…"   2 minutes ago    Up 2 minutes   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp   mariadb-container
```

### Acceder a la interfaz de CloudBeaver
Accedemos a http://localhost:8978

