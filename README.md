# Notas del Curso de Github

Índice
- [Establecer Repositorio Remoto]( #Establecer-Repositorio-Remoto)

# Inicializar Repositorio

<pre>
<code> $ git init</code>
</pre>

# Confinguracion

**Establecer nombre de usuario y correo**

<pre>
<code>$ git config --global user.name "Example Name"
$ git config --global user.email "example@gmail.com"</code>
</pre>

para poder ver estos datos entre otros se utiliza el comando
<pre>
<code>$ git config -l</code>
</pre>


# Establecer Repositorio Remoto

 - **Cambiar nombre de la rama de Master a Main**
<pre>
<code>$ git banch -M main</code>  
</pre>
- **Agregar ruta remota del repositorio**
<pre>
 <code>$ git remote add origin https://github.com/ExampleRep/Example.git</code>
</pre>

**Cuando el repositorio ya existe pude ser el siguiente orden**
<pre>
<code>$ git remote add origin https://github.com/ExampleRep/Example.git
$ git banch -M main</code>
</pre>

# Ver url del repositorio origen
<pre>
<code>$ git remote -v</code>
</pre>

# Comandos sobre un archivo

## **Estados de un archivo**
Los archivos tienen dos estados:
- Untracked (sin rastrear)
- Tracked (rastreado)

Para establecer un archivo al estado **tracked** se utiliza el comando **Add** esto tambien agrega el archivo al stagin area.  

## **Staging Area**
El staging es el lugar donde se guardan temporalmente los cambios, para luego ser llevados definitivamente al repositorio

Agregar archivo al stagin area
<pre>
<code>$ git add file.ext</code>
</pre>
Agregar todos los archivos
<pre>
<code>$ git add .</code>
</pre>

## Comando **git rm**
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


### Ver historial de un archivo
<pre>
<code>$ git log archivo.ext</code>
</pre>

### Ver la diferencia entre dos versiones de un archivo

<pre>
<code>$ git diff commit-ID-1 commit-ID-2</code>
</pre>

## Git Checkout
Nos permite viajar en el tiempo. Podemos volver a cualquier versión anterior de un archivo específico o incluso del proyecto entero. 
<pre>
<code>$ git checkout commit-ID file.ext</code>
</pre>
Esta también es la forma de crear ramas y movernos entre ellas.

## **Git Reset**
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

# **Branches (Ramas)**

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

## Git Merge

Pasar los cambios de una rama a otra
<pre>
<code>$ git rama-destino merge rama-con-cambios</code>
</pre>

# 
<pre>
<code>$ git pull origin main --allow-unrelated-histories</code>
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

## Encender el “servidor” de llaves SSH de tu computadora (windows y linux)

<pre>
<code>eval $(ssh-agent -s)</code>
</pre>

## Añadir tu llave SSH a este “servidor”

<pre>
<code>ssh-add ruta-donde-guardaste-tu-llave-privada</code>
</pre>
Supuniendo que se guardo en la ruta home del computador podemos usar 
<pre>
<code>~ -> este contiene la ruta del home
ssh-add ~/.ssh/id_rsa</code>
</pre>

# Conectar repositorio con SSH

## Cambiar origin del repo
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

## Borrar tag
<pre><code>$ git tag -d nombre-del-tag</code></pre>

## Publicar tag en el repositorio remoto
<pre><code>$ git push origin --tags</code></pre>

## Borrar tag del repositorio remoto
<pre><code>$ git tag -d nombre-del-tag
$ git push origin :refs/tags/nombre-del-tag</code></pre>

# Forks (Github)

Los forks o bifurcaciones son una característica única de GitHub en la que se crea una copia exacta del estado actual de un repositorio directamente en GitHub. Este repositorio podrá servir como otro origen y se podrá clonar (como cualquier otro repositorio). En pocas palabras, lo podremos utilizar como un nuevo repositorio git cualquiera











