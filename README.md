Notas del Curso de Github

Estas son anotaciones y textos que obtuve de un curso de Git y Github para establecer una guia personal, por lo que los comandos no cuentan con toda la informacion y opciones que cada uno contiene. Para ver los comandos a mayor detallo puede revisar la [documentacion oficial](https://git-scm.com/doc).

Índice
- [Inicializar Repositorio](#inicializar-repositorio)
- [Confinguracion](#confinguracion)
- [Repositorio Remoto](#repositorio-remoto)
- [Estados de un archivo](#estados-de-un-archivo)
- [Staging Area](#staging-area)
- [Git Commit](#git-commit)
- [Git rm](#git-rm)
  - [rm --cached](#rm---cached)
  - [rm --force](#rm---force)
- [Git Diff](#git-diff)
- [Git Checkout](#git-checkout)
- [Git Reset](#git-reset)
- [Branches (Ramas)](#branches-ramas)
  - [Crear rama](#crear-rama)
  - [Eliminar rama](#eliminar-rama)
  - [Ver Ramas](#ver-ramas)
  - [Git Merge](#git-merge)
- [Configurar SSH](#configurar-ssh)
  - [Generar llave SSH](#generar-llave-ssh)
  - [Encender el servidor de llaves SSH de tu pc (windows y linux)](#encender-el-servidor-de-llaves-ssh-de-tu-pc-windows-y-linux)
  - [Añadir tu llave SSH a este servidor](#añadir-tu-llave-ssh-a-este-servidor)
  - [Conectar repositorio con SSH](#conectar-repositorio-con-ssh)
- [Alias](#alias)
- [Tags](#tags)
  - [Ver Tags](#ver-tags)
  - [Borrar Tag](#borrar-tag)
  - [Publicar Tag en el repositorio remoto](#publicar-tag-en-el-repositorio-remoto)
  - [Borrar Tag del repositorio remoto](#borrar-tag-del-repositorio-remoto)
- [Forks (Github)](#forks-github)
- [Añadir otra fuente remota](#añadir-otra-fuente-remota)
- [Rebase](#rebase)
- [Git Stash](#git-stash)
  - [Recuperar Stash](#recuperar-stash)
  - [Crear una rama con el stash](#crear-una-rama-con-el-stash)
  - [Eliminar elementos del stash](#eliminar-elementos-del-stash)
- [Git Clean](#git-clean)
  - [Revisar que archivos no tienen seguimiento](#revisar-que-archivos-no-tienen-seguimiento)
  - [Eliminar los archivos listados de no seguimiento](#eliminar-los-archivos-listados-de-no-seguimiento)
- [Git Cherry-pick](#git-cherry-pick)
- [Git Log](#git-log)
- [Git Reset y Reflog](#git-reset-y-reflog)
- [Git Ammend](#git-ammend)
- [Git con Grep y log](#git-con-grep-y-log)
  - [Buscar en commits](#buscar-en-commits)
- [Comandos y recursos colaborativos en Git y GitHub](#comandos-y-recursos-colaborativos-en-git-y-github)

# Inicializar Repositorio

<pre>
<code> $ git init</code>
</pre>

# Confinguracion

Establecer nombre de usuario y correo

<pre>
<code>$ git config --global user.name "Example Name"
$ git config --global user.email "example@gmail.com"</code>
</pre>

para poder ver estos datos entre otros se utiliza el comando
<pre>
<code>$ git config -l</code>
</pre>

# Repositorio Remoto

Cambiar nombre de la rama de Master a Main
<pre>
<code>$ git banch -M main</code>  
</pre>
Agregar ruta remota del repositorio
<pre>
 <code>$ git remote add origin https://github.com/ExampleRep/Example.git</code>
</pre>

Cuando el repositorio ya existe pude ser el siguiente orden
<pre>
<code>$ git remote add origin https://github.com/ExampleRep/Example.git
$ git banch -M main</code>
</pre>

Ver origen del Respositorio
<pre>
<code>$ git remote -v</code>
</pre>

Obtener el repositorio remoto incluyendo la historia no relacionada
<pre>
<code>$ git pull origin main --allow-unrelated-histories</code>
</pre>


# Estados de un archivo
Los archivos tienen dos estados:
- Untracked (sin rastrear)
- Tracked (rastreado)

Para establecer un archivo al estado **tracked** se utiliza el comando **Add** esto tambien agrega el archivo al stagin area.  

# Staging Area
El staging es el lugar donde se guardan temporalmente los cambios, para luego ser llevados definitivamente al repositorio

Agregar archivo al stagin area
<pre>
<code>$ git add file.ext</code>
</pre>
Agregar todos los archivos
<pre>
<code>$ git add .</code>
</pre>

# Git Commit 

Luego de agregar el archivo al stagin area debemos agregarlo al repositorio para eso utilzando **git commit**

<pre>
<code>$ git commit -m "mensaje"</code>
</pre>

Si queremos agregar el archivo y a la vez hacer commit utilizamos 

<pre>
<code>$ git commit -am "mensaje"</code>
</pre>

_Nota: **-am** funciona con archivos **tracked** (rastreados) en caso de ser un archivo nuevo tiene que utilizarse el comand **git add**_

# Git rm
El comando **git rm** quita un archivo o grupo de archivos de un repositorio de Git. Se elimina un archivo tanto del equipo como del repositorio de Git.
<pre>
<code>$ git rm file.ext</code>
</pre>

## rm --cached
El indicador Git rm –-cached Elimina los archivos de nuestro repositorio local y del área de staging, pero los mantiene en nuestro disco duro. Básicamente le dice a Git que deje de trackear el historial de cambios de estos archivos, por lo que pasaran a un estado **untracked**.
<pre>
<code>$ git rm --cached file.ext</code>
</pre>

## rm --force

Elimina los archivos de Git y del disco duro. Git siempre guarda todo, por lo que podemos acceder al registro de la existencia de los archivos, de modo que podremos recuperarlos si es necesario (pero debemos usar comandos más avanzados).
<pre>
<code>$ git rm --force file.ext</code>
</pre>

# Git Diff
Enumera los cambios entre el directorio de trabajo actual y el área de ensayo.
<pre>
<code>$ git diff commit-ID-1 commit-ID-2</code>
</pre>

# Git Checkout
Nos permite viajar en el tiempo. Podemos volver a cualquier versión anterior de un archivo específico o incluso del proyecto entero. 
<pre>
<code>$ git checkout commit-ID file.ext</code>
</pre>
Esta también es la forma de crear ramas y movernos entre ellas.

# Git Reset
Nos permite volver en el tiempo y ademas borrar los cambios que hicimos después de ese commit.

Hay dos formas de usar git reset: con el argumento 
- **--hard** : borrando toda la información que tengamos en el área de staging (y perdiendo todo para siempre).
- **--soft** : que mantiene allí los archivos del área de staging para que podamos aplicar nuestros últimos cambios pero desde un commit anterior.

<pre>
<code>$ git reset commit-ID --hard
$ git reset commit-ID --soft
$ git reset HEAD</code>
</pre>

**reset HEAD** es el comando para sacar archivos del área de staging. No para borrarlos ni nada de eso, solo para que los últimos cambios de estos archivos no se envíen al último commit, a menos que cambiemos de opinión y los incluyamos de nuevo en staging con git add, por supuesto.

Para moverse a un commit anterior a HEAD con:
<pre>
<code>$ git reset HEAD^ 
$ git reset HEAD~1
$ git reset --hard 'HEAD@{1}'</code>
</pre>

Para moverse dos commits anteriores a HEAD con:
<pre>
<code>$ git reset HEAD~2</code>
</pre>

# Branches (Ramas)

## Crear rama

Para crear una rama se puede de hacer de dos formas
<pre>
<code>$ git branch nombre-rama</code>
</pre>
Para crear la rama y al mismo tiempo acceder a la rama se utliza:
<pre>
<code>$ git checkout -b nombre-rama</code>
</pre>

## Eliminar rama

Para eliminar un rama local
<pre>
<code>$ git branch -d nombre-rama</code>
</pre>
Para forzar la eliminacion en caso de algun error
<pre>
<code>$ git branch -D nombre-rama</code>
</pre>
Eliminar rama del repositorio remoto
<pre>
<code>$ git push origin :nombre-rama</code>
</pre>

## Ver Ramas
Ver ramas del repositorio local
<pre><code>$ git branch</code></pre>
Ver ramas del repositorio remoto
<pre><code>$ git branch -r</code></pre>
Ver todas las ramas
<pre><code>$ git branch -a</code></pre>

## Git Merge

Pasar los cambios de una rama a otra
<pre>
<code>$ git rama-destino merge rama-con-cambios</code>
</pre>

#
#
# Configurar SSH

## Generar llave SSH

<pre>
<code>ssh-keygen -t rsa -b 4096 -C "tu-correo@email.com"</code>
</pre>
donde:
- **-t**  : se utiliza para seleccionar el algoritmo
- **-b**  : se utiliza para establecer el tamaño de la clave
- **rsa** : un antiguo algoritmo basado en la dificultad de factorizar grandes números. Se recomienda un tamaño de clave de al menos 2048 bits para RSA; 4096 bits es mejor.
- **-C**  : para establecer el correo electronico

## Encender el servidor de llaves SSH de tu pc (windows y linux)

<pre>
<code>eval $(ssh-agent -s)</code>
</pre>

## Añadir tu llave SSH a este servidor

<pre>
<code>ssh-add ruta-donde-guardaste-tu-llave-privada</code>
</pre>
Supuniendo que se guardo en la ruta home del computador podemos usar 
<pre>
<code>~ -> este contiene la ruta del home
ssh-add ~/.ssh/id_rsa</code>
</pre>

## Conectar repositorio con SSH

Si ya se tiene una conexion con http para cambiar el origin del repositorio a ssh se utiliza el siguiente comando
<pre>
<code>$ git remote set-url origin ssh-url</code>
</pre>

# Alias

Nota: en la terminal de VsCode puede que presente error. En cambio en git bash funciona sin problema

<pre>
<code>$ alias nombre="comando"</code>
</pre>
Ejemplo

<pre>
<code>$ alias superlog="git log --graph --decorate --oneline"</code>
</pre>
para utilizarlo solamente se llama al alias ej.
<pre>
<code>$ superlog</code>
</pre>

Alias en Git
<pre><code>$ git config --global alias.alias "comando"</code></pre>

# Tags

<pre>
<code>$ git tag -a nombre-del-tag commit-ID</code>
</pre>
Tambien puede escribir un mensaje
<pre>
<code>$ git tag -a nombre-del-tag -m "mensaje" commit-ID</code>
</pre>

## Ver Tags
<pre><code>$ git tag</code></pre>
otra forma con mas detalles
<pre><code>$ git show-ref --tags</code></pre>

## Borrar Tag
<pre><code>$ git tag -d nombre-del-tag</code></pre>

## Publicar Tag en el repositorio remoto
<pre><code>$ git push origin --tags</code></pre>

## Borrar Tag del repositorio remoto
<pre><code>$ git tag -d nombre-del-tag
$ git push origin :refs/tags/nombre-del-tag</code></pre>

# Forks (Github)

Los forks o bifurcaciones son una característica única de GitHub en la que se crea una copia exacta del estado actual de un repositorio directamente en GitHub. Este repositorio podrá servir como otro origen y se podrá clonar (como cualquier otro repositorio). En pocas palabras, lo podremos utilizar como un nuevo repositorio git cualquiera

# Añadir otra fuente remota

<pre>
<code>$ git remote add nombre-cualquiera URL-Repositorio</code>
</pre>
por ejemplo
<pre>
<code>$ git remote add upstream https://github.com/ExampleRep/Example.git</code>
</pre>

Con esto podriamos tener un repositorio Fork como **origin** y el repositorio original en **upstream** para obtener los cambios que este reciba para que nuestro Fork no se quede atras. O no necesariamente con repositorios Fork, sino donde se requiera tener mas de una fuente remota.

# Rebase

Rebase es el proceso de mover o combinar una secuencia de confirmaciones en una nueva confirmación base. Reescribe la historia del repositorio, cambia la historia de donde comenzó la rama y solo debe ser usado de manera local ya que hacerlo a un repositorio remoto no se considera buena practica.

Primero tenemos que hacer rebase a la rama experimental

<pre>
<code>$ git checkout feature
$ git rebase main</code>
</pre>

y luego hacemos rebase a la rama main

<pre>
<code>$ git checkout main
$ git rebase feature</code>
</pre>

A nivel de historia del log la rama feature no exitió, por eso no es buena practica en repositorios remotos ya que es mejor que la historia quede intacta.

# Git Stash

El stashed nos sirve para guardar cambios para después, Es una lista de estados que nos guarda algunos cambios que hicimos en Staging para poder cambiar de rama sin perder el trabajo que todavía no guardamos en un commit

Ésto es especialmente útil porque hay veces que no se permite cambiar de rama, ésto porque tenemos cambios sin guardar, no siempre es un cambio lo suficientemente bueno como para hacer un commit, pero no queremos perder ese código en el que estuvimos trabajando.

El stashed nos permite cambiar de ramas, hacer cambios, trabajar en otras cosas y, más adelante, retomar el trabajo con los archivos que teníamos en Staging, pero que podemos recuperar, ya que los guardamos en el Stash.

<pre>
<code>$ git stash</code>
</pre>
Este comando guarda el trabajo actual del Staging en una lista diseñada para ser temporal llamada Stash, para que pueda ser recuperado en el futuro.

Podemos poner un mensaje en el stash, para asi diferenciarlos en git stash list por si tenemos varios elementos en el stash
<pre>
<code>$ git stash save "mensaje"</code>
</pre>

## Recuperar Stash
Para recuperar los últimos cambios desde el stash a tu staging area utiliza el comando
<pre>
<code>$ git stash pop</code>
</pre>

Para aplicar los cambios de un stash específico y eliminarlo del stash
<pre>
<code>$ git stash pop 'stash@{numero}'</code>
</pre>

para ver el numero del stash puede verse con 
<pre>
<code>$ git stash list</code>
</pre>

Para retomar los cambios de una posición específica del Stash puedes utilizar el comando
<pre>
<code>$ git stash apply 'stash@{numero}'</code>
</pre>

## Crear una rama con el stash

Para crear una rama y aplicar el stash más reciente podemos utilizar el comando
<pre>
<code>$ git stash branch nombre-rama</code>
</pre>

Si deseas crear una rama y aplicar un stash específico (obtenido desde git stash list) puedes utilizar el comando
<pre>
<code>$ git stash branch nombre_de_rama 'stash@{numero}'</code>
</pre>

## Eliminar elementos del stash

Para eliminar los cambios más recientes dentro del stash (el elemento 0), podemos utilizar el comando
<pre>
<code>$ git stash drop</code>
</pre>

Pero si, en cambio, conoces el índice del stash que quieres borrar (mediante git stash list) puedes utilizar el comando
<pre>
<code>$ git stash drop 'stash@{numero}'</code>
</pre>

Si, en cambio, deseas eliminar todos los elementos del stash, puedes utilizar
<pre>
<code>$ git stash clear</code>
</pre>

# Git Clean

Mientras estamos trabajando en un repositorio podemos añadir archivos a él, que realmente no forma parte de nuestro directorio de trabajo, archivos que no se deberían de agregar al repositorio remoto.

El comando clean actúa en archivos sin seguimiento, este tipo de archivos son aquellos que se encuentran en el directorio de trabajo, pero que aún no se han añadido al índice de seguimiento de repositorio con el comando add.

<pre>
<code>$ git clean</code>
</pre>

La ejecución del comando predeterminado puede producir un error. La configuración global de Git obliga a usar la opción **force** con el comando para que sea efectivo. Se trata de un importante mecanismo de seguridad ya que este comando no se puede deshacer.

## Revisar que archivos no tienen seguimiento
<pre>
<code>$ git clean --dry-run</code>
</pre>

## Eliminar los archivos listados de no seguimiento
<pre>
<code>$ git clean -f</code>
</pre>

# Git Cherry-pick

Es un comando que permite tomar uno o varios commits de otra rama sin tener que hacer un merge completo. Así, gracias a cherry-pick, podríamos aplicar los commits relacionados con nuestra funcionalidad en la rama master sin necesidad de hacer un merge.
<pre>
<code>$ cherry-pick commit-ID</code>
</pre>

# Git Log
Muestra el registro de commits realizados 
<pre>
<code>$ git log</code>
</pre>

# Git Reset y Reflog

Git guarda todos los cambios aunque decidas borrarlos, al borrar un cambio lo que estás haciendo sólo es actualizar la punta del branch, para gestionar éstas puntas existe un mecanismo llamado registros de referencia o reflogs
<pre>
<code>$ git reflog
$ git reset --hard HASH-del-Commit</code>
</pre>

puede user 
- --hard
- --soft

en la seccion de [reset](#Git-Reset) se muestran sus significados


# Git Ammend

Remendar un commit con amend puede modificar el commit más reciente (enmendar) en la misma rama. 

Este comando sirve para agregar archivos nuevos o actualizar el commit anterior y no generar commits innecesarios. También es una forma sencilla de editar o agregar comentarios al commit anterior porque abrirá la consola para editar este commit anterior.

<pre>
<code>$ git add file.ext
$ git commit --amend</code>
</pre>

En caso de no querer editar el mensaje puede usarse:
<pre>
<code>$ git commit --amend --no-edit</code>
</pre>

# Git con Grep y log

A medida que nuestro proyecto en Git se hace más grande, vamos a querer buscar ciertas cosas.

Por ejemplo: ¿cuántas veces en nuestro proyecto utilizamos la palabra color?

Para buscar, empleamos el comando 
<pre><code>$ git grep color</code></pre> 
y nos buscará en todo el proyecto los archivos en donde está la palabra color.

Con el siguiente comando nos saldrá un output el cual nos dirá en qué línea está lo que estamos buscando.
<pre><code>$ git grep -n color</code></pre> 


Con **-c** nos saldrá un output el cual nos dirá cuántas veces se repite esa palabra y en qué archivo.
<pre><code>$ git grep -c color</code></pre> 

Si queremos buscar cuántas veces utilizamos un atributo de HTML lo hacemos con:

## Buscar en commits
<pre><code>$ git log valor-a-buscar</code></pre> 

# Comandos y recursos colaborativos en Git y GitHub

A continuación veremos una lista de comandos colaborativos para facilitar el trabajo remoto en GitHub:

muestra cuantos commit han hecho cada miembro del equipo.
<pre><code>$ git shortlog -sn</code></pre> 

muestra cuantos commit han hecho cada miembro del equipo, hasta los que han sido eliminados.
<pre><code>$ git shortlog -sn --all</code></pre>

muestra cuantos commit ha hecho cada miembro, quitando los eliminados sin los merges.
<pre><code>$ git shortlog -sn --all --no-merge</code></pre> 

muestra quien hizo cada cosa línea por línea.
<pre><code>$ git blame ARCHIVO</code></pre> 

muestra como funciona el comando.
<pre><code>$ git COMANDO --help</code></pre>

muestra quien hizo cada cosa línea por línea, indicándole desde qué línea ver. Ejemplo -L35,50.
<pre><code>$ git blame ARCHIVO -Llinea_inicial,linea_final</code></pre> 

se muestran todas las ramas remotas.
<pre><code>$ git branch -r</code></pre> 

se muestran todas las ramas, tanto locales como remotas.
<pre><code>$ git branch -a</code></pre> 


 









