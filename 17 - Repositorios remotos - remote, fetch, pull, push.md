# Repositorios remotos con Git



Colaborar con otras personas implica gestionar repositorios remotos, que no son más que versiones del proyecto alojadas en internet, con permisos de lectura o lectura-escritura.

## Ver repositorios remotos

El comando `git remote` muestra los nombres de los repositorios remotos que se tienen configurados. La opción `-v` muestra las *URLs* que Git ha asociado al nombre y que serán usadas para leer (*fetch*) y escribir (*push*) en dicho repositorio remoto.

`origin` es el nombre por defecto que recibe el repositorio que ha sido clonado.

~~~powershell
$ git remote -v
defunkt https://github.com/defunkt/grit (fetch)
defunkt https://github.com/defunkt/grit (push)
koke git://github.com/koke/grit.git (fetch)
koke git://github.com/koke/grit.git (push)
origin git@github.com:mojombo/grit.git (fetch)
origin git@github.com:mojombo/grit.git (push)
~~~

## Añadir repositorios remotos

El comando `git remote add [name] [url]` permite añadir un repositorio remoto nuevo y asociarlo a un nombre que se pueda referenciar fácilmente.

~~~powershell
$ git remote
origin

$ git remote add pb https://github.com/paul/ticgit

$ git remote -v
origin https://github.com/schacon/ticgit (fetch)
origin https://github.com/schacon/ticgit (push)
pb https://github.com/paul/ticgit (fetch)
pb https://github.com/paul/ticgit (push)
~~~

## Traer datos y combinar repositorios remotos

El comando `git fetch [remote]` permite obtener datos de un repositorio remoto. Trae todos los nuevos datos que aún no se tienen en el repositorio local, pero no los combina con el trabajo local, para esto, se debe fusionar manualmente.

El comando `git pull [remote]` trae y combina el repositorio remoto con el local. La instrucción `git pull origin master --allow-unrelated-histories` permite traer datos del repositorio remoto, así no se tengan *commits* en común.

Cuando se descargan nuevas ramas remotas, no se obtiene automáticamente una copia local editable de las mismas. Para esto se usa `git checkout -b [branch] [remoteBranch]` que crea y salta a una rama local que hace seguimiento a la rama remota.

~~~powershell
$ git fetch pb
remote: Counting objects: 43, done.
remote: Compressing objects: 100% (36/36), done.
remote: Total 43 (delta 10), reused 31 (delta 5)
Unpacking objects: 100% (43/43), done.
From https://github.com/paul/ticgit
* [new branch] master -> pb/master
* [new branch] ticgit -> pb/ticgit
~~~

## Enviar datos al repositorio remoto

El comando `git push [remote] [branch]` permite compartir un proyecto si se tienen permisos de escritura, al enviar todos los *commits* de una rama local al servidor remoto. Mientras que `git push [remote] [branch]:[otherName]` envía una rama local a una rama remota con un nombre distinto. Si la rama no existe en el repositorio remoto, la crea.

Si han habido nuevos cambios en el repositorio remoto y se desea enviar otra información, primero se debe descargar la nueva información y luego la rama remota con la local. Después de esto si es posible subir los cambios al repositorio remoto.

Por lo anterior, una buena práctica es siempre hacer primero `git pull` antes de subir nuevos cambios.

~~~powershell
$ git push origin master
~~~

## Inspeccionar un repositorio remoto

El comando `git remote show [remote]` muestra información detallada acerca de un repositorio remoto en particular, como por ejemplo la *URL* de dicho repositorio y la información del rastreo de ramas.

~~~powershell
$ git remote show origin
* remote origin
Fetch URL: https://github.com/schacon/ticgit
Push URL: https://github.com/schacon/ticgit
HEAD branch: master
Remote branches:
master tracked
dev-branch tracked
Local branch configured for 'git pull':
master merges with remote master
Local ref configured for 'git push':
master pushes to master (up to date)
~~~

## Eliminar y renombrar repositorios remotos

El comando `git remote rename [name] [newName]` permite renombrar un repositorio remoto. Por otro lado, el comando `git remote rm [remote]` elimina el repositorio remoto.

En el siguiente ejemplo, se cambia el nombre del repositorio remoto `pb` por `paul`. Al hacer esto también cambia el nombre de las ramas remotas (`pb/master` a `paul/master`). Al final, dicho repositorio remoto se elimina.

~~~powershell
$ git remote rename pb paul

$ git remote
origin
paul

$ git remote rm paul

$ git remote
origin
~~~

## Eliminar una rama remota del repositorio

El comando `git push [remote] --delete [remoteBranch]` permite eliminar una rama remota del repositorio remoto.



## Ramas remotas de seguimiento

Las ramas remotas son marcadores que indican el estado en que se encontraba el repositorio remoto la última vez que se conectó a él. Se mueven automáticamente al establecer comunicación en la red. 

Estas ramas remotas se referencian como `[remote]/[branch]`. Por ejemplo, la rama `origin/master`, la cual es distintas de la rama `master` local.

Al clonar un repositorio, la rama local hace seguimiento a la rama remota del mismo nombre, apuntando al mismo sitio. Pero con los nuevos *commits*, solo avanzará la rama local. Mientras no se tenga contacto con el servidor, el apuntador de la rama remota no se moverá.