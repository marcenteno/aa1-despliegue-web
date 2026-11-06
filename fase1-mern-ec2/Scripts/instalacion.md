
# Instalación y comprobación del software

## 1. Entorno de trabajo

Para desplegar la aplicación MERN se ha utilizado una instancia EC2 de AWS con Ubuntu 24.04 LTS.

El entorno cuenta con las siguientes herramientas y servicios:

| Herramienta | Versión o servicio |
|---|---|
| Sistema operativo | Ubuntu 24.04 LTS |
| Node.js | 22.23.4 |
| npm | 10.9.9 |
| Nginx | 1.24.0 |
| Git | 2.43.0 |
| Base de datos | MongoDB Atlas (M0) |

## 2. Comprobación de versiones

Para verificar la instalación de las herramientas se utilizaron los siguientes comandos:

**Node.js**
```bash
node -v
```

**npm**
```bash
npm -v
```

**Nginx**
```bash
nginx -v
```

**Git**
```bash
git --version
```

## 3. Comprobación del servidor web

Nginx se utiliza como servidor web y como punto de entrada a la aplicación.

Para consultar su estado:

```bash
sudo systemctl status nginx
```

Para comprobar que la configuración no contiene errores:

```bash
sudo nginx -t
```

## 4. Comprobación del backend

El backend de la aplicación se ejecuta mediante un servicio de systemd llamado `mern-todo`.

Para consultar si está funcionando:

```bash
sudo systemctl status mern-todo
```

Para comprobar que se inicia automáticamente al arrancar la instancia:

```bash
sudo systemctl is-enabled mern-todo
```

## 5. Base de datos

La aplicación utiliza MongoDB Atlas como servicio de base de datos en la nube.

La conexión se configura mediante la variable de entorno `MONGO_URI`, almacenada en un archivo `.env` dentro de la carpeta del backend.

Este archivo no se incluye en el repositorio público porque contiene información sensible.

## 6. Seguridad

La instancia EC2 utiliza un grupo de seguridad que permite únicamente el tráfico necesario:

- SSH (puerto 22): acceso restringido a la IP autorizada.
- HTTP (puerto 80): acceso público para visualizar la aplicación.
- El puerto del backend (5000) no está expuesto públicamente.
- El puerto de MongoDB (27017) tampoco está expuesto públicamente.

La aplicación utiliza Nginx como punto de entrada y este redirige las peticiones correspondientes al backend.
