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

### Ver historial de un archivo

<pre>
<code>$ git log archivo.ext</code>
</pre>