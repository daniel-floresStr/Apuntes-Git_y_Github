# Trabajo individual
Daniel Teodoro Flores Mamani
## Clase 1
Git es un sistema de control de versiones que permmite guardar archivos y versiones de estos a lo largo del tiempo 
### Nacimiento 
Su nacimiento se remonta a discusion provocada entre Linus Torvalds y el manejo del software Bitkeeper el cual era muy restrictivo y solo permitia el uso de sus propios componentes, por lo cual Torvalds en un aproximado de 2 - 4 semanas pudo encontrar una solución para desplazar Bitkeeper
### Instalación 
Su instalacion depende del sistema operativo que se usa en mi caso con Windows se hace con la instalacion de un ejecutable que mediante permisos instale y accedi a la ultima version de git
### Configuraciones basicas 
Las usadas serian:
- ```git config --list``` (todas las configuraciones realizadas)
- ```git config --global user.name "Daniel Teodoro Flores Mamani"``` (configuracion del nombre de usuario)
- ```git config --global user.email "danieltfloresmamani@gmail.com" ``` (configuracion del correo a usar)
## Clase 2 
### States y commits
Tipos de estados:
- **Directorio de trabajo:** Carpeta donde se guardara el trabajo "escritura de codigo".
    Archivo de guardado los cataloga segun:
    - **Untracked:** Se observa archivos nuevos, archivos donde no hay una version anterior
    - **Modificated:** Se observan archivos que ya tienen versiones anteriores y se les va a hacer alguna modificacion 

    ``` git status ``` Una forma de verificar los estados de las carpetas (untracked, modificated)
    ```git restore ``` Restaura todos los cambios realizados (eliminaciones, creacion de nuevas carpetas, lo devuelve a un estado anterior)
    ```.gitignore``` Para archivos ocultos en donde al momento de editar el archivo y agregarle el documento que no se quiere mostrar en el nuevo commit 
- **Stage Area:** Area de espera.
Selecciona los archuvos y se guardan en el historial con ```git add .``` (guarda todas las modificaciones) ```git add."nombre del archivo" ``` solo guarda esa modificacion.
Para deshacer  ```git restore``` staged "nombre del archivo"
    
- **Repositorio Local:** El historial de cambios realizados.
Guarda cambios con ```git commit -m "mensaje descriptivo"``` crea un punto de guardado
```git log --oneline``` resumen de versiones
Para resetear o cambiar mi commit ```git reset --soft HEAD ~1```
### Buenas practicas 
- ¿Cada cuanto debo hacer un commit?
    Concepto de commit atomico --> hacer cuando haces un cambio pequeño, cambios cortos,simples que cambien la funcionalidad; que tengan significado 
- Descripcion del commit
    Lleva el siguiente ```git commit -m "tipo de commit: descripcion"```
    En verbos imperativos y con palabras demostrativas como feat, fix, docs, etc
Con el comando ```git commit``` se abre el editor vim donde se añade varias funcionalidades de un commit
## Clase 3
### Github
Es una plataforma en la nube que permite alojar, gestionar y colaborar en proyectos usando git
### Git vs Github
Git es un control de versiones que se gestiona en el dispositivo local mientras que Github controla versiones y estas lo comparte en la red donde cualquier persona puede acceder a la informacion (mediante accesos)
### SSH vs HTTPS
- HTTPS: Al momento de clonar un repositorio de Github y querer hacer un cambio en este, se necesita una autenticacion el cual es tedioso porque se lo hace cada momento y ademas no es tan viable porque no siempre se puede completar correctamente la autenticacion
- SSH: Nos brinda una mejora en cuanto a la comparacion de HTTPS en caso de una autenticacion con la condicion de generar una conexion mediante una llave (key) y ya no nos pedira la autenticacion al momento de editar
    Como generamos la conexion: En gitbash ejecutamos 
        ```ssh-keygen -t ed25519 -C "danieltfloresmamani@gmail.com"```
        ```cat ~/.ssh/id_ed25519.pub```
        El resultado del ultimo comando copiarlo y pegarlo en las configuraciones de nuestro repositorio 
        Para confirmar de que se realizo con exito la conexion ejecutar el comando 
        ```ssh -T git@github.com```
