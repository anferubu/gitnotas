# Buscar dentro de fichero



`git grep ["expression"]` permite buscar una expresión determinada dentro de los archivos del directorio de trabajo. 

La opción `-n` indica el número de línea en donde aparece la coincidencia.

La opción `-c` señala el número de coincidencias por archivo.

La opcion `-- [file]` permite buscar la expresión en un fichero determinado.

La opción `-- :^[file]` busca la expresión en todos los ficheros, menos en el archivo especificado.



~~~powershell
#### Busca "addition" en el archivo Main.java
$ git grep -n "addition" -- Main.java
Main.java:6:        int addition = Maths.addition(a, b);
Main.java:7:        System.out.printf("%d + %d = %d\n", a, b, addition);
~~~

