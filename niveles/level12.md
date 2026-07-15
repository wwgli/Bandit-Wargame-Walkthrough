# Nivel 12

## Objetivo
Recuperar la contraseña oculta dentro de un archivo que ha sido transformado repetidamente mediante volcados hexadecimales y múltiples capas de compresión.

## Creación de entornos temporales y gestión de permisos
Un aspecto fundamental de este nivel es la necesidad de trabajar dentro de directorios temporales (ubicados en `/tmp`). Al operar en un servidor compartido, el directorio de inicio suele tener restricciones de escritura. 

Al crear nuestro propio espacio temporal, adquirimos libre albedrío dentro de esa carpeta específica, lo que significa que contamos con permisos totales de **lectura, escritura y ejecución** (`rwx`). Esto nos permite generar y modificar archivos sin restricciones.

> **Nota de seguridad crucial (Diferencia con SUID):** Es sumamente importante no confundir este control total del directorio con los permisos **SUID (Set Owner User ID)**. Aunque tengamos permisos de ejecución (`x`) sobre las herramientas o scripts que guardemos en `/tmp`, estos procesos correrán estrictamente bajo el contexto y privilegios de nuestro usuario actual (`bandit12`). El bit SUID es un permiso especial que permite a un archivo ejecutarse con los privilegios del propietario del archivo (por ejemplo, `root`), lo cual no aplica en este entorno temporal controlado por nosotros.

## Metodología
El archivo original `data.txt` es un volcado hexadecimal (*hexdump*). El proceso requiere usar primero el comando `xxd -r` para revertir este volcado a su estado binario original. 

A partir de ahí, el binario pasa por múltiples capas de compresión. Un factor crucial en este nivel es que **cada uno de estos archivos debe tener su extensión o terminación correcta para que la descompresión sea efectiva y se pueda realizar**. Herramientas como `gzip` o `bzip2` no procesarán el archivo si no cuenta con su extensión nativa. Por lo tanto, el flujo de trabajo obligatorio en cada paso consiste en:
1. Analizar el archivo con `file` para identificar su tipo real.
2. Renombrar el archivo con `mv` para asignarle la extensión que le corresponde (`.gz`, `.bz2`, `.tar`).
3. Ejecutar el comando de descompresión adecuado.

### Herramientas de descompresión y extensiones requeridas

| Comando | Tipo de Compresión | Extensión Obligatoria | Comando de Descompresión |
| :--- | :--- | :--- | :--- |
| `xxd` | Volcado Hexadecimal | No requiere (`.txt`) | `xxd -r archivo > salida` |
| `gzip` | Compresión GNU | `.gz` | `gzip -d archivo.gz` |
| `bzip2` | Compresión por bloques | `.bz2` | `bzip2 -d archivo.bz2` |
| `tar` | Empaquetado Tarball | `.tar` | `tar -xf archivo.tar` |

## Acceso SSH
ssh bandit12@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
# 1. Crear directorio temporal para tener permisos totales y moverse a él
mkdir /tmp/mi_espacio_seguro
cd /tmp/mi_espacio_seguro

# 2. Revertir el volcado hexadecimal original
xxd -r ~/data.txt > data_binario

# 3. Ejemplo del ciclo de descompresión (repetir según el formato detectado):
file data_binario
mv data_binario data_binario.gz    # Asignar la terminación correcta para que sea efectivo
gzip -d data_binario.gz            # Descomprimir