### Creacion de un repositorio en Github
1. Entrar a tu usuario y buscar repositorios en donde se presiona "new"
2. Poner nombre del repositorio, poner detalle (opcional) y luego en "Create Repository" 
### Conexion entre un repositorio local de Git con uno en Github
Para la conexion de un repositorio local existente en una cuenta de github se ejecuta el comando 
    ```git remote add origin git@github.com:daniel-floresStr/Seguimiento.git```
    ```git branch -M main``` Renombra la rama actual a "main" y que la rama principal tenga ese nombre
    ```git push -u origin main``` Envia los cambios locales al repositorio llamado "origin" en la rama "main"
### Clonar un repositorio en GIT
Uso del comando 
    ```git clone "git@github.com:daniel-floresStr/Seguimiento.git"
O simplemente seleccionarlo en github, buscar el repositorio y seleccionar si por HTTPS o SSH
### Realizar cambios en Github
- Subir cambios con el comando
    ```git push origin <rama>``` git push (empuja los commits), origin (a donde va dirigido), ```<rama> ```(la rama seleccionada)
- Bajar cambios con el comando 
    ```git pull origin <rama>``` git pull (trae los commits del servidor), origin (de donde), ```<rama>``` (de que rama seleccionada)
## Clase 4
### Git Remote
Nos permite gestionar nuestras conexiones
    ```git remote -v ```Nos permite ver las URLs de nuestro repositorio
    ```git remote add "apodo" "url"``` Vincula repositorios locales con los de github
    ```git remote set-url "apodo" "url"``` Cambia la url en donde nuestro repositorio esta apuntado
### Multiples SSH
Esto nos permite tener acceso si tenemos mas de una cuenta en Github a ditintos repositorios por lo cual es conveniente tener mas llaves SSH para que no se ocasionen choques. Su configuracion se hace con lo siquiente
    ```ssh-keygen -t ed25519 -C "correo de github" -f ~/.ssh/id_niname```
Ademas se crean archivos config para que no choquen las keys
- Cuenta Personal (la de siempre)
Host github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_ed25519
- Cuenta del otro correo
Host github-miname
HostName github.com
User git
IdentityFile ~/.ssh/id_miname

Host: Es el apodo o alias que le pones a la conexion. Es lo que escribes en la terminal despues de git@.
HostName: Es la direccion real del servidor a donde nos conectamos. Siempre sera github.com
User: Es el nombre de usuario del sistema remoto. Para GitHub, siempre, siempre es git.
IdentityFile: Es la ruta exacta hacia la "escalera" (la llave privada) que quieres usar para ese Host especifico.

Para ver si funciona ejecutamos 
    ```ssh -T git@github-miname```
### Git Checkout 
Comando que nos permite mover el Head principal (nuestra ultima actualizacion) a cualquiera que tengamos esto es funcional porque podemos recuperar archivos antiguos, ver configuraciones, etc
Para ir atras se ejecuta el comando 
    ```git checkout "hash de un commit antiguo"```
    ```git checkout "rama"```
### Detached HEAD
Somos espectadores en el pasado podemos ver todo, pero no tienes rama.
Si te vas al presente sin "encarnar" en una rama,tus cambios se pierden en el vacio.
### Buenas practicas 
- No trabajar mucho en Detached Head
- Limpiar el directorio de trabajo 
- Solo es conveniente para aprender
## Clase 5
### Ramas 
Las ramas son una excelente forma de representación de la creación de versiones alternas del codigo donde tenemos un mejor control en tanto a las modificaciones realizadas en un proyecto, ademas considerando que nuestra rama principal (main) es de donde se producen las demas ramas
### Git Branch 
Comando que permite gestionar las ramas que tienen un proyecto a base de distintos comandos como ser :
- ```git branch ```: Muestra todas las ramas que tenemos en nuestro proyecto y ademas nos muestra el posicionamiento actual mediante un HEAD.
- ```git branch <rama>```: Crea una rama (tener en cuenta las buenas prácticas) a partir de la rama en el que estemos posicionados.
- ```git branch -D <rama>```: Comando que elimina la rama. 
### Git checkout
Git checkout que ademas de que nos sirve para volver a ver a posiciones anteriores de nuestros commits (viaje en el tiempo) tiene funcionalidades especializadas en ramas como ser los códigos de:
- ```git checkout <rama>```: Comando para movernos de rama en rama (controlar de que el commit se haya completado).
- ```git checkout -b <rama>```: Comando que funciona tanto para la creacion de la rama y ademas para el posicionamiento a esta 
### Git switch
Git switch es un comando mas especializado en ramas que utiliza estos comandos:
- ```git switch <rama>```: Realiza un cambio de rama 
- ```git switch -c <rama>```: Crea la rama y cambia de posicionamiento automaticamente.
### Git checkout vs Git switch
La distincion de ambos es que **Git checkout** es un multi-funcionamiento mientras que **Git switch** esta enfocado directamente en ramas, Git switch es una mejor forma de control en cuanto a evitar los errores de confusion de escritura (confusiones entre nombre de ramas y commits).
### Git flow 
Es un flujo de trabajo el cual nos permite mantener de manera ordenada y coherente las ramas creadas al momento de hacer un proyecto esto mediante reglas establecidas y consignas permitiendo una mayor comprension entre los colaboradores del proyecto y orden visual
- **main**: Es la rama creada por defecto y ademas nuestra rama de codigo en produccion (principal).
- **develop**: Rama creada a base de la principal donde su caracteristica es que se realizan pruebas, o la agregacion de nuevas funcionalidades las cuales todavia no estan validadas pero que pronto seran lanzadas.
- **Ramas de apoyo**: Permiten la escritura y ayuda en nuestro codigo pueden ser las siguientes:
    - **feature**: Rama de apoyo que funciona a partir de querer agregar una nueva funcionalidad al proyecto. Nace del Develop y cuando es aprobada se fusiona a este y es eliminada.
    - **release**: En teoria es donde se realizan las pruebas (QA). Se crean en develop y se fusionan con este o son main.
    - **hotfix**: Es una rama que funciona como parche para arreglar un bug o algun error no previsto por lo cual este debe nacer explicitamente a partir de la rama **main** y no de un **develop**
**Tabla resumen**

| Rama | Nacimiento | Fusion | Proposito | Ejemplo |
|------|------------|--------|-----------|---------|
| main | De ninguna otra rama (es la principal) | Ninguna | Es la rama puesta en producción | main |
| develop | main | main | Funcionalidades puestas a prueba con falta de aprobacion | develop |
| feacture/ | develop | develop | Una funcionalidad específica | feacture/sum-function |
| release/ | develop | develop o main | Se realizan pruebas y se pule la version final | release/v1.0.0 |
| hotfix/ | main | main y develop | Arreglar un bug | hotfix/login-authentication-error |

## Clase 6
### Git merge 
Git merge nos permite fusionar nuestras ramas creadas (develop, feature/, release/, hostfix/) esto en el sentido de que ya fueron aprobadas las nuevas funcionalidades y se quieran agregar al proyecto general.
```git merge <rama>```: Fusiona las ramas pero sin hacer un commit antes (un aviso de que se fusionaron las ramas).
### Flujo de trabajo
Para realizar correctamente la fusion de ramas se debe hacer la ejecución de los siguientes comandos:
- ```git checkout develop```: Principalmente moverse a la rama develop para fusionarla con otra rama
- ```git fetch ```: Permite ver si hubo cambios en la rama o cualquier bifurcación de esta, genera un aviso.
- ```git pull origin develop```: Permite traer todos los cambios que tiene el repositorio de la maquina para no tener problemas al momento de subirla.
- ```git merge --no-ff <nombre_rama>```: Comienza la fusion de ramas en donde controlamos y forzamos a hacer un commit a esta acción para informar a todos los colaboradores y nosotros mismos que se hizo una fusion de ramas.
- ```git branch -D <nombre_rama>```: Eliminamos la rama que fusionamos para evitar que vea ramas innecesarias
- ```git push origin develop```: Subimos los cambios realizados

## Clase 7
### Pull request (PRs)
El pull request es una forma profesional de trabajar con git, github el cual permite ver quien esta mergeando una rama al proyecto 
### Creacion 
Para la creacion de este hay que seguir estos pasos
- Dirigirse a la cuenta de github
- Ir a ajustes
- Buscar la opcion de rulesets 
- Darle un nombre 
- Configurar a que rama se puede mergear (en este caso develop) 
- Configurar cuantos colaboradores son necesarios para autorizar que se haga un merge
- Seleccionar add rulesets
- Seleccionar add tarjet
### Flujo de trabajo con pull request 
El flujo para un correcto trabajo es el siguiente (Comandos usados anteriormente).
- ```git checkout develop```
- ```git fetch```
- ```git pull origin develop```
- ```git checkout <rama>``` Agregas -b si estás creando la rama
- ```git merge develop``` Solo si hubo cambios en develop
Trabajas en tu rama
- ```git push origin <rama>``` Agregas -u si es la primera vez que subes cambios al repositorio remoto
- ```git checkout develop```
- ```git fetch```
- ```git checkout <rama>```
- ```git merge develop``` Solo si hubo cambios en develop antes de hacer la Pull Request
Resuelves manualmente los archivos fallidos y sus conflictos
- ```git add .```
- ```git commit```
- ```git push origin <rama>```

**¿Porque hacemos esto?**
Esto lo hacemos para mantener un control en lo que es la modificacion de nuestro proyecto ya que solo con estas restricciones no cualquier persona puede realizar un merge en nuestra rama principal, ya que hay la posibilidad de que pueda meter codigo malicioso o directamente destruir nuestro proyecto. A la existencia de ese riesgo se implementa estas configuraciones que solo si con la autorizacion de los colaboradores pueda realizar un merge
Ademas tomar en cuenta de que hay una posibilidad de que un no colaborador externo pueda agregar alguna modificacion en el proyecto pero con esta configuracion podemos observar y ademas permitir o denegar las modificaciones (cumpliendo las condiciones de los colaboradores a confirmar) que realiza el intruso. **Dato curioso:** Solo es aceptado las modificaciones cuando se hayan aprobado esas condiciones y si es que uno de ellos lo denego no se podra realizar ningun cambio.
## Clase 8 (Final)
### ¿Qué hacer cuando se aprobó un Pull Request que afecta archivos que yo estoy tocando?
Cuando los cambios de un compañero se integran a la rama principal (main) y entran en conflicto con tu trabajo local, debes seguir estos pasos para mantener tu rama actualizada:

1. **Guardar cambios locales:** Si no estás listo para un commit, usa git stash.
2. **Actualizar rama principal:**
   - ```git checkout main```
   - ```git pull origin main```
3. Integrar cambios a tu rama: Regresa a tu rama y realiza un merge.
   - ```git checkout tu-rama```
   - ```git merge main```
4. Resolver conflictos: Git marcará los archivos en conflicto. Debes editarlos, elegir qué cambios conservar, y luego hacer:
   - ```git add .```
   - ```git commit -m "Fix: resolver conflictos con main"```
## Git Stash: Almacenamiento Temporal
El comando stash permite guardar provisionalmente los cambios del área de trabajo para tener un directorio limpio sin necesidad de hacer un commit incompleto.
- ```git stash```: Guarda los cambios modificados (no guardados en commit) y limpia el directorio de trabajo.
- ```git stash -m "mensaje"```: Permite añadir una descripción al stash.
- ```git stash list```: Muestra la lista de todos los estados guardados en el historial de stash.
- ```git stash pop```: Recupera el último stash guardado, lo aplica a tu rama actual y lo elimina de la lista de stashes.
## Git Diff: Inspección de Cambios
|Comando|Descripción|
|-------|------------|
|git diff|Muestra cambios en el directorio de trabajo que aún no han sido agregados al index (stage).|
|git diff .	|Muestra todos los cambios en el directorio actual y subdirectorios.|
|git diff <archivo>	|Muestra los cambios realizados específicamente en un archivo concreto.|
|git diff --staged .|	Compara los archivos que ya están en el stage (listos para commit) contra el último commit.|
|git diff --staged <archivo>|	Igual al anterior, pero filtrado por un archivo específico.|
|git diff rama1 rama2|	Muestra las diferencias exactas entre dos ramas distintas.|
## Buenas Prácticas: Limpieza de Ramas
Es una buena práctica fundamental borrar las ramas locales y remotas una vez que el Pull Request ha sido mergeado exitosamente.

**¿Por qué hacerlo?**

**Claridad:** Evita tener un listado interminable de ramas obsoletas.

**Prevención de errores:** Impide trabajar accidentalmente sobre una rama que ya es historia.

**Orden:** Facilita la navegación en el repositorio para nuevos integrantes del equipo.

**Comandos:**

- Borrar rama local: ```git branch -d <nombre-de-la-rama>```
- Borrar rama remota: ```git push origin --delete <nombre-de-la-rama>```