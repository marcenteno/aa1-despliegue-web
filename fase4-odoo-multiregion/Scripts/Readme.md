# Fase 4. Odoo en dos regiones con Route 53

## 1. Objetivo

El objetivo de esta fase es desplegar una aplicación empresarial Odoo en dos regiones diferentes de AWS, Norte de Virginia y Oregón, y permitir el acceso a ambas instalaciones mediante un único nombre DNS privado.

Para ello, se ha utilizado Amazon EC2 para alojar las instancias de Odoo y Amazon Route 53 para configurar una zona alojada privada y una política de enrutamiento por latencia.

## 2. Infraestructura desplegada

Se han creado dos instancias EC2 independientes, una en cada región:

| Región | Aplicación | IP elástica |
|---|---|---|
| Norte de Virginia (us-east-1) | Odoo Virginia | 52.54.225.120 |
| Oregón (us-west-2) | Odoo Oregón | 44.242.101.78 |

En ambas instancias se ha utilizado el script `odoo_ec2_00_Monolito.sh`, situado en la carpeta `07` del repositorio Odoo-Aws.

Cada instalación dispone de su propia base de datos y se ha configurado con una identificación de empresa diferente para distinguir las dos regiones.

También se ha cambiado la contraseña del administrador de ambas instalaciones.

## 3. Configuración de Route 53

Se ha creado una zona alojada privada con el nombre:

`aa1-daw.internal`

Esta zona se ha asociado a las VPC de las dos regiones, permitiendo que las instancias EC2 puedan resolver los nombres DNS privados.

Dentro de la zona se ha configurado el nombre:

`odoo.aa1-daw.internal`

Este nombre dispone de dos registros A, uno para cada instalación:

- Virginia: `52.54.225.120`
- Oregón: `44.242.101.78`

## 4. Política de enrutamiento elegida

Se ha elegido la política de **enrutamiento por latencia** de Route 53.

Esta política permite dirigir las consultas DNS hacia la región que ofrece menor latencia de acuerdo con la ubicación de la consulta.

La elección responde al escenario planteado, en el que existen oficinas en las costas este y oeste de Estados Unidos. De esta manera, los usuarios pueden acceder a la instalación regional que proporcione mejores tiempos de respuesta.

Se ha preferido esta política frente a otras alternativas:

- **Enrutamiento simple:** no permite seleccionar entre varias regiones en función de la latencia.
- **Enrutamiento ponderado:** distribuye las consultas según los pesos configurados, no según la proximidad de los usuarios.
- **Enrutamiento por geolocalización:** dirige las consultas según la ubicación geográfica, pero no selecciona necesariamente la región con menor latencia.
- **Enrutamiento de conmutación por error (Failover):** está orientado a disponer de una instalación principal y otra secundaria, en lugar de priorizar los tiempos de respuesta.
- **Enrutamiento multivalor:** permite devolver varios valores, pero no selecciona la región más rápida.

## 5. Pruebas realizadas

### Prueba 1. Resolución DNS privada

Se ha ejecutado `nslookup odoo.aa1-daw.internal` desde las instancias de Virginia y Oregón.

En ambas regiones se ha obtenido una dirección IP válida. También se ha realizado la consulta desde un equipo externo a las VPC, donde el nombre no se ha podido resolver.

Esto demuestra que la zona alojada es privada y que su resolución está disponible desde las redes asociadas.

### Prueba 2. Comportamiento de la política de enrutamiento

Se han realizado consultas DNS desde las dos regiones para comprobar las respuestas de Route 53.

Desde Virginia se ha obtenido la dirección correspondiente a Odoo Virginia:

`52.54.225.120`

Desde Oregón se ha obtenido la dirección correspondiente a Odoo Oregón:

`44.242.101.78`

Los comandos utilizados han sido:

```bash
nslookup odoo.aa1-daw.internal
```

### Prueba 3. Caída de una región

Se ha detenido la instancia EC2 de Oregón para comprobar el comportamiento de Route 53 cuando una de las regiones deja de estar disponible.

Después de detenerla, se han realizado nuevas consultas DNS y comprobaciones HTTP desde la instancia de Virginia:

```bash
nslookup odoo.aa1-daw.internal
```

```bash
curl -I http://odoo.aa1-daw.internal
```

También se ha comprobado la respuesta completa siguiendo las redirecciones:

```bash
curl -IL http://odoo.aa1-daw.internal
```

La instalación de Virginia ha continuado respondiendo correctamente.

### Prueba 4. Datos independientes por región

Se ha creado un contacto de prueba en Odoo Virginia:

- Nombre: `Contacto prueba Virginia`
- Correo: `virginia.prueba@test.com`

Posteriormente, se ha accedido a Odoo Oregón y se ha activado la aplicación Contacts para buscar el mismo contacto.

El contacto no ha aparecido en Oregón.

Esto demuestra que cada instalación utiliza una base de datos independiente. Para compartir los datos sería necesario utilizar una base de datos común o implementar un sistema de replicación o sincronización.

## 6. Conclusiones

La fase ha permitido desplegar dos instalaciones independientes de Odoo en regiones diferentes de AWS y conectarlas mediante un nombre DNS privado gestionado por Route 53.

La política de enrutamiento por latencia permite orientar las consultas hacia la región que ofrece mejores tiempos de respuesta.

Las pruebas han permitido comprobar la resolución privada, el comportamiento del enrutamiento, la respuesta ante la detención de una instancia y la independencia de los datos almacenados en cada región.

Para conseguir que ambas instalaciones compartan la misma información empresarial sería necesario diseñar una arquitectura adicional de almacenamiento y sincronización de datos.