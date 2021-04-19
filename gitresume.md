# Resumen Git

## Configuración y ayuda

| `git config --global user.name [name]`          | establece el nombre de usuario del repo. local. |
| ----------------------------------------------- | ----------------------------------------------- |
| `git config --global user.mail [email]`         | establece el e-mail del repositorio local.      |
| `git config --global core.editor [editor]`      | establece el editor de texto por defecto.       |
| `git config [key]`                              | muestra el valor de la propiedad.               |
| `git config --global alias.[alias] ["command"]` | establece un alias.                             |
| `git --help [command]`                          | muestra el manual de dicho comando.             |

## Crear / Inicializar un repositorio

| `git clone [repository]` | clona el repositorio remoto en el directorio actual.     |
| ------------------------ | -------------------------------------------------------- |
| `git init`               | inicializa un repositorio local en el directorio actual. |

## Agregar / Sacar ficheros del área de preparación

| `git status -s`          | muestra el estado resumido del directorio de trabajo.        |
| ------------------------ | ------------------------------------------------------------ |
| `git add [file..]`       | añade fichero(s) al área de preparación.                     |
| `git add [dir/..]`       | añade directorio(s) al área de preparación.                  |
| `git add .`              | añade todos los ficheros del directorio de trabajo al área de preparación. |
| `git rm --caches [file]` | saca archivo del área de preparación. Queda como *no rastreado*. |
| `git reset HEAD [file]`  | saca archivo del área de preparación. Queda como *modificado sin preparar*. |
| `git reset HEAD`         | vacía el área de preparación. Los archivos quedan como *no preparados*. |

## Deshacer / Confirmar cambios

| `git checkout -- [file]`         | deshace los últimos cambios no preparados.                   |
| -------------------------------- | ------------------------------------------------------------ |
| `git checkout [SHA-1] -- [file]` | recupera la versión indicada del fichero.                    |
| `git commit -m ["msg"]`          | realiza un *commit* y añade el mensaje de confirmación.      |
| `git show [SHA-1]`               | muestra los cambios introducidos en dicho *commit*.          |
| `git blame -c [file]`            | muestra cada línea del archivo con el último *commit* que la modificó. |
| `git commit --amend -m ["msg"]`  | modifica el último *commit* y añade otro mensaje de confirmación. |
| `git reset [SHA-1]`              | elimina los *commits* posteriores. Los cambios se mantienen *sin preparar*. |
| `git reset [SHA-1] -- [file]`    | restablece el fichero al estado del *commit*. Cambios *sin preparar*. |
| `git reset --mixed HEAD^`        | elimina el último *commit*, manteniendo los cambios sin preparar. |
| `git reset --mixed HEAD~[n]`     | elimina los últimos `n` *commits*, manteniendo los cambios *sin preparar*. |
| `git reset --hard HEAD^`         | elimina el último *commit* y se pierden los cambios realizados. |
| `git reset --hard HEAD~[n]`      | elimina los últimos `n` *commits* y se pierden los cambios realizados. |
| `git reset --hard [branch]`      | restablece el directorio de trabajo al estado de la rama y pierde los cambios. |
| `git revert HEAD`                | añade un nuevo *commit* que deshace los cambios del último *commit*. |
| `git revert [SHA-1]`             | añade un nuevo *commit* que deshace los cambios del *commit* señalado. |

## Historial de confirmaciones

| `git log --graph --oneline` | lista cada *commit* en una sola línea con la gráfica de divergencia entre ramas. |
| --------------------------- | ------------------------------------------------------------ |
| `git log --name-status`     | muestra el estado de los ficheros involucrados en cada *commit*. |
| `git log -[n]`              | lista los últimos `n` *commits*.                             |
| `git log [file]`            | lista los *commits* que afectan al fichero señalado.         |
| `git shortlog`              | lista los *commits* que ha hecho cada miembro del equipo.    |
| `git shortlog -sn`          | muestra el número de *commits* que ha hecho cada miembro del equipo. |

## Registro de cambios

| `git diff`                          | muestra los cambios que no se han añadido al área de preparación. |
| ----------------------------------- | ------------------------------------------------------------ |
| `git diff HEAD`                     | muestra los cambios del directorio de trabajo con relación al último *commit*. |
| `git diff [SHA-1]`                  | muestra los cambios del directorio de trabajo con relación al *commit*. |
| `git diff [branch]`                 | muestra los cambios de la rama activa con relación a la rama indicada. |
| `git diff [SHA-1A] [SHA-1B] [file]` | muestra las diferencias del fichero en los dos *commits*.    |

