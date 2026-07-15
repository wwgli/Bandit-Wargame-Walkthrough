# Nivel 6

## Objetivo
Encontrar un archivo con propiedades específicas de tamaño, usuario propietario y grupo asignado, ubicado en algún lugar del servidor.

## El modelo de propiedad en Linux (Usuarios y Grupos)
En sistemas basados en Unix, la seguridad se gestiona a nivel de archivos asignando un **propietario (user)** y un **grupo (group)** a cada elemento. Esto define quién tiene el control del archivo y qué permisos tienen los miembros de un equipo de trabajo. 

Cuando realizamos auditorías de seguridad o búsquedas en todo el sistema (empezando desde la raíz `/`), es común cruzarnos con directorios a los que nuestro usuario actual no tiene permiso de acceder, lo que satura la terminal con mensajes de error ("Permission denied"). Para mantener la salida limpia, redirigimos el flujo de errores (`stderr`) al "agujero negro" de Linux (`/dev/null`).

## Metodología
Utilizaremos de nuevo el comando `find`, pero esta vez buscando desde la raíz del sistema (`/`) y agregando filtros de pertenencia:
* **Filtro de usuario propietario (`-user`):** Especifica el nombre del usuario dueño del archivo.
* **Filtro de grupo (`-group`):** Especifica el grupo al que pertenece el archivo.
* **Redirección de errores (`2>/dev/null`):** 
  * `2` representa el canal de error estándar (stderr).
  * `>` es el operador de redirección.
  * `/dev/null` es un dispositivo virtual que descarta toda la información que recibe.
  * Al usar `2>/dev/null`, ocultamos los mensajes de "Permiso denegado" para ver solo el resultado que nos interesa.

## Acceso SSH
ssh bandit6@bandit.labs.overthewire.org -p 2220

## Solucion técnica

```bash 
# Buscar un archivo de 33 bytes, propiedad del usuario bandit7 y grupo bandit6 en todo el disco
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null

# Leer la contraseña del archivo encontrado (ejemplo de ruta habitual)
cat /var/lib/dpkg/info/bandit7.password
