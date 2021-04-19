# Etiquetar *commits*



El *SHA-1* es el indicador de cada *commit*, pero se pueden utilizar etiquetas para señalar *commits* específicos. Esto se suele utilizar para marcar versiones de lanzamiento en repositorios remotos, por ejemplo, con *GitHub*.

En general, existen dos tipos de etiquetas: una **etiqueta ligera** que simplemente es un puntero a un *commit* determinado, y una **etiqueta anotada** la cual contiene además, la información del etiquetador.

## Listar etiquetas

El comando `git tag` **lista en orden alfabético las etiquetas** disponibles en el proyecto. La opción `-l` permite buscar etiquetas con un patrón particular.

~~~powershell
$ git tag
v0.1
v1.3
v1.7

$ git tag -l 'v1*'
v1.3
v1.7
~~~

## Crear y ver etiquetas

Para crear una **etiqueta ligera** del último *commit* se utiliza el comando `git tag [tag]`. Mientras que, para crear una **etiqueta anotada** se usa la instrucción `git tag -a [tag] -m ["message"]`.

Para ver la información de la etiqueta junto al *commit* etiquetado se utiliza el comando `git show [tag]`.

~~~powershell
# etiqueta ligera
$ git tag v1.2

$ git show v1.2
commit ca82a6dff817ec66f44342007202690a93763949
Author: 	Scott Chacon <schacon@gee-mail.com>
Date: 	Mon Mar 17 21:52:11 2008 -0700

	changed the version number
~~~

~~~powershell
# etiqueta anotada
$ git tag -a v1.4 -m 'my version 1.4'

$ git show v1.4
tag v1.4
Tagger: 	Ben Straub <ben@straub.cc>
Date: 	Sat May 3 20:19:12 2014 -0700

	my version 1.4

commit ca82a6dff817ec66f44342007202690a93763949
Author: 	Scott Chacon <schacon@gee-mail.com>
Date: 	Mon Mar 17 21:52:11 2008 -0700

	changed the version number
~~~

## Etiquetado tardío

Es posible etiquetar un *commit* mucho tiempo después de haberlo creado. Para esto, se debe utilizar el comando `git tag -a [tag] [SHA-1] -m ["message"]`. No es necesario escribir todo el *checksum SHA-1* del *commit*, con los primeros siete caracteres basta.

~~~powershell
$ git log --pretty=oneline
15027957951b64cf874c3557a0f3547bd83b3ff6 Merge branch 'experiment'
a6b4c97498bd301d84096da251c98a07c7723e65 beginning write support
0d52aaab4479697da7686c15f77a3d64d9165190 one more thing
6d52a271eda8725415634dd79daabbc4d9b6008e Merge branch 'experiment'

$ git tag -a v1.9 0d52aaa -m 'my version 1.9'

$ git show v1.9
tag v1.9
Tagger: 	Scott Chacon <schacon@gee-mail.com>
Date: 	Mon Feb 9 15:32:16 2009 -0800

	my version 1.9

commit 0d52aaab4479697da7686c15f77a3d64d9165190
Author: 	Magnus Chacon <mchacon@gee-mail.com>
Date: 	Sun Apr 27 20:43:35 2008 -0700

	one more thing
~~~

## Compartir etiquetas

Aunque las etiquetas no son cambios que se puedan confirmar, se pueden compartir y enviar a un servidor remoto. El comando `git push [remote] [tag]` permite **compartir una etiqueta con el servidor remoto indicado**.

De forma similar, el comando `git push [remote] --tags` enviará todas las etiquetas que aún no existen al repositorio remoto.

~~~powershell
$ git push origin --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 160 bytes | 0 bytes/s, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:schacon/simplegit.git
	* [new tag] 			v1.4 -> v1.4
	* [new tag] 			v1.4-lw -> v1.4-lw
~~~

## Eliminar etiquetas

Para eliminar una etiqueta del repositorio local se utiliza el comando `git tag -d [tag]`, mientras que, para eliminarla del repositorio remoto se debe utilizar además, la instrucción `git push origin :refs/tags/[tag]`.

~~~powershell
$ git tag -d v1.0
Deleted tag 'v1.0' (was ecfd964)

$ git tag

$ git push origin :refs/tags/v1.0
To https://github.com/anferubu/geomarket.git
 - [deleted]         v1.0
~~~

