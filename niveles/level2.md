# Nivel 2

## Objetivo
Leer un archivo que tiene espacios en su nombre (el archivo se llama `spaces in this filename`) para obtener la contraseña del siguiente nivel.

## Requisitos previos
Para poder realizar esta conexión, necesitas:
* **Acceso SSH al nivel:** Conectarse al servidor usando la contraseña obtenida en el nivel anterior.
* **Comprensión de caracteres especiales:** Entender cómo la terminal interpreta los espacios como separadores de argumentos.
* **Terminal:** Acceso a una interfaz de línea de comandos.

## El problema de los espacios
En Linux, los espacios en blanco actúan como separadores de comandos. Si intentas ejecutar `cat spaces in this filename`, la terminal intentará abrir cuatro archivos distintos (llamados `spaces`, `in`, `this` y `filename`). Es importante mencionar que utilizar espacios en los nombres de archivos es una mala práctica en entornos de sistemas, ya que complica la automatización, el manejo mediante scripts y la administración general.

## Metodología
Para tratar el nombre como una sola unidad, debemos proteger los espacios. La forma más común es envolver el nombre del archivo en comillas dobles o simples. También se pueden utilizar caracteres de escape o incluso el autocompletado del sistema.

## Acceso SSH
ssh bandit2@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
cat "spaces in this filename
"
# Utilizando comillas simples
cat 'spaces in this filename'

# Utilizando el carácter de escape (barra invertida)
cat spaces\ in\ this\ filename

# Utilizando autocompletado (presionando la tecla Tab)
cat spaces[TAB]
