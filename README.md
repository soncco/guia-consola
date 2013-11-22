# Guía de la Consola de Linux

*Si te dices a ti mismo web developer y no sabes usar la consola, no eres un web developer*

## <a name="INDEX">Índice</a>

  1. [Introducción](#introduccion)
  2. [Ayuda](#ayuda)
  3. [Sistema de archivos](#archivos)
    - [Rutas relativas y absolutas](#rutas)
    - [Comandos básicos](#comandos)
    - [Búsqueda](#busqueda)
    - [Listado](#listado)
    - [Permisos](#permisos)
    - [Enlaces simbólicos](#enlaces)
  4. [Compresión de descompresión](#compresion)
  5. [Estado del sistema](#estado)
  6. [Editando archivos](#editar)
  7. [Introducción a SSH](#ssh)
  8. [Olvídate del FTP](#ftp)
  9. [Recursos](#recursos)

## <a name="introduccion">Introducción</a>

El ser desarrollador web el día de hoy requiere dominar herramientas básicas como la consola o terminal para ser más productivo.

Los sistemas UNIX proveen navitamente terminales con los cuales podemos hacer muchas de las operaciones que hacemos desde una GUI. 

Esta pequeña guía está enfocada a los comandos más usados por los desarrolladores web y también tiene la intención de ayudar a novatos a su uso.

**[[ Volver al índice ]](#INDEX)**

## <a name="ayuda">Ayuda</a>

Podemos obtener ayuda sobre un comando de las siguientes maneras:

  - ### Comando <code>man</code>

  ```bash
  $ man <comando>
  ```

  Muestra el manual del comando

  - ### Opción <code>--help</code>

  ```bash
  $ <comando> --help
  ```

  - ### Desde la web

  [Explain Shell](http://explainshell.com/), un sitio que permite explicar específicamente la mayoría de comandos.

**[[ Volver al índice ]](#INDEX)**

## <a name="archivos">Sistema de archivos</a>

Olvidémonos de C:, D:, E:, etc :)

  - ### <a name="rutas">Rutas relativas y absolutas</a>

  En Linux, si existe el usuario <code>braulio</code>, entonces también existe una carpeta en la ruta <code>/home/braulio</code>.

  Crearemos una carpeta dentro de <code>braulio</code> llamada <code>images</code>.

  Entonces podemos acceder a estas carpetas mediante:

  * #### Ruta absoluta

    ```bash
    # Para acceder a la carpeta images
    $ cd /home/braulio/images

    # Para acceder a la carpeta braulio
    $ cd /home/braulio

    # Para acceder a la carpeta home
    $ cd /home
    ```

    Donde el <code>/</code> inicial se refiere a la raiz del sistema de archivos.

  * #### Rutas relativas

    ```bash
    # Si estuviera en la carpeta /home/braulio, accedo a images con:
    $ cd images
    $ cd ~/images
    $ cd ./images

    # Si estoy en la carpeta /home/braulio/images regreso a la carpeta padre con:
    $ cd .. # /home/braulio

    # Y a la carpeta padre del padre con:
    $ cd ../.. # /home
    ```

    Donde:

    - El <code>~</code> significa la carpeta del usuario, es decir, /home/braulio.
    - El <code>.</code> se refiere a la carpeta en sí misma.
    - El <code>..</code> se refiere a la carpeta padre.

  **[[ Volver al índice ]](#INDEX)**

  - ### <a name="comandos">Comandos básicos</a>

  * #### Creación de archivos y directorios 

  ```bash
  # Creamos el archivo index.html
  $ touch index.html

  # Creamos el directorio logs
  $ mkdir logs

  # Creamos varios directorios
  $ mkdir media templates

  # Creamos directorios dentro de directorios, aunque no existan
  $ mkdir -p public/{images,css,js} # Crea el archivo public y dentro de este la carpeta images, css y js
  
  ```

  * #### Moverse entre directorios

  ```bash
  # Cambiar a cierto directorio
  $ cd <directorio>

  # Ir al directorio padre
  $ cd ..

  # Ir al directorio /home/braulio desde cualquier lugar
  $ cd ~
  $ cd

  # Ir al directorio raiz
  $ cd /
  ```

  * #### Listar directorios

  ```bash
  # Muestra carpetas y archivos en el directorio actual
  $ ls

  # Muestra carpetas y archivos en un directorio
  $ ls <directorio>

  # Muestra las carpetas y archivos incluyendo los ocultos, y los muestra en forma de columnas.
  $ ls -la

  # Similar al anterior en Ubuntu
  $ ll
  ```

  * #### Copiar, mover, renombrar, borrar
  ```bash
  # Copiar directorio
  $ cp braulio braulito
  # Ahora tengo dos directorios, uno llamado braulio y otro braulito

  # Copiar archivos
  $ cp index.html inicio.html
  # Ahora tengo dos archivos, uno llamado index.html y otro inicio.html

  # Copiar archivos dentro de un directorio a otro
  $ cp braulio/* otrodirectorio

  # Copiar sólo los archivos html
  $ cp braulio/*.html otrodirectorio

  # Renombra la carpeta braulito a brau
  $ mv braulito brau

  # Mueve la carpeta brau al directorio padre
  $ mv brau ..

  # Mueve la carpeta index que está en la carpeta padre a mi directorio actual
  $ mv ~/brau .

  # Si no funciona podemos usar el parámetro -f (Force)
  $ mv -f ~/brau .

  # Borra un archivo
  $ rm inicio.html

  # Borra los archivos .html
  $ rm *.html

  # Borra una carpeta
  $ rm -rf braulio
  ```

  * #### Para los curiosos

  ```bash
  # Ver mi directorio actual
  $ pwd

  # Ver el contenido de un archivo página por página
  $ less archivo.html
  # Después de verlo podemos salir presionando q

  # Concatenar el contenido de varios archivos y mostrarlos
  $ cat archivo.html estilo.css

  # Ver desde donde se ejecuta un comando
  $ which cat
  # /bin/cat

  # Ver como funciona cierto comando
  $ type ls
  # ls es un alias de 'ls --color=auto' (en Ubuntu)
  ```
