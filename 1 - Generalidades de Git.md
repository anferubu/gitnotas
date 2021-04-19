# Generalidades



## Sistema de Control de Versiones

Un **Sistema de Control de Versiones** (***VCS***) **registra los cambios realizados en uno o más archivos de texto plano a lo largo del tiempo**, permitiendo luego acceder a versiones específicas de dichos ficheros, para así revertir uno o varios archivos a un estado previo, comparar los cambios que se han realizado o poder ver quién realizó un determinado cambio.

### Tipos de sistemas de control de versiones

#### 1. Sistema de Control de Versiones Local (*LVCS*)

Consiste en una **base de datos local** con las diferentes versiones de un archivo dentro de un único computador. Al estar el fichero en un único sitio, se dificulta el trabajo entre colaboradores y se pone en riesgo la información.

#### 2. Sistema de Control de Versiones Centralizado (*CVCS*)

Consiste en un ***único servidor*** **que contiene un** ***repositorio central*** con todos los archivos versionados, y varios usuarios descargan los ficheros desde ese *servidor central*. Similar al caso anterior, es posible perder toda la información del proyecto si el servidor central se corrompe.

#### 3. Sistema de Control de Versiones Distribuido (*DVCS*)

En este sistema, **cada usuario posee una** ***copia local*** **completa del** ***repositorio***. Así, los distintos repositorios se pueden intercambiar y es posible mezclar revisiones entre ellos. De esta manera, si un servidor deja de funcionar, cualquiera de los repositorios disponibles puede ser copiado con el fin de restaurar la información.





---



## ¿Qué es Git?

Git es un ***Sistema de Control de Versiones Distribuido (DVCS)***, el cual se caracteriza por su velocidad, diseño sencillo, soporte para desarrollo no lineal (*ramificación*) y capacidad de manejar grandes proyectos eficientemente.

La mayoría de VCS manejan la información como un **conjunto de archivos y modificaciones** hechas a través del tiempo. En cambio, Git maneja los datos como un **conjunto de copias instantáneas** (*commits*) del aspecto de todos los archivos en ese momento.

La **mayoría de operaciones en Git solo necesitan archivos y recursos locales** para funcionar, ya que se tiene una copia del repositorio en el disco local. Así, es posible trabajar sin conexión a internet, y se pueden confirmar los cambios en la base de datos, para luego subirlos cuando haya internet.

**Git verifica todos los archivos antes de almacenarlos** y los identifica a partir de ese momento mediante una *suma de comprobación* (*checksum* *- valor* *hash SHA-1*), la cual consiste en una cadena de 40 caracteres hexadecimales. Esto significa que no se puede perder información durante la transmisión o sufrir corrupción de archivos sin que Git sea capa de detectarlo.

**Casi todas las acciones en Git consisten en añadir información a su base de datos**. Es muy difícil conseguir que el sistema borre información. Se pueden perder cambios que no han sido confirmados aún, pero después de confirmar una *copia instantánea*, es muy difícil perderla, especialmente si se envía la base de datos a otro repositorio con regularidad.



### Secciones de un proyecto en Git

#### 1. Directorio de Git (*Git directory*)

Es el repositorio donde se almacena la base de datos y los cambios del proyecto. Es aquello que se copia cuando se clona un repositorio desde otra computadora.

#### 2. Directorio de trabajo (*Working directory*)

Es una copia local del directorio de Git, es decir, es una versión del proyecto sobre la cual se trabaja y modifica. Para guardar las modificaciones en el *directorio de Git*, se deben pasar los archivos al área de preparación.

#### 3. Área de preparación (*Staging area / Index*)

Almacena la información acerca de los archivos modificados en el *directorio de trabajo*, que serán registrados en el *repositorio* en la próxima confirmación. Los archivos que están aquí se puede ver con `git status`.



![](/home/anfeterol/Documents/informatica/git/img/secciones_proyecto_git.png)



### Estados de un fichero en el repositorio

#### 1. Archivos sin rastrear (*Untracked files*)

Son los ficheros nuevos del *directorio de trabajo* que no estaban en la *última instantánea*, es decir, son *archivos* que no han sido listados en el *área de preparación*.

#### 2. Archivos rastreados (*Tracked files*)

Son aquellos ficheros que estaban en la *última instantánea* del proyecto, es decir, son los archivos ya preparados que Git conoce. Estos a su vez se clasifican en tres tipos:

-   ​	**Archivo preparado** (***Staged file***): fichero modificado o no rastreado que ha sido añadido al área de preparación para agregarlo al directorio de Git en la próxima confirmación.
-   ​	**Archivo modificado** (***Modified file***): fichero que ha sufrido cambios desde que se obtuvo del repositorio, pero aún no ha sido confirmado en el *directorio de Git*.	
-   ​	**Archivo confirmado** (***Committed file***): fichero cuya última versión concreta está almacenada de manera segura en el *directorio de Git*.



![](/home/anfeterol/Documents/informatica/git/img/estados_archivo_git.png)



##### ¿Cuál es la diferencia entre un archivo sin rastrear y un archivo no preparado?

Un ***archivo sin rastrear*** existe en el *directorio de trabajo*, pero nunca ha estado en el *área de preparación*. Mientras que un ***archivo no preparado*** ha estado en el *área de preparación*, pero ha sido modificado posteriormente. En ambos casos, ejecutar el comando `git add` hará que el archivo se comience a rastrear y se prepare.



### Flujo de trabajo básico en Git

Se **preparan** (`git add`) los **archivos no rastreados** y aquellos **modificados** del *directorio de trabajo*, y después se **confirman los cambios** (`git commit`) cada vez que el proyecto alcance un estado que se quiera conservar. Al realizar un *commit*, se toman los archivos del *área de preparación* y se almacenan en una *copia instantánea* de manera permanente en el *directorio de Git*.



![](/home/anfeterol/Documents/informatica/git/img/flujo_trabajo_git.jpeg)
