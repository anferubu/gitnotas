# Ramas locales en Git



Una rama es un **apuntador móvil que señala a uno de los *commits* del proyecto**. La rama por defecto se denomina `master`, la cual se crea con el primer *commit* realizado en el proyecto. Con cada nuevo *commit*, la rama irá avanzando automáticamente, siendo el apuntador `HEAD` quien señala el último *commit* de la rama activa.

**Cuando se salta a otra rama, los ficheros del *directorio de trabajo* cambian** al estado en el que se encontraban durante el último *commit* realizado en dicha rama. Esto ocasiona que los nuevos cambios divergan entre ramas del mismo proyecto.



![](/home/anfeterol/Documents/informatica/git/img/rama_local.png)



Algunos equipos de desarrollo siguen el siguiente estándar: la rama `master` contiene todo lo que va a producción, la rama `development` contiene las nuevas características y actualizaciones del proyecto que aún no están listas para unirse a `master`. Por último, todos los errores se solucionan en la rama `hotfix`.



## Ver las ramas actuales del proyecto

El comando `git branch` **lista las ramas presentes en el proyecto**. La rama activa es señalada con el símbolo `*`.

~~~powershell
$ git branch
* master
~~~

## Crear una rama

El comando `git branch [branch]` crea una nueva rama, un apuntador al último *commit* realizado, pero no salta a dicha rama.

~~~powershell
$ git branch testing

$ git branch
* master
  testing
~~~

## Renombrar una rama

El comando `git branch -m [branch] [newName]` permite renombrar una rama, incluso la rama activa.

~~~powershell
$ git branch
  development
* master
  testing

$ git branch -m development desarrollo

$ git branch
  desarrollo
* master
  testing
~~~

## Eliminar una rama

El comando `git branch -d [branch]` elimina una rama especificada. Tenga en cuenta que no se puede eliminar la rama activa.

~~~powershell
$ git branch
  development
* master
  testing

$ git branch -d development
Deleted branch development (was 7a73427).

$ git branch
* master
  testing
~~~

## Ver el último *commit* en cada rama

El comando `git branch -v` muestra todas las ramas del proyecto en orden alfabético, junto con el último *commit* al que apunta cada una.

De manera similar, la instrucción `git show [branch]` presenta el último *commit* de la rama especificada junto al *diff* (*registro de cambios*) asociado.

~~~powershell
$ git log --oneline
1e7260d (HEAD -> testing) Se eliminó notas.txt
1ff52a3 Se añade el archivo prueba.txt
7a73427 (master) Se añade el archivo faltantes.txt
ef0e167 Se añade el archivo notas.txt

$ git branch -v
  master  7a73427 Se añade el archivo faltantes.txt
* testing 1e7260d Se eliminó notas.txt
~~~

## Crear una rama en un *commit* indicado

El comando `git branch [branch] [SHA-1]` crea una rama y la ubica en el *commit* señalado.

~~~powershell
$ git log --oneline
2169673 (HEAD -> master) Se añade MaestroDoc.txt
be30c37 Se añade Otros.txt
2312be1 Se modifica Leeme.txt, Licencia.txt
173d323 Se añaden Leeme.txt, Licencia.txt, Nota.txt

$ git branch hotfix 2312be1

$ git log --oneline
2169673 (HEAD -> master) Se añade MaestroDoc.txt
be30c37 Se añade Otros.txt
2312be1 (hotfix) Se modifica Leeme.txt, Licencia.txt
173d323 Se añaden Leeme.txt, Licencia.txt, Nota.txt
~~~

## Comparar *commits* entre ramas

El comando `git log [branch1]..[branch2]` muestra todos los *commits* presentes en la segunda rama que no están en la primera. Esto sirve para mantener una rama actualizada y previsualizar lo que se va a fusionar.

Por ejemplo, `git log origin/master..HEAD` muestra lo que está apunto de publicarse en el servidor remoto.

~~~powershell
$ git log --oneline
e684e89 (HEAD -> testing) Se modifican Otros.txt, Prueba.txt
9758c62 Se añade Prueba.txt
c06c823 (master) Se modifica Leeme.txt
be30c37 Se añade Otros.txt
2312be1 Se modifica Leeme.txt, Licencia.txt
173d323 Se añaden Leeme.txt, Licencia.txt, Nota.txt

$ git log master..testing --oneline
e684e89 (HEAD -> testing) Se modifican Otros.txt, Prueba.txt
9758c62 Se añade Prueba.txt
~~~



El comando `git log [branch1] [branch2] ^[branch3]` muestra todos los *commits* que están en la primera y segunda rama, pero que no están en la tercera rama.

~~~powershell
$ git log --oneline
7d4a7e4 (HEAD -> development) Se añade Dev1.txt
e684e89 (testing) Se modifican Otros.txt, Prueba.txt
9758c62 Se añade Prueba.txt
c06c823 (master) Se modifica Leeme.txt
be30c37 Se añade Otros.txt
2312be1 Se modifica Leeme.txt, Licencia.txt
173d323 Se añaden Leeme.txt, Licencia.txt, Nota.txt

$ git log testing development ^master --oneline
7d4a7e4 (HEAD -> development) Se añade Dev1.txt
e684e89 (testing) Se modifican Otros.txt, Prueba.txt
9758c62 Se añade Prueba.txt
~~~



El comando `git log --left-right [branch1]...[branch2]` muestra los *commits* que están en la primera o segunda rama, pero no en ambas.

~~~powershell
$ git log --oneline --decorate --graph --all
* 2169673 (HEAD -> master) Se añade MaestroDoc.txt
| * 485a379 (testing) Se añade Prueba2.txt
| * 43ecb63 Se modifica Nota.txt y Prueba.txt
| | * 1f888fb (development) Se modifican Dev1.txt y Dev2.txt
| | * 71b0da0 Se añade Dev2.txt
| | * 7d4a7e4 Se añade Dev1.txt
| |/
| * e684e89 Se modifican Otros.txt, Prueba.txt
| * 9758c62 Se añade Prueba.txt
|/
* c06c823 Se modifica Leeme.txt
* be30c37 Se añade Otros.txt
* 2312be1 Se modifica Leeme.txt, Licencia.txt
* 173d323 Se añaden Leeme.txt, Licencia.txt, Nota.txt

$ git log --left-right testing...development --oneline
< 485a379 (testing) Se añade Prueba2.txt
< 43ecb63 Se modifica Nota.txt y Prueba.txt
> 1f888fb (development) Se modifican Dev1.txt y Dev2.txt
> 71b0da0 Se añade Dev2.txt
> 7d4a7e4 Se añade Dev1.txt
~~~



## Saltar a una rama específica

`git checkout [branch]` permite saltar a la rama especificada, siempre y cuando no se tengan cambios sin confirmar en la rama activa, restaurando así el directorio de trabajo al último estado de dicha rama.

La opción `-b` permite crear una nueva rama y saltar inmediatamente a ella.

~~~powershell
#### Salta a una rama existente.
$ git checkout testing
Switched to branch 'testing'

$ git branch
  master
* testing
~~~

~~~powershell
#### Crea una nueva rama y salta a ella.
$ git checkout -b development
Switched to a new branch 'development'

$ git branch
* development
  master
  testing
~~~



