
## Índice
* Ramas
* Fusiones de ramas
* Conflictos
* Remotos
* Flujos de trabajo con ramas

## Referencias
- [Libro de Git](https://git-scm.com/book/es/v2/)
- [Hoja de referencia de Git](https://training.github.com/)
- [Hoja de referencia de Git (PDF)](https://training.github.com/downloads/es_ES/github-git-cheat-sheet.pdf)
- [Herramienta "Visualizing Git"](http://git-school.github.io/visualizing-git/) (muy interesante para comprender el funcionamiento interno de Git y el trabajo con ramas y remotos)

## Contenidos

### Ramas

* Definición de ramas
  - Una rama es un *puntero* que apunta a un determinado commit.
  - Un repositorio debe tener una rama como mínimo.
  - El nombre de la rama que se crea por defecto es master. Este nombre no es especial ni tiene una función o significado especial. En *GitHub* la rama que se crea por defecto si se inicializa un repositorio a través de su interfaz web (lo veremos en la sesión siguiente) se llama main.
  - Existe un puntero especial llamado HEAD que apunta a la rama en la que estamos en ese momento.
  - Al cambiar de rama se modifica el contenido del directorio de trabajo: éste se muestra tal como estaba en la rama a la que hemos saltado.
  - La creación y el cambio de ramas se realizan de forma instantánea: no tienen apenas coste.
  - El trabajo con ramas es muy interesante por los siguientes motivos:
     - Se pueden hacer pruebas sin modificar el código en producción.
    - Se puede separar el trabajo en tareas o subproyectos que no afecten unos a otros.
    - Cada miembro del equipo puede trabajar sin ser interferido por los demás.

#### Crear ramas
  ```bash
    git branch <nombre_rama>
  ```
Este comando creará una rama nueva con el nombre seleccionado. Si no se indica ningún parámetro adicional, la rama creada apuntará **HEAD**, es decir, el *último commit de la rama en la que nos encontremos*.

Una alternativa es ejecutar **git checkout -b <nombre_rama>**. Este comando creará una rama con el nombre indicado y cambiará a dicha rama.

Es posible crear una rama que apunte a un commit o una rama determinada mediante el comando:
  ```bash
    git branch <nombre_rama> <COMMIT_HASH>
    git branch <nombre_rama> <NOMBRE_RAMA_EXISTENTE>
  ```
#### Ver ramas disponibles
  ``` bash
  git branch
  ``` 

  Este comando mostrará las *ramas locales* existentes en el repositorio. Si se desea ver las ramas existentes en el remoto (ver sección siguiente) se puede ejecutar **git branch --all**.

#### Cambiar de rama
  ``` bash
    git checkout <nombre_rama>
    git switch <nombre_rama>
  ```

Cualquiera de los dos comandos anteriores cambiará a la rama indicada. Es posible que el comando falle *si hay cambios en el directorio de trabajo* que no estén integrados en ningún commit: si dichos cambios pueden ser sobreescritos por los cambios de la rama a la que se desea cambiar, `git` abortará el cambio de rama y nos indicará el problema. En ese caso deberemos crear un commit con los cambios que estemos realizando (o bien guardarlos mediante `git stash`) y a continuación volver a ejecutar el comando de cambio de rama.

#### Fusionar una rama
Fusionar una rama, en inglés /merge/, consiste en incorporar los cambios presentes en una rama a la rama en la que nos encontramos actualmente. Para realizar una fusión hay que realizar las siguientes acciones:

1. Primero nos posicionamos en la rama sobre la que se va a realizar la fusión (la rama que va a recibir los cambios)
2. Para realizar la fusión ejecutar:
    ```bash
      git merge <nombre_rama_a_fusionar>
    ```
Si por ejemplo queremos integrar en la rama principal (`master`) los cambios presentes en la rama `feature1`, cambiaremos a la rama principal (si no estamos ya en ella) mediante `git checkout master` y a continuación ejecutaremos `git merge feature1`.

#### Conflictos
**Al fusionar una rama** pueden producirse **conflictos**. Un conflicto se produce cuando **diferentes commits introducen cambios en las mismas líneas de los mismos archivos**. Si por ejemplo estamos en un commit referenciado por dos ramas y realizamos desde ese punto común un commit en cada una de las ramas de manera que afecten a la misma línea del mismo fichero, se producirá un conflicto **al fusionar una rama en la otra**.

Por ejemplo, en esta imagen podría producirse un conflicto si queremos incorporar los cambios de la rama `master` en la rama `rama1` mediante `git merge master` (siempre que los cambios producidos en los commits afecten a las mismas líneas de los mismos ficheros).


![image](https://user-images.githubusercontent.com/46388534/225649649-99007dd5-c7bf-4ad0-baa5-335677c7a174.png)

Al producirse un conflicto, git no sabe qué cambios deben prevalecer: los de la rama A, los de la rama B, los dos, ninguno, algo totalmente distinto,... En este caso **es necesaria la intervención humana**. Git modificará los ficheros afectados incluyendo **delimitadores** para indicar los cambios que vienen de una rama y los que vienen de `HEAD`, es decir, de la rama en la que nos encontremos.

Es importante recalcar que **git no perderá información**: la incluirá toda, junto con los delimitadores para identificar la procedencia de los cambios.

Si se produce un conflicto **git quedará en un estado intermedio**: añadirá al área de preparación (color verde) los archivos que no presenten conflictos e ***indicará los archivos en conflicto***, en color rojo, para que el usuario los edite y resuelva los conflictos.

Resolver los conflictos pasa por **editar el archivo**, localizar los **delimitadores** y *-dejar el archivo como queremos que quede**. Normalmente esta última acción consistirá en decidir *qué cambios son los que queremos dejar y eliminar los delimitadores*. Al final, *el fichero debe quedar tal como queremos que quede*: en ocasiones una de las versiones será la correcta; en otras, la otra versión; en otras, ninguna; en obras, ambas; en otras, algo totalmente distinto.

