# Guardado rápido en Git



El comando `git stash -u` **guarda los cambios no confirmados en una zona temporal** (*incluyendo los ficheros no rastreados*), dejando el *directorio de trabajo* como estaba durante el último *commit*. Esto permite saltar a otra rama sin hacer un *commit*.

`git stash list` muestra la lista de cambios almacenados en el área temporal. 

`git stash apply` aplica los cambios guardados en la rama activa.

`git stash drop stash@{[n]}` elimina los cambios guardados en la zona temporal. Debido a que se pueden realizar más cambios y guardarlos en la zona temporal, cada uno está señalado con un índice `n`.

`git stash pop stash@{[n]}` aplica los cambios guardados y los elimina de la zona temporal al mismo tiempo.

`git stash branch [branch]` crea una rama y aplica los cambios no confirmados que están en el área temporal.

~~~powershell
$ git status -s
 M licencia.txt
 M prueba.txt

$ git stash
Saved working directory and index state WIP on master: 936078f Se modifica licencia.txt

$ git status
On branch master
nothing to commit, working tree clean

$ git stash list
stash@{0}: WIP on master: 936078f Se modifica licencia.txt

$ git stash drop stash@{0}
Dropped stash@{0} (65fcce59619051871dcea22a4e2ecdd5e6b64169)
~~~

~~~powershell
$ git checkout -b testing
Switched to a new branch 'testing'

$ git stash apply stash@{0}
On branch testing
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

        modified:   licencia.txt
        modified:   prueba.txt

no changes added to commit (use "git add" and/or "git commit -a")
~~~

