## Historial de confirmaciones

`git log` lista los *commits* realizados sobre el repositorio, siendo el primera el más reciente. Cada confirmación consta del *checksum SHA-1*, el nombre y el e-mail del autor, así como la fecha y el mensaje de confirmación.

`git log [file]` muestra solo aquellos *commits* que introdujeron algún cambio en el fichero especificado. El nombre siempre es el último parámetro.

### Formato de salida

Este comando posee varios parámetros que permiten personalizar lo que se desea mostrar. A continuación se muestran algunos de estos parámetros:

| **Parámetro**                               | **Descripción**                                              |
| ------------------------------------------- | ------------------------------------------------------------ |
| `-p`                                        | *diff* de cada confirmación.                                 |
| `--stat`                                    | estadísticas sobre modificaciones.                           |
| `--shortstat`                               | estadísticas resumidas en una línea.                         |
| `--name-only`                               | lista de archivos afectados.                                 |
| `--name-status`                             | lista de archivos afectados con su estado abreviado.         |
| `--abbrev-commit`                           | *SHA-1* abreviado.                                           |
| `--relative-date`                           | fecha en formato relativo.                                   |
| `--graph`                                   | gráfica ASCII con la historia de ramificaciones y uniones.   |
| `--pretty`                                  | formato alternativo. <br />Opciones: `oneline`, `short`, `full`, `fuller`, `format`. |
| `-n [number]`                               | últimas `[number]` confirmaciones.                           |
| `--since=["date"]`<br />`--after=["date"]`  | confirmaciones realizadas después de la fecha.               |
| `--until=["date"]`<br />`--before=["date"]` | confirmaciones realizadas antes de la fecha.                 |
| `--author=["author"]`                       | confirmaciones realizadas por tal autor.                     |
| `--committer=["committer"]`                 | confirmaciones realizadas por tal confirmador.               |
| `-S["str"]`                                 | confirmaciones que añaden o eliminan la cadena.              |
| `--grep ["key"]`                            | confirmaciones con la expresión en los mensajes del *commit*. |

-   Los parámetros de tiempo aceptan fechas concretas, por ejemplo `2008-01-15` o fechas relativas como `2 years 1 day 3 minutes ago`.
-   Si se quieren aplicar las opciones `--author` y `--grep` simultáneamente, se debe añadir `--all-match` o sino, el comando mostrará las confirmaciones que cumplan cualquiera de las dos, no necesariamente ambas a la vez.



El parámetro `--pretty` **modifica el formato de salida**. Así, por ejemplo `git log --pretty=oneline` imprime cada confirmación en una única línea. Las opciones `short`, `full`, `fuller` añaden menos o más información, respectivamente. Para especificar un formato propio se escribe `git log --pretty=format:["options"]`. A continuación, se muestran algunas opciones válidas.

| **Opción** | **Descripción**                 |
| ---------- | ------------------------------- |
| `%s`       | asunto.                         |
| `%t`       | *hash* árbol abreviado.         |
| `%h`       | *hash commit* abreviado.        |
| `%H`       | *hash commit*.                  |
| `%an`      | nombre del autor.               |
| `%ae`      | e-mail del autor.               |
| `%ad`      | fecha de autoría.               |
| `%ar`      | fecha relativa de autoría.      |
| `%cn`      | nombre del confirmador.         |
| `%ce`      | e-mail del confirmador.         |
| `%cd`      | fecha de confirmación.          |
| `%cr`      | fecha relativa de confirmación. |

-   El *autor* es la persona que escribió originalmente el trabajo, mientras que el *confirmador* es quién lo aplicó.



~~~powershell
#### Último commit con las estadísticas resumidas.
$ git log --shortstat -1
commit dc283e15e5afdf629658869005725a481110a19a (HEAD -> master)
Author: Andrés Felipe Ruiz Buriticá <anferubu@gmail.com>
Date:   Mon Apr 22 19:22:16 2019 -0500

    Se eliminó el archivo Notas.txt

 1 file changed, 8 deletions(-)
~~~

~~~powershell
#### Commits posteriores a la fecha.
$ git log --since='2019-04-22 19:19:50'
commit dc283e15e5afdf629658869005725a481110a19a (HEAD -> master)
Author: Andrés Felipe Ruiz Buriticá <anferubu@gmail.com>
Date:   Mon Apr 22 19:22:16 2019 -0500

    Se eliminó el archivo Notas.txt
~~~

~~~powershell
#### Commits cuyo mensaje de confirmación contiene la cadena 'Leeme.txt'.
$ git log --grep 'Leeme.txt'
commit 58f7ad1ab184de3d463a71746eb352b4c7d5a351
Author: Andrés Felipe Ruiz Buriticá <anferubu@gmail.com>
Date:   Mon Apr 22 19:21:07 2019 -0500

    Se modificaron los archivos Leeme.txt y Notas.txt

commit ecf8ee21132dbaa4e5f6a33445391a88267b48a4
Author: Andrés Felipe Ruiz Buriticá <anferubu@gmail.com>
Date:   Mon Apr 22 19:14:55 2019 -0500

    Se añadió el nuevo archivo Leeme.txt
~~~

~~~powershell
#### Último commit con un formato especial.
$ git log --pretty=format:'%an, %ar: %s' -1
Andrés Felipe Ruiz Buriticá, 44 minutes ago: Se eliminó el archivo Notas.txt
~~~

~~~powershell
#### Último commit con el identificador acortado y la lista de ficheros afectados.
$ git log --abbrev-commit --name-status -1
commit dc283e1 (HEAD -> master)
Author: Andrés Felipe Ruiz Buriticá <anferubu@gmail.com>
Date:   Mon Apr 22 19:22:16 2019 -0500

    Se eliminó el archivo Notas.txt

D       Notas.txt
~~~

