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
 
1. Accedar al servicio **S3**:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-01.png)

2. Crear un nuevo *bucket*:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-02.png)

3. Escoger un nombre para el *bucket*. El nombre debe ser único globalmente:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-03.png)

7. Confirmar la creación del *bucket* y comprobar que fue correctamente creado:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/s3-04.png)

## Criação do objeto

8. Fazer o *upload* de uma imagem qualquer:
   ![](https://raw.githubusercontent.com/josecastillolema/fiap/master/shift/multicloud/img/s3-10.png)

9. Habilitar accesso público no objeto:
   ![](https://raw.githubusercontent.com/josecastillolema/fiap/master/shift/multicloud/img/s3-11.png)

10. Seleccionar o *tier* `Standard`:
   ![](https://raw.githubusercontent.com/josecastillolema/fiap/master/shift/multicloud/img/s3-12.png)

11. Confirmar a criação do objeto:
   ![](https://raw.githubusercontent.com/josecastillolema/fiap/master/shift/multicloud/img/s3-13.png)

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
