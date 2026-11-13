# Fase 3 – Publicación web con dominio y HTTPS

## 1. Objetivo

El objetivo de esta fase es publicar una página web en una instancia EC2 de AWS, utilizando Nginx como servidor web, configurar un dominio gratuito y habilitar HTTPS mediante un certificado digital gratuito de Let's Encrypt.

## 2. Aplicación web seleccionada

Para realizar esta fase se ha elegido la plantilla **Plain**, perteneciente al repositorio [website-templates](https://github.com/santos-pardos/website-templates).

Es una plantilla web sencilla desarrollada con HTML y CSS, que incluye imágenes y diferentes apartados de navegación.

Se descargó únicamente la carpeta correspondiente a esta plantilla mediante Git Sparse Checkout, evitando descargar el repositorio completo.

## 3. Infraestructura y despliegue

La página web se ha publicado en una instancia EC2 con Ubuntu 24.04 en la región Norte de Virginia (us-east-1).

Se ha utilizado Nginx como servidor web y se han copiado los archivos de la plantilla en el siguiente directorio:

`/var/www/plain`

Se ha creado un sitio virtual propio en Nginx mediante el archivo:

`/etc/nginx/sites-available/plain`

La configuración permite servir la página principal y sus recursos estáticos, como las hojas de estilo y las imágenes.

## 4. Configuración del dominio

Se ha registrado gratuitamente el dominio **plainweb.work.gd** mediante el proveedor DNSExit.

En su panel de administración se ha configurado el registro DNS para que el dominio apunte a la dirección IP pública de la instancia EC2.

La resolución del dominio se ha comprobado utilizando la herramienta Verify DNS de DNSExit.

## 5. Instalación del certificado digital

Para habilitar HTTPS se ha utilizado Let's Encrypt, junto con Certbot y su complemento para Nginx.

Instalación de las herramientas:

```bash
sudo apt update
sudo apt install -y certbot python3-certbot-nginx
```

Comprobación de la versión:

```bash
certbot --version
```

Solicitud e instalación del certificado para el dominio principal y el subdominio www:

```bash
sudo certbot --nginx -d plainweb.work.gd -d www.plainweb.work.gd
```

Certbot obtuvo el certificado correctamente y modificó la configuración de Nginx para habilitar HTTPS.

Los archivos del certificado se almacenan en:

- Certificado: `/etc/letsencrypt/live/plainweb.work.gd/fullchain.pem`
- Clave privada: `/etc/letsencrypt/live/plainweb.work.gd/privkey.pem`

La clave privada no debe publicarse ni subirse al repositorio.

## 6. Redirección de HTTP a HTTPS

Para garantizar que todas las conexiones se realicen de forma segura, se configuró Nginx para redirigir automáticamente las peticiones HTTP a HTTPS mediante una respuesta 301.

La directiva utilizada es:

```nginx
return 301 https://$host$request_uri;
```

Después de modificar la configuración se comprobó su sintaxis y se recargó el servicio:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

Se comprobó que al acceder mediante `http://plainweb.work.gd` el navegador redirige automáticamente a `https://plainweb.work.gd`.

## 7. Renovación del certificado

Certbot configura una tarea programada para comprobar y renovar automáticamente el certificado antes de su fecha de caducidad.

Para verificar que la renovación funciona correctamente, se realizó una prueba simulada mediante el siguiente comando:

```bash
sudo certbot renew --dry-run
```

La prueba finalizó correctamente, confirmando que el proceso de renovación está preparado.

## 8. Resultado final

La plantilla Plain se encuentra publicada y accesible mediante el dominio:

**https://plainweb.work.gd**

Se ha configurado Nginx como servidor web, el dominio DNSExit apunta a la instancia EC2 y el certificado de Let's Encrypt permite establecer conexiones HTTPS.

También se ha configurado la redirección automática de HTTP a HTTPS y se ha comprobado el funcionamiento de la renovación del certificado.

## 9. Evidencias

Las capturas y comprobaciones de esta fase se encuentran en la carpeta `Evidencias` y en el documento de documentación paso a paso.

Se incluyen las siguientes pruebas:

1. Registro del dominio en DNSExit.
2. Comprobación de la resolución DNS.
3. Configuración del sitio virtual de Nginx.
4. Certificado digital en el navegador, con su emisor y fechas de validez.
5. Redirección automática de HTTP a HTTPS.
6. Prueba de renovación del certificado con Certbot.
