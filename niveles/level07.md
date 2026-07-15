# Nivel 7

## Objetivo
Localizar una contraseña específica dentro del archivo `data.txt` que se encuentra al lado de la palabra "millionth".

## Búsqueda de contenido (Diferencia entre `find` y `grep`)
Mientras que `find` se utiliza para buscar **archivos y directorios** en el disco basándose en sus metadatos (nombre, tamaño, permisos), `grep` se utiliza para buscar **cadenas de texto o patrones** dentro del contenido de los propios archivos. 

En producción o análisis de logs, es común enfrentarse a archivos de texto masivos con miles de líneas de datos. Inspeccionar estos archivos manualmente con un editor de texto consume demasiado tiempo y recursos; `grep` escanea el archivo de forma instantánea línea por línea y devuelve únicamente las coincidencias.

## Metodología
Utilizaremos el comando `grep` apuntando al archivo `data.txt` y especificando el patrón "millionth" para filtrar la línea exacta que contiene la contraseña.

### Flags fundamentales de `grep`
Estas son las opciones más utilizadas y útiles en el día a día para refinar búsquedas:

| Flag | Nombre / Función | Descripción |
| :--- | :--- | :--- |
| `-i` | *Ignore case* | Ignora mayúsculas y minúsculas (ej: busca tanto "Millionth" como "millionth"). |
| `-v` | *Invert match* | Invierte la búsqueda; muestra todas las líneas que **no** contienen el patrón. |
| `-n` | *Line number* | Muestra el número de línea exacto dentro del archivo donde se encontró la coincidencia. |
| `-r` | *Recursive* | Busca el patrón de forma recursiva en todos los archivos del directorio actual y subdirectorios. |
| `-w` | *Word regexp* | Busca la palabra exacta, evitando coincidencias que formen parte de palabras más largas. |
| `-c` | *Count* | Solo muestra el número total de líneas que coinciden con el patrón. |
 
## Acceso ssh 
ssh bandit7@bandit.labs.overthewire.org -p 222

```bash
# Buscar la palabra exacta "millionth" dentro de data.txt
grep "millionth" data.txt
