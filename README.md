# Documentacion

## Parte 1:

Engadimos a carpeta cos documentos que fixemos antes a un novo repositorio local

---------------------------------

**entrada:**
`$git init`

**saida:**

Initialized empty Git repository in C:/Users/Hp/prueba_git/.git/

---------------------------------

Isto crea un directorio denominado .git, onde gardamos toda a información do histórico do repositorio.

Neste momento os dous arquivos que temos dentro son **untracked**, é dicir, que git non os ten en conta para ser parte do repositorio.

Podemos velo co seguinte comando:

**entrada:**

`$ git status`

**saida:**

```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        script.sh.txt
        texto.txt.txt

nothing added to commit but untracked files present (use "git add" to track)
```

---------------------------------

Os arquivos están no directorio, pero non xestionados por git. Os arquivos non xestionados non se replicarán noutras máquinas coas que estexamos compartindo.

Se nos fixamos, na primeira liña pon **master**, se usamos o seguinte prompt podemos cambiar este nome a **main**, por exemplo:

**entrada**

`$ git branch -m main`

**saida**

`Hp@DESKTOP-V2N8KPD MINGW64 ~/prueba_git (main)`

Para restauralo a master simplemente poñemos ->  `$ git branch -m master`

---------------------------------

Para engadir a arquivos rastreados introducidos a seguinte liña: 

**entrada**

`$ git add script.sh`
`$ git status`

**saida**

```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   script.sh

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        texto.txt
```

script.sh pasa a ser **tracked**, é dicir, rastreado. Agora queda texto.txt sen estar rastreado. rastreado significa que comprobará se hai cambios desde a última versión, ainda que para iso ten que estar confirmado, agora mesmo non se sincroniza cos equipos remotos.

Polo tanto temos que confirmar ou facer un commit.

**entrada**

`$ git commit -m "confirmación inicial"`

**saida**
```
[master (root-commit) 72ba43d] confirmación inicial
 1 file changed, 2 insertions(+)
 create mode 100644 script.sh
``` 

**entrada**

`$ git status`

**saida**
``` 
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        texto.txt

nothing added to commit but untracked files present (use "git add" to track)
``` 
Aparécenos o aviso de que **texto.txt** ainda non está en seguemento. O resto está gardado como versión. Cando confirmamos engadimos unha mensaxe que queda gardada con cada commit.

---------------------------------

Coa seguinte liña podemos buscar os ultimos commit:

**entrada**

` $ git log` 

**saida**
``` 
commit 72ba43d99382d41e20876f5e985343ad06b85c38 (HEAD -> master)
Author: Roi <roiduarte.drive@gmail.com>
Date:   Mon Oct 26 12:43:48 2026 +0100

    confirmación inicial
``` 
Coa seguinte liña, usando as 4 ou 6 primeiras cifras do numero do commit, podemos ver o que hai gardado dentro do hash: 

**entrada**
` $ git cat-file 72ba -t` 
**saida**
commit

Engadimos texto:

**entrada**
`$ git add texto.txt` 
`$ git commit -m "Añadido archivo texto.txt"`
**saida**
```
[master 0876a23] Añadido archivo texto.txt
 1 file changed, 3 insertions(+)
 create mode 100644 texto.txt
 ```

 Comprobamos:

**entrada**
`$ git status`
**saida**
```
On branch master
nothing to commit, working tree clean
```

Está todo confirmado.

Engadimos "cuatro" ao arquivo texto.txt. Se comprobamos...

**entrada**
`$ git status`
**saida**
```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Avisanos de que se modificou texto.txt. Para preparalo para o seguinte commit hai que executar de novo add. Ademais de engadir rastreos a novos arquivos tamén os prepara para o seguinte commit.

**entrada**

`$ git add texto.txt`
`$ git status`

**saida**
```
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   texto.txt
```
Antes de facer un commit engadimos a texto "cinco". Se comprobamos con git status sáenos que aparece en stage (preparado para commit) e en modificado sen preparar.

Se se fai commit agora, confirmaríase a versión anterior, non a última modificada. Ao sincronizar con outro equipo sincronizaría esa versión. Temos que facer add se queremos incluir todo.

**entrada**
```
$ git add texto.txt
$ git commit -m "Ampliada la explicación del texto"
```
**saida**
```
[master 533ad53] Ampliada la explicación del texto
 1 file changed, 3 insertions(+), 1 deletion(-)
 ```

**entrada**
`$ git status`
**saida**
```
On branch master
nothing to commit, working tree clean
```

Volve a estar todo limpo.

Para non ter que estar constantemente engadindo e confirmando podemos resumir isto coa seguinte liña.

**entrada**

`$ git commit -a -m “Nueva versión”`

Hay que ter en conta que se hai un novo archivo estamos obrigados a facer un add. Só é válido para modificacións.

-------------------

Se queremos ver información sobre a última versión modificada:

**entrada**


`$ git show`

**saida** 
```
commit 533ad53fc741d5e5829b8f50cb287636c3cfedd9 (HEAD -> master)
Author: Roi <roiduarte.drive@gmail.com>
Date:   Mon Oct 26 13:47:34 2026 +0100

    Ampliada la explicación del texto

