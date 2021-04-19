# Ignorar archivos en Git



Es posible tener algún tipo de archivo que no se desea añadir automáticamente a Git o incluso, que ni siquiera se desea que aparezca como *archivo no rastreado*. Por ejemplo, archivos generados como trazas o creados por el sistema de compilación.

Para estos casos, se crea un archivo llamado `.gitignore`, el cual lista las expresiones regulares que corresponden a los nombres de ficheros que se quieren ignorar.

Para crear estos patrones definidos se deben seguir unas reglas:

-   En el fichero `.gitignore`, se ignoran las líneas en blanco y aquellas que inician con el carácter `#`.
-   Se aceptan las expresiones regulares simplificadas:

  *   `*` : representa cero o más caracteres.
  *   `?` : representa un carácter cualquiera.
  *   `[abc]` : representa un carácter cualquiera dentro de los corchetes.
  *   `[0-9]` : representa un carácter cualquiera dentro del intervalo.
  *   `**` : permite indicar un directorio anidado, por ejemplo `dir1/**/dir5`.
-   El nombre de un directorio termina con el carácter `/`.
-   Un patrón de búsqueda se puede negar si se antepone el carácter `!`.



Una buena práctica consiste en crear un archivo `.gitignore` antes de comenzar a trabajar, para así evitar confirmar accidentalmente archivos que en realidad no se querían incluir en el repositorio de Git.

~~~powershell
# ignora los archivos terminados en .exe, pero no ignora lib.exe
*.exe
!lib.exe

# ignora los archivos terminados en .o o .a
# suelen ser producto de compilar el código
*.[oa]

# ignora los archivos terminados en ~, suelen serarchivos temporales
*~

# ignora todos los archivos del directorio build/
build/

# ignora doc/notes.txt, pero no doc/other/arch.txt
doc/*.txt

# ignora todos los archivos .txt el directorio doc/
doc/**/*.txt

# ignora todos los .jpg, ya que no es recomendable
# alojar archivos binarios en el repositorio Git.
*.jpg
~~~

