# Nivel 10

## Objetivo
Decodificar una cadena en formato Base64 dentro de un archivo para obtener la contraseña del siguiente nivel.

## Codificación Base64 vs. Cifrado
En este nivel nos enfrentamos al formato **Base64**. Su función principal es convertir datos binarios (como imágenes, archivos o ejecutables) en texto plano legible (usando caracteres ASCII). Esto se hace con el fin de agilizar y asegurar el envío de información a través de sistemas de red o protocolos que originalmente solo soportan texto plano (como el correo electrónico o formularios web), evitando que los datos se corrompan en el camino.

Es sumamente importante mencionar que **Base64 NO es un método de cifrado**. No proporciona confidencialidad ni seguridad, ya que cualquier persona puede decodificarlo instantáneamente sin necesidad de una clave. Su único propósito es la representación y compatibilidad de datos. 

Una de las características más comunes para identificar visualmente una cadena en Base64 es la presencia de uno o dos signos de igual (`=`) o (`==`) al final del texto, los cuales se utilizan como caracteres de relleno (*padding*) para completar bloques de datos.

## Metodología
Utilizaremos el comando `cat` para leer el archivo que contiene la cadena codificada. En lugar de procesarlo a mano, abriremos una tubería (`|`) para enviar ese contenido de texto directamente al comando `base64` con la bandera de decodificación, logrando obtener la contraseña en texto claro al instante.

### Opciones clave del comando `base64`
Estas son las flags esenciales para trabajar con esta herramienta en la terminal:

| Flag | Nombre / Función | Descripción |
| :--- | :--- | :--- |
| `-d` o `--decode` | *Decode* | Decodifica la entrada de Base64 a su estado original de texto plano o binario. |
| `-w` o `--wrap` | *Wrap* | Ajusta las líneas a un número específico de caracteres (por defecto 76). Usa `0` para desactivar el salto de línea. |

## Acceso SSH
ssh bandit9@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
# Decodificar el contenido del archivo que está almacenado en formato Base64
cat data.txt | base64 -d
