# Lab 5 - Amazon SageMaker

Como analista de datos, a menudo es necesario crear documentos que combinan texto con imágenes para análisis. Los ***Jupyter notebooks*** son una herramienta de código abierto que puede usarse para crear este tipo de narrativas. Con [Amazon SageMaker](https://aws.amazon.com/es/sagemaker/) se pueden crear rápidamente *notebooks* para realizar análisis y alojar las correspondientes presentaciones. SageMaker es un servicio completamente administrado que está diseñado para analistas de datos que crean sistemas de aprendizaje automático.

Existen muchas herramientas de código abierto diferentes para visualizar los datos (por ej. [Bokeh](https://docs.bokeh.org/)). Estas herramientas permiten crear *notebooks* que combinan los datos con una representación visual del análisis. En este laboratorio, crearemos un *notebook* en SageMaker a partir de datos almacenados en S3.

![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/sagemaker-00.png)

## Objetivos
 - Creación de *Jupyter notebooks* con SageMaker
 - Importación de datos de S3


## Índice
- [Lab 5 - Amazon SageMaker](#lab-5---amazon-sagemaker)
  - [Objetivos](#objetivos)
  - [Índice](#índice)
  - [Prerrequisitos](#prerrequisitos)
  - [Creación del *notebook*](#creación-del-notebook)
  - [Acceso al *notebook*](#acceso-al-notebook)
  - [Importación de datos de S3](#importación-de-datos-de-s3)
  - [Desafíos](#desafíos)
  - [*Clean up*](#clean-up)

## Prerrequisitos
 
- Un *bucket* con [este archivo `.csv`](https://github.com/josecastillolema/iffe/blob/main/lab01-iaas-s3/lab1.csv)
- El archivo `.csv` debe estar dentro de un directório cualquiera en el *bucket* y no en la raíz del mismo (por ejemplo `data`):
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/athena-01.png)

## Creación del *notebook*

1. Acceder al servicio **SageMaker AI**:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/sagemaker-01.png)

2. Crear un nuevo *notebook*: **Notebook** -> **Notebook instances** -> **Create notebook instance**:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/sagemaker-02.png)

   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/sagemaker-03.png)

3. Escoger un nombre para el *notebook* y `ml.t3.medium` como *flavor*:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/sagemaker-04.png)

4. Definir `LabRole` como IAM *role*. Estos permisos son creados de forma automática por el ambiente AWS Academy:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/sagemaker-05.png)

5. Confirmar la creación del *notebook* y esperar a que se encuentre disponible:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/sagemaker-06.png)

## Acceso al *notebook*

6. Entrar en el ambiente Jupyter recién creado usando la opción **Open Juypter** y crear un nuevo *notebook* de tipo `conda_python3`:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/sagemaker-07.png)

## Importación de datos de S3

7. Ejecutar los siguientes comandos para importar [este archivo `.csv`](https://github.com/josecastillolema/iffe/blob/main/lab01-iaas-s3/lab1.csv) desde el *notebook*:

    ```
    import pandas as pd

    df = pd.read_csv('s3://iffe-mbd/data/lab1.csv')
    ```
    ```
    df
    ```
    ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/sagemaker-08.png)

## Desafíos

- Prueba alguna visualización usando [Bokeh](https://docs.bokeh.org/). Intenta hacer un histograma de clientes por estado.
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/sagemaker-09.png)


## *Clean up*

8. Borrar el *notebook*
