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

.. important::
   Para que funcione bien el enrutamiento, recuerda repasar tus servidors DHCP y DNS, comprobando que todo esté correctamente configurado.


Finalmente, sería conveniente configurar todo lo anterior de manera que el servicio se iniciara con el arranque del SO para evitar tener que reconfigurar en caso de reinicio del servidor.
Puedes encontrar un HOW-TO en el `siguiente tutorial web <https://smr.iesharia.org/wiki/doku.php/src:recetas:enrutamiento>`_


      .. code-block:: shell-session

                  1. net.ipv4.ip_forward=1net.ipv4.ip_forward=1
                  #!/bin/bash
                  2.- iptables -A FORWARD -j ACCEPT
                  3. iptables -t nat -A POSTROUTING -s 192.168.100.0/24 -o eth0 -j MASQUERADE


.. warning::
   En relación con las lineas anteriores:

   1. Poniendo ese bit de sistema a 1 **activas únicamente el enrutamiento** entre tarjetas
   2. Iptables acepta paquetes FORWARD (aquellos que llegan al servidor con destino a otras redes). Esta linea es opcional.
   3. Configuras iptables para que envíe los paquetes de la red local(*192.168.200.0/24*) a la tarjeta externa(*enp0s3*) realizando la traducción correspondiente (usamos la palabra MASQUERADE, aunque puede usarse SNAT también. En la `siguiente web te explican las diferencias entre una y otra <https://terrywang.net/2016/02/02/new-iptables-gotchas.html>`_ ).

Si lo prefieres, también puedes ver como se realiza esto en multitud de videotutoriales.

.. raw:: html

            <iframe width="250" style="display:block; margin-left:auto; margin-right:auto;"src="https://www.youtube.com/embed/HeUyUDV697E" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></br>

.. raw:: html

        </br>
        <div style="text-align: justify; color: orange; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
        <u><b>PRÁCTICA 1</b></u></br>
        Realiza la práctica 1 del Tema 4 del aula virtual, convirtiendo tus servidores en enrutadores.
        </div>
        </br>
