## Renombrar fichero

La instrucción `git mv [name] [newName]` permite renombrar un archivo y lo prepara al mismo tiempo, para posteriormente poder confirmar el cambio.

~~~powershell
#### Renombra prueba.java como testing.java.
$ git mv prueba.java testing.java
~~~

~~~powershell
#### Lo anterior es una manera corta de hacer esto:
$ mv prueba.java testing.java
$ git add testing.java
$ git rm prueba.java
~~~



## Eliminar fichero

El comando `git rm [file]` elimina un fichero y prepara el cambio del *directorio de trabajo*, para luego poder confirmar dichos cambios. Para eliminar un archivo que está en el *área de preparación* con cambios aún no confirmados, se debe forzar la eliminación con la opción `-f`, mientras que para eliminar un directorio con su contenido se debe utilizar la opción `-r`.

~~~powershell
#### Fuerza la eliminación del fichero con cambios preparados.
$ git rm -f Notas.txt
rm 'Notas.txt'
~~~

