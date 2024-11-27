- [Tarea 3](#tarea-3)
  - [Copiar el .war al contenedor](#copiar-el-war-al-contenedor)
  - [Acceder a la aplicacion](#acceder-a-la-aplicacion)
  - [Docker Inspect](#docker-inspect)

## Tarea 3
### Copiar el .war al contenedor
> [!TIP]
> Copiar el .war al contenedor

Comando:
```bash
docker cp /home/alumno/Descargas/sample.war tomcat-server:/usr/local/tomcat/webapps/
```
Salida:
```bash
Successfully copied 6.66kB to tomcat-server:/usr/local/tomcat/webapps/
```

### Acceder a la aplicacion
Accedemos a http://localhost:9090/sample

Y se muestra la pagina del .war descargado satisfactoriamente

### Docker Inspect
> [!TIP]
> muestra informacion detallada del contenedor

Comando:
```bash
docker inspect tomcat-server
```
Salida:
```bash
...
"IPAddress": "172.17.0.2"
...
```