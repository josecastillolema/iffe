# Lab 2 - AWS EC2

## Creando la instancia
Usaremos la imagem oficial `Amazon Linux` para aprender algunos conceptos importantes de [**Amazon Elastic Computing**](https://aws.amazon.com/es/ec2/):
 - ***flavors***
 - ***security groups***
 - **[cloud-init](https://cloud-init.io/)**

1. Acceder al servicio **EC2**:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-01.png)

2. Lanzar el asistente de creación de instancias:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-02.png)

3. Escoger un nombre para la VM y la **imagem** `Amazon Linux 2 AMI`:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-03.png)

4. Escoger el ***flavor*** `t2.micro`:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-04.png)

5. Creación de una **llave SSH** para poder acceder a la instancia de forma segura:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-05.png)
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-06.png)

6. En ***Advanced details***, usaremos un *script* de **`cloud-init`** para personalizar la instancia:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-07.png)

7. Validar la instancia:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-08.png)


## Accediendo a la VM

8. [**Linux/MAC**] Seguimos las propias indicaciones de EC2:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-09.png)

    [**Windows**] Usaremos el cliente nativo de SSH (o si no está disponible [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) siguiendo estas [instrucciones](https://docs.aws.amazon.com/es_es/AWSEC2/latest/UserGuide/putty.html)). Como alternativa a PuTTy, [MobaXterm](https://mobaxterm.mobatek.net/) es una buena opción.

9. [**Linux/MAC**] En un terminal local:
    ```
    $ chmod 400 iffe.pem
    $ ssh -i "iffe.pem" ec2-user@ec2-34-207-181-0.compute-1.amazonaws.com

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

    https://aws.amazon.com/amazon-linux-2/
    [ec2-user@ip-172-31-50-1 ~]$
    ```

10. Una vez logado en la máquina virtual, confirmar que el script de **cloud-init** fue ejecutado:
    ```
    $ ls /tmp/
    cloudInitFunciona
    ```

## Instalando un servidor web

1.  Instalar el paquete `httpd`:
    ```
    [ec2-user@ip-172-31-50-1 ~]$ sudo yum install -y httpd
    Failed to set locale, defaulting to C
    Loaded plugins: extras_suggestions, langpacks, priorities, update-motd
    amzn2-core                                                                                                                     | 2.4 kB  00:00:00     
    Resolving Dependencies
    --> Running transaction check
    ---> Package httpd.x86_64 0:2.4.43-1.amzn2 will be installed
    --> Processing Dependency: httpd-tools = 2.4.43-1.amzn2 for package: httpd-2.4.43-1.amzn2.x86_64
    --> Processing Dependency: httpd-filesystem = 2.4.43-1.amzn2 for package: httpd-2.4.43-1.amzn2.x86_64
    --> Processing Dependency: system-logos-httpd for package: httpd-2.4.43-1.amzn2.x86_64
    --> Processing Dependency: mod_http2 for package: httpd-2.4.43-1.amzn2.x86_64
    --> Processing Dependency: httpd-filesystem for package: httpd-2.4.43-1.amzn2.x86_64
    --> Processing Dependency: /etc/mime.types for package: httpd-2.4.43-1.amzn2.x86_64
    --> Processing Dependency: libaprutil-1.so.0()(64bit) for package: httpd-2.4.43-1.amzn2.x86_64
    --> Processing Dependency: libapr-1.so.0()(64bit) for package: httpd-2.4.43-1.amzn2.x86_64
    --> Running transaction check
    ---> Package apr.x86_64 0:1.6.3-5.amzn2.0.2 will be installed
    ---> Package apr-util.x86_64 0:1.6.1-5.amzn2.0.2 will be installed
    --> Processing Dependency: apr-util-bdb(x86-64) = 1.6.1-5.amzn2.0.2 for package: apr-util-1.6.1-5.amzn2.0.2.x86_64
    ---> Package generic-logos-httpd.noarch 0:18.0.0-4.amzn2 will be installed
    ---> Package httpd-filesystem.noarch 0:2.4.43-1.amzn2 will be installed
    ---> Package httpd-tools.x86_64 0:2.4.43-1.amzn2 will be installed
    ---> Package mailcap.noarch 0:2.1.41-2.amzn2 will be installed
    ---> Package mod_http2.x86_64 0:1.15.3-2.amzn2 will be installed
    --> Running transaction check
    ---> Package apr-util-bdb.x86_64 0:1.6.1-5.amzn2.0.2 will be installed
    --> Finished Dependency Resolution

    Dependencies Resolved

    ======================================================================================================================================================
     Package                                  Arch                        Version                                   Repository                       Size
    ======================================================================================================================================================
    Installing:
     httpd                                    x86_64                      2.4.43-1.amzn2                            amzn2-core                      1.3 M
    Installing for dependencies:
     apr                                      x86_64                      1.6.3-5.amzn2.0.2                         amzn2-core                      118 k
     apr-util                                 x86_64                      1.6.1-5.amzn2.0.2                         amzn2-core                       99 k
     apr-util-bdb                             x86_64                      1.6.1-5.amzn2.0.2                         amzn2-core                       19 k
     generic-logos-httpd                      noarch                      18.0.0-4.amzn2                            amzn2-core                       19 k
     httpd-filesystem                         noarch                      2.4.43-1.amzn2                            amzn2-core                       23 k
     httpd-tools                              x86_64                      2.4.43-1.amzn2                            amzn2-core                       87 k
     mailcap                                  noarch                      2.1.41-2.amzn2                            amzn2-core                       31 k
     mod_http2                                x86_64                      1.15.3-2.amzn2                            amzn2-core                      146 k

    Transaction Summary
    ======================================================================================================================================================
    Install  1 Package (+8 Dependent packages)

    Total download size: 1.8 M
    Installed size: 5.1 M
    Downloading packages:
    (1/9): apr-util-1.6.1-5.amzn2.0.2.x86_64.rpm                                                                                   |  99 kB  00:00:00
    (2/9): apr-util-bdb-1.6.1-5.amzn2.0.2.x86_64.rpm                                                                               |  19 kB  00:00:00
    (3/9): apr-1.6.3-5.amzn2.0.2.x86_64.rpm                                                                                        | 118 kB  00:00:00
    (4/9): generic-logos-httpd-18.0.0-4.amzn2.noarch.rpm                                                                           |  19 kB  00:00:00
    (5/9): httpd-filesystem-2.4.43-1.amzn2.noarch.rpm                                                                              |  23 kB  00:00:00
    (6/9): httpd-2.4.43-1.amzn2.x86_64.rpm                                                                                         | 1.3 MB  00:00:00
    (7/9): httpd-tools-2.4.43-1.amzn2.x86_64.rpm                                                                                   |  87 kB  00:00:00
    (8/9): mailcap-2.1.41-2.amzn2.noarch.rpm                                                                                       |  31 kB  00:00:00
    (9/9): mod_http2-1.15.3-2.amzn2.x86_64.rpm                                                                                     | 146 kB  00:00:00
    ------------------------------------------------------------------------------------------------------------------------------------------------------
    Total                                                                                                                 6.2 MB/s | 1.8 MB  00:00:00
    Running transaction check
    Running transaction test
    Transaction test succeeded
    Running transaction
      Installing : apr-1.6.3-5.amzn2.0.2.x86_64                                                                                                       1/9
      Installing : apr-util-bdb-1.6.1-5.amzn2.0.2.x86_64                                                                                              2/9
      Installing : apr-util-1.6.1-5.amzn2.0.2.x86_64                                                                                                  3/9
      Installing : httpd-tools-2.4.43-1.amzn2.x86_64                                                                                                  4/9
      Installing : generic-logos-httpd-18.0.0-4.amzn2.noarch                                                                                          5/9
      Installing : mailcap-2.1.41-2.amzn2.noarch                                                                                                      6/9
      Installing : httpd-filesystem-2.4.43-1.amzn2.noarch                                                                                             7/9
      Installing : mod_http2-1.15.3-2.amzn2.x86_64                                                                                                    8/9
      Installing : httpd-2.4.43-1.amzn2.x86_64                                                                                                        9/9
      Verifying  : apr-util-1.6.1-5.amzn2.0.2.x86_64                                                                                                  1/9
      Verifying  : apr-util-bdb-1.6.1-5.amzn2.0.2.x86_64                                                                                              2/9
      Verifying  : httpd-2.4.43-1.amzn2.x86_64                                                                                                        3/9
      Verifying  : mod_http2-1.15.3-2.amzn2.x86_64                                                                                                    4/9
      Verifying  : httpd-filesystem-2.4.43-1.amzn2.noarch                                                                                             5/9
      Verifying  : apr-1.6.3-5.amzn2.0.2.x86_64                                                                                                       6/9
      Verifying  : mailcap-2.1.41-2.amzn2.noarch                                                                                                      7/9
      Verifying  : generic-logos-httpd-18.0.0-4.amzn2.noarch                                                                                          8/9
      Verifying  : httpd-tools-2.4.43-1.amzn2.x86_64                                                                                                  9/9

    Installed:
      httpd.x86_64 0:2.4.43-1.amzn2

    Dependency Installed:
      apr.x86_64 0:1.6.3-5.amzn2.0.2                      apr-util.x86_64 0:1.6.1-5.amzn2.0.2              apr-util-bdb.x86_64 0:1.6.1-5.amzn2.0.2
      generic-logos-httpd.noarch 0:18.0.0-4.amzn2         httpd-filesystem.noarch 0:2.4.43-1.amzn2         httpd-tools.x86_64 0:2.4.43-1.amzn2
      mailcap.noarch 0:2.1.41-2.amzn2                     mod_http2.x86_64 0:1.15.3-2.amzn2

    Complete!
    ```

2.  Habilitar el servicio `httpd`:
    ```
    [ec2-user@ip-172-31-50-1 ~]$ sudo service httpd start
    Redirecting to /bin/systemctl start httpd.service
    ```

3.  Crear un *website* de teste, en el archivo `/var/www/html/index.html` (como usuário *admin*):
    ```
    <h1>
       IFFE o/ !!!
    </h1>
    ```

4.  Testar localmente el servidor web:
    ```
    [ec2-user@ip-172-31-50-1 ~]$ curl localhost
    <h1>
        IFFE i/ !!!
    </h1>
    ```

5.  Obtener el IP público da la VM:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-08.png)

6.  Testar el acceso por el IP público (no debería funcionar):
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-12.png)

7.  Como era esperado, el acesso web no funciona porque la puerta HTTP (TCP/80) debe ser liberada en los *security groups* de la VM. Incluir una regla para esta puerta en el *security group* asociado a la instancia:
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-10.png)
   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-11.png)

8. Intentar acceder nuevamente:

   ![](https://raw.githubusercontent.com/josecastillolema/iffe/main/img/ec2-13.png)
