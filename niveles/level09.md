# Nivel 9

## Objetivo
Localizar una contraseña legible dentro del archivo binario `data.txt`, la cual se encuentra precedida por varios caracteres de igual (`=`).

## El análisis de archivos binarios (Comando `strings`)
Cuando intentamos leer un archivo binario o compilado utilizando herramientas estándar como `cat`, la terminal suele llenarse de símbolos extraños, caracteres no imprimibles y "basura" visual que incluso puede llegar a desconfigurar el comportamiento de nuestra consola. 

En auditorías de seguridad y análisis forense, utilizamos el comando `strings` para solucionar esto. Este comando escanea archivos binarios y extrae únicamente las secuencias de caracteres legibles (ASCII) de forma limpia. En este nivel, como sabemos que la contraseña está rodeada por varios caracteres `=`, podemos combinar la extracción de texto con un filtro específico.

## Metodología
Utilizaremos el comando `strings` apuntando al archivo `data.txt` para filtrar y desechar toda la información binaria no legible. El resultado lo pasaremos a través de una tubería (`|`) al comando `grep` buscando el patrón `==` para dar directamente con la línea que esconde la contraseña.

### Flags útiles de `strings`
Estas opciones son de gran ayuda al analizar binarios pesados o buscar firmas específicas:

| Flag | Función | Descripción |
| :--- | :--- | :--- |
| `-n [número]` | *Min-len* | Define la longitud mínima que debe tener una cadena para considerarse legible (por defecto es 4). |
| `-a` | *All* | Escanea el archivo completo en lugar de solo las secciones de datos inicializadas del binario. |
| `-t [formato]` | *Radix* | Muestra la ubicación (offset) exacta en bytes donde se encuentra cada cadena dentro del archivo. |

## Acceso SSH
ssh bandit9@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
# Extraer solo el texto legible de data.txt y filtrar las líneas con múltiples caracteres "="
strings data.txt | grep "=="
