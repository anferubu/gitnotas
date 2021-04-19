# Registro de cambios

## Comando `git diff`

`git diff` muestra los cambios sin preparar en todos los archivos modificados, al comparar el *directorio de trabajo* con el *área de preparación*.

`git diff --staged` presenta los cambios preparados en los archivos modificados que serán incluidos en la próxima confirmación, al comparar los cambios preparados con la última instantánea confirmada.

`git diff [SHA-1]` muestra los cambios del *directorio de trabajo* con relación al *commit* indicado.

`git diff [SHA-1A] [SHA-1B] [file]` muestra las diferencias del fichero en ambos *commits*.

`git diff [branch]` muestra los cambios de la rama activa con relación a la rama indicada.



~~~powershell
$ git status -s
?? Licencia.txt

$ git add Licencia.txt

$ git diff --staged
diff --git a/Licencia.txt b/Licencia.txt
new file mode 100644
index 0000000..6c274bc
--- /dev/null
+++ b/Licencia.txt
@@ -0,0 +1,5 @@
+IMPORTANTE^M
+^M
+Esta es la Licencia del producto,^M
+Por favor no distribuir sin^M
+permiso de los autores.
\ No newline at end of file
~~~



## Comando `git show`

`git show [SHA-1]` es otro comando similar, el cual muestra el *commit* señalado junto al *diff* asociado. 

`git show [file]` muestra el último *commit* que afectó al archivo junto al *diff* asociado.

`git show [branch]` muestra el último *commit* de la rama especificada, junto al *diff* asociado.

~~~powershell
$ git show b924d5d
commit b924d5d9f0fe12650d205856adf910491d20cd8d (HEAD -> master)
Author: Andrés Felipe Ruiz Buriticá <anferubu@gmail.com>
Date:   Mon Jul 29 18:43:19 2019 -0500

    se añade Notas.txt y se modifica Leeme.txt

diff --git a/Leeme.txt b/Leeme.txt
index e69de29..df70a31 100644
--- a/Leeme.txt
+++ b/Leeme.txt
@@ -0,0 +1,3 @@
+Aviso importante!^M
+^M
+Este es un producto libre y gratuito.
\ No newline at end of file
diff --git a/Notas.txt b/Notas.txt
new file mode 100644
index 0000000..e69de29
~~~

