# Git & GitHub

## Que es Git

Git es un sistema de control de versiones distribuido (DVCS) que facilita a los desarrolladores registrar y seguir cambios en archivos, en especial código fuente, a lo largo del tiempo. Fue diseñado para manejar desde pequeños a muy grandes proyectos con velocidad y eficiencia. Algunos de sus aspectos técnicos más destacados son:

- **Instantáneas, no diferencias:** A diferencia de muchos otros sistemas de control de versiones, Git registra instantáneas del archivo en lugar de diferencias. Cada vez que se realiza un commit, esencialmente Git toma una instantánea del aspecto de todos los archivos y almacena una referencia a esa instantánea.

- **Integridad de datos:** Todos los objetos en Git son verificados por un checksum antes de ser almacenados, y son referenciados por ese checksum. Esto garantiza la integridad y la consistencia de los datos.

- **Estructura de datos:** Git utiliza una estructura de datos llamada DAG (Directed Acyclic Graph) para representar la historia del proyecto. Cada nodo del DAG es un commit.

- **Localmente distribuido:** La mayoría de las operaciones en Git solo necesitan archivos y recursos locales para operar, ya que cada desarrollador tiene una copia local completa de toda la historia del proyecto.

- **Áreas de trabajo:** Git maneja tres principales "áreas" que son el directorio de trabajo, el área de preparación (o "staging area"), y el directorio de Git (donde Git almacena los metadatos y la base de datos del objeto).

- **Compresión y eficiencia:** A pesar de almacenar instantáneas en lugar de diferencias, Git es eficiente en el almacenamiento y rendimiento utilizando compresión y otras técnicas.

- **Brancheo y fusión:** Git permite la creación rápida de ramas y fusiones eficientes, lo que facilita la experimentación y la segregación de características o versiones.

## Instalación de Git

Despues de instalar Git compreuba la version con el siguiente comando `git --version`

### Windows

1. Visita la página oficial de descargas de Git: https://git-scm.com/download/win
2. Descargese el ejecutable haciendo clcik en _Click here to download the latest (2.42.0) 64-bit versi..._
3. Ejecuta el archivo .exe descargado.
4. Sigue las instrucciones del asistente de instalación. **Durante el proceso de instalación asegurese de instalar Git Bash**

### MacOS

Si tienes instalado **Homebrew**, ejecuta:

```
brew install git
```

Si no utilizas Homebrew, ve a la página oficial de descargas de Git: https://git-scm.com/download/mac y descarga el instalador para macOS.

### Linux (Debian/Ubuntu):

```bash
sudo apt-get update
sudo apt-get install git
```

## Configuración inicial de Git

`git config --global`

> `--global` Sirve para que los cambios se apliquen de manera general y no por proyecto.

### User Name & email

Estos serán utilizados para identificar quién ha realizado cada commit.

Configurar git con nuestro nombre con el comando `user.name "name"`

```bash
git config --global user.name "A-esh"
```

```bash
git config --global user.email "a-esh_test@gmail.com"
```

### Configurar editor de texto

Por defecto, Git usa el editor que está configurado en tu variable de entorno $EDITOR. Si deseas cambiar esto, puedes especificar un editor diferente.

Nano

```bash
git config --global core.editor "nano --wait"
```

Visual Studio Code

```bash
git config --global core.editor "code --wait"
```

> **flag `--wait`**
>
> Cuando Git abre un archivo para que lo edites (por ejemplo, para escribir un mensaje de commit), **`code --wait` mantendrá la ventana de VSCode abierta** y esperará a que cierres ese archivo/tab específico antes de que Git continúe con la siguiente operación.
>
> ```
> hint: Waiting for your editor to close the file...
> ```

### Configurar el control de fin de línea `core.autocrlf`

**En Windows:** Git puede convertir automáticamente los finales de línea LF que usa Linux a CRLF que usa Windows cuando se clona un repositorio y viceversa cuando se empuja:

```bash
git config --global core.autocrlf true
```

En Linux/Mac: Puedes configurar Git para simplemente mantener los finales de línea LF (Es necesario por si el editor agrega CR):

```bash
git config --global core.autocrlf input
```

### Verificar la configuración

```bash
git config --global -e
```

> Flag `-e` <br> Abrira el editor de texto que configuramos, si cambia alguna configuración guardela `Crtl + S`

> Explora mas configuraciones con `git config -h`

## Git BASH Bourne Again Shell

Terminal para ejecutar comandos de git y emular comandos de Linux o MacOS

### Listar archivos `ls`

`ls` Lista los archivos en el directorio actual.

`ls -l` Lista los archivos con formato detallado (permisos, propietario, tamaño, etc.).

`ls -a` Muestra todos los archivos, incluidos los ocultos.

### Ubicacion actual `pwd`

