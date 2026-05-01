# 📘 Trabajo Individual
**Daniel Teodoro Flores Mamani**

![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

---

## 📚 Clase 1 — Introducción a Git

Git es un sistema de control de versiones que permite guardar archivos y versiones de estos a lo largo del tiempo.

### 🌱 Nacimiento

Su nacimiento se remonta a una discusión provocada entre Linus Torvalds y el manejo del software Bitkeeper, el cual era muy restrictivo y solo permitía el uso de sus propios componentes, por lo cual Torvalds en un aproximado de 2 - 4 semanas pudo encontrar una solución para desplazar Bitkeeper.

### 💻 Instalación

Su instalación depende del sistema operativo que se usa. En mi caso con Windows se hace con la instalación de un ejecutable que mediante permisos instalé y accedí a la última versión de git.

### ⚙️ Configuraciones Básicas

Las usadas serían:

```bash
git config --list                                              # Todas las configuraciones realizadas
git config --global user.name "Daniel Teodoro Flores Mamani"  # Configuración del nombre de usuario
git config --global user.email "danieltfloresmamani@gmail.com" # Configuración del correo a usar
```

---

## 📚 Clase 2 — States y Commits

### 🔄 Tipos de Estados

- **🗂️ Directorio de trabajo:** Carpeta donde se guardará el trabajo "escritura de código".  
  El archivo de guardado los cataloga según:
  - **Untracked:** Se observan archivos nuevos, archivos donde no hay una versión anterior.
  - **Modificated:** Se observan archivos que ya tienen versiones anteriores y se les va a hacer alguna modificación.

  ```bash
  git status   # Verifica los estados de las carpetas (untracked, modificated)
  git restore  # Restaura todos los cambios realizados (eliminaciones, creación de nuevas carpetas)
  ```

  > `.gitignore` → Para archivos ocultos donde, al momento de editar el archivo y agregarle el documento, no se mostrará en el nuevo commit.

- **⏳ Stage Area:** Área de espera.  
  Selecciona los archivos y se guardan en el historial:

  ```bash
  git add .                    # Guarda todas las modificaciones
  git add "nombre del archivo" # Solo guarda esa modificación
  git restore --staged "nombre del archivo"  # Deshace el stage
  ```

- **🏛️ Repositorio Local:** El historial de cambios realizados.

  ```bash
  git commit -m "mensaje descriptivo"  # Crea un punto de guardado
  git log --oneline                    # Resumen de versiones
  git reset --soft HEAD~1              # Resetear o cambiar el último commit
  ```

### ✅ Buenas Prácticas

> **¿Cada cuánto debo hacer un commit?**  
> Concepto de **commit atómico** → hacer cuando realizas un cambio pequeño, cambios cortos, simples que cambien la funcionalidad; que tengan significado.

> **Descripción del commit:**  
> Lleva el siguiente formato:
> ```bash
> git commit -m "tipo de commit: descripcion"
> ```
> En verbos imperativos y con palabras demostrativas como `feat`, `fix`, `docs`, etc.

Con el comando `git commit` se abre el editor vim donde se añaden varias funcionalidades de un commit.

---

## 📚 Clase 3 — GitHub

### ☁️ ¿Qué es GitHub?

Es una plataforma en la nube que permite alojar, gestionar y colaborar en proyectos usando git.

### ⚖️ Git vs GitHub

| | Git | GitHub |
|---|---|---|
| **Tipo** | Control de versiones | Plataforma en la nube |
| **Alcance** | Local | En red / colaborativo |
| **Acceso** | Solo local | Cualquier persona (con permisos) |

### 🔐 SSH vs HTTPS

- **HTTPS:** Al momento de clonar un repositorio de GitHub y querer hacer un cambio, se necesita una autenticación que es tediosa porque se realiza en cada momento y no siempre se puede completar correctamente.

- **SSH:** Brinda una mejora en cuanto a la autenticación con la condición de generar una conexión mediante una llave (key), y ya no pedirá la autenticación al momento de editar.

  ```bash
  ssh-keygen -t ed25519 -C "danieltfloresmamani@gmail.com"
  cat ~/.ssh/id_ed25519.pub
  # Copiar el resultado y pegarlo en las configuraciones del repositorio
  ssh -T git@github.com  # Confirmar que la conexión fue exitosa
  ```

### 📁 Creación de un Repositorio en GitHub

1. Entrar a tu usuario y buscar repositorios, donde se presiona **"New"**.
2. Poner nombre del repositorio, detalle (opcional) y luego en **"Create Repository"**.

### 🔗 Conexión entre Repositorio Local y GitHub

```bash
git remote add origin git@github.com:daniel-floresStr/Seguimiento.git
git branch -M main        # Renombra la rama actual a "main"
git push -u origin main   # Envía los cambios locales al repositorio remoto
```

### 📥 Clonar un Repositorio

```bash
git clone "git@github.com:daniel-floresStr/Seguimiento.git"
```

> O simplemente seleccionarlo en GitHub, buscar el repositorio y elegir entre HTTPS o SSH.

### 🔁 Realizar Cambios en GitHub

```bash
git push origin <rama>   # Sube commits al servidor
git pull origin <rama>   # Trae commits del servidor
```

---

## 📚 Clase 4 — Remote y SSH Múltiple

### 🌐 Git Remote

Permite gestionar las conexiones con repositorios remotos.

```bash
git remote -v                    # Ver las URLs del repositorio
git remote add "apodo" "url"     # Vincular repositorios locales con GitHub
git remote set-url "apodo" "url" # Cambiar la URL a la que apunta el repositorio
```

### 🔑 Múltiples SSH

Esto permite tener acceso si se tienen más de una cuenta en GitHub, evitando choques entre llaves.

```bash
ssh-keygen -t ed25519 -C "correo de github" -f ~/.ssh/id_niname
```

Además se crean archivos `config` para que no choquen las keys:

```
# Cuenta Personal (la de siempre)
Host github.com
HostName github.com
User git
IdentityFile ~/.ssh/id_ed25519

# Cuenta del otro correo
Host github-miname
HostName github.com
User git
IdentityFile ~/.ssh/id_miname
```

| Campo | Descripción |
|---|---|
| `Host` | Apodo o alias de la conexión. Es lo que se escribe después de `git@`. |
| `HostName` | Dirección real del servidor. Siempre será `github.com`. |
| `User` | Nombre de usuario del sistema remoto. Para GitHub, siempre es `git`. |
| `IdentityFile` | Ruta exacta hacia la llave privada que se quiere usar para ese Host. |

```bash
ssh -T git@github-miname  # Verificar si la conexión funciona
```

### ⏪ Git Checkout

Comando que permite mover el HEAD principal a cualquier punto del historial — útil para recuperar archivos antiguos, ver configuraciones, etc.

```bash
git checkout "hash de un commit antiguo"
git checkout "rama"
```

### 👻 Detached HEAD

> Somos espectadores en el pasado — podemos ver todo, pero no tenemos rama.  
> Si te vas al presente sin "encarnar" en una rama, tus cambios se pierden en el vacío.

### ✅ Buenas Prácticas

- No trabajar mucho en Detached HEAD.
- Limpiar el directorio de trabajo.
- Solo es conveniente para aprender.

---

## 📚 Clase 5 — Ramas

### 🌿 ¿Qué son las Ramas?

Las ramas son una excelente forma de representación de la creación de versiones alternas del código donde se tiene un mejor control de las modificaciones realizadas en un proyecto. La rama principal `main` es de donde se producen las demás ramas.

### 🛠️ Git Branch

```bash
git branch              # Muestra todas las ramas y el posicionamiento actual (HEAD)
git branch <rama>       # Crea una rama a partir de la rama actual
git branch -D <rama>    # Elimina la rama
```

### 🔀 Git Checkout (en ramas)

```bash
git checkout <rama>    # Moverse de rama en rama
git checkout -b <rama> # Crear la rama y posicionarse en ella
```

### 🔀 Git Switch

```bash
git switch <rama>      # Cambio de rama
git switch -c <rama>   # Crea la rama y cambia automáticamente
```

### ⚖️ Git Checkout vs Git Switch

La distinción de ambos es que **Git checkout** es un multi-funcionamiento mientras que **Git switch** está enfocado directamente en ramas. Git switch es una mejor forma de control para evitar errores de confusión (entre nombres de ramas y commits).

### 🌊 Git Flow

Es un flujo de trabajo que permite mantener de manera ordenada y coherente las ramas creadas en un proyecto, mediante reglas y consignas que permiten una mayor comprensión entre los colaboradores.

- **`main`**: Rama creada por defecto y rama de código en producción (principal).
- **`develop`**: Rama creada a partir de la principal, donde se realizan pruebas o se agregan nuevas funcionalidades aún no validadas.
- **Ramas de apoyo:** Permiten la escritura y ayuda en el código:
  - **`feature`**: Nace del develop para agregar una nueva funcionalidad. Cuando es aprobada se fusiona al develop y es eliminada.
  - **`release`**: Donde se realizan pruebas (QA). Se crean en develop y se fusionan con este o con main.
  - **`hotfix`**: Parche para arreglar un bug no previsto. Debe nacer explícitamente de **main** y no de develop.

**Tabla resumen:**

| Rama | Nacimiento | Fusión | Propósito | Ejemplo |
|------|------------|--------|-----------|---------|
| `main` | De ninguna otra (es la principal) | Ninguna | Código en producción | `main` |
| `develop` | `main` | `main` | Funcionalidades en prueba | `develop` |
| `feature/` | `develop` | `develop` | Una funcionalidad específica | `feature/sum-function` |
| `release/` | `develop` | `develop` o `main` | Pruebas y pulido de versión final | `release/v1.0.0` |
| `hotfix/` | `main` | `main` y `develop` | Arreglar un bug | `hotfix/login-authentication-error` |

---

## 📚 Clase 6 — Git Merge

### 🔀 ¿Qué es Git Merge?

Git merge permite fusionar ramas creadas (develop, feature/, release/, hotfix/) cuando las nuevas funcionalidades ya fueron aprobadas.

```bash
git merge <rama>  # Fusiona las ramas sin hacer un commit previo
```

### 🔁 Flujo de Trabajo

```bash
git checkout develop             # Moverse a la rama develop
git fetch                        # Verificar si hubo cambios en la rama
git pull origin develop          # Traer todos los cambios del repositorio remoto
git merge --no-ff <nombre_rama>  # Fusionar forzando un commit de la acción
git branch -D <nombre_rama>      # Eliminar la rama fusionada
git push origin develop          # Subir los cambios realizados
```

---

## 📚 Clase 7 — Pull Requests (PRs)

### 🤝 ¿Qué es un Pull Request?

El pull request es una forma profesional de trabajar con git y GitHub que permite ver quién está mergeando una rama al proyecto.

### 📋 Creación

1. Dirigirse a la cuenta de GitHub.
2. Ir a ajustes.
3. Buscar la opción de **Rulesets**.
4. Darle un nombre.
5. Configurar a qué rama se puede mergear (en este caso `develop`).
6. Configurar cuántos colaboradores son necesarios para autorizar el merge.
7. Seleccionar **Add Rulesets**.
8. Seleccionar **Add Target**.

### 🔁 Flujo de Trabajo con Pull Request

```bash
git checkout develop
git fetch
git pull origin develop
git checkout <rama>           # Agregar -b si se está creando la rama

git merge develop             # Solo si hubo cambios en develop
# --- Trabajas en tu rama ---
git push origin <rama>        # Agregar -u si es la primera vez

git checkout develop
git fetch
git checkout <rama>
git merge develop             # Solo si hubo cambios antes de hacer la PR
# --- Resuelves conflictos manualmente ---
git add .
git commit
git push origin <rama>
```

> **¿Por qué hacemos esto?**  
> Para mantener un control sobre la modificación del proyecto: solo con estas restricciones no cualquier persona puede realizar un merge en la rama principal, evitando la introducción de código malicioso o la destrucción del proyecto.  
>
> Además, si un colaborador externo quiere agregar una modificación, esta configuración permite observar, aprobar o denegar los cambios (cumpliendo las condiciones de aprobación de los colaboradores). **Dato curioso:** Solo se aceptan las modificaciones cuando todas las condiciones han sido aprobadas; si uno las deniega, no se podrá realizar ningún cambio.

---

## 📚 Clase 8 (Final) — Conflictos, Stash y Diff

### ⚡ ¿Qué hacer cuando se aprobó un Pull Request que afecta archivos que yo estoy tocando?

Cuando los cambios de un compañero se integran a la rama principal y entran en conflicto con tu trabajo local, debes seguir estos pasos:

1. **Guardar cambios locales:** Si no estás listo para un commit, usa `git stash`.
2. **Actualizar rama principal:**
   ```bash
   git checkout main
   git pull origin main
   ```
3. **Integrar cambios a tu rama:** Regresa a tu rama y realiza un merge.
   ```bash
   git checkout tu-rama
   git merge main
   ```
4. **Resolver conflictos:** Git marcará los archivos en conflicto. Edítalos, elige qué cambios conservar y luego:
   ```bash
   git add .
   git commit -m "Fix: resolver conflictos con main"
   ```

---

### 📦 Git Stash — Almacenamiento Temporal

El comando stash permite guardar provisionalmente los cambios del área de trabajo para tener un directorio limpio sin necesidad de hacer un commit incompleto.

```bash
git stash                  # Guarda los cambios y limpia el directorio de trabajo
git stash -m "mensaje"     # Añade una descripción al stash
git stash list             # Muestra todos los estados guardados en el historial
git stash pop              # Recupera el último stash, lo aplica y lo elimina de la lista
```

---

### 🔍 Git Diff — Inspección de Cambios

| Comando | Descripción |
|---------|-------------|
| `git diff` | Muestra cambios en el directorio de trabajo que aún no han sido agregados al stage. |
| `git diff .` | Muestra todos los cambios en el directorio actual y subdirectorios. |
| `git diff <archivo>` | Muestra los cambios realizados específicamente en un archivo concreto. |
| `git diff --staged .` | Compara los archivos en stage contra el último commit. |
| `git diff --staged <archivo>` | Igual al anterior, pero filtrado por un archivo específico. |
| `git diff rama1 rama2` | Muestra las diferencias exactas entre dos ramas distintas. |

---

### 🧹 Buenas Prácticas: Limpieza de Ramas

Es una buena práctica fundamental borrar las ramas locales y remotas una vez que el Pull Request ha sido mergeado exitosamente.

**¿Por qué hacerlo?**

- **🔎 Claridad:** Evita tener un listado interminable de ramas obsoletas.
- **🛡️ Prevención de errores:** Impide trabajar accidentalmente sobre una rama que ya es historia.
- **📂 Orden:** Facilita la navegación en el repositorio para nuevos integrantes del equipo.

```bash
git branch -d <nombre-de-la-rama>            # Borrar rama local
git push origin --delete <nombre-de-la-rama> # Borrar rama remota
```

