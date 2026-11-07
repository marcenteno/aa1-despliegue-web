# Fase 2. Despliegue de la aplicación con Docker Compose

## 1. Objetivo

El objetivo de esta fase es desplegar la aplicación MERN Todo de la Fase 1 mediante contenedores Docker, utilizando Docker Compose para iniciar todos los servicios necesarios con un único comando.

El despliegue se realiza en una segunda instancia EC2 de AWS, manteniendo independiente la infraestructura de la Fase 1.

## 2. Infraestructura utilizada

- **Proveedor:** AWS Academy.
- **Servicio:** Amazon EC2.
- **Sistema operativo:** Ubuntu 24.04.
- **Tipo de instancia:** t3.micro.
- **Dirección IP elástica:** 52.205.27.139.
- **Puerto de acceso a la aplicación:** 8080.
- **Contenedores:** frontend, backend y MongoDB.

La aplicación está disponible en:

http://52.205.27.139:8080

## 3. Estructura del proyecto

La carpeta de esta fase contiene los siguientes elementos:

- `Código/10-MERN-Todo/backend/`: código del backend y su Dockerfile.
- `Código/10-MERN-Todo/frontend/`: código del frontend y su Dockerfile.
- `docker-compose.yml`: configuración de los servicios y su comunicación.
- `evidencias/`: capturas de pantalla de las configuraciones y pruebas realizadas.

## 4. Tecnologías utilizadas

- **Docker:** creación y ejecución de contenedores.
- **Docker Compose:** coordinación de los servicios.
- **Node.js:** ejecución del backend y construcción del frontend.
- **React y Vite:** desarrollo y compilación del frontend.
- **Nginx:** servidor web del frontend y proxy hacia el backend.
- **MongoDB 7:** almacenamiento de los datos.

## 5. Servicios desplegados

El archivo `docker-compose.yml` define tres servicios:

| Servicio | Función | Puerto |
|---|---|---|
| frontend | Sirve la aplicación mediante Nginx | 8080:80 |
| backend | Gestiona la API y las operaciones CRUD | 5000 interno |
| mongodb | Almacena las tareas | 27017 interno |

Los servicios se comunican mediante una red interna de Docker denominada `mern-network`.

Únicamente el frontend publica un puerto hacia el exterior. El backend y MongoDB permanecen accesibles únicamente dentro de la red de Docker.

## 6. Persistencia y reinicio automático

Para conservar los datos aunque se eliminen y vuelvan a crear los contenedores, se ha configurado un volumen Docker denominado `mongo-data`, asociado al directorio `/data/db` de MongoDB.

Además, los tres servicios utilizan la política de reinicio:

`restart: unless-stopped`

De esta manera, Docker puede volver a iniciar los contenedores cuando se produce un reinicio de la instancia EC2, siempre que no se hayan detenido manualmente.

## 7. Configuración de seguridad

- El puerto 8080 está publicado para permitir el acceso externo a la aplicación.
- Los puertos 5000 y 27017 no están publicados en la instancia.
- La comunicación entre los servicios se realiza mediante la red interna de Docker.
- No se incluyen credenciales ni archivos `.env` con secretos en el repositorio.
- El archivo `.gitignore` evita subir archivos de configuración local y posibles credenciales.

## 8. Despliegue de la aplicación

Una vez instalada la herramienta Docker y Docker Compose en la instancia EC2, se clona el repositorio:

```bash
git clone https://github.com/marcenteno/aa1-despliegue-web.git
```

Se accede a la carpeta de la Fase 2:

```bash
cd ~/aa1-despliegue-web/fase2-docker-compose
```

Se comprueba la configuración:

```bash
sudo docker compose config -q
```

Para construir las imágenes y levantar todos los servicios:

```bash
sudo docker compose up -d --build
```

## 9. Comandos de administración

Consultar el estado de los contenedores:

```bash
sudo docker compose ps
```

Consultar los logs de los servicios:

```bash
sudo docker compose logs --tail=30
```

Reiniciar los servicios:

```bash
sudo docker compose restart
```

Detener y eliminar los contenedores y la red, conservando el volumen de datos:

```bash
sudo docker compose down
```

Volver a iniciar los servicios:

```bash
sudo docker compose up -d
```

**Importante:** no utilizar `docker compose down -v` si se desea conservar el volumen de MongoDB.

## 10. Pruebas realizadas

Se han realizado las siguientes comprobaciones:

1. **Funcionamiento de la aplicación:** acceso desde el navegador y comprobación de las operaciones de creación, consulta, modificación del estado y eliminación de tareas.
2. **Persistencia de los datos:** eliminación y recreación de los contenedores mediante `docker compose down` y `docker compose up -d`. Se comprobó que las tareas almacenadas seguían disponibles.
3. **Reinicio automático:** reinicio de la instancia EC2 y posterior comprobación de que los contenedores volvieron a iniciarse automáticamente.
4. **Comprobación de servicios:** verificación de que frontend, backend y MongoDB aparecen en estado `Up`.
5. **Logs:** revisión de los registros para comprobar el arranque de los servicios y la comunicación entre el backend y MongoDB.

## 11. Evidencias

Las capturas de las configuraciones y pruebas realizadas se encuentran organizadas en la carpeta `evidencias`, agrupadas por los siguientes apartados:

- Dockerfiles y archivo Docker Compose.
- Contenedores en ejecución.
- Logs de los servicios.
- Aplicación funcionando en el navegador.
- Prueba de persistencia al eliminar y recrear contenedores.
- Prueba de arranque automático tras reiniciar EC2.

## 12. Resultado final

La aplicación MERN Todo ha quedado desplegada en una segunda instancia EC2 mediante Docker Compose.

Los tres servicios funcionan de forma coordinada, los datos se conservan mediante un volumen persistente, los contenedores cuentan con una política de reinicio automático y únicamente el frontend está expuesto al exterior.