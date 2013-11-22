# Guía de la Consola de Linux

*Si te dices a ti mismo web developer y no sabes usar la consola, entonces no eres un web developer.*

## <a name="INDEX">Índice</a>

  1. [Introducción](#introduccion)
  1. [Ayuda](#ayuda)
  1. [Sistema de archivos](#archivos)
    - [Rutas relativas y absolutas](#rutas)
    - [Comandos básicos](#comandos)
    - [Listar directorios](#listado)
    - [Búsqueda](#busqueda)
    - [Permisos](#permisos)
    - [Enlaces simbólicos](#enlaces)
  1. [Compresión y descompresión de archivos](#compresion)
  1. [Editando archivos](#editar)
  1. [Introducción a SSH](#ssh)
  1. [Olvídate del FTP](#ftp)
  1. [Recursos](#recursos)

## <a name="introduccion">Introducción</a>

El ser desarrollador web el día de hoy requiere dominar herramientas básicas como la consola o terminal para ser más productivo.

Los sistemas UNIX proveen navitamente terminales con los cuales podemos hacer muchas de las operaciones que hacemos desde una GUI. 

Esta pequeña guía está enfocada a los comandos más usados por los desarrolladores web y también tiene la intención de ayudar a novatos a su uso.

**[[ Volver al índice ]](#INDEX)**

## <a name="ayuda">Ayuda</a>

Podemos obtener ayuda sobre un comando de las siguientes maneras:

### Comando <code>man</code>

  ```bash
  # Muestra el manual del comando
  $ man <comando>
  ```

### Opción <code>--help</code>

  ```bash
  # Muestra la ayuda del comando
  $ <comando> --help
  ```

### Desde la web

[Explain Shell](http://explainshell.com/), un sitio que permite explicar específicamente la mayoría de comandos.

**[[ Volver al índice ]](#INDEX)**

## <a name="archivos">Sistema de archivos</a>

Olvidémonos de C:, D:, E:, etc :)

### <a name="rutas">Rutas relativas y absolutas</a>

En Linux, si existe el usuario <code>braulio</code>, entonces también existe una carpeta en la ruta <code>/home/braulio</code>.

Crearemos una carpeta dentro de <code>braulio</code> llamada <code>images</code>.

Entonces podemos acceder a estas carpetas mediante:

#### Ruta absoluta

  ```bash
  # Para acceder a la carpeta images
  $ cd /home/braulio/images

  # Para acceder a la carpeta braulio
  $ cd /home/braulio

  # Para acceder a la carpeta home
  $ cd /home
  ```

Donde el <code>/</code> inicial se refiere a la raiz del sistema de archivos.

#### Rutas relativas

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

### <a name="comandos">Comandos básicos</a>

#### Creación de archivos y directorios

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

#### Moverse entre directorios

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

#### Copiar, mover, renombrar, borrar

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

#### Descarga de archivos

  ```bash
  # Descargar un archivo usando wget
  $ wget http://nodejs.org/dist/v0.10.22/node-v0.10.22.tar.gz

  # Descargar un archivo usando curl
  $ curl http://nodejs.org/dist/v0.10.22/node-v0.10.22.tar.gz
  ```

 * #### Para los curiosos

  ```bash
  # Ver el espacio ocupado en la carpeta actual
  $ du

  # Lo mismo pero para humanos
  $ du -hs

  # Ver el tamaño de cierto archivo
  $ du -hs index.html

  # Ver de cierta carpeta
  $ du -hs braulio

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

  # Ver todos los comandos que he escrito desde el inicio de los tiempos
  $ less ~/.bash_history
  ```

**[[ Volver al índice ]](#INDEX)**

### <a name="listado">Listar directorios</a>

  ```bash
  # Muestra carpetas y archivos en el directorio actual
  $ ls

  # Muestra carpetas y archivos en un directorio
  $ ls <directorio>

  # Muestra las carpetas y archivos incluyendo los ocultos, y los muestra en forma de columnas.
  $ ls -la

  # Similar al anterior en Ubuntu
  $ ll

  # Puedes crear tu propio comando con
  $ alias myll='ls -la'

  # Y lo usas con
  $ myll

  # Ver la salida anterior mostrando cierto patrón
  $ ll | grep html
  # Muestra la lista resaltando todos los que contienen el string html en su nombre

  # Guardar la salida a un archivo
  $ ll > listado1.txt
  # Se crea un archivo listado1.txt con la salida de ll
   ```

**[[ Volver al índice ]](#INDEX)**

### <a name="busqueda">Búsqueda</a>

  ```bash
  # Muestra todos los archivos y carpetas recursivamente dentro del directorio actual
  $ find

  # Lo mismo pero más complicado
  $ find .

  # Muestra recursivamente solo los archivos que tengan .html en la carpeta actual
  $ find . -name \*.html

  # Lo mismo
  $ find . -name '*.html'

  # Lo mismo pero con grep
  $ find . | grep .html

  # Lo mismo pero en otra carpeta
  $ find <otracarpeta> | grep .html

  # El comando locate guarda una base de datos de todos los archivos y carpetas que tenemos, actualiza estos cada cierto tiempo
  # Para actualizarlo ahora mismo

  $ updatedb

  # Para encontrar cierto archivo o carpeta con el nombre brau
  $ locate brau
  ```

**[[ Volver al índice ]](#INDEX)**

### <a name="permisos">Permisos</a>

Si usamos el listado en esta carpeta lo que encontremos es:

  ```bash
  drwxr-xr-x  3 brau brau  4096 nov 22 09:35 ./
  drwxrwxr-x 33 brau brau  4096 nov 21 23:13 ../
  drwxrwxr-x  8 brau brau  4096 nov 22 10:18 .git/
  -rw-rw-r--  1 brau brau 11325 nov 21 23:13 LICENSE
  -rw-rw-r--  1 brau brau  6920 nov 22 10:18 README.md
  ```

Vemos 7 columnas las cuales indican:

  1. Permisos
  1. Directorios
  1. Usuario
  1. Grupo
  1. Tamaño en bytes
  1. Fecha de modificación
  1. Archivo o directorio

Tomando la primera columna la dividimos en cuatro subcolumnas y las separamos por <code>|</code> para explicarlo mejor, en el caso del archivo README.md

  ```bash
  -|rw-|rw-|r--
  ```

  - La primera columna muestra <code>-</code> y nos indica que <code>README.md</code> es un archivo, caso contrario sería un directorio y mostraría <code>d</code>.

  - La segunda columna muestra <code>rw-</code> y nos indica que este archivo tiene permisos de lectura (r), de escritura (w), mas no de ejecución(x) **por parte del usuario**.

  - La tercera columna muestra <code>rw-</code> y nos indica que este archivo tiene permisos de lectura (r), de escritura (w), mas no de ejecución(x) **por parte del grupo**.

  - La tercera columna muestra <code>r-</code> y nos indica que este archivo tiene permisos de lectura (r), mas no de escritura (w) ni de ejecución(x) **por parte de otros**.

#### Cambiando permisos

Cada permiso está representado por un número de la siguiente manera:

  - Read (r) vale 4
  - Write (w) vale 2
  - Execute (x) vale 1

Sabiendo esto puedo cambiar los permisos del archivo index.html:

  ```bash
  # Cambiando los permisos de index.html
  $ chmod 775 index.html
  ```

Donde:
- El primer 7 viene de <code>4+2+1</code>, es decir, que <code>index.html</code> tiene permisos de <code>rwx</code> para el usuario.
- Igual que el anterior pero para el grupo.
- El 5 viene de <code>4+1</code>, es decir, que <code>index.html</code> tiene permisos de <code>r-x</code> para otros.

Para los directorios:

  ```bash
  # Cambiando los permisos de la carpeta braulio
  $ chmod 444 braulio
  # Ahora la carpeta braulio es de sólo lectura.

  # Cambiando los permisos de la carpeta Braulio y de todo su contenido recursivamente
  $ chmod -R 444 braulio 
  ```

#### Cambiando de propietario y grupo

  ```bash
  # index.html pertenecía al usuario brau, ahora pertenecerá al usuario deicy
  $ chown deicy index.html

  # index.html pertenecía al grupo brau, ahora pertenecerá al grupo deicy
  $ chgrp deicy index.html

  # Juntando ambos comandos
  $ chown deicy:deicy index.html
  ```

### Cambiando de usuario

  ```bash
  # Estoy con el usuario braulio, y quiero usar el usuario deicy
  $ su deicy

  # Quiero ejecutar los comandos como root
  $ sudo mkdir carpeta
  # Crea una carpeta como superman
  ```

**[[ Volver al índice ]](#INDEX)**

### <a name="enlaces">Enlaces simbólicos</a>

Los enlaces simbólicos sirven para tener una referencia a un archivo o carpeta y acceder a esta sin tener que ir a la ruta.

El ejemplo más básico lo vemos en los hostings que usan CPanel, donde encontramos la carpeta <code>public_html</code> y el enlace simbólico <code>www</code>, si entramos a ambos, veremos el mismo contenido.

  ```bash
  # Creamos el enlace simbólico <code>www</code> para <code>public_html</code>
  $ ln -ls ~/public_html www
  ```

**[[ Volver al índice ]](#INDEX)**

## <a name="compresion">Compresión y descompresión de archivos</a>