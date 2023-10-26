<h1 align="center">
  Git Commands
</h1>

`Git` es un software de control de versiones, pensando en la eficiencia, la confiabilidad y compatibilidad del mantenimiento de versiones de aplicaciones cuando estas tienen un gran número de archivos de código fuente.

> [!NOTE]
> Debes tener **Git** Instalado o actualizado https://git-scm.com/downloads.

Para comprobar la instalación ingresamos por **CMD** la siguiente línea de comando `git --version`  
El cual nos dará la versión que disponemos por ejemplo `git version 2.42.0.windows.2` caso contrario dará error y se tendrá que hacer la instalación.

A continuación, se detallará cada uno de los comandos de *Git* empezando por lo básico.

##  Git Basico

- `git config --global user.name "your name"` o `git config --global user.email "your email"`

Estos comandos de Git nos permiten setear el nombre y el correo en las configuraciones de Git.  
Para comprobar si están agregados ingresamos el siguiente comando `git config --list`  
Aparecerán muchas configuraciones relacionadas a Git pero la que acabamos de configurar es el name y email tal como se muestra en la siguiente imagen.

![gitConfig--list](img/gitConfig--list.png)

- `git init`

Para crear un repositorio local debemos crear una carpeta con un nombre y por Consola o CMD debemos ir a la carpeta con **cd** ya ubicado en la carpeta debemos inicializar, con el siguiente comando `git init`  


```
Initialized empty Git repository in C:/Users/LuisChi/Desktop/clase Maestria/my-first-repo/.git/
```
En la carpeta se nos crea un nuevo directorio **.git**

![carpetaGitInit](img/carpetaGitInit.png)

- `git status`

Este comando nos permite ver en que rama estamos, que cambios, nuevo por cambiar tenemos.  
La salida del comando es la siguiente
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.js

nothing added to commit but untracked files present (use "git add" to track)
```
otro ejemplo

![statusmultiple](img/statusmultiple.png)

- `git add index.js` o `git add .`

`git add index.js` este nos permite agregar los cambios por archivo.  
`git add .` este agrega todos los cambios de todos los archivos con cambios.  
Y con `git status` podemos ver los archivos con cambios que se agregaron
```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   index.js
```
- `git commit -m "primer commit"`

Este comando crea un **commit** de todos los cambios agregados por el comando `git add .`  
La salida del comando es la siguiente
```
[master (root-commit) 143d0fc] primer commit
 1 file changed, 3 insertions(+)
 create mode 100644 index.js
 ```
- `git log`

Muestra todo los **commits** creados dentro del repositorio.
```
commit 5f6b0cb7b1715e8caa84a394b240bd8a4ad9a2fb (HEAD -> master)
Author: lchichan <lchichan@pichincha.com>
Date:   Wed Oct 25 00:29:16 2023 -0500

    add index2

commit 143d0fc3ba4185e37ac47bc98742833c67f75dad
Author: lchichan <lchichan@pichincha.com>
Date:   Wed Oct 25 00:04:51 2023 -0500

    primer commit
```
- `git diff`

Este comando nos permite ver los cambios echo en los archivos ya agregados por el comando `git add .`,  
los archivos nuevos no se ven cambios porque no tienen con que comparar.
```
diff --git a/index.js b/index.js
index 36ba89b..b59c02b 100644
--- a/index.js
+++ b/index.js
@@ -1,3 +1,6 @@
 function suma(a,b){
     return a+b;
+}
+function subtract(a,b){
+    return a-b;
 }
\ No newline at end of file
```

## Trabajo en equipo con Git

- `git checkout -b luischi/tarea-1` o `git branch luischi/tarea-1`

Estos comandos crean una rama a partir de la que estamos, la diferencia es que uno automáticamente nos pasa a la nueva rama y esto se logra con el `git checkout -b luischi/tarea-1`  
A continuación, podemos ver que con el `git status` nos dice que estamos en la nueva rama creada y que no tenemos cambios

```
C:\Users\LuisChi\Desktop\clase Maestria\my-first-repo>git checkout -b luischi/tarea-1
Switched to a new branch 'luischi/tarea-1'

C:\Users\LuisChi\Desktop\clase Maestria\my-first-repo>git status
On branch luischi/tarea-1
nothing to commit, working tree clean
```
![gitCheckout](img/gitCheckout.png)

```mermaid
    gitGraph
       commit
       commit
       branch luischi/tarea-1
       commit
       checkout main
       commit
```

Con el otro comando me crea la rama pero me mantengo en la **main o master** o en la rama que estemo.

![gitBranch](img/gitBranch.png)

- `git checkout master`

Este nos permite cambiarnos de rama

![gitramaCheckout](img/gitramaCheckout.png)

Como funciona esto de las **ramas** a continuación se observa un pequeño grafico el cual del nodo **A** vendría siendo main o master de el se desprenden nuevas ramas podemos podemos añadir código dependiendo del requerimiento.

```mermaid
graph LR;
    A-->B;
    A-->C;
```

Cuál es el objetivo de crear múltiples ramas es que los desarrolladores puedan trabajar simultáneamente sin intervenir en el trabajo del otro.

- `git branch`

Con `git branch` podemos ver todas las ramas que existen y además nos da la indicación en que rama nos encontramos ubicado.

![gitBranch2](img/gitBranch2.png)

- `git merge luischi/tarea-1`

Este comando sirve para unir una rama dentro de otra.  
Ya ejecutado nos dice que archivo se han agregado o han sufrido cambios.

```
C:\Users\LuisChi\Desktop\clase Maestria\my-first-repo>git merge luischi/tarea-1
Updating 5f6b0cb..bfb22e2
Fast-forward
 index.js | 3 +++
 1 file changed, 3 insertions(+)
 ```
Hay que tener cuidado por que se da el caso de que en las diferentes ramas se trabajan con los mismos archivos o lineas y a la hora de unir aparecen conflictos tal como se muestra a continuación:

```
C:\Users\LuisChi\Desktop\clase Maestria\my-first-repo>git merge luischi/tarea2
Auto-merging index.js
CONFLICT (content): Merge conflict in index.js
Automatic merge failed; fix conflicts and then commit the result.
```
Esto sucedió porque dos desarrolladores trabajaron en las mismas líneas, en el código podemos ver que la función multiply es la que ya teníamos o la que se agrego a master en el primer merge y cuando se hiso el segundo merge ocurrió el conflicto por que agrego en la misma línea otra función llamada divide.

![codeConflict](img/codeConflict.png)

Como se soluciona primero revisar si necesitamos los dos cambios después solucionar manual mente, también el visual code o cualquier otra herramienta o Ide nos pude ayudar aceptando que cambios queremos mantener o ambos.

Si hacemos `git status` podemos ver que todavía aparece el conflicto. Después de eso lo agregamos con `git add .`

```
C:\Users\LuisChi\Desktop\clase Maestria\my-first-repo>git status
On branch master
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   index.js

no changes added to commit (use "git add" and/or "git commit -a")
```

Después del `git add .` le hacemos git status y nos pedirá que hagamos un `git commit`

```
C:\Users\LuisChi\Desktop\clase Maestria\my-first-repo>git add .

C:\Users\LuisChi\Desktop\clase Maestria\my-first-repo>git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:
        modified:   index.js
```
Automáticamente se nos abrirá un editor de consola el cual debemos guardarlo

![editorConsola](img/editorConsola.png)

Después de guardar se creará un nuevo **commit**

```
C:\Users\LuisChi\Desktop\clase Maestria\my-first-repo>git commit
[master 9870458] Merge branch 'luischi/tarea2'
```
![commitLogMerge](img/commitLogMerge.png)

