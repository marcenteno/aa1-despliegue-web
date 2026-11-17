# AA1 – Despliegue de Aplicaciones Web

**Ciclo formativo:** 2.º Desarrollo de Aplicaciones Web (DAW)  
**Curso académico:** 2026/2027

---

## Descripción del proyecto

Este repositorio contiene el desarrollo de la actividad **AA1 – Despliegue de Aplicaciones Web**, realizada durante el curso de 2.º DAW.

El proyecto está dividido en cuatro fases prácticas en las que se trabajan diferentes tecnologías y servicios de AWS para desplegar aplicaciones web, configurar infraestructuras y comprobar su funcionamiento.

Cada fase incluye los archivos necesarios, documentación técnica, scripts de configuración y evidencias de las pruebas realizadas.

## Fases del proyecto

### Fase 1. Despliegue tradicional de una aplicación MERN en EC2

Despliegue de una aplicación MERN (MongoDB, Express, React y Node.js) en una instancia EC2 de AWS.

Se trabaja la configuración del servidor Ubuntu, la instalación de Node.js y Nginx, la conexión con MongoDB Atlas y la ejecución del backend como servicio.

**Contenido:** aplicación, documentación, scripts y evidencias.

### Fase 2. Despliegue de una aplicación con Docker Compose

Despliegue de la aplicación mediante contenedores Docker y Docker Compose.

Se configura la comunicación entre los servicios, la persistencia de los datos mediante volúmenes y el reinicio automático de los contenedores.

**Contenido:** archivos de Docker Compose, documentación, código y evidencias.

### Fase 3. Publicación de una web con dominio y HTTPS

Publicación de una plantilla web en una instancia EC2 utilizando Nginx.

Se configura un dominio, su resolución DNS y un certificado digital gratuito de Let's Encrypt mediante Certbot. También se establece la redirección automática de HTTP a HTTPS y se comprueba la renovación del certificado.

**Contenido:** código de la plantilla, configuración de Nginx, documentación y evidencias.

### Fase 4. Despliegue de Odoo multirregión

Despliegue de Odoo en dos regiones de AWS: Norte de Virginia y Oregón.

Se configura una zona alojada privada en Amazon Route 53, asociada a las dos VPC, y una política de enrutamiento por latencia para gestionar el acceso a las instancias.

Se realizan distintas pruebas para comprobar la resolución DNS, el comportamiento de la política y el funcionamiento de los servicios entre ambas regiones.

**Contenido:** documentación, script de configuración y evidencias de las pruebas.

---

## Estructura del repositorio

```text
aa1-despliegue-web/
│
├── fase1-mern-ec2/
│   ├── Código/
│   ├── evidencias/
│   ├── Scripts/
│   ├── Fase1 - Documentación.docx
│   └── README.md
│
├── fase2-docker-compose/
│   ├── Código/
│   ├── evidencias/
│   ├── docker-compose.yml
│   ├── Fase2-Documentacion.docx
│   └── README.md
│
├── fase3-dominio-https/
│   ├── Código/
│   ├── Evidencias/
│   ├── Scripts/
│   ├── Fase3 - Documentacion.docx
│   └── README.md
│
├── fase4-odoo-multiregion/
│   ├── Evidencias/
│   ├── Scripts/
│   ├── Fase4.docx
│   ├── Pruebas.docx
│   └── README.md
│
└── README.md
```

## Tecnologías y servicios utilizados

- **Amazon Web Services (AWS):** infraestructura en la nube.
- **Amazon EC2:** creación y administración de instancias virtuales.
- **Ubuntu:** sistema operativo de los servidores.
- **Node.js y Express:** desarrollo y ejecución del backend.
- **MongoDB Atlas:** almacenamiento de datos de la aplicación MERN.
- **Nginx:** servidor web y proxy inverso.
- **Docker y Docker Compose:** contenedorización y despliegue de aplicaciones.
- **DNS y Amazon Route 53:** configuración y resolución de nombres de dominio.
- **Let's Encrypt y Certbot:** obtención y renovación de certificados HTTPS.
- **Odoo:** aplicación desplegada en dos regiones de AWS.

## Documentación y evidencias

Cada carpeta de fase contiene los recursos correspondientes al trabajo realizado.

- Los archivos README describen los objetivos, la configuración y los procedimientos seguidos.
- Los documentos de cada fase recogen la documentación técnica.
- Las carpetas `Evidencias` incluyen capturas de pantalla de las configuraciones y pruebas realizadas.
- Las carpetas `Scripts` contienen archivos de configuración y automatización utilizados durante el despliegue.

## Autoría

Proyecto realizado como parte de la actividad AA1 de la asignatura **Despliegue de Aplicaciones Web**, correspondiente al segundo curso del ciclo formativo de Desarrollo de Aplicaciones Web (DAW).

**Curso académico:** 2026/2027.