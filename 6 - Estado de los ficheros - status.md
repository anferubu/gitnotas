# Estado de los ficheros en Git



`git status` determina el estado en el que se encuentran los ficheros no confirmados de un repositorio. Este comando suele dar instrucciones para preparar y confirmar los ficheros, o para deshacer los últimos cambios.

La opción `-s` muestra el estado de los archivos de una manera más compacta:

-   `??` (*untracked file*) : archivo nuevo sin rastrear.
-   `A` (*added file*) : archivo nuevo preparado que aún no ha sido confirmado por primera vez.
-   `M` (*modified file*) : archivo modificado. Ya ha sido preparado antes, pero ha sufrido cambios. Puede aparecer de tres formas distintas:
    -   `M_` (*columna izquierda*) : archivo modificado y preparado.
    -   `_M` (*columna derecha*) : archivo modificado y sin preparar.
    -   `MM` : archivo que presenta cambios preparados y sin preparar.
-   `D` (*deleted file*) : archivo eliminado.
-   `R` (*renamed file*) : archivo renombrado.
-   `C` (*copied file*) : archivo copiado.
-   `U` (*updated but unmerged file*) : archivo actualizado, pero no fusionado.



~~~powershell
#### Directorio de trabajo limpio, sin nuevos cambios.
$ git status
On branch master
nothing to commit, working directory clean
~~~

