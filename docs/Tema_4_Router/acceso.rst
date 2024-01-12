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
En las distribuciones Linux no necesitamos instalar ningún servicio para conseguir el enrutamiento y la NAT, ya que con las utilidades que incorpora el núcleo del SO podremos conseguir lo que pretendemos.
Tenemos varias opciones para crear rutas:

* Con el uso del comando **ip route** (https://www.cyberciti.biz/faq/linux-route-add/)
* Inclyendo **rutas estáticas en nuestro fichero de netplan** de configuración de red (https://linuxconfig.org/how-to-add-static-route-with-netplan-on-ubuntu-20-04-focal-fossa-linux) 
* A través de **NETFILTER**  (https://es.wikipedia.org/wiki/Netfilter) que es el  framework disponible en el núcleo de Linux que permite interceptar y manipular paquetes de red. Dicho framework permite interactuar con paquetes en diferentes etapas del procesamiento dentro del sistema operativo, ofreciendo funcionalidades de cortafuegos y otras utilidades relacionadas. Los componentes más populares son:
   - Las clásicas **IPTABLES** (http://es.tldp.org/Manuales-LuCAS/doc-iptables-firewall/doc-iptables-firewall.pdf).
   - Sustituidas por las más modernas (y probablemente sencillas) **NFTABLES** (https://www.josedomingo.org/pledin/2020/01/nftables-cortafuegos-perimetral-nat/). 


Debemos incluir los comandos necesarios para:

* Enrutar los paquetes que vengan de nuestra red local a nuestra tarjeta interna. Activando el ip_forward entre tarjetas.
* De estos paquetes identificar cuales tienen como destino otra red.
* Reenviarlos por la tarjeta externa del servidor.
* Realizar la NAT para que se puedan comunicar con la red destino.

.. important::
   Para que funcione bien el enrutamiento, recuerda repasar tus servidors DHCP y DNS, comprobando que todo esté correctamente configurado.




.. raw:: html

        </br>
        <div style="text-align: justify; color: orange; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
        <u><b>PRÁCTICA 1</b></u></br>
        Realiza la práctica 1 del Tema 4 del aula virtual, convirtiendo tus servidores en enrutadores.
        </div>
        </br>