## Renombrar / Eliminar / Buscar dentro de ficheros

| `git mv [name] [newName]` | renombra fichero.                                            |
| ------------------------- | ------------------------------------------------------------ |
| `git rm -f [file]`        | elimina fichero, incluso si está en el área de preparación.  |
| `git rm -r [dir/]`        | elimina un directorio y todos sus archivos.                  |
| `git grep ["expression"]` | busca la expresión dentro de los ficheros del directorio de trabajo. |

## Ramas

| `git branch`                          | lista las ramas del proyecto.                                |
| ------------------------------------- | ------------------------------------------------------------ |
| `git branch [branch]`                 | crea una nueva rama en el *commit* actual sin saltar a ella. |
| `git branch [branch] [SHA-1]`         | crea una nueva rama en el *commit* sin saltar a ella.        |
| `git branch -m [name] [newName]`      | renombra una rama.                                           |
| `git branch -d [branch]`              | elimina una rama, no se puede eliminar la rama activa.       |
| `git branch -v`                       | muestra el último *commit* en cada rama.                     |
| `git branch -vv`                      | muestra las ramas de seguimiento que se tienen.              |
| `git branch --merged`                 | ramas que se han fusionado con la activa (se pueden eliminar). |
| `git branch --no-merged`              | ramas que no se han fusionado con la activa (presentan cambios). |
| `git checkout [branch]`               | salta a la rama indicada. No pueden haber cambios sin confirmar. |
| `git checkout [SHA-1]`                | salta al *commit* señalado. No pueden haber cambios sin confirmar. |
| `git diff [branch1] [branch2] [file]` | muestra las diferencias de un fichero en ambas ramas.        |
| `git show [branch]:[file]`            | muestra el archivo de una rama específica.                   |
| `git show [branch]`                   | muestra el último *commit* de la rama y lo compara con los nuevos cambios. |

## Fusionar / Reorganizar ramas

| `git merge [branch]`   | fusiona la rama señalada con la rama activa.                 |
| ---------------------- | ------------------------------------------------------------ |
| `git merge --abort`    | cancela una fusión (cuando existe algún conflicto).          |
| `git merge --continue` | realiza la fusión después de solucionar un conflicto manualmente. |
| `git rebase [branch]`  | toma los *commits* de la rama activa y los replica en la rama especificada.<br />Reorganiza el historial de forma lineal. Solo hacerlo en local. |

## Guardado rápido: saltar entre ramas sin confirmar cambios

| `git stash -u`                          | guarda todos los cambios no confirmados de forma temporal.<br />Deja el directorio de trabajo como el último *commit*. |
| --------------------------------------- | ------------------------------------------------------------ |
| `git stash list`                        | lista los *stashes* disponibles actualmente.                 |
| `git stash show stash@{[n]}`            | muestra los cambios almacenados en el *stash*.               |
| `git stash pop stash@{[n]}`             | aplica los cambios guardados en la rama activa y elimina el *stash*. |
| `git stash clear`                       | elimina todos los *stash* existentes.                        |
| `git stash drop stash@{[n]}`            | elimina un *stash* específico.                               |
| `git stash branch [branch] stash@{[n]}` | crea una rama y aplica los cambios guardados en el *stash* indicado. |

## Ramas remotas

| `git branch -a`                    | muestra las ramas locales y remotas que se tienen configuradas. |
| ---------------------------------- | ------------------------------------------------------------ |
| `git remote -v`                    | muestra los repositorios remotos y sus *URLs* que se tienen configurados. |
| `git remote add [url]`             | añade un nuevo repositorio remoto.                           |
| `git remote show [remote]`         | muestra información detallada sobre un repositorio remoto.   |
| `git remote rm [remote]`           | elimina un repositorio remoto.                               |
| `git fetch [remote]`               | descarga la información del repositorio remoto.<br />No la fusiona con el directorio de trabajo actual. |
| `git pull [remote]`                | descarga y combina automáticamente los nuevos cambios del repo. remoto. |
| `git push`                         | actualiza el repositorio remoto con todos los *commits* locales de las ramas en común. |
| `git push [remote] [branch]`       | envía todos los *commits* de una rama nueva o existente al repositorio remoto. |
| `git checkout -b [local] [remote]` | crea una rama local, la cual existe en el servidor, y salta a ella. |
| `git log origin/master..HEAD`      | muestra aquello que está a punto de publicarlo en el repositorio remoto. |