`pwd` Muestra el directorio actual en el que te encuentras.

### Movernos entre carpetas `cd`

`cd <directorio>` Cambia al directorio especificado.

`cd ..` Regresa al directorio padre, _al anterior_.

`cd` Sin argumentos, regresa al directorio de inicio del usuario.

> Mientras escribimos la ruta del direcototio podemos pulsar `TAB` para autocompletar.

### Modificaciób de directorios `mkdir` `rmdir`

`mkdir <nombre_del_directorio>` Crea un nuevo directorio.

`rmdir <nombre_del_directorio>` Elimina un directorio (debe estar vacío).


### Crear archivos
El comando `touch` puede ser usado para crear archivos vacíos.
```bash
touch nombre_del_archivo.txt
```
#### Usar redirecciones
```bash
echo "Contenido del archivo" > nombre_del_archivo.txt
```
> `echo "texto" > <archivo>` Escribe "texto" en el archivo especificado. Si el archivo ya existe, sobrescribe su contenido.

#### Usando un editor de texto
Puedes usar un editor de texto como nano, vim, emacs, etc., para crear un archivo:
```bash
code nombre_del_archivo.txt
```
### Modificar archivos

`rm <archivo>` Elimina un archivo.

`rm -r <directorio>` Elimina un directorio y su contenido (usar con precaución).

> Flag `-r` indicar un comportamiento "recursivo". El comando actuará sobre el directorio dado y todos sus subdirectorios y archivos.

## Iniciar Repostitorio `git init`
`git init` Crea un nuevo subdirectorio llamado `.git` en el directorio actual. Este subdirectorio contiene todos los archivos y directorios necesarios para mantener el historial de revisiones de un proyecto. Es aquí donde Git guarda todos los metadatos y la base de datos del objeto del repositorio.
> Convierte el directorio actual en un repositorio de Git, permitiendo empezar a rastrear un proyecto existente.

Para iniciar un repositorio debemos crear un directorio para nuestro proyecto. Movernos a la driección de nuestro repositorio y usar el comando `git init`

```bash
mkdir curso_git
cd curso_git
git init
```

>Para ver la carpeta **".git"** usaremos el comando `ls -a`una vez enocntrado el directorio nos moveremosa a este usando `cd .git`
>> Flag `-a` con `ls` Estás indicando que muestre todos los archivos en el directorio, incluyendo aquellos que comienzan con un punto (.), que son considerados archivos ocultos en sistemas Unix/Linux.
>   
>>Nota: `.` y `..` son entradas especiales. `.` representa el directorio actual y `..` representa el directorio padre. Estas entradas siempre están presentes y son mostradas con `ls -a`. Son esenciales para la navegación en la línea de comandos. Por ejemplo, puedes usar `cd ..` para moverte al directorio padre del directorio actual. Aunque suelen ser invisibles con un simple `ls`, son componentes fundamentales de la estructura de directorios de Unix/Linux.

Plataformas como **GitHub** ahora usan **"main"** como el nombre predeterminado para la rama principal en nuevos repositorios.
```bash
git branch -m master main
```

## Áreas Principales de Git:
- **Área de Trabajo (Working Directory)**: Es el directorio en tu sistema de archivos donde realizas cambios en tus archivos.

- **Área de Preparación (Staging Area o Index)**: Es una capa intermedia que alberga los cambios que están listos para ser confirmados (committed). Es como una zona de preparación antes de hacer un commit.

- **Repositorio Git (o Repository)**: Es donde Git guarda el historial de versiones. Contiene todos los commits y el historial del proyecto.

## Flujo de trabajo

El flujo de trabajo en Git está diseñado alrededor del modelo de control de versiones distribuido. Es fundamental entender cómo funcionan las áreas principales y cómo se mueven los cambios a través de ellas para aprovechar al máximo Git. Aquí te explico el flujo de trabajo básico en Git:

### 1. **Áreas Principales de Git**:

- **Área de Trabajo (Working Directory)**: Es el directorio en tu sistema de archivos donde realizas cambios en tus archivos.

- **Área de Preparación (Staging Area o Index)**: Es una capa intermedia que alberga los cambios que están listos para ser confirmados (committed). Es como una zona de preparación antes de hacer un commit.

- **Repositorio Git (o Repository)**: Es donde Git guarda el historial de versiones. Contiene todos los commits y el historial del proyecto.

### 2. **Flujo Básico de Trabajo**:

1. **Modificar Archivos**: Realizas cambios en tus archivos dentro del Área de Trabajo.
2. **Preparar Cambios**: Una vez que estés satisfecho con los cambios, los añades al Área de Preparación usando
3. **Hacer un Commit**: Cuando estés listo para guardar estos cambios en el Repositorio Git, haces un "commit":
4. **Push y Pull (en el contexto de trabajar con remotos)**: Si estás trabajando con un repositorio remoto (por ejemplo, en GitHub o GitLab)
5. **Branching y Merging**: Git permite crear ramas (branches) para trabajar en características o correcciones específicas sin afectar la línea principal de desarrollo. Una vez que la característica o corrección está lista, puedes fusionar (merge) esa rama de regreso a la línea principal.

