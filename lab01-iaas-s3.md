# Lab 1 - AWS S3

Todas las soluciones de *big data* comienzan con el almacenamiento de datos. Este es el primer paso en el *pipeline* de *big data*. [Amazon Simple Storage Service](https://docs.aws.amazon.com/es_es/s3/index.html?id=docs_gateway#lang/es) (Amazon S3) es uno de los servicios más utilizados para almacenar datos.

En este laboratorio, practicaremos el uso de la consola de administración de AWS para crear un *bucket* de S3. Luego cargaremos archivos en Amazon S3 y ejecutaremos consultas simples sobre los datos.

## Objetivos
 - Familiarizarse con S3 en la consola de administración de AWS
 - Crear un *buckets* en S3
 - Cargar datos (objetos) en un *bucket*
 - Hacer consultas SQL a objetos
 - Control de permisos de accesso
 - Alojamiento de sitios web estáticos

## Índice
- [Lab 1 - AWS S3](#lab-1---aws-s3)
  - [Objetivos](#objetivos)
  - [Índice](#índice)
  - [Creación del *bucket*](#creación-del-bucket)
  - [Creación de objetos](#creación-de-objetos)
    - [Una imagen con acceso público](#una-imagen-con-acceso-público)
      - [Cambio de clase de almacenamiento](#cambio-de-clase-de-almacenamiento)
      - [Acceso público](#acceso-público)
    - [Datos con acceso privado](#datos-con-acceso-privado)
      - [Versionamiento](#versionamiento)
      - [Consulta SQL](#consulta-sql)
  - [Alojamiento de sitios web estáticos](#alojamiento-de-sitios-web-estáticos)
  - [Clean up](#clean-up)

## Creación del *bucket*
 
1. Acceder al servicio **S3**:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-01.png)

2. Crear un nuevo *bucket*:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-02.png)

3. Escoger un nombre para el *bucket*. El nombre debe ser único globalmente:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-03.png)

7. Confirmar la creación del *bucket* y comprobar que fue correctamente creado:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-04.png)

## Creación de objetos

### Una imagen con acceso público

8. Hacer el *upload* de una imagen cualquiera:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-06.png)

9. Comprobar la creación del objeto:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-07.png)
   
#### Cambio de clase de almacenamiento

10. En la pestaña de **Propiedades** del objecto, cambiar la clase de almacenamiento de *Standard* para *Intelligent-Tiering*:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-08.png)

#### Acceso público

11. Habilitar las *Access Control List* (ACLs) en la pestaña de **Permisos** del *bucket*:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-09.png)

12. En la misma pestaña, habilitar acceso público:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-10.png)
   
13. En la pestaña de **Permisos** del objeto, habilitar accesso público:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-11.png)

14. Confirmar el accesso público a la imagen mediante la URL del objeto:

    |          | bucket      |                    | objeto        |
    |----------|-------------|--------------------|-------------- |
    | https:// | iffe-mbd    | .s3.amazonaws.com/ | sic.jpg       |
    
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-12.png)
   
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-13.png)


### Datos con acceso privado

15. Hacer el *upload* de [este archivo .csv](https://github.com/josecastillolema/iffe/blob/main/lab01-iaas-s3/lab1.csv) y comprobar la creación del objeto:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-14.png)

#### Versionamiento

16. En la pestaña de **Propiedades** del objecto, habilitar versionamiento:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-15.png)

#### Consulta SQL

17. En la descripción del objeto, seleccionar **Object actions -> Query with S3 Select**:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-16.png)

18. Probar algunas *queries*:
    - `SELECT * FROM s3object s;`
    - `SELECT count(*) FROM s3object s;`
  
      ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-17.png)

      ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-18.png)

## Alojamiento de sitios web estáticos
    
19.  En la pestaña de **Propiedades** del *bucket*, alterar la configuración para permitir el alojamiento de sitios web estáticos e introducir el nombre del archivo `html` principal:
      ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-19.png)

20. Hacer el *upload* de [este archivo .html](https://github.com/josecastillolema/iffe/blob/main/lab01-iaas-s3/index.html) y comprobar la creación del objeto:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-20.png)

21. Habilitar acceso público para este objeto como descrito en [Acceso público](#acceso-público)

22. Consultar la nueva URL en la pestaña de **Propiedades** del *bucket*. La URL en el modo de alojamiento de sitios web estáticos tiene un formato nuevo:

    |          | bucket      |            | region    |               |
    |----------|-------------|------------|---------- | --------------|
    | https:// | iffe-mbd    | s3-website | us-east-1 | amazonaws.com |

      ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-21.png)

23. Accesar el sitio web por la nueva URL:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-22.png)   


## Clean up

21. Borrar el bucket
