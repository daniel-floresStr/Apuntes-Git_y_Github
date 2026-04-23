# Trabajo indivudual
Daniel Teodoro Flores Mamani
## Clase 1
Git es un sistema de control de versiones que permmite guardar archivos y versiones de estos a lo largo del tiempo 
### Nacimiento 
Su nacimiento se remonta a discusion provocada entre Linus Torvalds y el manejo del software Bitkeeper el cual era muy restrictivo y solo permitia el uso de sus propios componentes, por lo cual Torvalds en un aproximado de 2 - 4 semanas pudo encontrar una solución para desplazar Bitkeeper
### Instalación 
Su instalacion depende del sistema operativo que se usa en mi caso con Windows se hace con la instalacion de un ejecutable que mediante permisos instale y accedi a la ultima version de git
### Configuraciones basicas 
Las usadas serian:
- git config --list (todas las configuraciones realizadas)
- git config --global user.name "Daniel Teodoro Flores Mamani" (configuracion del nombre de usuario)
- git config --global user.email "danieltfloresmamani@gmail.com" (configuracion del correo a usar)
## Clase 2 
### States y commits
Tipos de estados:
- Directorio de trabajo: Carpeta donde se guardara el trabajo "escritura de codigo".
    Archivo de guardado los cataloga segun:
    - Untracked: Se observa archivos nuevos, archivos donde no hay una version anterior
    - Modificated: Se observan archivos que ya tienen versiones anteriores y se les va a hacer alguna modificacion 

    --- git status --- Una forma de verificar los estados de las carpetas (untracked, modificated)
    --- git restore --- Restaura todos los cambios realizados (eliminaciones, creacion de nuevas carpetas, lo devuelve a un estado anterior)
    --- .gitignore --- Para archivos ocultos en donde al momento de editar el archivo y agregarle el documento que no se quiere mostrar en el nuevo commit 
- Stage Area: Area de espera.
Selecciona los archuvos y se guardan en el historial con --- git add .--- (guarda todas las modificaciones) --- git add."nombre del archivo" solo guarda esa modificacion.
Para deshacer  --- git restore -- staged "nombre del archivo"
    
- Repositorio Local: El historial de cambios realizados.
Guarda cambios con --- git commit -m "mensaje descriptivo" crea un punto de guardado
--- git log --oneline ---- resumen de versiones
Para resetear o cambiar mi commit --- git reset --soft HEAD ~1 --- 
### Buenas practicas 
- ¿Cada cuanto debo hacer un commit?
    Concepto de commit atomico --> hacer cuando haces un cambio pequeño, cambios cortos,simples que cambien la funcionalidad; que tengan significado 
- Descripcion del commit
    Lleva el siguiente --- git commit -m "tipo de commit: descripcion" ---
    En verbos imperativos y con palabras demostrativas como feat, fix, docs, etc
Con el comando --- git commit --- se abre el editor vim donde se añade varias funcionalidades de un commit

