## Deshacer cambios locales

El comando `git reset [SHA-1]` revierte el repositorio al estado en que estaba durante el *commit* señalado, pero mantiene el *directorio de trabajo* igual. Los cambios hechos posteriormente a dicho *commit* se mantienen como cambios sin preparar.

Con la opción `--soft` no cambia el *área de preparación* ni el *directorio de trabajo*, por lo que los cambios posteriores se mantienen como preparados.

En cambio, con la opción `--hard` se revierte el *área de preparación* y el *directorio de trabajo* al estado en que estaban durante la confirmación especificada, perdiendo así todos los cambios realizados posteriormente.

| **`git reset`**                     | `--soft` | `(--mixed)` | `--hard` |
| ----------------------------------- | -------- | ----------- | -------- |
| Revierte el *directorio de trabajo* | No       | No          | Si       |
| Revierte el *área de preparación*   | No       | Si          | Si       |
| Mantiene los cambios posteriores.   | Si       | Si          | No       |

~~~powershell
#### Commits existentes
$ git log --oneline
80bd0be (HEAD -> master) Se modifica la salida de Main.java y se añade README.txt
281ba14 Se crea Main.java y Maths.java
2859531 Se añade el fichero .gitignore
dee114f Creación de la clase HelloWorld.java
~~~

~~~powershell
#### Reestablecemos el directorio de trabajo al estado del penúltimo commit
$ git reset --hard 281ba14
HEAD is now at 281ba14 Se crea Main.java y Maths.java
~~~

~~~powershell
#### El último commit y sus cambios han desaparecido.
$ git log --oneline
281ba14 (HEAD -> master) Se crea Main.java y Maths.java
2859531 Se añade el fichero .gitignore
dee114f Creación de la clase HelloWorld.java
~~~



## Deshacer cambios compartidos

No se recomienda deshacer o modificar un *commit* que ya se haya compartido (*subido a un repositorio remoto*), pues esto puede ocasionar conflictos y confusiones entre los miembros del proyecto.

Pero, si se requiere modificar un *commit* que ya se haya subido a un repositorio remoto, se usa el comando `git revert [SHA-1]`, que genera un nuevo *commit* que deshace los cambios introducidos en el *commit* señalado, aplicando los cambios además, a la rama activa.

Si al revertir un *commit*, el contenido de un fichero cambia, se producirá un conflicto. Se deberá solucionar manualmente, para luego preparar y confirmar los cambios.

~~~powershell
$ git log --oneline
80bd0be (HEAD -> master) Se modifica la salida de Main.java y se añade README.txt
281ba14 Se crea Main.java y Maths.java
2859531 Se añade el fichero .gitignore
dee114f Creación de la clase HelloWorld.java
~~~

~~~powershell
git revert 2859531
Removing .gitignore
[master b978aed] Revert "Se añade el fichero .gitignore"
 1 file changed, 4 deletions(-)
 delete mode 100644 .gitignore
~~~

~~~powershell
$ git log --oneline
b978aed (HEAD -> master) Revert "Se añade el fichero .gitignore"
80bd0be Se modifica la salida de Main.java y se añade README.txt
281ba14 Se crea Main.java y Maths.java
2859531 Se añade el fichero .gitignore
dee114f Creación de la clase HelloWorld.java
~~~



## Restarurar fichero

El comando `git checkout [SHA-1] [file]` sobrescribe el fichero con la versión guardada en el *commit* señalado.

El comando `git checkout [branch] [file]` sobrescribe el fichero de la rama activa con la versión de la rama indicada.



~~~powershell
#### Contenido de HelloWorld.java con cambios sin preparar.
$ more HelloWorld.java
public class HelloWorld {

    public static void main(String[] args) {
        System.out.println("¡Hola mundo!");
    }
}
~~~

~~~powershell
#### Se deshacen los cambios no preparados.
$ git checkout HEAD -- HelloWorld.java
~~~

~~~powershell
#### Ahora, el contenido es el mismo al del último commit.
$ more HelloWorld.java
public class HelloWorld {

    public static void main(String[] args) {
        System.out.println("Hello, world!");
    }
}
~~~


