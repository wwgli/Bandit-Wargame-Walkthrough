# Nivel 11

## Objetivo
Desencriptar la contraseña del archivo `data.txt`, la cual ha sido alterada utilizando el método de rotación ROT13.

## El cifrado de sustitución ROT13
El cifrado ROT13 es un método sumamente básico de manipulación de texto, ya que solo se encarga de rotar las letras 13 lugares hacia adelante en el abecedario. Siguiendo esta lógica, la letra `A` se convierte en `N`, la `B` se convierte en `O`, y así sucesivamente hasta llegar a la `M`, que se convierte en `Z`. 

Debido a que el alfabeto tiene 26 letras, este sistema es simétrico: si vuelves a aplicar la misma rotación de 13 posiciones a un texto ya cifrado, este se descifra automáticamente regresando a su estado original. Al ser una técnica tan simple, no ofrece seguridad real en la actualidad.

## Metodología
Para lograr descifrar este mensaje en la terminal, utilizaremos el comando `tr` (translate). Este comando nos permite mapear un rango de caracteres de entrada y reemplazarlos de forma exacta por un rango de salida. Definiremos el abecedario completo (tanto en minúsculas como en mayúsculas) y le indicaremos a `tr` el desplazamiento correspondiente para que haga la sustitución de caracteres de manera instantánea.

### Parámetros de sustitución en el comando `tr`
El mapeo se estructura indicando el orden en que se van a intercambiar las letras:

| Rango Original | Rango de Sustitución (Rotado) | Descripción |
| :--- | :--- | :--- |
| `a-z` | `n-za-m` | Mapea las letras minúsculas desplazándolas 13 posiciones. |
| `A-Z` | `N-ZA-M` | Mapea las letras mayúsculas manteniendo el mismo desplazamiento. |

## Acceso SSH
ssh bandit11@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
# Leer el archivo y aplicar el comando tr para revertir la rotación de 13 posiciones
cat data.txt | tr 'a-zA-Z' 'n-za-mN-ZA-M'
