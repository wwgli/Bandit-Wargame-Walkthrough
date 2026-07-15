# Nivel 17

## Objetivo
Identificar la contraseña del siguiente nivel comparando dos archivos de texto (`passwords.old` y `passwords.new`) y localizando la única línea que fue modificada entre ambos.

## Automatización vs. Procesos Engorrosos: El uso de `diff`
Comparar dos archivos con múltiples líneas de texto de forma manual es un proceso lento, tedioso y propenso a errores humanos. En la administración de sistemas y la ciberseguridad, la eficiencia es fundamental. 

Para evitar este trabajo engorroso, Linux cuenta con el comando **`diff`**. 

> **Funcionamiento básico:** `diff` actúa como un comparador automático. Analiza ambos archivos simultáneamente bajo el capó y, en lugar de mostrarte todo el contenido, limpia el ruido y **te proyecta en pantalla únicamente la diferencia exacta** entre el archivo viejo y el nuevo.

## Metodología
Ejecutaremos el comando `diff` pasando como argumentos el archivo antiguo y el archivo nuevo. Al hacerlo, el comando nos mostrará en la terminal la línea de texto que difiere. La línea que pertenezca al archivo `.new` será nuestra contraseña para `bandit18`.

## Acceso SSH
ssh bandit17@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
# Comparar el archivo viejo con el nuevo para extraer la única línea modificada
diff passwords.old passwords.new
