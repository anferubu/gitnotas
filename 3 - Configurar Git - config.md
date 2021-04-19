# Configurar Git

Después de instalar Git, es necesario personalizar el entorno de trabajo. Esto se realiza una sola vez en la computadora y se puede cambiar en cualquier momento ejecutando de nuevo los comandos correspondientes.

## Identidad de usuario y editor de texto

Inicialmente, se debe establecer el **nombre de usuario**, **dirección de correo electrónico** y un **editor de texto**. La identidad de usuario es utilizada por los *commits* que se envían, mientras que el editor de texto se emplea cuando se requiere introducir algún mensaje. Si no se especifica, Git usará el editor por defecto del sistema.

 ~~~powershell
#### Establecer identidad de usuario y editor de texto.
$ git config --global user.name "John Doe"
$ git config --global user.email john@gmail.com
$ git config --global core.editor nano
 ~~~

La opción `--global` aplica esta configuración a todo el sistema. Para crear proyectos específicos dentro del mismo equipo, con otra *identidad de usuario*, se ejecuta `git config` sin la opción `--global`.



## Evitar problemas con espacios en blanco

Windows utiliza *retorno-de-carro* (*CR*) y *salto-de-línea* (*LF*) para marcar finales de línea en archivos. Mientras que, Mac y Linux utilizan solo *salto-de-línea*. Esta es una sútil, pero molesta diferencia que puede causar problemas al comparar ficheros en proyectos compartidos. Para solucionar esto se utiliza la propiedad `core.autocrlf`. 

En Windows se debe establecer dicha propiedad como `true`, esto convierte *LF* en *CRLF* al recibir ficheros desde Mac/Linux. 

En Mac/Linux, se establece esa propiedad como `input`, esto convierte *CRLF* en *LF* al recibir los archivos desde WIndows.

~~~powershell
#### Si está en Windows.
$ git config --global core.autocrlf true
~~~

~~~powershell
#### Si está en Mac/Linux.
$ git config --global core.autocrlf input
~~~



## Comprobar la configuración

El comando `git config --list` muestra todas las propiedades configuradas en Git. Para ver qué valor utiliza una clave específica, se ejecuta `git config [key]`.

~~~powershell
#### Se comprueba el valor de la propiedad user.name.
$ git config user.name
John Doe
~~~



## Establecer un alias

Si no se quiere escribir el nombre completo de un comando en Git, se puede establecer fácilmente un alias para cada comando mediante la instrucción `git config --global alias.[alias] [command]`.

~~~powershell
#### En vez de [git commit], se llama [git ci]
$ git config --global alias.ci commit
~~~

~~~powershell
#### En vez de [git log -1 HEAD], se llama [git last]
$ git config --global alias.last 'log -1 HEAD'
~~~



## ¿Cómo obtener ayuda?

Cada comando Git posee su propio manual, el cual se puede consultar en cualquier momento en búsqueda de ayuda. Para poder ver dicho manual, se utiliza la instrucción `git --help [command]`.

~~~powershell
#### Se abre el manual del comando git config.
$ git --help config
~~~

