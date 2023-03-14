# Git
#### ¿Que es Git?
Es un software libre de control de versiones creado por Linus Torvalds

### ¿Para que sirve?
Facilitar el desarrollo y mantenimiento de proyectos tanto de forma individual como grupal.

### ¿Cómo lo hace?
Creando un registro de todos los cambios que hagamos en los archivos

### Funcionalidad 
Ramas que permite el trabajo en paralelo de nuestro proyecto.


### Los 3 estados 
- **working directory**: Espacio donde se crean y se editan los archivos de nuestro proyecto
- **Staging area**: donde se inicia el seguimiento de los cambios que realicemos a los archivos 

- **Repository**: Donde se guardan los registros de los archivos una vez confirmados los cambios

- ## Instalacion
  [https://git-scm.com/download](https://git-scm.com/download)

- ## Configuración
```bash
Opciones obligatorias (nombre y correo)
git config --global user.name "Nombre y apellido"
git config --global user.email CORREO@ELECTRONICO
# Editor de preferencia: elegir solo una opción

# Editor de preferencia. Como primer ejemplo se incluye Notepad++ en Windows
git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"

# Editor de preferencia. Como segundo ejemplo se incluye Visual Studio Code
# Referencia: https://stackoverflow.com/questions/30024353/how-to-use-visual-studio-code-as-default-editor-for-git
git config --global core.editor "code --wait"
```
- ## Verificación
```bash
 git --version
```

## Creación de repositorios
```bash
 git init
```
## Ciclo de vida

![](https://camo.githubusercontent.com/2f5084d2a28564283a8dff925fdf8fcf1e33377c1e879c33f94d2316f324654c/68747470733a2f2f6769742d73636d2e636f6d2f626f6f6b2f656e2f76322f696d616765732f6c6966656379636c652e706e67)

## Revisando el estado
```bash
 git status
```
Esquema de colores:

-   **Rojo**  - Identifica los archivos  **modificados o nuevos**. Si se crean archivos dentro de carpetas nuevas,  `git status`  solo mostrará el nombre de la carpeta, no su contenido. Si se desea ver el contenido de las carpetas nuevas se deberá ejecutar  `git status -u`.
-   **Verde**  - Identifica los archivos en el  **área de preparación**.

## Visualizar cambios
```bash
 git diff
 git diff <archivo_o_ruta>
```
Este es uno de los comandos más utilizados en  `git`. Nos permite ver los cambios en los archivos del repositorio o en una ruta específica.

## Añadir archivos al área de preparación (stage)

```bash
git add <archivo> # Añadir archivos individuales
git add .         # Añadir todos los archivos nuevos o modificados
```
El  **área de preparación**  contiene los  **cambios que se añadirán a la nueva versión**  cuando ejecutemos un  `commit`. Es posible la siguiente situación:
-   Modificar un fichero (aparecerá en color rojo al hacer un  `git status`)
-   Añadir el fichero al área de preparación mediante  `git add FICHERO`
-   El fichero aparecerá en color  **verde**  al hacer un  `git status`
-   Volver a modificar el fichero
-   El fichero aparecerá  **dos veces**  al hacer un  `git status`:
    -   En color  **verde**, indicando que se ha añadido el  **primer cambio**  al área de preparación
    -   En color  **rojo**, indicando que hay un  **segundo cambio**  posterior que  **no se ha incluido**  en el área de preparación
-   Si se ejecuta un  `git commit`  en este momento  **solamente se incorporará el primer cambio**  al repositorio como nueva versión. El segundo cambio seguirá existiendo (el archivo no habrá cambiado), pero no estará guardado en el commit
-   Si se desea agregar el segundo cambio se deberá ejecutar nuevamente  `git add`  para añadirlo al área de preparación

## Visualizar cambios de los archivos en el área de preparación
```bash
git diff --staged
git diff --staged <archivo>
```
Este comando muestra los cambios que se han agregado al área de preparación (diferencia entre la última versión guardada en el repositorio y el área de preparación).

## Confirmar cambios (commit)
```bash
git commit -m "MENSAJE"
```
Un commit equivale a una nueva **versión** en el repositorio. Cada commit tiene un **identificador único**, denominado `hash`. Los commits están relacionados entre sí mediante una **red de tipo grafo**.

En la siguiente sesión estudiaremos como volver atrás en la historia para acceder a una versión anterior del repositorio si se desea.

## Ignorar archivos

-   Archivo  `.gitignore`
-   Plantillas de archivos  [.gitignore](https://github.com/github/gitignore).

Las rutas y nombres de archivo que aparezcan en el fichero `.gitignore` serán ignoradas por `git`  **siempre que no hayan sido añadidas previamente al área de preparación o al repositorio**. Por ejemplo, si añadimos un archivo al área de preparación mediante `git add` y a continuación lo añadimos al fichero `.gitignore`, `git` lo seguirá manteniendo en el área de preparación, por lo que será incluido en el repositorio si ejecutamos un `git commit`.

De igual manera, si previamente hemos guardado un archivo en el repositorio mediante `git commit` y a continuación lo incluimos en el fichero `.gitignore`, git no lo borrará: será necesario borrarlo del sistema de ficheros (a través de la consola o el navegador de archivos) y añadir los cambios (`git add` y `git commit`) para que se borre del repositorio. Una vez borrado, si lo volvemos a crear veremos que `git` sí que lo ignora si está incluido en el fichero `.gitignore`.

## Historial de cambios
```bash
git log
git log --graph
```
  
Este comando muestra el histórico de los commits del repositorio. Se puede navegar en el listado mediante los cursores y la barra espaciadora. Para salir hay que pulsar la tecla `q`.

## Ver cambios realizados en anteriores commits

```bash
git show <commit>
```
  
Este comando nos permite mostrar los cambios que se introdujeron en un determinado commit. En primer lugar se puede ejecutar  `git log`  para buscar el hash del commit que nos interese y a continuación ejecutar  `git show`  indicando después el hash del commit correspondiente.

Los hash de los commits tienen 40 caracteres, pero no es necesario copiarlos enteros: basta con indicar entre los  [8 y 10 primeros caracteres](http://git-scm.com/book/en/v2/Git-Tools-Revision-Selection#Short-SHA-1)  para identificar un commit correctamente.

## Quitar archivo del área de preparación
```bash
git reset <archivo>
```
En ocasiones nos encontramos con que hemos añadido cambios al área de preparación que no queremos incorporar al commit. Para ello podemos utilizar este comando, que elimina los cambios del fichero correspondiente del área de preparación. **Los cambios no se pierden** en ningún caso.

## Eliminar las modificaciones con respecto al último commit

```bash
# ¡PELIGRO! Todos los cambios que se hayan hecho al archivo desde el último commit se eliminarán
git checkout -- <archivo>
```
Este comando es peligroso, ya que **elimina todos los cambios del archivo** que no hayan sido guardados en el repositorio. Es decir, si el archivo tiene cambios y está en color **rojo**, se perderán dichos cambios. Este comando puede ser útil para dejar un archivo tal como estaba en la última versión guardada del repositorio.

## Etiquetado
```bash
git tag NOMBRE_TAG
```
Este comando crea un  `tag`  en el commit en que nos encontremos en este momento. Un  `tag`  es un  **alias**  que se utiliza para  **hacer referencia a un commit**  sin necesidad de saber su hash. Normalmente se utiliza para  **indicar números o nombres de versiones**  asociadas a un determinado commit. De esta manera podemos  **identificar una versión de una manera más amable**.

El nombre de los  `tag`  se puede utilizar con los comandos de git: por ejemplo,  `git show`.

## Guardado temporal

```bash
# Guardado temporal de cambios no añadidos al área de preparación
git stash

# Restaurar cambios guardados mediante git stash
git stash pop
```
En ocasiones se hacen cambios que se desea preservar para más adelante: por ejemplo, trabajamos en una modificación de un fichero y de repente nos avisan de que hay un bug en otro fichero que tiene que ser resuelto inmediatamente. Para no trabajar en ambas tareas a la vez podemos ejecutar `git stash`: los cambios que tenemos en ese momento y que no están en el área de preparación (es decir, los cambios que están en color rojo) se guardan en un área temporal; al ejecutar `git status` veremos que no hay ninguna modificación, el directorio de trabajo está limpio.

A continuación trabajamos en el bug, hacemos cambios y al terminar ejecutamos `git add` y `git commit` para resolverlo. Una vez resuelto, ejecutamos `git stash pop` y recuperamos los cambios que estábamos realizando antes de ser interrumpidos: veremos que `git status` nos muestra en color rojo los archivos que habíamos modificado al principio.

## Tareas
Realiza las tareas que se indican a continuación. Incluye las  **capturas de pantalla**  que se pidan en un documento tipo  **LibreOffice**  o  **Word**.

Cuando se pida realizar un  _commit_  recuerda que previamente hay que añadir los archivos al área de preparación si no se ha indicado antes en las instrucciones. En esos casos, un  _commit_  significa ejecutar los comandos  `git add`  y  `git commit`.

**¡IMPORTANTE!**  No utilices el bloc de notas de Windows para editar los archivos de texto de las tareas. Utiliza en su lugar un editor específico. Algunas sugerencias son:
-   [Visual Studio Code](https://code.visualstudio.com/)
-   [Atom](https://atom.io/)
-   [Brackets](http://brackets.io/)
-   [Sublime Text](https://www.sublimetext.com/)
-   [Notepad ++](https://notepad-plus-plus.org/)

El bloc de notas de Windows utiliza una codificación de caracteres específica de Windows y además incluye la extensión `.txt` por defecto al final de los nombres de archivo. Por tanto, no es una buena elección para trabajar.

Las tareas a realizar son:

1.  Instala Git en tu sistema operativo. Adjunta una captura de pantalla en la que aparezca el resultado de la ejecución del comando  `git --version`.
2.  Realiza la  **configuración de Git**  según lo indicado en el tema (nombre, correo electrónico y editor de preferencia). Adjunta una captura de pantalla con el resultado de la ejecución del comando ` git config --list`
3.  Crea una carpeta denominada  `S1R1`. Realiza las siguientes acciones en ella:
    1.  Crea un repositorio Git.
    2.  Crea un fichero denominado  `libros.txt`. Añade tres títulos de libros cada uno en una línea distinta.
    3.  Haz un primer  _commit_.
    4.  Añade dos libros al archivo  `libros.txt`.
    5.  Haz un segundo  _commit_.
    6.  Crea un fichero denominado  `peliculas.txt`. Añade tres títulos de películas a dicho archivo.
    7.  Haz una captura de pantalla del comando  `git status`.
    8.  Crea un fichero denominado  `comidas.txt`. Añade tres nombres de comidas a dicho archivo.
    9.  Haz un tercer  _commit_  que incluya los archivos  `peliculas.txt`  y  `comidas.txt`.
    10.  Elimina el archivo  `comidas.txt`  desde el navegador de archivos.
    11.  Añade dos películas más al archivo  `peliculas.txt`.
    12.  Haz una captura de pantalla que muestre los cambios en el directorio de trabajo.
    13.  Añade los cambios al área de preparación.
    14.  Haz una captura de pantalla del comando  `git status`. Debe indicar que se ha borrado el archivo  `comidas.txt`  y que se ha modificado el archivo  `peliculas.txt`.
    15.  Haz un cuarto  _commit_.
    16.  Crea un archivo denominado  `datos.bak`. Añade tres títulos de libros a dicho archivo.  **¡IMPORTANTE! No añadas el archivo al área de preparación ni hagas ningún commit.**
    17.  Crea una subcarpeta denominada  `output`. Crea un archivo denominado  `salida.txt`  en su interior. Escribe tu nombre y apellidos en dicho archivo.  **¡IMPORTANTE! No añadas los archivos al área de preparación ni hagas ningún commit.**
    18.  Haz una captura de pantalla del comando  `git status`. Deben aparecer el archivo  `datos.bak`  y la carpeta  `output`  como archivos nuevos (color rojo). Recuerda que, por defecto,  `git`  no muestra el contenido de una carpeta desconocida, sino solo el nombre de dicha carpeta; si se desea mostrar los archivos nuevos dentro de carpetas desconocidas se debe ejecutar  `git status -u`.
    19.  Crea un archivo  `.gitignore`  para que los ficheros con extensión  `.bak`  y el contenido de la carpeta  `output/`  no se incluyan en el repositorio.
    20.  Haz una nueva captura de pantalla del comando  `git status`. Ahora no deben aparecer los archivos  `datos.bak`  y  `output/salida.txt`  como archivos nuevos, sino que en su lugar debe aparecer únicamente el archivo  `.gitignore`.
    21.  Haz un último  _commit_  para incluir el archivo  `.gitignore`  en el repositorio.
    22.  Haz una captura de pantalla que muestre el histórico de cambios del repositorio.


## Entrega de la tarea
Guarda el fichero con las capturas en formato  **PDF**  y nómbralo según el patrón  `APELLIDOS_NOMBRE_sesion1.pdf`. La entrega del fichero se realizará a través de la plataforma Classroom


