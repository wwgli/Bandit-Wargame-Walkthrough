# Nivel 16

## Objetivo
Escanear un rango de 1000 puertos (del 31000 al 32000) en la máquina local para identificar cuál de ellos tiene un servicio activo con cifrado SSL/TLS, y enviarle la contraseña actual para obtener las credenciales del siguiente nivel.

## El problema de la eficiencia y la solución con Nmap
En este nivel se nos presenta un nuevo problema: el servicio objetivo se encuentra oculto en un rango de 1000 puertos posibles. Intentar hacer una conexión manual uno por uno para adivinar cuál es el correcto resultaría un proceso sumamente lento e ineficiente. 

Para resolver esto de forma profesional, hacemos uso de una de las mejores y más potentes herramientas en el mundo de las redes y la ciberseguridad: **Nmap** (Network Mapper). 

> **Analogía técnica:** Imaginemos que nos encontramos en un cuarto completamente oscuro a ciegas; **Nmap será nuestra linterna**. Con un solo ráfaga de luz, nos iluminará el entorno y nos dirá de forma instantánea qué accesos están abiertos, cuáles están cerrados y qué hay dentro de ellos sin necesidad de ir a tocarlos a ciegas uno por uno.

## Metodología (Estrategia de Escaneo en Dos Fases)
Para abordar este reto de la forma más eficiente y realista posible, aplicaremos una metodología de reconocimiento dividida en dos etapas:

1. **Fase de Descubrimiento Rápido:** Lanzaremos un primer barrido de alta velocidad configurando el temporizador en `-T4` (modo agresivo/rápido) y aplicando el filtro `--open`. Esto nos permite ignorar por completo los puertos cerrados o filtrados, enfocando la linterna únicamente en los objetivos que están respondiendo.
2. **Fase de Enumeración Agresiva:** Una vez identificados los puertos de interés, realizaremos un escaneo específico y profundo empleando banderas de detección de servicios (`-sV` o `-A`) para auditar qué versiones están corriendo bajo esos puertos y confirmar cuál de ellos implementa cifrado SSL/TLS de forma real.

## Acceso SSH
ssh bandit16@bandit.labs.overthewire.org -p 2220

## Solución técnica

```bash
# Paso 1: Descubrimiento a alta velocidad de puertos abiertos únicamente
nmap --open -T4 -p 31000-32000 localhost

# Paso 2: Escaneo agresivo dirigido al puerto detectado para extraer servicios y versiones
# (Sustituir [PUERTO] por el resultado del paso anterior, por ejemplo: 31790)
nmap -sV -p [PUERTO] localhost

# Paso 3: Establecer la conexión cifrada e inyectar la credencial actual
cat /etc/bandit_pass/bandit16 | ncat --ssl localhost [PUERTO]
