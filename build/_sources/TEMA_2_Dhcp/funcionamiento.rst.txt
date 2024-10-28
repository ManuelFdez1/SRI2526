Funcionamiento del protocolo
=============================

DHCP (Dynamic Host Configuration Protocol) es un protocolo de red Cliente/Servidor que permite a los clientes de una red IP obtener sus parámetros de configuración automáticamente.
El intercambio de paquetes que se produce es el siguiente (con un programas como **Wireshark** podrías capturarlo y analizarlo):

.. image:: img/protocoloDHCP.png
   :width: 400 px
   :alt: Funcionamiento protcolo DHCP
   :align: center

**VENTAJAS**
  * Facilita el mantenimiento de la red.
  * Inclusión de nuevos equipos con facilidad.
  * Cambios en la red simples.

**INCONVENIENTES**
  * Falta de seguridad en el acceso a la red.
  * Servicio candidato a ataques.
  * Saturación de la red (muchos paquetes de **difusión/broadcast**).

En el siguiente video puedes ver una explicación visual y muy práctica del funcionamiento de este protocolo:

.. raw:: html

      <iframe width="280" height="157" style="display:block; margin-left:auto; margin-right:auto;" src="https://www.youtube.com/embed/S43CFcpOZSI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></br>


Parámetros de configuración
=============================

Además de proporcionar una dirección IP, el servicio DHCP puede asignar valores a los siguientes parámetros de red (**tanto para IPv4 como para IPv6**):

  1. Dirección IP
  2. Máscara de subred
  3. Dirección del servidor/es DNS
  4. Dir. IP Puerta de enlace.
  5. Broadcast address
  6. Más parámetros en el `siguiente enlace <https://www.iana.org/assignments/bootp-dhcp-parameters/bootp-dhcp-parameters.xhtml>`_.

.. raw:: html

    <div style="text-align: center; color: BLUE; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
    Los parámetros de configuración de las interfaces de red del servidor DHCP han de ser coherentes con la configuración del servicio (en concreto con los ÁMBITOS que se creen), en caso contrario ni siquiera podemos iniciar su funcionamiento.
    </div></br>
