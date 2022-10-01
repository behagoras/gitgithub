# ⌨️ Comandos en Git (La guía completa) ⭐

Autor: Johan Mosquera
GitHub: https://github.com/jocode

## :coffee: Agregar la identidad
Es necesario configurar la primera vez git, y eso lo hacemos usando los siguientes comandos. Para descargar git en windows, lo podemos hacer en la siguiente dirección https://git-scm.com/download/win.

### instalar Gitk

* `$ sudo apt-get update`
* `$ sudo apt-get install gitk`
* `$ gitk #Iniciar gitk`

### Identidad

* `$ git config --global user.name "John Doe"`
* `$ git config --global user.email johndoe@example.com`

###  Editor por defecto

* `$ git config --global core.editor emacs`

### Herramienta de diferencias
Esta herramienta se usa para resolver conflictos

* `$ git config --global merge.tool vimdiff`

### Comprobar configuración

* `$ git config --list`

### Obtener ayuda

* `$ git help <comando>`
* `$ git <comando> --help`
* `$ man git-<comando>`

### Conectando a github mediante SSH

Para agregar la clave ssh a github, en caso de realizar conexiones al servidor mediante este protocolo, ver el la documentación de github [Conectando a github con SSH](https://help.github.com/articles/connecting-to-github-with-ssh/)

Tutorial de platzi
https://platzi.com/tutoriales/1557-git-github/4067-configurar-llaves-ssh-en-git-y-github/


## :coffee: Comandos Básicos

### Iniciar un repositorio en un directorio existente

* `$ git init`
* `$ git add *.c`
* `$ git add README`
* `$ git commit –m 'versión inicial del proyecto'`
* `$ git commit `	Abre una ventana en Vim para escribir el mensaje de la confirmación del cambio

* `$ git remote set-url origin url-ssh-del-repositorio-en-github` Definimos el repositorio remoto origin usando la conexión por SSH (Podemos cambiar la dirección del repositorio remoto).
* `$ git remote add origin url-ssh-repo` Se usa para agregar un repositorio remoto.

## :coffee: Eliminar commit

* `$ git reset --soft HEAD~1`  Elimina el commit más reciente, guardando el trabajo realizado
* `$ git reset --hard HEAD~1`  Elimina el commit más reciente destruyendo el trabajo que has hecho

### Cambiar el ultimo commit enviado a GitHub
Si ya he enviado ina confirmación y deseo cambiarlo, debo forzar el envio del commit cambiado con el comando. Recuerde que ya debe haber cambiado el commit localmente

* `$ git push --force origin master`

### Cambiar mensaje de commit antiguos

* `git rebase -i HEAD~3` Displays a list of the last 3 commits on the current branch
* `pick e499d89 Delete CNAME`
* `reword 0c39034 Better README`

Luego reemplazar pick con reword antes de cada mensaje del commit que desee cambiar y guardar los cambios.
Finalmente forzar el envío

* `git push --force`



## :coffee: Clonar un Repositorio

* `$ git clone [url]`
* `$ git clone git://github.com/schacon/grit.git mirepo` Renombra el directorio al clonar, con el nombre `<mirepo>`

## Comprobar estado de los archivos

* `$ git status` Muestra los archivos añadidos o eliminados
* `$ git diff` Muestra las líneas añadidas y eliminadas, muestra los cambios que no han sido preparados.


### Saltar el área de preparación

* `$ git commit -a -m 'added new benchmarks'` Prepara todos los archivos, sin necesidad de agregar el comando git add

## :coffee: Eliminando archivos

* `$ git rm <file>` Elimina el archivo del staging area

## Moviendo archivos

* `$ git mv <file_from> <file_to>`  Renombra los archivos

## :coffee: Viendo el histórico de confirmaciones 

* `$ git log`
* `$ git log -p`  Muestra las diferencias introducidas en cada confirmación
* `$ git log -2`  Muestra únicamente las dos últimas entradas del histórico
* `$ git log --stat`  Muestra las estadísticas de cada confirmación
* `$ git log --oneline`  Muesta información de un commit en una línea

### Modificando la última confirmación 

* `$ git commit --amend`  Reescribe el mensaje y los archivos para realizar la confirmación

### Deshaciendo preparación de un archivo 

* `$ git reset HEAD <file>`  Saca el archivo del staging area

### Deshaciendo la modificación de un archivo

* `$ git checkout -- <file>`  Elimina las modificaciones que le hayas hecho al archivo



## :coffee: Trabajando con repositorios remotos 

### Mostrar repositorios remotos

* `$ git remote`    Obtiene el nombre del repositorio remoto
* `$ git remote -v`  Obtiene la url del repositorio

### Añadiendo repositorios remotos

* `$  git remote add [nombre] [url]`

### Recibiendo repositorios remotos

* `$ git fetch [remote-name]` Recupera todos los datos del proyecto remoto que no tengas todavía pero no une las rama remota con la local.
* `$ git pull`  Trae los datos del proyecto remoto y lo une a las rama del repositorio local

### Enviar datos a repositorio remoto

* `$ git push [nombre-remoto][nombre-rama]`

**Importante**
Este comando funciona únicamente si has clonado de un servidor en el que tienes permiso de escritura, y nadie ha enviado información mientras tanto. Si tú y otra persona clonais a la vez, y él envía su información y luego envías tú la tuya, tu envío será rechazado. Tendrás que bajarte primero su trabajo e incorporarlo en el tuyo para que se te permita hacer un envío. Véase el Capítulo 3 para ver en detalle cómo enviar a servidores remotos

### Inspeccionando un repositorio remoto

* `$ git remote show [nombre]`

### Renombrando repositorios remotos

* `$ git remote rename [from] [to]`


## :coffee: Etiquetas
Especifica puntos especificos importantes en la historio, por ejemplo versiones.

### Listar etiquetas

* `$ git tag`

* `$ git tag -l 'v1.4.2.*'` Etiquetas por un patron en particular

### Crear etiquetas anotadas

* `$ git tag -a v1.4 -m 'my version 1.4'`

Esto muestra la información del autor de la etiqueta, la fecha en la que la confirmación fue etiquetada, y # el mensaje de anotación antes de mostrar la información de la confirmación.

### Crear etiquetas firmadas

* `$ git tag -s v1.5 -m 'my signed 1.5 tag'`
Crea una etiqueta firmada con GPG, siempre que tengas una clave privada


### Crear etiquetas ligeras

* `$ git tag v1.4-lw`   Este tipo de etiqueta no almacena información extra

### Verificar etiquetas firmadas

* `git tag -v [tag-name]`


### Etiquetar commit

* `$ git tag -a v1.2 -m 'version 1.2' 9fceb02` Agregar una etiqueta a un commit

### Editar etiquetas 

* `$ git tag <tag name> <tag name> -f -m "<new message>"` Creará una nueva etiqueta con el mismo nombre sobreescribiendo la original

* `$ git tag --force [tag name] [commit id]`  Edita una etiqueta a un commit específico.

* `$ git push origin --force --tags` En caso de que haya subido ya la etiqueta debe forzar envío

### Enviar etiquetas

* `git push origin [tagname]` y

Git no manda las etiquetas al servidor cuando de hace un push, para ello se debe hacer un push al igual como una rama pero con el nombre de la etiqueta

* `$ git push origin --tags`  Envía varias etiquetas a la vez

### Eliminar tags

* `$ git tag -d nombre-tag` Para eliminar un tag (localmente)
* `$ git push origin ref/tags/nombre-tag` Para eliminar un tag en origin


## :coffee: Alias en Git

Git permite colocar alias a los comandos que vienen por defecto

* `$ git config --global alias.co checkout`
* `$ git config --global alias.br branch`
* `$ git config --global alias.ci commit`
* `$ git config --global alias.st status`

* `$ git config --global alias.unstage 'reset HEAD --' ` 
* `$ git config --global alias.last 'log -1 HEAD'`


## :coffee: Branch

* `$ git branch` Lista ramas del proyecto local

* `$ git branch name-branch`  Crear ramas

* `$ git checkout -b name-branch`  Crear ramas y cambiar a la rama creada

*  `$ git show-branch`  Y
*  `$ git show-branch --all` Muestran las ramas y su historia

* `$ git pull origin name-branch` Traer ramas remotas

* `$ git branch -D name-branch` Eliminar ramas local

* `$ git push origin --delete name-branch` Y
* `$ git push origin :name-branch` Eliminar ramas remotas


## :coffee: Merge

* `$ git merge nombre-rama` Une la rama "nombre-rama" a la rama principal (main), esto solo lo hace el dueño del repositorio

Despues de esto hacemos

* `$ git pull origin master`
* `$ git push origin master`

## :coffee: Creación de primeros archivos para repositorio

Crear un nuevo repositorio en la línea de comandos

* `$ echo "# repositorio" >> README.md`
* `$ git init`
* `$ git add README.md`
* `$ git commit -m "first commit"`
* `$ git remote add origin git@github.com:user/repositorio.git`
* `$ git push -u origin master`


Enviar un repositorio exitente desde la línea de comandos

* `$ git remote add origin git@github.com:user/repositorio.git`
* `$ git push -u origin master`



En el caso de crear submodulos que luego quiere agregarlos al repositorio principal podemos usar el comando 

- `$ git rm --cached <path_to_submodule>` Elimina las secciones submodule en el archivo *.git/config*
