# Nivel 4

## Objetivo
Identificar un archivo que contiene la contraseña del siguiente nivel entre muchos otros archivos, utilizando el comando `file` para evitar la inspección manual.

## El problema de las extensiones
A diferencia de Windows, donde el sistema operativo utiliza la extensión para saber qué programa abrir, en Linux el sistema ignora las extensiones. Un archivo puede llamarse `datos.txt` y ser en realidad un binario ejecutable o una imagen. El comando `file` es la herramienta estándar para inspeccionar el contenido de un archivo y determinar su tipo real sin necesidad de intentar abrirlo.

## Metodología
Al entrar en el directorio `inhere`, nos encontramos con numerosos archivos. Hacer `cat` a cada uno sería ineficiente. Utilizaremos el comando `file` sobre todos los archivos del directorio para filtrar cuáles son de texto plano y así encontrar la contraseña rápidamente.

## Acceso SSH
ssh bandit4@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
# Entrar al directorio
cd inhere

# Identificar el tipo de todos los archivos
file ./*

# Leer el archivo que sea identificado como texto ASCII
cat ./-file07
