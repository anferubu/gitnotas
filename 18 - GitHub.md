# GitHub

## Crear repositorio

Desde el perfil de usuario en *GitHub* es posible crear un repositorio. Para esto se pulsa sobre `New repository`, esto abre un formulario cuyo único campo obligatorio es el nombre del proyecto. Después se pulsa sobre `Create repository` y listo, se habrá creado el repositorio remoto en *GitHub*, con el nombre `[user]/[project]`.

Una buena práctica consiste en agregar un archivo `README.md`, el cual explique el contenido del repositorio al público en general.



![](/home/anfeterol/Documents/informatica/git/img/new_repository.png)

![](/home/anfeterol/Documents/informatica/git/img/create_repository.png)



## Trabajar con colaboradores

Si se va a trabajar con otras personas y se quiere dar acceso de escritura (*push*), se debe añadirlas como colaboradores. 

Para esto se presiona en el menú `Settings` del repositorio, luego se selecciona `Manage access` del menú de la izquierda y luego en `Invite a collaborator`. Ahora, simplemente se debe escribir el usuario (o e-mail) y pulsar en `Select a collaborator above`. Esto se repite las veces que se necesite para sar acceso a otras personas. Para quitar el acceso, simplemente se pulsa en la `x` del lado derecho del usuario.

![](/home/anfeterol/Documents/informatica/git/img/settings.png)

![](/home/anfeterol/Documents/informatica/git/img/invite_collaborator.png)



## Participar en un proyecto existente

También es posible participar en un proyecto existente, en donde no se tengan permisos de escritura. El proyecto se puede bifurcar (*crear un fork*), es decir, se crea una copia completa del repositorio ajeno en el propio perfil de *GitHub*, la cual a su vez se clona localmente, se crea una rama y se realizan cambios sobre el código fuente para luego enviar dichos cambios de nuevo a *GitHub*.

Para bifurcar un proyecto, se debe visitar la página del mismo y pulsar sobre el botón `fork` ubicado en la parte superior derecha de la ventana. Esto redireccionará a una página nueva del proyecto, en tu cuenta y con tu propia copia del código fuente. De esta forma, los proyectos no necesitan añadir colaboradores con acceso de escritura.

Las personas pueden bifurcar un proyecto, enviar sus propios cambios a su copia y luego remitir esos cambios al repositorio original para su aprobación, creando lo que se llama un `Pull request` (*una fusión de los repositorios*).

Después de modificar el *fork*, se pulsa sobre `Create pull request`, se abre una página que permite añadir un título y una descripción, después de pulsar de nuevo sobre `Create pull request`, el propietario del proyecto bifurcado recibirá una notificación de que alguien sugiere un cambio, junto a un enlace con toda la información.

Al recibir el `pull request`, el propietario puede revisar y comentar el cambio sugerido, rechazarlo o bien incorporarlo presionando sobre `Merge pull request` para fusionar los cambios. Luego es posible eliminar la rama secundaria, pues ya todos los archivos son iguales al de la rama principal.

En resumen, en *GitHub*, el flujo de trabajo está centrado en las solicitudes de integración `pull request`. El funcionamiento habitual es:

-   Se crea una rama a partir de master.
-   Se realizan algunos *commits* hacia esa rama.
-   Se envía esa rama hacia la copia (*fork*) del proyecto.
-   Se abre un Pull Request en GitHub.
-   Se participa en la discusión asociada y opcionalmente, se realizan nuevos *commits*.
-   El propietario del proyecto original cierra el `Pull request`, bien fusionando su rama con los otros cambios o bien rechazándolos.



## Sitio web público con *GitHub pages*

En el sitio [GitHub pages](https://pages.github.com/) se explica muy bien cómo crear una página web. Primero, se crea un repositorio público cuyo nombre sea `[user].github.io`. Luego se clona y localmente se crea un archivo `index.html`. 

Después de preparar, confirmar y enviar los cambios de nuevo al repositorio remoto, se puede ingresar al sitio web a través de `https://[user].github.io`.



![](/home/anfeterol/Documents/informatica/git/img/github_pages.png)



~~~powershell
# se clona el repositorio
$ git clone https://github.com/ferudasel/ferudasel.github.io

# se entra en el directorio del proyecto y se añade index.html
$ cd ferudasel.github.io
$ echo "Hello World" > index.html

# se preparan, confirman y envían los cambios al repositorio remoto
$ git add --all
$ git commit -m "Initial commit"
$ git push -u origin main
~~~



Hay que asegurarse de que esté seleccionada la opción `master branch` en el menú `Settings > Pages > Source`  del repositorio.



## Configurar llaves SSH en local

El *protocolo SSH* (*Secure Shell*) tiene como función principal el acceso remoto a un servidor por medio de una canal seguro en el que toda la información está cifrada.

Para generar llaves SSH para un usuario, se utiliza el comando `ssh-keygen -t rsa -b 4096 -C ["e-mail"]`.

En el siguiente ejemplo, ubicado en el directorio `home/` se genera la llave SSH. Es posible especificar la carpeta donde se guardarán las claves y agregar otra clave más (*passphrase*).

En la carpeta `.sh/` se tienen dos ficheros: la clave privada `id_rsa` y la clave pública `id_rsa.pub`.

~~~powershell
$ ssh-keygen -t rsa -b 4096 -C "anferubu@gmail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/Andrés F.  Ruiz/.ssh/id_rsa):
Created directory '/c/Users/Andrés F.  Ruiz/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/Andrés F.  Ruiz/.ssh/id_rsa.
Your public key has been saved in /c/Users/Andrés F.  Ruiz/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:4hLP8ce1AigLC5DRBmTZh1GnQ0XJMLZBBV5aLwEK5Jc anferubu@gmail.com
The key's randomart image is:
+---[RSA 4096]----+
|=Bo.=@OO.        |
|o++o*.Xoo        |
|oo E.* . .       |
|. .   ...        |
|. . o + S   .    |
| . o B + o . .   |
|  . o + . + .    |
|     .   . .     |
|                 |
+----[SHA256]-----+
~~~



El comando `eval $(ssh-agent -s)` permite comprobar que el servidor de claves esté corriendo en el sistema operativo.

En el siguiente ejemplo, `Agent` significa que el servidor SSH está corriendo y `pid 6892` es el identificador del proceso (*Process ID*).

~~~powershell
$ eval $(ssh-agent -s)
Agent pid 6892
~~~



Para agregar la llave privada al entorno del sistema operativo se escribe `ssh-add ~/.ssh/id_rsa`, asumiendo que la carpeta que contiene las claves está en `home/`. Recuerde que al añadir la llave privada, debe ingresar la contraseña (*passphrase*).

~~~powershell
$ ssh-add ~/.ssh/id_rsa
Enter passphrase for /c/Users/Andrés F.  Ruiz/.ssh/id_rsa:
Identity added: /c/Users/Andrés F.  Ruiz/.ssh/id_rsa (anferubu@gmail.com)
~~~



## Conexión a GitHub con SSH

En GitHub hay que ir a la opción `Settings > SSH and GPG keys > New SSH key`. En `title` se agrega una descripción que indique a qué pertenece dicha llave, y en `key` se pega el contenido del fichero `id_rsa.pub`. Luego se presiona sobre `Add SSH key`.

Ahora es posible clonar el repositorio utilizando SSH. De esta manera, con una llave SSH es posible comunicarse de forma segura y sin necesidad de escribir un usuario y contraseña todo el tiempo.