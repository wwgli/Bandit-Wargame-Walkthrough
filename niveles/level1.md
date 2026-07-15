# Nivel 1

## Objetivo
Leer un archivo que tiene un nombre "especial" (un guion `-`) y obtener la contraseña del siguiente nivel.

## ¿Qué son las rutas y los caracteres especiales?
En Linux, una **ruta absoluta** es la dirección exacta y completa de un archivo o carpeta dentro de un sistema, comenzando siempre desde la raíz (`/`). Por otro lado, una **ruta relativa** es la dirección desde nuestra ubicación actual. Algunos caracteres como el guion (`-`) tienen funciones especiales en la terminal (como indicar parámetros o banderas); si un archivo comienza con estos, la terminal los interpreta como una instrucción y no como el nombre del archivo.

## Metodología
Primero, acceder al servidor con el usuario `bandit1`. Una vez dentro, al intentar ejecutar `cat -`, el sistema falla porque interpreta el guion como una bandera de comando. Se debe especificar la ruta relativa (`./-`) o la ruta absoluta (`/home/bandit1/-`) para que el sistema lo reconozca como un nombre de archivo y muestre su contenido.

## Acceso SSH
ssh bandit1@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
cat ./-
