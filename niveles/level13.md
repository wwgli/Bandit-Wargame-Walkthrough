# Nivel 13

## Objetivo
Utilizar una clave privada de SSH alojada en el servidor para autenticarse directamente como el usuario `bandit14` y extraer su contraseña correspondiente de los archivos del sistema.

## Autenticación basada en Claves Privadas y la importancia de `chmod 600`
En este nivel se introduce el uso de las claves privadas de SSH, un método de autenticación criptográfico que resulta sumamente importante en entornos profesionales, ya que nos permite saltarnos el paso de colocar la contraseña directamente, facilitando accesos rápidos y automatizaciones seguras. 

Para utilizarla, se introduce la flag `-i` (*identification file*), la cual nos permite especificar la ruta del archivo que contiene la llave de identidad SSH. 

Sin embargo, al tratarse de información de acceso tan crítica, el sistema operativo exige una gestión de privilegios sumamente estricta. Si el archivo de la clave privada tiene permisos demasiado abiertos (permitiendo que otros usuarios del servidor lo lean), el cliente SSH bloqueará la conexión por seguridad. Para corregir esto y asegurar el archivo, se hace uso del comando `chmod 600`.

### El sistema numérico de `chmod` (Suma de valores rwx)
Para entender por qué utilizamos exactamente el número `600`, es fundamental comprender que el comando `chmod` funciona mediante la suma de los valores asignados a cada tipo de permiso básico (**rwx**):
* **r** (Lectura / *Read*) vale **4**
* **w** (Escritura / *Write*) vale **2**
* **x** (Ejecución / *Execute*) vale **1**

El comando recibe tres dígitos que representan al **Propietario**, al **Grupo** y a los **Otros**, respectivamente. En nuestro caso:
* **Primer dígito (6):** Es la suma de `4 (lectura) + 2 (escritura) = 6`. Esto nos otorga permisos completos para leer y modificar nuestra propia llave.
* **Segundo dígito (0):** No se suma ningún valor. El grupo tiene acceso denegado.
* **Tercer dígito (0):** No se suma ningún valor. Cualquier otro usuario del sistema tiene el acceso totalmente denegado.

Al aplicar `chmod 600`, garantizamos que únicamente nuestro usuario tenga control sobre la llave, cumpliendo con los requisitos de seguridad de SSH.

## Metodología
1. Ajustaremos los permisos de la llave privada (`sshkey.private`) usando la suma octal de `chmod 600`.
2. Ejecutaremos el comando de conexión apuntando a `localhost` utilizando la bandera `-i` seguida del archivo de la llave para migrar directamente a la sesión de `bandit14`.
3. Una vez dentro de la sesión de `bandit14`, utilizaremos el comando `cat` sobre la ruta global `/etc/bandit_pass/bandit14` para revelar y recuperar la contraseña real que nos permitirá avanzar al siguiente reto.

## Acceso SSH
ssh bandit13@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
# 1. Asignar los permisos obligatorios calculando el valor octal (4+2=6)
chmod 600 sshkey.private

# 2. Conectarse al usuario bandit14 usando la llave de identificación
ssh -i sshkey.private bandit14@localhost -p 2220

# 3. Leer el archivo del sistema para extraer la contraseña real del nivel 14
cat /etc/bandit_pass/bandit14
