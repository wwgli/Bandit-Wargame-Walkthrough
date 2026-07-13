# Nivel 0

## Objetivo
Conectarse al servidor de Bandit mediante SSH.

## Requisitos previos
Para poder realizar esta conexión, necesitas:
* **Un cliente SSH instalado:** En sistemas Linux (como Manjaro) ya viene instalado por defecto a través del paquete `openssh`.
* **Conectividad a internet:** El servidor de Bandit es un servicio externo, por lo que requieres una conexión activa.
* **Terminal:** Acceso a una interfaz de línea de comandos.

## ¿Qué es SSH?
SSH (Secure Shell) es un protocolo de red que permite acceder de forma remota a otros equipos de manera segura. Cifra toda la comunicación, lo que garantiza que los datos no viajen en texto plano por la red.

## Metodología
Utilizar el cliente SSH para autenticarse con el usuario `bandit0` en el host `bandit.labs.overthewire.org` usando el puerto `2220`.

## Solución técnica
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
