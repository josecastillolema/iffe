# Lab 3 - AWS Glue

Los problemas de Big Data a menudo involucran una gran cantidad de fuentes de datos heterogéneas. Es posible que en algunas situaciones el esquema de algunas fuentes de datos no sea conocido. Este es el aspecto de variedad de las cinco V de big data (Volumen, **Variedad**, Velocidad, Veracidad y Valor).

[AWS Glue](https://aws.amazon.com/es/glue/) puede importar una fuente de datos e inferir un esquema en función de los tipos de datos que descubre, creando un catálogo que contiene metadatos sobre las distintas fuentes de datos. Glue es parecido a Athena en el sentido en que los datos reales que analiza permanecen en la fuente de datos (S3 en nuestro ejemplo). La diferencia clave es que puede crear un rastreador (*crawler*) con AWS Glue para descubrir de forma automática el esquema.

AWS Glue se integra con las siguientes fuentes de datos:
 - Amazon Athena
 - Amazon Redshift
 - Amazon EMR

![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/glue-00.png)

## Objetivos
 - Familiarizarse con Glue en la consola de administración de AWS
 - Crear tablas importando datos de S3 descubriendo atomáticamente su esquema
 - Crear rastreadores (*crawlers*)
 - Consultar datos en S3 desde Athena con el catálogo de datos de AWS Glue

## Índice
- [Lab 3 - AWS Glue](#lab-3---aws-glue)
  - [Objetivos](#objetivos)
  - [Índice](#índice)
  - [Prerequisitos](#prerequisitos)
  - [Creación del *crawler*](#creación-del-crawler)
  - [Visualización de los datos importados desde Athena](#visualización-de-los-datos-importados-desde-athena)
  - [Desafios](#desafios)
  - [Clean up](#clean-up)

## Prerequisitos
 
- Un *bucket* de S3 para almacenar los resultados de Athena
- Otro *bucket* (puede ser el mismo) con [este archivo `.csv`](https://github.com/josecastillolema/iffe/blob/main/lab01-iaas-s3/lab1.csv)
- El archivo `.csv` debe estar dentro de un directório cualquiera en el *bucket* y no en la raíz del mismo (por ejemplo `data`):
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/athena-01.png)

## Creación del *crawler*

1. Acceder al servicio **Glue**:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/glue-01.png)

2. Crear una nueva tabla usando la opción ***Add tables using crawler***:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/glue-02.png)

3. En el primer paso, escoger un nombre para el *crawler*:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/glue-03.png)

4. En el segundo paso, configurar S3 como fuente de datos apuntando para el directório del bucket que contiene el [archivo .`csv`]((https://github.com/josecastillolema/iffe/blob/main/lab01-iaas-s3/lab1.csv)):
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/glue-04.png)

5. En el tercer paso, definir `LabRole` como IAM *role*. Estos permisos son creados de forma automática por el ambiente AWS Academy:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/glue-05.png)

6. En el cuarto paso, escoger la base de datos y el prefijo de la tabla que será creada al importar los datos. En este paso es posible también definir la frecuencia con la qual rodar el *crawler* (por demanda, diariamente, etc.):
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/glue-06.png)
   
7. Una vez creado el *crawler*, ejecutarlo usando la opción ***Run crawler*** y aguardar a que termine:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/glue-07.png)

8. Una nueva tabla (`imported_data`) debería estar disponíble en la pestaña de tablas (puede ser necesário hacer un *refresh* para que aparezca):
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/glue-08.png)

## Visualización de los datos importados desde Athena

9. La nueva tabla importada nos da la opción de visualizar los datos en Athena. Nótese que en la sección inferior podemos ver el esquema que fue automáticamente extraído a partir de los datos:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/glue-09.png)

10. En Athena podemos hacer un _preview_ de los datos para confirmar que fueron correctamente importados:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/glue-10.png)

## Desafios

 - En Athena, recuperar la lista de *Customer IDs* y *Last Names*

## Clean up

11.   Borrar la base de datos y las tablas creadas
