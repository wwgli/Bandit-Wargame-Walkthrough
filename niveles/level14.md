# Nivel 14

## Objetivo
Enviar la contraseña del nivel actual al puerto 30000 en la máquina local (`localhost`) utilizando Netcat para recibir las credenciales del siguiente nivel.

## Fundamentos de Redes con Netcat (`nc`)
En este nivel se presenta la herramienta **Netcat (`nc`)**, una utilidad sumamente versátil en redes y ciberseguridad que se utiliza para el envío y recepción de datos a través de conexiones de red. Es fundamental saber que **este envío de datos no es cifrado**, lo que significa que la información viaja en texto plano y puede ser escuchada, interceptada y comprendida con total facilidad por un tercero en la red.

Para utilizar Netcat de forma efectiva, se necesitan dominar dos conceptos clave:

1. **Dirección IP (Internet Protocol):** Así como nosotros usamos números de teléfono para llamarnos, las máquinas usan una IP para identificarse y comunicarse. Existen dos tipos principales:
   * **IP Privada:** La que se utiliza exclusivamente dentro de redes locales (como tu casa o laboratorio).
   * **IP Pública:** La dirección con la que una red sale hacia Internet.
   * **Localhost:** En este escenario en particular, utilizamos el parámetro `localhost` (o la IP loopback `127.0.0.1`), ya que la comunicación la estamos realizando de forma interna dentro de la misma máquina local.

2. **Puerto:** Para entender los puertos, imaginemos que la IP es la dirección de un gran edificio, y dentro de ese edificio viven muchas personas, donde **cada una de ellas ofrece un servicio diferente**. El número de puerto es el "departamento" exacto al que debemos dirigirnos para interactuar con un servicio específico (por ejemplo, la web usa el puerto 80/443, SSH usa el 22, y en este reto, el servicio objetivo escucha en el puerto 30000).

## Metodología
Haciendo uso de la sesión de `bandit14` que obtuvimos en el nivel anterior, leeremos la contraseña actual. Posteriormente, abriremos una conexión de red directa usando `nc` apuntando a `localhost` en el puerto `30000`. Una vez establecida la conexión en texto plano, le enviaremos la contraseña actual como si fuera el mensaje requerido para que el servicio del "departamento 30000" nos devuelva la contraseña de `bandit15`.

## Acceso SSH
ssh bandit14@bandit.labs.overthewire.org -p 2220

## Solución técnica
```bash
# Conectarse al puerto 30000 de la máquina local y enviarle la contraseña actual
 nc localhost 30000
