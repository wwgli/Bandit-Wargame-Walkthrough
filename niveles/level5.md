Nivel 5

## Objetivo
Localizar un archivo con propiedades específicas oculto dentro de una estructura compleja de subdirectorios para obtener la contraseña del siguiente nivel.

## El problema de la búsqueda por propiedades (Metadatos)
Cuando nos enfrentamos a sistemas con miles de archivos sin nombres descriptivos u organizados en múltiples subcarpetas, la inspección manual o el uso de comandos simples como `ls` se vuelve inviable. En administración de sistemas y seguridad informática, es fundamental saber filtrar búsquedas basándonos en los metadatos del archivo (como su tamaño, tipo de archivo y permisos de ejecución) en lugar de su nombre.

## Metodología
Utilizaremos el comando `find`, que nos permite recorrer directorios de forma recursiva aplicando filtros avanzados:
* **Filtro de tipo (`-type`):** Define qué tipo de elemento estamos buscando.
  * `-type f`: Busca únicamente **archivos** regulares (file).
  * `-type d`: Busca únicamente **directorios** o carpetas (directory).
* **Filtro de tamaño (`-size`):** Especificamos el tamaño exacto del archivo usando la sintaxis de modificadores y unidades.
* **Negación lógica (`!`):** El operador `!` (NOT) invierte el resultado del filtro que le sigue. Lo usaremos junto a `-executable` para buscar específicamente los archivos que **no** se puedan ejecutar.

### Referencia rápida de tamaños en `find`
Para tus búsquedas, puedes estructurar el parámetro `-size` de la siguiente forma: `[operador][valor][unidad]`.

**Operadores:**
* `(sin operador)`: Busca un tamaño exacto.
* `+`: Busca archivos más grandes que el valor indicado.
* `-`: Busca archivos más pequeños que el valor indicado.

**Unidades comunes:**
* `c`: Bytes
* `k`: Kilobytes
* `M`: Megabytes
* `G`: Gigabytes

*Ejemplo: `-size +10M` buscaría archivos mayores a 10 Megabytes.*

## Acceso SSH
```bash
ssh bandit5@bandit.labs.overthewire.org -p 2220

## Solucion tecnica 

# Buscar recursivamente un archivo de exactamente 1033 bytes que NO sea ejecutable
find . -type f -size 1033c ! -executable

# Leer el archivo resultante
cat ./maybehere07/.file2
