
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
