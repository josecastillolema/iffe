# Lab 4 - Amazon Redshift

Los analistas de datos a menudo trabajan con conjuntos de datos muy grandes. Por ejemplo, algunos *data warehouses* pueden contener varios petabytes de datos y los *datalakes* pueden ser incluso más grandes. Este lab aborda el aspecto de volumen de los problemas de big data (**Volumen**, Variedad, Velocidad, Veracidad y Valor).

[Amazon Redshift](https://aws.amazon.com/es/redshift/) está diseñado para manejar conjuntos de datos extremadamente grandes. A diferencia de los sistemas de administración de bases de datos relacionales tradicionales, Redshift utiliza almacenamiento de datos columnar mejorando el rendimiento de las consultas y ahorrando en costos de almacenamiento.

![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-00.png)

## Objetivos
 - Acceder a Redshift en la consola de administración de AWS
 - Crear un clúster de Redshift
 - Cargar datos de S3 en Redshift
 - Consultar datos en Redshift

## Índice
- [Lab 4 - Amazon Redshift](#lab-4---amazon-redshift)
  - [Objetivos](#objetivos)
  - [Índice](#índice)
  - [Prerrequisitos](#prerrequisitos)
  - [Creación del clúster](#creación-del-clúster)
  - [Conexión al banco](#conexión-al-banco)
  - [Importación de datos de S3](#importación-de-datos-de-s3)
  - [Desafíos](#desafíos)
  - [*Clean up*](#clean-up)

## Prerrequisitos
 
- Un *bucket* con [este archivo `.csv`](https://github.com/josecastillolema/iffe/blob/main/lab01-iaas-s3/lab1.csv)
- El archivo `.csv` debe estar dentro de un directório cualquiera en el *bucket* y no en la raíz del mismo (por ejemplo `data`):
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/athena-01.png)

## Creación del clúster

Los *clusters* son el principal componente de infraestructura de un *data warehouse* de Redshift. Un clúster se compone de uno o más nodos de cómputo. Si hay más de un nodo, uno de los nodos será el nodo líder y los otros nodos serán nodos de cálculo. Las aplicaciones cliente interactúan con el nodo líder. El siguiente diagrama ilustra la infraestructura general de Amazon Redshift:
![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-01.png)


1. Acceder al servicio **Redshift**:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-02.png)

2. Crear un nuevo clúster:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-03.png)

3. Escoger un nombre para el clúster, `dc2.large` como *flavor* y 2 nodos como tamaño:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-04.png)

4. Escoger una contraseña para el banco de datos:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-05.png)

5. Definir `LabRole` como IAM *role*. Estos permisos son creados de forma automática por el ambiente AWS Academy:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-06.png)

6. Confirmar la creación del clúster y esperar a que se encuentre disponible:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-07.png)

## Conexión al banco

7. Escoger la opción ***Query data*** -> ***Query in query editor***:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-08.png)

8. Conectar al banco de datos recién creado:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-09.png)

## Importación de datos de S3

9. Ejecutar la siguiente *query* para crear una tabla `american_customers` con el esquema adecuado:
    ```
    CREATE TABLE american_customers (
      customerID int,
      first_name varchar(10),
      last_name varchar(10),
      join_date varchar(10),
      street_address varchar(30),
      city varchar(10),
      state varchar(2),
      phone varchar(12)
    )
    ```
    ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-10.png)

10. Para acceder a los datos de S3 desde Redshift necesitamos el *Amazon Resource Name* (ARN) de el IAM *role* `LabRole` (estos permisos son creados de forma automática por el ambiente AWS Academy). En una nueva pestaña del navegador, copiar el ARN correspondiente:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-11.png)

11. Ejecutar la siguiente *query* para importar los datos de S3 en la tabla `american_customers`:
    ```
    COPY american_customers FROM 's3://iffe-mbd/data/lab1.csv'
    credentials 'aws_iam_role=<iam-role-arn>'
    IGNOREHEADER 1
    CSV
    ```
    ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-12.png)

12. Ejecutar un *preview* de la tabla para confirmar que los datos fueron correctamente importados:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/redshift-13.png)

## Desafíos

- Crear una nueva tabla `american_customers_norm` convirtiendo `join_date` de tipo de dato `varchar` a `date`
- Número de clientes registrados desde 2014

## *Clean up*

13. Borrar el clúster
