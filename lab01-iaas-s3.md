# Lab 1 - AWS S3

Todas las soluciones de *big data* comienzan con el almacenamiento de datos. Este es el primer paso en el *pipeline* de *big data*. [Amazon Simple Storage Service](https://docs.aws.amazon.com/es_es/s3/index.html?id=docs_gateway#lang/es) (Amazon S3) es uno de los servicios más utilizados para almacenar datos.

En este laboratorio, practicaremos el uso de la consola de administración de AWS para crear un *bucket* de S3. Luego cargaremos archivos en Amazon S3 y ejecutaremos consultas simples sobre los datos.

## Objetivos
 - Familiarizarse con S3 en la consola de administración de AWS
 - Crear un *buckets* en S3
 - Cargar datos (objetos) en un *bucket*
 - Hacer consultas SQL en *buquets*
 - Control de permisos de accesso
 - Alojamiento de sitios web estáticos

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

9. Conprobar la creación del objeto:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-07.png)
   
#### Cambio de clase de almacenamiento

10. En la pestaña de **Propiedades** del objecto, cambiar la clase de almacenamiento de *Standard* para *Intelligent-Tiering*:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-08.png)

#### Acceso público

11. Habilitar las *Access Control List* (ACLs) en la pestaña de **Permisos** del *bucket*:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-09.png)

12. En la misma pestaña, habilitar acceso público:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-10.png)
   
13. En la pestaña de Permisos del objeto, habilitar accesso público:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-11.png)

14. Confirmar el accesso público a la imagen mediante la URL del objeto:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-12.png)
   
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-13.png)


### Datos con acceso privado



12. Conferir que o objeto foi criado:
   ![](https://raw.githubusercontent.com/josecastillolema/fiap/master/shift/multicloud/img/s3-14.png)

13. Na descrição do objeto, podemos obter a url do mesmo:

    |          | bucket-name |                   | objeto        |
    |----------|-------------|-------------------|-------------- |
    | https:// | fiap-mba    | .s3.amazonaws.com | sicmundus.jpg |

   ![](https://raw.githubusercontent.com/josecastillolema/fiap/master/shift/multicloud/img/s3-15.png)    

14. Accessar a imagem pela URL do objeto:
   ![](https://raw.githubusercontent.com/josecastillolema/fiap/master/shift/multicloud/img/s3-16.png)    


## Hospedagem de sites estáticos
    
15. Alterar a configuração do bucket para permitir o armazenamento de sites estáticos:
   ![](https://raw.githubusercontent.com/josecastillolema/fiap/master/shift/multicloud/img/s3-17.png)    

16. Introducir o nome do arquivo `html` principal:
   ![](https://raw.githubusercontent.com/josecastillolema/fiap/master/shift/multicloud/img/s3-18.png)    

17. Fazer *upload* do arquivo [`index.html`](https://github.com/josecastillolema/fiap/blob/master/shift/multicloud/lab05-iaas-s3/index.html) (ou de qualquer outro arquivo `html`) com permissão de accesso público, como descrito na [criação de objeto](#criação-do-objeto)

17. A URL no modo armazenamento de sites estáticos apresenta um novo formato:

    |          | bucket-name |            | region    |               |
    |----------|-------------|------------|---------- | --------------|
    | https:// | fiap-mba    | s3-website | us-east-1 | amazonaws.com |

18. Acessar o site pela nova URL do *bucket*:
   ![](https://raw.githubusercontent.com/josecastillolema/fiap/master/shift/multicloud/img/s3-19.png)    
