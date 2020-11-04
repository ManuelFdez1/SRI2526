Seguridad. Proxy-Caché
==============================

Un proxy es un programa o dispositivo que realiza una acción en representación de otro. Esta situación estratégica de punto intermedio suele ser aprovechada para soportar una serie de funcionalidades:

* PROPORCIONAR CACHÉ.
* CONTROL DE ACCESO
* REGISTRO DEL TRÁFICO
* PROHIBIR CIERTO TIPO DE TRÁFICO.
* REGULACION ANCHO DE BANDA

El uso mas común de este servicio se encuentra en Internet. Se trata de un **proxy para el control del acceso a la web (principalmente los protocolos HTTP y HTTPS)**, proporcionando una caché para las páginas web y los contenidos descargados. Cuando esto sucede se dice que el proxy web está haciendo un servicio de proxy-cache. Esta caché es compartida por todos los usuario del proxy, con la consiguiente mejora en los tiempos de acceso para consultas coincidentes. Al mismo tiempo libera la carga de los enlaces hacia Internet.

Squid
--------

Vamos a estudiar uno de los proxy más ampliamente utilizado en la actualidad, **SQUID**, encontramos la version para Windows y para Linux. Siendo más utilizado en servidores Linux-Unix, ya que originariamente es un SW de esta platarfoma. La configuración es exactamente igual en los dos Sistemas Operativos.

Ya teniendo instalado nuestro servidor squid, ahora deberemos saber en donde se encuentra toda la configuración del mismo(**/etc/squid**). Ya dentro de esta carpeta se encontraran varios archivos pero el mas importante es el **squid.conf** el cual se encarga de la configuración del servicio. En la configuración de squid hay que distinguir varios elementos:

1 Configuración General: Parámetros generales de funcionamiento del servicio.
2 ACL (Lista de control de acceso): Definición de conjunto de elementos a los que se aplicarán reglas.
3 REGLAS: Decisiones de autorización/denegación de acceso a ACL.

Los recursos que podéis encontrar en la web son muchos, por ejemplo el siguiente videotutorial:

.. raw:: html

            <iframe width="250" style="display:block; margin-left:auto; margin-right:auto;"src="https://www.youtube.com/embed/zXusMCM6p_k" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></br>

O también podéis encontrar manuales, como en el `siguiente enlace <http://www.alcancelibre.org/staticpages/index.php/19-0-como-squid-general>`_.


Proxy transparente
------------------

La principal desventaja del uso de proxy es la necesidad de configurar los navegadores ”a mano”,  con la consiguiente desventaja en cuanto a seguridad y escalabilidad. La solución a esta situación pasa por la utilización de un **proxy transparente**. Para ello debe existir una configuración física como la que muestra la imagen.

.. image:: img/proxytransparente.png
        :width: 400 px
        :alt: Reenvío de puertos en SO
        :align: center

Debemos configurar iptables para que TODO el trafico http(80) y https(443) sean redirigidos al puerto donde esté trabajando el proxy(por defecto squid trabaja en  el 3128)

echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -A FORWARD -j ACCEPT
iptables -t nat -A POSTROUTING -s 192.168.100.0/24 -o eth0 -j MASQUERADE
iptables -t nat -A PREROUTING -s 192.168.100.0/24 -p tcp --dport 80 -j REDIRECT --to-port 3128
iptables -t nat -A PREROUTING -s 192.168.100.0/24 -p tcp --dport 443 -j REDIRECT --to-port 3128
