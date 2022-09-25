# Crear varias claves SSH para diferentes repositorios #

## Indice ##
 * [Crear multiples claves ssh](#title1)
 * [Descargar un proyecto con la nueva clave ssh](#title2)
 * [Actualizar ssh de un proyecto existente](#title3)

## Crear multiples claves ssh <a id="title1"></a>##

Para crear multiples claves SSH, primero se debe eliminar las claves anteriores como tambien desvincularlos de los repositorios bitbucket y GitHub (en caso estuvieran vinculados).
Después ejecutar este código

```
ssh-keygen -f ~/.ssh/NOMBRE_DEL_KEY -C "NOMBRE_DEL_KEY"
```
Por ejemplo si se desea crear una clave **personal** sería así:

```
ssh-keygen -f ~/.ssh/personal -C "personal"
```
Después editar el archivo **~/.ssh/config** (si no existe crearlo), y agregar la configuración con la siguiente extructura:
```
Host ALIAS_DEL_KEY
HostName bitbucket.org
IdentityFile ~/.ssh/NOMBRE_DEL_KEY
```
En este caso se tiene dos claves SSH, uno **personal** y otro de **trabajo**, y el archivo **config** quedaría de la siguiente forma:
```
Host personal
 HostName bitbucket.org
 IdentityFile ~/.ssh/personal
Host trabajo
 HostName bitbucket.org
 IdentityFile ~/.ssh/trabajo
```
El HostName debe ser reemplazado por la url del repositorio donde se va usar en este caso ambas claves serán para el repositorio de Bitbucket.

Una vez añadida la configuración se debe validar las claves, para ello correr el siguiente comando:
```
ssh-add -l
```
Si retorna sólo una clave SSH es por que aún no reconoce las dos agregadas
```
2048 68:ef:d6:1e:4b:3b:a3:52:6f:b0:c3:4b:da:e8:d1:9f ~/.ssh/personal (RSA)
```
Para que reconozca las demás se debe correr lo siguiente:
```
ssh-add ~/.ssh/ALIAS_DEL_KEY
```
En donde **ALIAS_DEL_KEY** debe ser reemplazado con el alias asignado por ejemplo **trabajo**, depues volver a correr el comando anterior y nos debe mostrar algo similar a esto:
```
2048 68:ef:d6:1e:4b:3b:a3:52:6f:b0:c3:4b:da:e8:d1:9f ~/.ssh/personal (RSA)
2048 1b:24:fe:75:4d:d2:31:a9:d5:4e:65:60:7c:60:7a:a3 ~/.ssh/trabajo (RSA)
```
Por último se debe agregar las claves SSH al Bitbucket o GitHub según convenga.

## Descargar un proyecto con la nueva clave ssh <a id="title2"></a>##
Para descargar un proyecto y asignarle la nueva clave generada se debe cambiar la ruta **bitbucket.org** por el alias creado por ejemplo **personal**, quedando de la siguiente forma:
```
git clone ssh://michaelhernandez@personal:sham4790/myrepo.git
```

## Actualizar ssh de un proyecto existente <a id="title3"></a>##
Si el repositorio ya se encuentra descargado se debe editar el archivo **.git/config** del repositorio descargado y editar la parte del **"remote"**:
```
[remote "origin"]
  fetch = +refs/heads/*:refs/remotes/origin/*
  url = https://michaelhernandez@bitbucket.org/sham4790/myrepo.git
```
Se debe reemplazar la **url** por el siguiente formato:
```
  url = git@ALIAS_DEL_KEY:NOMBRE_REPOSITORIO.git
```
Quedando así:
```
[remote "origin"]
  fetch = +refs/heads/*:refs/remotes/origin/*
  url = git@personal:sham4790/myrepo.git
```
