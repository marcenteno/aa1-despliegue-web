# Fase 1 – Despliegue de aplicación MERN en AWS EC2

## 1. Descripción

En esta fase se ha desplegado una aplicación web MERN (MongoDB, Express, React y Node.js) en una instancia EC2 de Amazon Web Services.

La aplicación seleccionada es **10-MERN-Todo**, del repositorio educativo [MERN-Stack-Guide](https://github.com/santos-pardos/MERN-Stack-Guide). Permite gestionar una lista de tareas mediante operaciones CRUD: crear, consultar, actualizar y eliminar tareas.

## 2. Arquitectura y tecnologías

- **AWS EC2:** instancia virtual Ubuntu 24.04 en la región US East (N. Virginia).
- **Elastic IP:** dirección IP pública fija para acceder a la aplicación.
- **Node.js y Express:** ejecución del servidor backend y de la API.
- **React y Vite:** desarrollo y compilación del frontend.
- **MongoDB Atlas:** almacenamiento de los datos en la nube.
- **Nginx:** servidor web y proxy inverso.
- **systemd:** gestión del backend como servicio del sistema.

## 3. Configuración del despliegue

### 3.1. Instancia EC2 y seguridad

Se ha creado una instancia EC2 con Ubuntu 24.04 y se le ha asociado una Elastic IP.

El grupo de seguridad permite:
- SSH (puerto 22): acceso restringido.
- HTTP (puerto 80): acceso público para visualizar la aplicación.

Los puertos del backend y de la base de datos no están expuestos directamente a Internet.

### 3.2. Backend

Se ha configurado el backend con Node.js y Express. La conexión con MongoDB Atlas se realiza mediante variables de entorno almacenadas en un archivo `.env`, que no se incluye en el repositorio por motivos de seguridad.

El backend se ejecuta como un servicio de systemd llamado `mern-todo`, lo que permite que se inicie automáticamente al arrancar la instancia.

### 3.3. Frontend y Nginx

Se ha compilado el frontend React mediante Vite y se han copiado los archivos generados al directorio de publicación de Nginx.

Nginx sirve el frontend y realiza un proxy inverso para dirigir las peticiones de la API al backend.

## 4. Comprobaciones realizadas

- Acceso a la aplicación mediante la Elastic IP.
- Creación de nuevas tareas.
- Consulta de las tareas existentes.
- Actualización del estado de las tareas.
- Eliminación de tareas.
- Comprobación de la persistencia de los datos al recargar la aplicación.
- Comprobación del inicio automático del backend después de reiniciar EC2.
- Verificación del acceso a la aplicación después del reinicio.

## 5. Evidencias

Las capturas y grabaciones de las pruebas realizadas se encuentran organizadas en la carpeta `evidencias`:

1. Grupo de seguridad de EC2.
2. Software instalado.
3. Configuración del servidor web.
4. Backend funcionando como servicio.
5. Aplicación funcionando en el navegador.
6. Prueba de reinicio y persistencia.

## 6. Archivos de configuración

En la carpeta `Scripts` se incluyen los archivos de referencia utilizados para documentar la configuración:

- `instalacion.md`
- `mern-todo.service`
- `nginx.conf`

**Nota de seguridad:** no se incluyen credenciales, claves privadas ni archivos con variables de entorno que contengan información sensible.

## 7. Resultado final

La aplicación MERN se encuentra desplegada y accesible mediante la Elastic IP de la instancia EC2. Se han comprobado las operaciones CRUD, el funcionamiento del backend como servicio y la persistencia de los datos después del reinicio de la instancia.

## 8. Comandos importantes

Los siguientes comandos permiten consultar y administrar los servicios utilizados durante el despliegue.

### 8.1. Backend

Consultar el estado del servicio:

```bash
sudo systemctl status mern-todo
```

Reiniciar el backend:

```bash
sudo systemctl restart mern-todo
```

Consultar los registros del servicio:

```bash
sudo journalctl -u mern-todo -f
```

Habilitar el inicio automático:

```bash
sudo systemctl enable mern-todo
```

### 8.2. Nginx

Comprobar que la configuración es correcta:

```bash
sudo nginx -t
```

Consultar el estado del servicio:

```bash
sudo systemctl status nginx
```

Recargar la configuración:

```bash
sudo systemctl reload nginx
```

### 8.3. Frontend

Instalar las dependencias:

```bash
npm install
```

Generar la versión de producción:

```bash
npm run build
```

Estos comandos deben ejecutarse desde la carpeta correspondiente del proyecto.

### 8.4. Backend

Instalar las dependencias:

```bash
npm install
```

Este comando debe ejecutarse desde la carpeta `backend`.

