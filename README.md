# AA1 – Despliegue de Aplicaciones Web

**Ciclo:** 2.º DAW  
**Curso:** 2026/2027

## ¿De qué trata este proyecto?

En este repositorio se recoge todo el trabajo realizado para la actividad AA1 de la asignatura Despliegue de Aplicaciones Web.

La actividad está dividida en cuatro fases. En cada una hemos trabajado con diferentes herramientas y servicios de AWS para aprender a desplegar aplicaciones, configurar servidores y comprobar que todo funciona correctamente.

He organizado el repositorio por fases para que sea más fácil encontrar el código, la documentación, los scripts y las capturas de las pruebas que he ido realizando.

## Fases realizadas

### Fase 1 – Despliegue de una aplicación MERN en EC2

En esta primera fase desplegué una aplicación MERN (MongoDB, Express, React y Node.js) en una instancia EC2 de AWS.

Para ello preparé un servidor Ubuntu, instalé las herramientas necesarias, configuré Nginx y conecté la aplicación con MongoDB Atlas. También comprobé que el backend funcionaba correctamente y que los datos se mantenían.

### Fase 2 – Despliegue con Docker Compose

En la segunda fase volví a desplegar la aplicación, pero esta vez utilizando Docker y Docker Compose.

Configuré los diferentes contenedores para que pudieran comunicarse entre ellos y preparé un volumen para mantener los datos aunque se reiniciaran los servicios.

También realicé varias comprobaciones para asegurarme de que la aplicación seguía funcionando correctamente.

### Fase 3 – Publicación de una web con dominio y HTTPS

En esta fase elegí una plantilla web y la publiqué en una instancia EC2 utilizando Nginx.

Después configuré un dominio para acceder a la página, instalé un certificado gratuito de Let's Encrypt mediante Certbot y preparé la redirección automática de HTTP a HTTPS.

Por último, comprobé que la web funcionaba con HTTPS y que la renovación del certificado se podía realizar correctamente.

### Fase 4 – Despliegue de Odoo multirregión

En la última fase trabajé con dos instancias de Odoo desplegadas en diferentes regiones de AWS: Norte de Virginia y Oregón.

Configuré una zona alojada privada en Route 53 y asocié las dos VPC. También preparé los registros DNS con una política de enrutamiento por latencia.

Para terminar, realicé distintas pruebas para comprobar cómo respondía DNS en cada región y qué ocurría cuando una de las instancias dejaba de estar disponible.

---

## Organización del repositorio

He separado el trabajo en cuatro carpetas, una para cada fase:

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

Dentro de cada carpeta se encuentran los archivos correspondientes a esa fase: código, configuraciones, documentación y capturas de pantalla.

## Herramientas utilizadas

Durante la actividad he trabajado con las siguientes herramientas y tecnologías:

- **AWS:** para crear y gestionar la infraestructura.
- **EC2:** para desplegar las máquinas virtuales.
- **Ubuntu:** como sistema operativo de los servidores.
- **Node.js y Express:** para ejecutar el backend de la aplicación MERN.
- **MongoDB Atlas:** para almacenar los datos.
- **Nginx:** para publicar las aplicaciones web.
- **Docker y Docker Compose:** para trabajar con contenedores.
- **Amazon Route 53:** para configurar los registros DNS y el enrutamiento.
- **Let's Encrypt y Certbot:** para configurar los certificados HTTPS.
- **Odoo:** para realizar el despliegue multirregión.

## Documentación y capturas

En cada fase he incluido la documentación necesaria para explicar los pasos que he seguido.

También he añadido capturas de pantalla de las configuraciones y de las pruebas realizadas para dejar constancia de que los despliegues funcionan correctamente.

Los scripts y archivos de configuración utilizados también están incluidos en sus respectivas carpetas.

---

**Actividad:** AA1 – Despliegue de Aplicaciones Web  
**Ciclo formativo:** 2.º DAW  
**Curso académico:** 2026/2027