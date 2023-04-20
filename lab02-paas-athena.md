# Lab 2 - Amazon Athena

Cuando trabajamos en soluciones de *big data*, a menudo es necesario acceder a datos de múltiples fuentes (una base de datos transaccional, un flujo de datos en vivo o contenido web no estructurado almazenado en Amazon S3). Con [Amazon Athena](https://aws.amazon.com/es/athena/) es posible agregar los archivos en Amazon S3 y reestructurar los datos para su posterior análisis. Athena es un servicio *serverless*, por lo que no es necesario configurar ni administrar ninguna infraestructura.

Athena puede usarse para consultar datos estructurados, no estructurados y semiestructurados. Además, Athena se integra con [AWS Glue](https://aws.amazon.com/es/glue/).

![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/athena-00.png)

## Objetivos
 - Familiarizarse con Athena en la consola de administración de AWS
 - Crear una base de datos
 - Crear tablas a partir de datos importados de S3
 - Definir columnas y tipos de datos
 - Ejecutar consultas simples y complejas

## Índice
- [Lab 2 - Amazon Athena](#lab-2---amazon-athena)
  - [Objetivos](#objetivos)
  - [Índice](#índice)
  - [Prerrequisitos](#prerrequisitos)
  - [Configuración del ambiente](#configuración-del-ambiente)
  - [Creación de la base de datos](#creación-de-la-base-de-datos)
    - [Importación de los datos de S3](#importación-de-los-datos-de-s3)
  - [Desafíos](#desafíos)
  - [*Clean up*](#clean-up)

## Prerrequisitos
 
- Un *bucket* de S3 para almacenar los resultados
- Otro *bucket* (puede ser el mismo) con [este archivo `.csv`](https://github.com/josecastillolema/iffe/blob/main/lab01-iaas-s3/lab1.csv)
- El archivo `.csv` debe estar dentro de un directório cualquiera en el *bucket* y no en la raíz del mismo (por ejemplo `data`):
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/athena-01.png)

## Configuración del ambiente

1. Acceder al servicio **Athena**:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/athena-02.png)

2. Lanzar el editor de consultas:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/athena-03.png)

3. Agregar un *bucket* para almacenar los resultados de las consultas:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/athena-04.png)
   
## Creación de la base de datos

10. Ejecutar la siguiente *query* para crear una nueva base de datos `customers`:
    ```
    CREATE DATABASE customers
    ``` 

    ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/athena-05.png)

### Importación de los datos de S3

11. Ejecutar la siguiente *query* para importar los datos del bucket de S3 a una nueva tabla `american_customers`:
    ```
    CREATE EXTERNAL TABLE american_customers (
      customerID int,
      first_name string,
      last_name string,
      join_date string,
      street_address string,
      city string,
      state string,
      phone string
    )
    ROW FORMAT DELIMITED
    FIELDS TERMINATED BY ','
    STORED AS TEXTFILE
    LOCATION 's3://iffe-mbd/data/'
    TBLPROPERTIES ('skip.header.line.count'='1')
    ``` 
    ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/athena-06.png)

12. Ejecutar un *preview* de la tabla recién creada para comprobar que los dados fueron correctamente importados:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/athena-07.png)
   
## Desafíos

 - Lista de *Customer IDs* y *Last Names*
 - Número de clientes de NY
 - Crear una nueva tabla `american_customers_norm` convirtiendo `join_date` de tipo de dato `string` a `date`
 - Número de clientes registrados desde 2014

## *Clean up*

13.  Borrar la base de datos y las tablas creadas
