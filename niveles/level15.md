# Nivel 15

## Objetivo
Enviar la contraseña del nivel actual al puerto 30001 de la máquina local (`localhost`), utilizando una conexión segura y cifrada mediante el protocolo SSL/TLS para obtener las credenciales del siguiente nivel.

## Introducción al cifrado en tránsito: SSL y TLS
Este nivel plantea exactamente el mismo escenario de comunicación del reto anterior, pero introduce un factor crítico en seguridad informática: **el cifrado de datos en tránsito**. 

Es de vital importancia comprender que **SSL (Secure Sockets Layer)** y su evolución **TLS (Transport Layer Security)** son protocolos de cifrado utilizados para asegurar que la información transmitida a través de una red sea completamente confidencial. Al aplicar este protocolo, los datos se vuelven ilegibles para cualquier atacante que intente interceptar el tráfico, garantizando que **únicamente el receptor y el emisor que los envía puedan interpretar y descifrar el mensaje**.

## Herramientas avanzadas de red: Ncat con soporte SSL
Para establecer este tipo de conexiones seguras desde la terminal de Linux, el Netcat clásico (`nc`) se queda corto, ya que no maneja cifrado de forma nativa. Por ello, se introduce **Ncat**, una versión mucho más robusta y moderna de la herramienta. 

Para interactuar con el servicio seguro que está escuchando en el servidor, invocaremos el comando `ncat` acompañado del parámetro específico `--ssl`, lo que le indica a la herramienta que debe negociar un canal cifrado seguro antes de realizar cualquier envío de datos hacia el puerto objetivo.

## Metodología
Utilizaremos el comando `ncat` apuntando a `localhost` en el puerto `30001`. Al añadir la bandera `--ssl`, el comando establecerá un túnel seguro con el servicio. Una vez que la conexión cifrada esté abierta, le inyectaremos el contenido de nuestra contraseña actual de `bandit15` (ubicada en `/etc/bandit_pass/bandit15`) para que el sistema la valide de forma segura y nos devuelva la contraseña del siguiente nivel.

## Acceso SSH
ssh bandit15@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
# Establecer una conexión cifrada por SSL/TLS al puerto 30001 e inyectar la contraseña actual
cat /etc/bandit_pass/bandit15 | ncat --ssl localhost 30001