diff --git a/texto.txt b/texto.txt
index 3664b17..d92e49a 100644
--- a/texto.txt
+++ b/texto.txt
@@ -1,3 +1,5 @@
 uno
 dos
-tres
\ No newline at end of file
+tres
+cuatro
+cinco
\ No newline at end of file
```

Se hai moito contido podemolo ver cos cursores e q para rematar.

------------

Se queremos ver os cambios que se realizaron en forma de historico:

**entrada**
 
`$ git log`

**saida**
```
commit 533ad53fc741d5e5829b8f50cb287636c3cfedd9 (HEAD -> master)
Author: Roi <roiduarte.drive@gmail.com>
Date:   Mon Oct 26 13:47:34 2026 +0100

    Ampliada la explicación del texto

commit 0876a233255d03587962992c5cb0af3cc1a577e8
Author: Roi <roiduarte.drive@gmail.com>
Date:   Mon Oct 26 13:01:07 2026 +0100

    Añadido archivo texto.txt

commit 72ba43d99382d41e20876f5e985343ad06b85c38
Author: Roi <roiduarte.drive@gmail.com>
Date:   Mon Oct 26 12:43:48 2026 +0100

    confirmación inicial
```

Isto é un log dos 3 commit que realizamos antes. Indica en que rama estamos traballando, o autor, a data e a hora.

Podemos ver os commit por separado con mais información coa seguinte liña:

**entrada**

`$ git cat-file *hash* -p `

-------------

Borrei a liña "tres" e engadín a liña "cinco" no arquivo "texto.txt"

Para coñecer as diferencias entre un arquivo modificado e o que se confirmou na última versión pódese usar o comando:

**entrada**

`$ git diff`

Devolve unha resposta en "Formato Unificado" (Unified format) o cal é un formato específico para ver diferencias entre arquivos.

**saida**
```
diff --git a/texto.txt b/texto.txt
index d92e49a..ea169a0 100644
--- a/texto.txt
+++ b/texto.txt
@@ -1,5 +1,5 @@
 uno
 dos
-tres
 cuatro
-cinco
\ No newline at end of file
+cinco
+seis
\ No newline at end of file
```

A parte importante comeza por dobre arroba (@@), o **-** lese como "arquivo previo" e o **+** como arquivo final. Aquí indícanos que se mostrar as filas da 1 á 5 no arquivo orixe e no final, o primeiro numero indica a fila inicial e o segundo a cantidade de liñas.

--------

**entrada**

`$ git commit -a -m "Probando diff"`

**saida**

```
[master ce2ea8d] Probando diff
 1 file changed, 2 insertions(+), 2 deletions(-)
 ```

 Da información do engadido e do eliminado.

 Engadimos "siete" ao arquivo "texto.txt" e probamos de novo:

 **entrada**

`$ git diff"`

**saida**

```
diff --git a/texto.txt b/texto.txt
index ea169a0..6acce31 100644
--- a/texto.txt
+++ b/texto.txt
@@ -2,4 +2,5 @@ uno
 dos
 cuatro
 cinco
-seis
\ No newline at end of file
+seis
+siete
\ No newline at end of file
```

Agora a @@ indica que o arquivo previo (-) preséntase a partires da liña 2 só 4 liñas (2,4) e no modificado preséntase a partir da liña 2, 5 liñas mais (2,5)

-------- 

Para evitar xestionar arquivos innecesarios, como un .class nun proxecto java, debemos crear un arquivo no propio directorio de traballo co nome ".gitignore"

Para este caso podemos escribir:

```

# ignora os arquivos rematados en .class
*.class

# ignora os arquivos rematados en ~
*.~

# pero non importante~
!importante~

```

--------

Para probalo:

Engadimos ao noso directorio o arquivo "Hola.java". Co seguinte codigo dentro:

```
class Hola {
  public static void main(String[] args){
    System.out.println("Welcome to the Java World");
  }
}
```

creamos tamén un arquivo temporal~ e outro importante~, ambos vacios.

Se executamos a seguinte liña:

**entrada**

`$ ls -a`

deberiamos obter o seguinte listado:

**saida**


```
.
.git
Hola.java
script.sh
texto.txt
..
.gitignore importante~
temporal~
```

Compilamos "Hola.java" para que apareza o .class.

**entrada**

`$ git status`

**saida**

```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   texto.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore
        Hola.java
        importante~

no changes added to commit (use "git add" and/or "git commit -a")

```

Podemos ver que algúns arquivos ignóranse.


**entrada**
```
$ git add .
$ git commit -m “Añadidos fuentes en java y archivos importantes”
```

Co **.** indicámoslle a add que engada todo o que está pendente.

**saída**

```
[master 83eb263] Añadidos fuentes en java y archivos importantes
4 files changed, 15 insertions(+)
create mode 100644 .gitignore
create mode 100644 Hola.java
create mode 100644 importante~
```

Para ver os arquivos que hai no directorio tras o último commit na rama principal

**entrada**

`$ git ls-tree --name-only -r HEAD`

**saida**

```
.gitignore
Hola.java
importante~
script.sh
texto.txt
```

**entrada**

`$ git log`

**saida**
```
commit 881632351b672b6512e41998e06c414e8a64be82 (HEAD -> master)
Author: Roi <roiduarte.drive@gmail.com>
Date:   Fri Oct 30 17:36:37 2026 +0100

    Añadidos fuentes en java y archivos importantes

commit ce2ea8d7f8e6641a7f3d1bbf8e5da542f2a48cb4
Author: Roi <roiduarte.drive@gmail.com>
Date:   Fri Oct 30 13:13:43 2026 +0100

    Probando diff

commit 533ad53fc741d5e5829b8f50cb287636c3cfedd9
Author: Roi <roiduarte.drive@gmail.com>
Date:   Mon Oct 26 13:47:34 2026 +0100

    Ampliada la explicación del texto

commit 0876a233255d03587962992c5cb0af3cc1a577e8
Author: Roi <roiduarte.drive@gmail.com>
Date:   Mon Oct 26 13:01:07 2026 +0100

    Añadido archivo texto.txt

commit 72ba43d99382d41e20876f5e985343ad06b85c38
Author: Roi <roiduarte.drive@gmail.com>
Date:   Mon Oct 26 12:43:48 2026 +0100

    confirmación inicial

```

Collemos o numero dalgun commit para con un show conseguir informacion do commit

**entrada**

`$ git show 72ba43d99382d41e20876f5e985343ad06b85c38`

**saída**
```
commit 72ba43d99382d41e20876f5e985343ad06b85c38
Author: Roi <roiduarte.drive@gmail.com>
Date:   Mon Oct 26 12:43:48 2026 +0100

    confirmación inicial

diff --git a/script.sh b/script.sh
new file mode 100644
index 0000000..273df79
--- /dev/null
+++ b/script.sh
@@ -0,0 +1,2 @@
+echo Listado completo
+ls -l
```

------

Para nombrar versións usamos tag:

**entrada**
```
$ git tag 0.7
$ git tag 0.3 72ba43d99382d41e20876f5e985343ad06b85c38
$ git log --oneline
```

**saída**
```
8816323 (HEAD -> master, tag: 0.7) Añadidos fuentes en java y archivos importantes
ce2ea8d Probando diff
533ad53 Ampliada la explicación del texto
0876a23 Añadido archivo texto.txt
72ba43d (tag: 0.3) confirmación inicial
```

`$ git log --oneline` é unha forma resumida de escribir o log.

------

Para crear unha rama no noso proxecto, é dicir, arquivos en paralelo, escribimos a seguinte liña:

**entrada**

`$ git branch Prueba`

Para ver las dos ramas escribimos 

`$ git log --oneline `


**saída**
```
8816323 (HEAD -> master, tag: 0.7, Prueba) Añadidos fuentes en java y archivos importantes
ce2ea8d Probando diff
533ad53 Ampliada la explicación del texto
0876a23 Añadido archivo texto.txt
72ba43d (tag: 0.3) confirmación inicial
```

