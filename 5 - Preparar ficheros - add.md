# Preparar ficheros en Git

En Git, *preparar un fichero* significa añadirlo al *área de preparación*. Así, cuando se confirmen los cambios, se guardará la versión del fichero correspondiente al instante en que se preparó por última vez dicho archivo.

`git add [file]`  permite **rastrear un archivo nuevo** o **preparar un archivo ya rastreado y modificado** para agregarlo al repositorio en una próxima confirmación de cambios. Para referirse a todos los ficheros del directorio se escribe `.`.

~~~powershell
#### Se tiene un fichero modificado y otro sin rastrear.
$ git status -s
 M HelloWorld.java
?? Maths.java
~~~

~~~powershell
#### Se preparan todos los ficheros.
$ git add .
~~~

~~~powershell
#### Ahora, todos los ficheros están preparados.
$ git status -s
M  HelloWorld.java
A  Maths.java
~~~

