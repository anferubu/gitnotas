# Confirmar cambios



Todo lo que está confirmado en Git puede recuperarse. Sin embargo, la información que nunca ha sido confirmada, se puede perder para siempre.

`git commit` **confirma los cambios previamente preparados** y los agrega al *directorio de Git*. En otras palabras, guarda una copia instantánea del área de preparación del proyecto. Al ejecutarlo, se abre el editor de texto para poder escribir un *mensaje de confirmación* del respectivo *commit*. Si no se escribe el mensaje, se cancela la confirmación. 

La opción `-m ["msg"]` permite escribir el mensaje de confirmación en la misma línea de la instrucción.

La opción `--amend` permite editar el mensaje y sobrescribir la última confirmación. Esto es útil cuando se olvida agregar algún archivo o se escribe mal el mensaje de confirmación.

~~~powershell
#### Main.java ha sido modificado y aún no se han preparado los cambios.
$ git status -s
 M Main.java
~~~

~~~powershell
#### Se preparan los cambios.
$ git add .
~~~

~~~powershell
#### Se confirman los cambios.
$ git commit
[master b1b159c] Se modifica la salida de Main.java
 1 file changed, 2 insertions(+), 1 deletion(-)
~~~

~~~powershell
#### Se abre el editor de texto para añadir el mensaje de confirmación.
Se modifica la salida de Main.java

Se añade una línea a Main.java que dice "Operación suma:" y se 
agrega una flecha antes de la operación.
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
# Changes to be committed:
#       modified:   Main.java
#
~~~