Se escribimos `$ git branch ` podemos ver as ramas do proxecto:

**entrada**
`$ git branch `

**saída**
 ```
  Prueba
* master
 ```

 O asterisco marca a rama coa que estamos traballando. As ramas almacénanse no directorio .git/refs/heads

 para cambiar á rama prueba:

 **entrada**

   `$ git switch Prueba `

   **saída**

  ```
   Switched to branch 'Prueba'
Hp@DESKTOP-V2N8KPD MINGW64 ~/prueba_git (Prueba)
  ```

**entrada**
  
`$ git branch`

**saida**
```
* Prueba
  master
```

Podemos ver que agora o asterisco está en Prueba

**entrada**
`$ git log --oneline`

**saída**
```
8816323 (HEAD -> Prueba, tag: 0.7, master) Añadidos fuentes en java y archivos importantes
ce2ea8d Probando diff
533ad53 Ampliada la explicación del texto
0876a23 Añadido archivo texto.txt
72ba43d (tag: 0.3) confirmación inicial
```

Agora HEAD, que é o punteiro de traballo, apunta a Prueba, por tanto, todo commit que se faga, farase nesa rama, deixando a principal intacta.

Engandinlle a seguinte liña ao arquivo Hola.java:

`System.out.println("I have no more branches to commit, said the Ent");`

**entrada**

`$ git commit -a -m "Llegan los Ents a Java"`

**saída**

`[Prueba d49df45] Llegan los Ents a Java`

**entrada**
```
$ git tag v0.7-Ent-Release
$ git log --oneline

```

**saída**
```
d49df45 (HEAD -> Prueba, tag: v0.7-Ent-Release) Llegan los Ents a Java
8816323 (tag: 0.7, master) Añadidos fuentes en java y archivos importantes
ce2ea8d Probando diff
533ad53 Ampliada la explicación del texto
0876a23 Añadido archivo texto.txt
72ba43d (tag: 0.3) confirmación inicial
```

**entrada**

`$ git switch master`

**saida**
`Switched to branch 'master'`

**entrada**
`$ cat Hola.java`

Con isto comprobamos se na rama principal Hola.java segue sendo como antes, é dicir, comprobamos se están separados.

**saída**
```
class Hola {
    public static void main(String[] args) {
        System.out.println("Welcome to the Java World");
    }
}
```

Non aparece a nova liña, así que efectivamente, as ramas están funcionando correctamente. Se os cambios experimentais na rama Prueba nos convencen podemos xuntar as ramas novamente.

**entrada**

`$ git merge Prueba`

**saída**
```
Updating 8816323..d49df45
Fast-forward
 Hola.java | 1 +
 1 file changed, 1 insertion(+)
```

Isto non sempre funciona ben, en ocasións informa de conflictos.

---------

**entrada**

`$ git rm importante~`


**saída**

`rm 'importante~'`

Se logo facemos un **commit** poderemos eliminar o arquivo.



Para sacar da zona de seguemento (head) certo arquivo, como por exemplo os .class, usamos a seguinte liña:

**entrada**

`$ git reset HEAD *.class`

------

Para clonar un proxecto de github ou de calquera outro repositorio remoto:

**entrada**

`$ git clone https://github.com/ColegioVivasCurro/HolaED`

**saída**
```
Cloning into 'HolaED'...
remote: Enumerating objects: 20, done.
remote: Total 20 (delta 0), reused 0 (delta 0), pack-reused 20 (from 1)
Receiving objects: 100% (20/20), done.
Resolving deltas: 100% (8/8), done.
```
Se abrimos o directorio de prueba_git podemos ver que se creo unha nova carpeta chamada HolaED, co proxecto do ligazón clonado.

-----

Despois de ter creado un repositorio en github, agora queremos sincronizar o noso proxecto git en local con el.

**entrada**

`$ git remote add origin https://github.com/RoiDuarte/RepositorioProba`

a ligazón ten que ser o do noso repositorio. Esta liña engade o repositorio remoto a origin.

**entrada** 

`$ git push -u origin main`


A nosa rama actual con isto subiuse ao remoto. Agora queda subir a rama Prueba:

**entrada**

`$ git push -u origin Prueba`

**saída**
```
branch 'Prueba' set up to track 'origin/Prueba'.
Everything up-to-date
```

































