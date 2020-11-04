======================
Interconexión de Redes
======================

Cuando se diseña una LAN se desea sacar el máximo rendimiento de sus capacidades. Para conseguir esto, la red debe estar preparada para efectuar conexiones a través de otras redes, sin importar qué características posean. El objetivo de la Interconexión de Redes (internetworking) es dar un servicio de comunicación de datos que involucre diversas redes con diferentes tecnologías de forma transparente para el usuario. Internet es, en realidad un conjunto de redes conectadas entre si.



.. raw:: html

    <div style="text-align:center;">
    <a title="Audit3, CC BY-SA 4.0 &lt;https://creativecommons.org/licenses/by-sa/4.0&gt;, via Wikimedia Commons" href="https://commons.wikimedia.org/wiki/File:Lanwan.gif"><img width="400" alt="Lanwan" src="https://upload.wikimedia.org/wikipedia/commons/9/98/Lanwan.gif"></a>
    </div>

El punto de entrada/salida de una red es el ROUTER cuya función principal consiste en enviar o encaminar paquetes de datos de una red, entendiendo por red un conjunto de máquinas en el mismo rango de IP/NETMASK y que, por tanto, se pueden comunicar sin la intervención de un router.

Los routers poseen, al menos, una interfaz conectada al exterior y otra conectada a la LAN  y realiza dos funciones:

  * Enrutamiento
  * NAT

**ENRUTAMIENTO**

Los routers son equipos con diversas tarjetas de interfaz de red, cada una conectada a una red distinta. La funcion de enrutamiento consiste en decidir por donde envia los paquetes para llegar de una red a otra. En la configuración más simple, el router sólo tiene que "mirar" en qué red se encuentra un equipo para enviarle datagramas desde el remitente. Recuerda la **configuración de rutas en los dispositivos de red**:

   - Rutas estáticas.
   - Rutas dinámicas.
   - Rutas por defecto.


**NAT (Network Address Translation - Traducción de Dirección de Red)**

Es un mecanismo utilizado por routers para intercambiar paquetes entre dos redes que con direcciones incompatibles(según si combinación IP/NETMASK). Consiste en convertir, en tiempo real, las direcciones utilizadas en los paquetes transportados.

.. raw:: html

    <div style="text-align:center;">
    <a href="https://en.wikipedia.org/wiki/Network_address_translation" target="_blank"><img width="600" alt="Lanwan" src="https://upload.wikimedia.org/wikipedia/commons/c/c7/NAT_Concept-en.svg"></a>
    </div></br>


.. important::
   Estas funciones se pueden activar dentro del software de un router o de un equipo para que actúe como dispositivo de e/s de una red local.

Además de el envío de tráfico entre distintas redes locales, también veremos como realizar esta conexión con un nivel mayor de seguridad, a través de la configuración de un proxy web. Todo ello lo veremos a través de los siguientes apartados:

.. toctree::
   :maxdepth: 2

   acceso
   puertos
   seguridad