## Comandos Git
### Comprobar `git status`
Con `git status` podemos ver que archivos se han modificado.
>Output:
> ```bash
>$ git status
>On branch master
>
>No commits yet
>
>Untracked files:
>  (use "git add <file>..." to include in what will be committed)
>        Hello git.py
>
>nothing added to commit but untracked files present (use "git >add" to track)
>```
>>Si el archivo no esta añadido aparecera de este color <font color="red">Hello git.py</font>
>
>>Si el archivo esta añadido aparecera de este color <font color="gree">Hello git.py</font>

### Añadir archivos `git add`
Con el comando `git add` agregaremos los archivos, para hacer el commit.

```bash
git add "Hello Git.py"
```

>Podemos agregar todo el directorio actual agregando un `.`, con esto se agregaran todos los cambios.
>```bash
>git add .
>```

### Commit `git commit`
Cuando estés listo para guardar estos cambios en el Repositorio Git, haces un "commit"
```bash
git commit -m "Añadida funcionalidad de saludar"
```
> Flag `-m` en `git commit`  Indica que el siguiente argumento será el mensaje del commit.
>> Los commits deben de tener siempre un texto descriptivo. Si no se utiliza la flag `-m` se abrira el editor de texto predeterminado.
#### Output
```bash
$ git commit -m "Enseñar a saludar"
[main (root-commit) 1cfc4e5] Enseñar a saludar
 1 file changed, 1 insertion(+)
 create mode 100644 Hello git.py
```
Vamos a desglosar y analizar el output que nos ha proporcionado:

1. **`$ git commit -m "Enseñar a saludar"`**:
   - Este es el comando que se ejecutó. Estás haciendo un "commit" con el mensaje "Enseñar a saludar".

2. **`[main (root-commit) 1cfc4e5] Enseñar a saludar`**:
   - `main`: Esta es la rama en la que estás haciendo el commit, en este caso, es la rama "main".
   - `(root-commit)`: Indica que este es el primer commit en el repositorio (es decir, estás inicializando el historial de commits del repositorio con este commit).
   - `1cfc4e5`: Este es un hash abreviado del commit, es un identificador único para ese commit en particular.
   - `Enseñar a saludar`: Es el mensaje del commit que proporcionaste.

3. **`1 file changed, 1 insertion(+)`**:
   - Indica que un archivo ha sido modificado en este commit y que se ha realizado una inserción. Esto sugiere que se agregó una nueva línea al archivo en cuestión.

4. **`create mode 100644 Hello git.py`**:
   - `create mode 100644`: Indica que se ha creado un nuevo archivo con los permisos `100644`, que en Git corresponde a un archivo regular (en contraposición a un directorio o un enlace simbólico, por ejemplo). 
   - `Hello git.py`: Es el nombre del archivo que se creó. Es probable que este archivo contenga algún código o instrucciones relacionadas con "enseñar a saludar", dado el mensaje del commit.
### Log `git log`
El comando `git log` se utiliza en Git para ver el historial de commits en un repositorio. Proporciona una lista de commits en orden cronológico inverso (el más reciente primero). Cada entrada en el log muestra el hash del commit, el autor, la fecha y el mensaje del commit.
> Output:
>```bash
>commit 1cfc4e52313e3a6723c9c79bd7d8e4b3a259454a (HEAD -> main)
>Author: A-esh <a-esh_test@gmail.com>
>Date:   Sat Aug 26 12:49:03 2023 +0200
>
>    Enseñar a saludar
>```

#### Algunas opciones útiles para `git log`:

- **`git log -p` o `git log -patch`**: Muestra la diferencia (el "diff") introducida en cada commit. Es útil para ver exactamente qué cambios se hicieron.

- **`git log --stat`**: Muestra algunas estadísticas del commit, como qué archivos fueron modificados y cuántas líneas fueron añadidas/eliminadas.

- **`git log --oneline`**: Muestra el historial de commits en un formato condensado de una línea por commit. Es útil para obtener una vista rápida del historial.

- **`git log --graph`**: Muestra un gráfico ASCII del historial de commits y ramas, lo que puede ser útil en repositorios con muchas ramas y merges.

- **`git log <archivo>`**: Muestra solo los commits que modificaron el archivo especificado.

- **`git log -S<string>`**: Busca commits que añadieron o eliminaron la cadena especificada.

- Mas opciones `git log --help` 


