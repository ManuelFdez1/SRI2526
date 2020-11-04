Acceso redes remotas
==============================

Vamos a configurar el enrutamiento HACIA EL EXTERIOR DE NUESTRA LAN, tanto en nuestra MV Windows Srv como en la distribución Linux que estemos utilizando, de manera que el tráfico que le llegue por la tarjeta interna con destino fuera de la red, lo reenvie por su tarjeta externa, realizando además las funciones de NAT.
Para activar el tráfico HACIA NUESTRA RED, si estamos configurando un PC como router debemos tener en cuenta si estamos ejecutando un cortafuegos. Si estamos configurando un router real debemos activar el reenvio (FORWARDING)  de puertos con las utilidades que incorpora el SW del dispositivo.

Windows
--------

**GUI**

Es un servicio muy sencillo de instalar a través de la función (ROLE) **ACCESO REMOTO(Remote Access)** y sus servicios correspondientes **ENRUTAMIENTO (Routing)**, puedes añadir los otros servicios de rol para dar acceso por VPN o configurar un proxy web. Puedes encontrar un buen ejemplo en el `siguiente tutorial <https://blogs.itpro.es/readyplayerone/2015/10/03/servicios-de-enrutamiento-en-windows-server-2016/>`_ .

.. raw:: html

    <div style="text-align:center;">
    <a href="https://i1.wp.com/blogs.itpro.es/readyplayerone/files/2015/10/07.png" target="_blank"><img width="800" alt="Lanwan" src="https://i1.wp.com/blogs.itpro.es/readyplayerone/files/2015/10/07.png"></a>
    </div></br>

**PowerShell**

Con dos sencillos comandos tendríamos navegando por Internet a nuestros clientes:

      .. code-block:: shell-session

                    Install-WindowsFeature  -Name Routing
                    Get-NetAdapter | Set-NetIPInterface -Forwarding Enabled
                    New-NetNat -Name LOCAL -InternalIPInterfaceAddressPrefix 192.168.100.0/24

      .. warning::
             **192.168.100.0/24** es el id de la red local


Linux
--------
En las distribuciones Linux no necesitamos instalar ningún servicio para conseguir el enrutamiento y la NAT, ya que con las utilidades que incorpora el núcleo del SO podremos conseguir lo que pretendemos. Para ello haremos uso de las `IPTABLES <https://es.wikipedia.org/wiki/Netfilter/>`_.

          .. raw:: html

              <p style="text-align: justify;"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/42/Pdf-2127829.png/480px-Pdf-2127829.png" alt="Perfil" width="50" style="vertical-align: middle; float:left;"/>  En el siguiente documento puedes encontrar un manual completo. </br> </br>

          .. image:: img/doc-iptables-firewall.pdf
              :width: 400 px
              :alt: Tutorial IpTables
              :align: center


Debemos incluir los comandos necesarios para:

* Enrutar los paquetes que vengan de nuestra red local a nuestra tarjeta interna.
* De estos paquetes identificar cuales tienen como destino otra red.
* Reenviarlos por la tarjeta externa del servidor.
* Realizar la NAT para que se puedan comunicar con la red destino.

Finalmente, sería conveniente configurar todo lo anterior de manera que el servicio se iniciara con el arranque del SO para evitar tener que reconfigurar en caso de reinicio del servidor.
Puedes encontrar mucha `ayuda en tutoriales en la web <https://smr.iesharia.org/wiki/doku.php/src:recetas:enrutamiento>`_


      .. code-block:: shell-session

                  net.ipv4.ip_forward=1net.ipv4.ip_forward=1
                  #!/bin/bash
                  iptables -A FORWARD -j ACCEPT
                  iptables -t nat -A POSTROUTING -s 192.168.100.0/24 -o eth0 -j MASQUERADE


.. warning::
   Recuerda que para ello tendrás que realizar tareas relacionadas con:

   * Scripting en Linux
   * Permisos de ejecución
   * Sistema de arranque de Linux. Servicios propios.
