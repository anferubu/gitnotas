## Inicializar repositorio

Para empezar a trabajar con Git en un proyecto nuevo o existente, se debe inicializar el *directorio de trabajo* con el comando `git init`, que crea una carpeta llamada `.git/`, que contiene todos los archivos requeridos por el repositorio.

Después de inicializar el *directorio de trabajo*, todos los archivos existentes estarán sin seguimiento, por lo cual se deben preparar dichos archivos no rastreados con la instrucción `git add .` y luego realizar un *commit* con `git commit -m ["message"]` para guardar una instantánea del repositorio.

~~~powershell
#### Se inicializa el repositorio en gitproject/.
$ git init
Initialized empty Git repository in /home/anfeterol/Documents/informatica/git/gitproject/.git/
~~~

~~~powershell
#### Se observa el estado de los archivos. Actualmente no están rastreados.
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	HelloWorld.class
	HelloWorld.java

nothing added to commit but untracked files present (use "git add" to track)
~~~

~~~powershell
#### Se añaden los archivos al área de preparación.
$ git add .
~~~

~~~powershell
#### Se realiza el primer commit.
$ git commit -m "Creación de la clase HelloWorld.java"
[master (root-commit) dee114f] Creación de la clase HelloWorld.java
 2 files changed, 6 insertions(+)
 create mode 100644 HelloWorld.class
 create mode 100644 HelloWorld.java
~~~





---



## Clonar repositorio

El comando `git clone [url]` permite crear una copia de un repositorio remoto, en el directorio de trabajo actual. Por ejemplo, al clonar el repositorio remoto *jquery*, en el directorio de trabajo actual se creará una carpeta llamada `/jquery`, la cual contiene toda la información del repositorio.

~~~powershell
#### Clona el repositorio jquery en el directorio actual.
$ git clone https://github.com/jquery/jquery.git
Cloning into 'jquery'...
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 43611 (delta 1), reused 1 (delta 1), pack-reused 43608
Receiving objects: 100% (43611/43611), 28.98 MiB | 250.00 KiB/s, done.
Resolving deltas: 100% (31202/31202), done.
~~~

También es posible clonar un repositorio en un directorio con un nombre distinto. Así, al ejecutar `git clone https://github.com/jquery/jquery.git myJQuery`, el repositorio clonado se alojará en la carpeta `/myJQuery`.