### Comandos personalizados `git alias`
>Podemos configurar nuestro propio comando sin tener que agregar todas las flags cada vez que queramos consultar algo.
>Para ello debemos uilizar:
><br>`git config --global alias.nombredetucomando "comando_personalizado"`
>```bash
> git config --global alias.tree "log --graph --decorate --all --oneline"
>```

### `.gitignore`
El archivo `.gitignore` especifica patrones de archivo y directorio que deben ser ignorados por Git. Al ejecutar git status, los archivos que coincidan con los patrones en `.gitignore` no se mostrarán como cambios no rastreados.

Debemos de crear el archivo:
```bash
touch .gitignore
```
> Abrirlo para editarlo `code .gitignore`

Para no tener en cuenta un fichero tenemos que usar las siguiente sintaxis:
`**/archivo_ignorado`

> En el sistema operativo MacOS es conveniente ingorar el archivo `.DS_Store`

#### Patrones 
- `*.log` ignora todos los archivos con extensión `.log`
- `temp/` ignora el directorio llamado temp y todo su contenido.
- `!example.log` no ignora el archivo example.log, incluso si hay un patrón que coincida con él. 
- El `!` se utiliza para negar un patrón.

### Diferencia de codigo `git diff`
#### **Uso Básico**:

- **`git diff` (sin argumentos)**:
  Muestra las diferencias entre el área de trabajo y el área de preparación. Es decir, los cambios en archivos que no has añadido al área de preparación con `git add`.

#### **Comparaciones Comunes**:

- **`git diff --staged` (o `git diff --cached`)**:
  Muestra las diferencias entre el área de preparación y el último commit. Estos son los cambios que se incluirán en el próximo commit si ejecutas `git commit` sin `-a`.

- **`git diff HEAD`**:
  Combina las dos anteriores y muestra todas las diferencias entre tu área de trabajo y el último commit.

- **`git diff <branch_name>`**:
  Muestra las diferencias entre tu área de trabajo actual y otra rama.

- **`git diff <commit1>..<commit2>`**:
  Muestra las diferencias entre dos commits específicos.

- **`git diff <commit>`**:
  Muestra las diferencias entre el commit especificado y tu área de trabajo actual.

Tanto `git checkout` como `git reset` son comandos en Git que permiten cambiar el estado de tu repositorio, pero se usan en diferentes contextos y tienen comportamientos distintos. Veamos cada uno en detalle:

### Desplazamientos por ramas `git checkout`:

El comando `git checkout` se usa principalmente para dos propósitos:

- **Cambiar entre ramas o commits**:
  Puedes usar `git checkout` seguido del nombre de una rama para cambiar a esa rama. También puedes usarlo para revisar un commit en específico al proporcionar el hash del commit.

   ```bash
   git checkout nombre-de-la-rama
   ```
   ```bash
   git checkout 1cfc4e5
   ```
   > Si el repositorio no es muy grande se puede trabajar con el hash abreviado.  
- **Deshacer cambios en el área de trabajo**:
  Si quieres revertir los cambios en un archivo específico al estado del último commit, puedes usar `git checkout` seguido del nombre del archivo.


  ```bash
  git checkout -- nombre-del-archivo.txt
  ```

  Esto descartará cualquier cambio no preparado (unstaged) en `nombre-del-archivo.txt`.

> A partir de Git 2.23, el comando `git switch` ha sido introducido como una forma más intuitiva de cambiar entre ramas, mientras que `git restore` es una nueva forma de revertir cambios en archivos, separando estas funciones del tradicional `git checkout`.

### `git reset`:

El comando `git reset` se utiliza para restablecer tu estado actual a un commit específico. Dependiendo de cómo lo uses, puede afectar el área de trabajo, el área de preparación (staging area) o el historial de commits:

- **`git reset --soft <commit>`**:
  Mueve el puntero HEAD y la referencia de la rama actual al commit especificado. Los cambios desde `<commit>` hasta ahora se mantienen en el área de preparación. Es decir, estarán listos para ser "commiteados" de nuevo.

- **`git reset --mixed <commit>` (o simplemente `git reset <commit>`)**:
  Similar al `--soft`, pero también resetea el área de preparación. Los cambios desde `<commit>` hasta ahora estarán en el área de trabajo, permitiendo editarlos o prepararlos de nuevo.

- **`git reset --hard <commit>`**:
  Restablece el puntero HEAD, el área de preparación y el área de trabajo al estado del commit especificado. Los cambios desde `<commit>` hasta ahora se pierden. Se debe usar con precaución.

Además, `git reset` también puede ser usado para deshacer la preparación (unstaging) de archivos:

- **`git reset <archivo>`**: Deshace la preparación del archivo especificado, pero mantiene sus cambios en el área de trabajo.

## `git reflog`:


## `git tag`:

## `git branch`:

## `git switch`:

## `git merge`:

## `git stash`: