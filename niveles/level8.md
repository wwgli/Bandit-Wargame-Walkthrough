# Nivel 8

## Objetivo
Localizar la única contraseña que no se repite dentro del archivo `data.txt`, el cual contiene una lista sumamente extensa de contraseñas duplicadas.

## El uso de tuberías y procesamiento de texto
Para resolver este nivel, el foco principal es entender cómo funciona una **tubería (pipe `|`)**. Básicamente, una tubería nos permite encadenar procesos: toma la salida del primer comando y, en lugar de mostrarla en pantalla o guardarla en un archivo, la envía directamente como entrada para que el siguiente comando haga algo con ella. 

El desafío aquí es que se nos presenta una lista enorme de contraseñas donde todas se repiten, excepto una. Para resolver esto de forma eficiente, mi estrategia se divide en dos pasos clave:
1. **Ordenar los datos (`sort`):** Primero organizamos todas las contraseñas alfabéticamente para que las que son idénticas queden juntas (consecutivas).
2. **Filtrar la única diferente (`uniq -u`):** Después de ordenar, abrimos una tubería hacia `uniq -u`. Esto es indispensable porque `uniq` solo detecta duplicados si están en líneas adyacentes. Al recibir la lista ya ordenada por la tubería, `uniq` puede descartar todos los duplicados y entregarnos únicamente la línea que aparece una sola vez.

## Metodología
Utilizaremos el comando `cat` para leer el archivo `data.txt`. Su salida se enviará mediante una tubería al comando `sort` para agrupar las líneas idénticas. Finalmente, abriremos otra tubería hacia el comando `uniq -u` para extraer la contraseña única.

### Flags útiles de `uniq` que apliqué en este análisis:

| Flag | Función | Descripción |
| :--- | :--- | :--- |
| `-u` | *Unique* | Muestra únicamente las líneas que **no** están duplicadas en el archivo. |
| `-d` | *Repeated* | Muestra únicamente las líneas que **sí** están duplicadas (una sola vez por grupo). |
| `-c` | *Count* | Antepone a cada línea el número de veces que aparece repetida. |

## Acceso SSH
ssh bandit8@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
# Ordenamos las contraseñas y pasamos el resultado por tubería para filtrar la única diferente
cat data.txt | sort | uniq -u
