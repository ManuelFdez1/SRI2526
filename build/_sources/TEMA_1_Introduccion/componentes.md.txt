Componentes de los Srv. de Red
===============================

Para poder configurar correctamente cualquier servicio, se deben tener claros algunos conceptos relacionados con las redes informáticas.

**PROTOCOLOS**

En el campo de las telecomunicaciones, un protocolo de comunicaciones es el conjunto de reglas normalizadas para la representación, señalización, autenticación y detección de errores necesario para enviar información a través de un canal de comunicación.
Al conjunto de protocolos que aseguran la comunicaciones entre dos o más sistemas las denominamos *pila de protocolos*. Conocemos dos modelos, uno funciona como marco práctico (**OSI**) y el otro es el más utilizado en la práctica (**TCP/IP**). Los distintos protocolos trabajan directamente con sus iguales en el otro extremo de la comunicación.

<a title="Cristianzambrano / CC BY-SA (https://creativecommons.org/licenses/by-sa/3.0)" href="https://commons.wikimedia.org/wiki/File:Osi_y_tcp-ip.jpg"><img width="512" alt="Osi y tcp-ip" src="https://upload.wikimedia.org/wikipedia/commons/0/03/Osi_y_tcp-ip.jpg" style="display:block;margin-left:auto;margin-right:auto;"></a>

En este módulo nos vamos a centrar en algunos de los protocolos más importantes de la **capa de Aplicación**

<a title="GISEPROI / CC BY-SA (https://creativecommons.org/licenses/by-sa/4.0)" href="https://commons.wikimedia.org/wiki/File:Suite_de_Protocolos_TCPIP.png"><img width="512" alt="Suite de Protocolos TCPIP" src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Suite_de_Protocolos_TCPIP.png/512px-Suite_de_Protocolos_TCPIP.png" style="display:block;margin-left:auto;margin-right:auto;"></a>


**DIRECCIONAMIENTO IP:**

Una dirección IP es una etiqueta numérica que identifica a un interfaz (elemento de comunicación/conexión) de un dispositivo (habitualmente una computadora) **dentro de una MISMA red** que utilice el protocolo IP (Internet Protocol), que corresponde al nivel de red del protocolo TCP/IP.

<u>CARACTERÍSTICAS:</u>
+ Existen 5 clases.
+ Nos interesan los tres primeros (A, B y C)
+ Hay dos tipos de  direcciones
  + Públicas
  + Privadas
+ IPv4 vs IPv6


<u>OTROS PARÁMETROS IP:</u>

Además de la dirección IP, todo equipo necesita tener definidos otros parámetros para poder interactuar en la red correctamente.
+ **MÁSCARA DE SUBRED**: La máscara permite distinguir los bits que identifican la red y los que identifican el host de una dirección IP.
+ **PUERTA DE ENLACE/GATEWAY/PASARELA**: Direccion del dispositivo que permite interconectar redes con protocolos y arquitecturas diferentes a todos los niveles de comunicación. *Obligatoriamente debe estar en la misma red que el equipo*.
+ **SERVIDOR/ES DNS**: Direccion/es de aquel/aquellos equipo/s encargado/s de traducir los nombres de dominio por su correspondiente IP. *Puede estar en una red externa*.



___
> **RECUERDA...**
1. ¿Que elemento maneja el nivel de enlace, el de red y el de transporte, para realizar sus funciones correspondientes?
2. Explica la estructura de las tres clases de direcciones IP que nos interesan, indicando la cantidad de redes existentes y el número de ordenadores que podemos incluir en cada una de esas redes. Indica, para cada clase, los rangos de direcciones públicas y privadas.
3. Explica las diferencias entre las dos versiones de IP comentadas.
4. Indica los comandos que utilizarías para averiguar la información IP, tanto en Windows como en Linux.
5. Averigua tu IP pública.¿Cual es la de tus compañeros?¿Podrías explicarlo?
6. ¿La puerta de enlace ha de pertenecer a tu red para funcionar correctamente?¿y los servidores DNS?
7. De los protocolos de la capa de aplicación, nombra 5 e indica su función y el nº de puerto que utilizan para operar.
8. ¿Qué es una **dirección** de red?¿y una de **broadcast**?
9. ¿Sabrías partir una red(**subnetting**) de tipo C en 4 subredes, por ejemplo *192.168.100.0/24*?
___

