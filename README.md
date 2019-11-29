## Introducción a Git y GitHub - [Curso de Platzi Resúmen](https://platzi.com/git)

Este repositorio sirve como

 es el repositorio que se trabajo con Freddy Vega CEO de Platzi,  en el curso profesional de Git y Github. Para entender todo lo que se  aprendió, intentaré escribir en este readme un pequeño resumen. Sin  embargo puedes clonar este repositorio, revisar cada commit, el trabajo  con las ramas o ir a [al curso de git y github de Platzi](https://platzi.com/git)

**Git** es un sistema de control de versiones (**VCS visual control system**), 

Registra los **cambios** realizados sobre un archivo o conjunto de archivos a lo largo del **tiempo**, por lo tanto no tendrás versiones como `tarea.txt, tarea2.txt, tarea2-final.txt tarea2-final2.txt tarea2-final2-esteeselbueno.txt`, además de que envés de guardar los archivos completos sólo se guardan **sólo los cambios**.

Git es algo así como el `Ctrl+Z` (deshacer) de los programadores, suponiendo que el `Ctrl Z` guardara todo el **historial de modificación** de los archivos, ya que con git puedes moverte en la historia (algo así como una máquina del tiempo).

## Flujo básico de git

`git init`: Empiezas un repositorio

`git add archivo.txt`: Agregas los cambios del archivo.txt al **staging area** para decirle a git que se prepare para guardar los cambios

`git commit -m 'Descripción del commit'`: Guarda los cambios en la base de datos del VCS (creando una nueva versión)

**Tipos de Control de versiones:**

* Local: Sólo funciona en una sóla máquina, es útil, pero no incorpora la colaboración.
* Centralizado (en un sólo servidor): Toda la información está depositada en un sólo repositorio, lo que hace que el trabajo se maneje directamente en el servidor. 
* Distribuído: La información se encuentra respaldada en diferentes peers, diferentes servidores y/o diferentes máquinas, lo que permite trabajar y compartir de manera sencilla.

## Archivos binarios y de texto plano

Git permite guardar tanto binarios como archivos de texto plano, pero está diseñado para modificar archivos de texto plano, ¿la razón? como git guarda los cambios entre versiones en el tiempo, son prácticamente no rastreables los cambios entre una versión y otra de un binario, mientras que son muy transparentes en los archivos de texto plano.

## Diferencias de git contra otros VCS

Git guarda referencia a los archivos no cambiados

Trabajo online efectivo

Git tiene Integridad: No puedes perder información durante su transmición

### Ventajas de git contra otros manejadores de versiones

* Veloz
* Diseño sencillo
* Fuerte apoyo del desarrollo no lineal
* Completamente distribuido
* Capaz de manejar grandes proyectos

## Operaciones principales de git

Es importante saber cuál es el estatus de tus cambios, ya que al modificar un archivo, éste no por defecto se va a git, sino que se modifica en el **working directory**, para que sea trackeado por git debe de pasar por el **staging area** y llegar al **repositorio**, opcionalmente podría llegar al **repositorio remoto**. A continuación más detalle.

* **Working directory (Local):** El working directory es el espacio de trabajo no rastreado por git, al modificar un archivo, este se modificará en el working directory andtes de que le des `git add` para agregarlo al staging area.

* **Staging Area:** Es un espacio en memoria ram dónde están guardados los cambios, pero todavía no están en el repositorio (no son trackeados por git). para agregar al staging area se utiliza el comando `git add`

  ```bash
  git add archivo.txt #Agrega el archivo.txt al staging area
  git add . #Agrega todos los cambios de los archivos en las subcarpetas del directorio en el que te encuentras al staging area
  git add -A #Agrega todos los cambios del repositorio en el que estás trabajando al staging area
  ```

* **Git repository:** Es el lugar dónde se trackean los cambios, cuando algo está en el repositorio, ya está en la historia de git y puedes acceder a ese historial mediante los commits. `git commit`

  ```bash
  git commit -m 'Commit 1' #Crea un commit (sube los cambios al repositorio local) con el nombre 'Commit 1'
  git commit #Se prepara para hacer commit y abre el editor por defecto de la terminal para ponerle nombre
  ```

  Es una buena práctica ser descriptivos con los cambios que se hicieron en cada commit.

* **Remote repository**: Acá entra github, el repositorio remoto es una copia de tu repositorio local, pero en Internet. Para mandar cambios al repositorio remoto es con el comando `git push`

  ```bash
  git push origin master #Empuja (envía) los cambios de la rama master al servidor remoto 'origin' 
  ```

## Commit

Un commit es un cambio rastreable (de 1 o varios archivos), es confirmar un conjunto de cambios provisionales de forma permanente y tenemos el superpoder de ponerle nombre a este cambio.

La historia de tu desarrollo se van guardando mediante commits, ya que cada cambio confirmado tiene modificaciones importantes hasta llegar al cambio actual.

Para hacer un commit, es muy sencillo, tenemos que tener agregado en el staging (`git add -A`) y usar el comando commit

```bash
Git commit -m 'commit'
```

Si trabajamos en algo experimental o que no queremos que sea parte del flujo principal, podemos hacer una nueva rama (**branch**), recordemos que la rama principal suela llamarse **master**, por lo tanto ésta branch nueva tendrá su propia historia (posterior al punto donde se creó).

Para crear una rama nueva con la información de la rama actual usamos el comando

```bash
git checkout -b nombre-del-branch
```

Si los cambios que realizaste en tu rama nueva son un avance en el código, puedes fusionarlo a la rama master (o a otra), para ésto tienes que cambiarte a master y hacer el comando es `merge`

```bash
git checkout master # nos cambiamos a la rama master
git merge rama-nueva # Fusionamos los cambios de la 'rama-nueva' en master
```



## Tracking files

- **Archivos Tracked**: Son los archivos que viven dentro de Git, no tienen cambios pendientes y sus últimas actualizaciones han  sido guardadas en el repositorio gracias a los comandos `git add` y `git commit`.
- **Archivos Staged**: Son archivos en Staging. Viven dentro de Git y hay registro de ellos porque han sido afectados por el comando `git add`, aunque no sus últimos cambios. Git ya sabe de la existencia de estos  últimos cambios pero todavía no han sido guardados definitivamente en el repositorio porque falta ejecutar el comando `git commit`.
- **Archivos Unstaged**: Entiendelos como archivos *“Tracked pero Unstaged”*. Son archivos que viven dentro de Git pero no han sido afectados por el comando `git add` ni mucho menos por `git commit`. Git tiene un registro de estos archivos pero está desactualizado, sus últimas versiones solo están guardadas en el disco duro.
- **Archivos Untracked**: Son archivos que NO viven dentro de Git, solo en el disco duro. Nunca han sido afectados por `git add`, así que Git no tiene registros de su existencia.

## Configurar el entorno de git

```bash
git config --global user.email "tu@email.com" # Configura el correo del usuario de git 
git config --global user.name "Tu Nombre" # Configura el nombre del usuario de git 

```

## Comandos

**git init**

```bash
git init #Empiezas un repositorio
```

**git add**

```bash
git add <archivo.txt> # Agregas los cambios del archivo.txt al **staging area** para decirle a git que se prepare para guardar los cambios
git add -A`

```

**Estado**

```bash
git status

```

**git commit**

```bash
git commit -m 'Descripción del commit': #Guarda los cambios en la base de datos del VCS (creando una nueva versión)
git commit --amend:

```

**Información**

```bash
git status:
git show:
git log:

```

**Repositorio**

```bash
git push
git pull

```

**git tag**

```bash
git tag -d #borrado del tag
git tag -f -a <version-nueva> -m  <Comentario> <version>
git tag -l Ver
git tag -a

```



**git log** 

Te muestra el historial de los commits que has hecho

```bash
git log # Muestra todos los commits con la información default
git log -3 #ultimos tres commits
git log --oneline #Resumido
git log --oneline --graph #Te lo muestra Resumido y bonito

```

**git show**

Es como log, pero con la diferencia de que muestra los cambios precisos que se hicieron en el commit

**git diff**

Nos compara y muestra los cambios sufridos entre los dos commits. Los id de los commit se pueden encontrar ejecutando git log.

```bash
git diff <referenci sha1> #
git diff <referencia2> <referencia1> <archivo>

```

**git reset**

```bash
git reset --soft #Agrega al staging
git reset --mixed #No lo agrega al staging
git reset --hard # 

```

**Cambiar el editor de código default de git**

```bash
git config --global core.editor “nano --wait”

```

**Branchs (Ramas)**

```bash
git branch nombre #Versiones alternas de un proyecto
git branch -d nombre
git branch -D nombre #Eliminar rama
git branch -m nombre_viejo nombre_nuevo
git checkout #cambiar de ramas
git checkout cambio_rama
git checkout -b nueva-imagen # Crear rama y switchear
git merge <rama-arreglada> # mezclando la rama actual con la <rama-arreglada> 
# Tenemos que estar en la rama output para hacer un merge o un rebase
git merge --abort
git rebase # hace prácticamente lo mismo que merge, cambiamos la historia de nuestro proyecto sin crear bifurcaciones del proyecto. Es mejor usar merge, 
#Usar solo git rebase de manera local.


```



### Git stash

git stash: es otro de los limbos, como el staging area. Para agregar los cambios estos deben estar en el staging area.
git stash list: nos muestra la lista de stash que tengamos.
git stash drop stash@{numero}: nos permite borrar un stash.
git stash apply: aplicamos el último cambio
Guardar en el limbo los cambios

git stash
git stash drop <numero_estado> #eliminar un stash
git stash apply #Agrega el estado ultimo
git stash apply <estado> #agregar stash exacto

### git cherry-pick 

Escoger commits
git cherry-pick [SHA1] nos permite cambiar un commit a otra rama para salvarnos la vida.
Vim
:wq #guardar y salir

MAC
pbcopy < “archivo”

## Fork

Copia local de un repositorio
git remote add origin master
Fetch
git fetch origin master
git push
git push origin master --tags
git push origin “branch”
git pull origin master
Llaves SSH
ssh-keygen -t rsa -b 4096 -C "davbelom@gmail.com"
Proyectos
Proyecto por feature grande