# Combinar ramas en Git



En Git hay dos formas de combinar cambios entre ramas: **fusionar** (*merge*) y **reorganizar** (*rebase*).

## Fusionar ramas

El comando `git merge [branch]` toma la rama especificada y la combina con la rama actual. Existen dos tipos de fusiones en Git:

### 1. Fusión *fast-forward*

Si ambas ramas siguen la misma línea directa en el historial de confirmaciones, se denomina una *fusión fast-forward*. En este caso Git simplemente mueve el apuntador hacia adelante.

~~~powershell
$ git log --oneline
1e7260d (HEAD -> testing) Se eliminó notas.txt
1ff52a3 Se añade el archivo prueba.txt
7a73427 (master) Se añade el archivo faltantes.txt
ef0e167 Se añade el archivo notas.txt

$ git checkout master
Switched to branch 'master'

$ git merge testing
Updating 7a73427..1e7260d
Fast-forward
 notas.txt => prueba.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename notas.txt => prueba.txt (100%)

$ git log --oneline
1e7260d (HEAD -> master, testing) Se eliminó el archivo notas.txt
1ff52a3 Se añade el archivo prueba.txt
7a73427 Se añade el segundo archivo faltantes.txt
ef0e167 Se añade el primer archivo notas.txt
~~~



### 2. Fusión recursiva

En este caso, el historial de confirmaciones de ambas ramas ha divergido en un punto anterior. Es por esto que al ejecutar el comando `git merge` se crea un nuevo *commit*.

~~~powershell
$ git log --oneline --decorate --graph --all
* f3493dc (testing) Se modifica faltantes.txt
| * 172e0e1 (HEAD -> master) Se modifica prueba.txt
|/
* 1e7260d Se eliminó el archivo notas.txt
* 1ff52a3 Se añade el archivo prueba.txt
* 7a73427 Se añade el segundo archivo faltantes.txt
* ef0e167 Se añade el primer archivo notas.txt

$ git merge testing
Merge made by the 'recursive' strategy.
 faltantes.txt | 0
 1 file changed, 1 insertions(+), 0 deletions(-)
 create mode 100644 faltantes.txt

$ git log --oneline --decorate --graph --all
*   3515ee0 (HEAD -> master) merge branch 'testing': se modifica prueba.txt y faltantes.txt
|\
| * f3493dc (testing) Se modifica faltantes.txt
* | 172e0e1 Se modifica prueba.txt
|/
* 1e7260d Se eliminó el archivo notas.txt
* 1ff52a3 Se añade el archivo prueba.txt
* 7a73427 Se añade el segundo archivo faltantes.txt
* ef0e167 Se añade el primer archivo notas.txt
~~~



### Ver ramas fusionadas

Para ver aquellas ramas que han sido fusionadas con la rama activa se utiliza el comando `git branch --merged`. En cambio, para ver las ramas que no han sido fusionadas aún se escribe la instrucción `git branch --no-merged`.

En el siguiente ejemplo vemos que la rama `hotfix` ya ha sido fusionada y como no está activa, puede ser eliminada sin problemas. En cambio, la rama `testing` contiene trabajo sin fusionar, por esto, al intentar eliminarla con `git branch -d` lanza un error. Si realmente se quiere borrar la rama y perder el trabajo contenido en ella, se puede forzar la eliminación con la opción `-D`.

~~~powershell
$ git branch --merged
  hotfix 
* master

$ git branch --no-merged
  testing

$ git branch -d testing
error: The branch 'testing' is not fully merged.
If you are sure you want to delete it, run 'git branch -D testing'.
~~~



### Conflictos al fusionar ramas

Si hay un conflicto, una opción es abortar la fusión con el comando `git merge --abort`. Después de solucionar manualmente los conflictos, se prosigue con la fusión por medio del comando `git merge --continue`.

#### 1. Cambios dispares en el mismo archivo

SI hay diferentes cambios en una misma porción de un mismo fichero en las dos ramas que se pretenden fusionar, Git no será capaz de fusionarlas directamente, si no que esperará a que el conflicto se resuelva manualmente.

~~~powershell
$ git merge testing
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.

$ git status
On branch master
You have unmerged paths.
	(fix conflicts and run "git commit")

Unmerged paths:
	(use "git add <file>..." to mark resolution)

	both modified: index.html

no changes added to commit (use "git add" and/or "git commit -a")
~~~



Git añade unos marcadores que sirven de guía al abrir manualmente los archivos implicados para editarlos y corregirlos. La versión `HEAD` contiene lo indicado por encima de la marca `=======`, mientras que la versión de la otra rama se encuentra por debajo. Para resolver el conflicto se elige una versión y se eliminan las líneas `<<<<<<<`, `=======` y `>>>>>>>`. Después el archivo se prepara y confirma.

~~~powershell
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
please contact us at support@github.com
</div>
>>>>>>> iss53:index.html
~~~



#### 2. Cambios sin confirmar antes de fusionar

Si existen cambios sin confirmar en alguna de las ramas que se pretenden fusionar, Git no realizará la fusión hasta que se confirmen todos los cambios.

~~~powershell
$ git merge testing
error: Merging is not possible because you have unmerged files.
hint: Fix them up in the work tree, and then use 'git add/rm <file>'
hint: as appropriate to mark resolution and make a commit.
fatal: Exiting because of an unresolved conflict.
~~~





---



## Reorganizar las ramas

La instrucción `git rebase [branch]` toma todos los *commits* de la rama activa y los replica en la rama especificada. Esto modifica (*reorganiza*) el historial de *commits*, dando como resultado, un historial de confirmaciones lineal y más limpio.

La reorganización es una manera de limpiar el trabajo y las confirmaciones locales antes de enviarlos a un repositorio remoto. Nunca se deben reorganizar *commits* que ya hayan sido compartidos.

De manera similar, el comando `git rebase [branch1] [branch2]` activa la segunda rama, toma todos sus *commits* y los replica en la primera rama indicada.

~~~powershell
$ git log --oneline --decorate --graph --all
* d69f0e7 (HEAD -> testing) Se modifica prueba.txt
* 69fd991 Se eliminó notas.txt
* 44ebbdc Se añade el archivo prueba.txt
| * 3577862 (master) Se modifica faltantes.txt
|/
* ecdfa13 Se añade el archivo faltantes.txt
* d6fa9fc Se añade el archivo notas.txt

$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: Se añade el archivo prueba.txt
Applying: Se eliminó notas.txt
Applying: Se modifica prueba.txt

$ git log --oneline --decorate --graph --all
* a9c70e0 (testing) Se modifica prueba.txt
* 69c521b Se eliminó notas.txt
* c6b4b5c Se añade el archivo prueba.txt
* 3577862 (HEAD -> master) Se modifica faltantes.txt
* ecdfa13 Se añade el archivo faltantes.txt
* d6fa9fc Se añade el archivo notas.txt

$ git checkout master
Switched to branch 'master'

$ git merge testing
Updating 3577862..a9c70e0
Fast-forward
 notas.txt  | 0
 prueba.txt | 1 +
 2 files changed, 1 insertion(+)
 delete mode 100644 notas.txt
 create mode 100644 prueba.txt

$ git log --oneline --decorate --graph --all
* a9c70e0 (HEAD -> master, testing) Se modifica prueba.txt
* 69c521b Se eliminó notas.txt
* c6b4b5c Se añade el archivo prueba.txt
* 3577862 Se modifica faltantes.txt
* ecdfa13 Se añade el archivo faltantes.txt
* d6fa9fc Se añade el archivo notas.txt
~~~

