# Nivel 3

## Objetivo
Localizar un archivo oculto dentro del directorio `inhere` y leer su contenido para obtener la contraseña del siguiente nivel.

## Requisitos previos
* **Acceso SSH al nivel:** Conectarse al servidor usando la contraseña obtenida en el nivel anterior.
* **Navegación de directorios:** Conocer el uso básico del comando `cd` (change directory).
* **Terminal:** Acceso a una interfaz de línea de comandos.

## El problema de los archivos ocultos
En sistemas Linux, cualquier archivo o directorio que comienza con un punto (`.`) es considerado oculto por el sistema y no se muestra al ejecutar un `ls` estándar. Esto se utiliza comúnmente para archivos de configuración de usuarios o del sistema, evitando que se saturen las carpetas principales y protegiéndolos de borrados accidentales.

## Metodología
Primero, debemos movernos al directorio `inhere`. Al listar los archivos con `ls`, veremos que la carpeta parece estar vacía. Para visualizar los archivos ocultos, utilizaremos la bandera `-a` (all) junto al comando `ls`. Una vez identificado el archivo, usaremos `cat` para leerlo.

## Acceso SSH
ssh bandit3@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
# Entrar al directorio
cd inhere

# Listar todos los archivos (incluyendo ocultos)
ls -a

# Leer el archivo oculto (por ejemplo, .hidden)
cat .hidden
