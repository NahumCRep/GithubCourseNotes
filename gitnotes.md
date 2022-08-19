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