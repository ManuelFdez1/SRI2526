Configuración del servicio
==============================

Configuración clientes
----------------------

Windows
^^^^^^^

        **GUI**

        El servicio cliente DNS debe estar en funcionamiento en el sistema(por defecto lo está). *Programas -> Herramientas Administrativas -> Servicios*

            .. image:: img/srvWinGui.png
                :width: 400 px
                :alt: NAS Diagram
                :align: center

        Las propiedades se realizan desde la configuración de las tarjetas de red, junto con el resto de parámetros de red.

            .. image:: img/propdnstarjeta.png
                :width: 300 px
                :alt: Conf. DNS windows GUI
                :align: center

        **Línea de comandos**

        En PowerShell, a través de los siguientes comandos:

        .. code-block:: shell-session

                    PS C:\> Set-DnsClientServerAddress -InterfaceIndex 12 -ServerAddresses ("10.0.0.1","10.0.0.2")
                    PS C:\> Get-DnsClientServerAddress


Linux
^^^^^^^

    **GUI**

    Los entornos gráficos (Gnome ,KDE....) proporcionan utilidades para la configuración de los clientes DNS en la configuración de las interfaces de red(muy parecido a Windows).

        .. image:: img/confdnsguilinux.png
            :width: 300 px
            :alt: conf. DNS Linux GUI
            :align: center

    **Línea de comandos**

    Si nuestra configuracion la realizamos sin GUI, debemos ubicar el fichero correspondiente, teniendo en cuenta que éste puede variar de una distro o version a otra.

    El fichero sobre el que trabajan la mayoria de las distribuciones es **/etc/resolv.conf(actualmente en muchos sistemas esto no es tan simple, y lo gestiona el demonio systemd)** que guarda las direcciones IP de los servidores DNS. En nuestras distros ya sabemos que esta configuración se realiza en el **fichero .yaml de netplan**.

                    .. code-block:: shell-session

                        nameservers:
                            addresses: [10.10.10.1, 1.1.1.1]


Configuración básica servidor
-----------------------------

Windows
^^^^^^^
    En este módulo no trataremos la instalación y configuración de controladores de dominio(AD), aunque **Active Directory necesita de DNS** para poder trabajar correctamente.

    **GUI**

    De manera visual a traves de la interfaz gráfica que ofrece Windows 20XX Server y la instalación de roles y características.

    Puedes encontrar un ejemplo de configuración paso a paso en el siguiente video:

    .. raw:: html

            <iframe width="250" style="display:block; margin-left:auto; margin-right:auto;"src="https://www.youtube.com/embed/B7I0dcHoxpg" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></br>

    .. raw:: html

        <p>
          <b>Línea de comandos </b><sup id="fnref:note1"><a class="footnote-ref" href="#fn:note1" role="doc-noteref">1</a></sup>
        </p>


    * Instalación. Podemos ejecutar el siguiente comando para buscar el nombre del rol que debemos instalar
                .. code-block:: shell-session

                  Get-WindowsFeature | where {($_.name -like “DNS”)}
                  #con el comando anterior averiguamos y ahora lo instalamos
                  Install-WindowsFeature DNS -IncludeManagementTools

    * Ponemos a escuchar al servidor únicamente por las interfaces que queramos(en nuestros escenarios en la tarjeta local):
                .. code-block:: shell-session

                  dnscmd /resetlistenaddresses 192.168.200.254

    * Configuramos los reenviadores(forwarders). Serán las direcciones IP a las que el servidor DNS reenvía las consultas DNS cuando no puede resolverlas de forma local.
                .. code-block:: shell-session

                  dnscmd /resetforwarders 8.8.8.8
    * Creación de una zona de búsqueda PRIMARIA y su correspondiente zona INVERSA
                .. code-block:: shell-session

                  PS C:\> Add-DnsServerPrimaryZone -ZoneName "asir.com" -ZoneFile "asir.com.dns" -verbose -passthru
                  PS C:\> Add-DnsServerPrimaryZone -NetworkId "192.168.200.0/24" -ZoneFile "200.168.192.in-addr.arpa.dns" -verbose -passthru

    * Creación de los **registros(RR)** que deseemos

      Podemos hacer uso de la instrucción `Add-DnsServerResourceRecord <https://docs.microsoft.com/en-us/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps#examples>`_  o del comando `DNSCmd/recordadd <https://docs.microsoft.com/es-es/windows-server/administration/windows-commands/dnscmd#dnscmd-recordadd-command>`_
                .. code-block:: shell-session

                  #añadir un NS (Servidor de nombres para zonas secundarias...)
                  Add-DnsServerResourceRecord -Name "asir.com" -NameServer "ns2.asir.com" -NS -ZoneName "asir.com"
                  #añadir un host(A) con su PTR para lo zona inversa correspondiente
                  Add-DnsServerResourceRecord -ZoneName "asir.com" -A -Name "www" -IPv4Address "192.168.200.5"
                  Add-DnsServerResourceRecordPtr -Name "5" -ZoneName "200.168.192.in-addr.arpa" -PtrDomainName "www.asir.com"
                  #añadir un alias(CNAME)
                  Add-DnsServerResourceRecord -CName -Name "www2" -HostNameAlias "www.asir.com" -ZoneName "asir.com" -AllowUpdateAny
                  #añadir un servidor de correo(MX) para mi dominio con una preferencia de 10. Debo añadir un registro tipo A para que me traduzca nombre por IP.
                  Add-DnsServerResourceRecord -ZoneName "asir.com" -A -Name "mail" -IPv4Address "192.168.200.6"
                  Add-DnsServerResourceRecord -Name "." -MX -ZoneName "asir.com" -MailExchange "mail.asir.com" -Preference 10

    * Exportar/Importar configuración de zona/s del DNS server a fichero/s de texto.
                .. code-block:: shell-session

                  #guarda los ficheros en C:\Windows\System32\dns
                  #también guardo la zona inversa
                  dnscmd /zoneexport "asir.com" "asir.com.cseg" #también con Export-dnsservervzone se podría hacer
                  dnscmd /zoneexport "asir.com" "asir.com.cseg"
                  #para importar, renombro los ficheros anteriores a acabados en .dns (sustituyendo el .cseg)
                  #deben estar ubicados en C:\Windows\System32\dns
                  dnscmd /zoneadd "asir.com" /primary /file "asir.com.dns" /load
                  dnscmd /zoneadd "200.168.192.in-addr.arpa" /primary /file "200.168.192.in-addr.arpa.dns" /load

Linux
^^^^^^^

    BIND o DnsMasq son los paquetes utilizados en todas las distribuciones Linux, sin interfaz gráfica añadida. Su administración configuración se realiza accediendo a varios ficheros de texto (INCLUIDO EL FICHERO DE ZONA).

    .. raw:: html

        <p>
          En nuestro caso vamos a optar con configurar el servidor <b>BIND</b><sup id="fnref:note2"><a class="footnote-ref" href="#fn:note2" role="doc-noteref">2</a></sup>. Podemos encontrar alternativas gráficas para poder configurar BIND, a través de la instalación de un panel de administración, como Webmin:
        </p>

    .. image:: img/dnswebmin.png
            :width: 400 px
            :alt: Pantalla webmin administración BIND
            :align: center

    Debemos entender la estructura de ficheros que monta BIND una vez instalado, para poder realizar correctamente su configuración:

    .. image:: img/ficherosbind.png
            :width: 200 px
            :alt: Ficheros instalador por BIND
            :align: center

    La configuración de **BIND se encuentra en named.conf**, la cual se distribuye con el **uso de la directiva include**, entre los ficheros:
        * **named.conf.options**: Parámetros a nivel global del servidor DNS.
        * **named.conf.local**: Aquí se crean las zonas con la instrucción zone. Uno de los parámetros será la ubicación y nombre del **fichero de zona**.
        * named.conf.default-zones: Algunas zonas que incluye BIND por defecto.
        * db.*: ficheros de zona creadas en named.conf.default-zones. db.root=srv. Raiz.
        * db.empty: plantilla de fichero de zona.

    Se crea un usuario bind que pertenece al grupo principal bind que también se crea. Este usuario es el que ejecuta el demonio /usr/sbin/named, al que se le pasan los argumentos especificados en **/etc/default/bind9**.
    **En /var/cache/bind, referencia para todas las rutas relativas (instrucción directory en el fichero de options), es donde crearemos nuestros ficheros de zona por defecto**.

    Podemos gestiónar el servicio con los siguiente comandos (podemos elegir entre las dos opciones):

                .. code-block:: shell-session

                  $sudo service bind9 [restart|start|stop|status]
                  $sudo systemctl [restart|start|stop|status] bind9

    En el siguiente video encontrarás un ejemplo de configuración muy sencillo:

    .. raw:: html

            <iframe width="250" style="display:block; margin-left:auto; margin-right:auto;"src="https://www.youtube.com/embed/cNr5aLz40fI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></br>


.. raw:: html

    <div style="text-align: justify; color: BLUE; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
    <u>¿Sabrías?</u></br>
    Realizar la instalación de un servidor DNS MAESTRO que únicamente atienda peticiones en la tarjeta local en cada uno de los tres SSOO que has virtualizado anteriormente
    </div></br>


Ampliando nuestra configuración
--------------------------------

A partir de aquí podemos trabajar sobre escenarios más complejos en los que podremos incluir:

* Servidores maestros
* Servidores esclavos
* Delegaciones de zona

          .. raw:: html

              <p style="text-align: justify;"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/42/Pdf-2127829.png/480px-Pdf-2127829.png" alt="Perfil" width="50" style="vertical-align: middle; float:left;"/>  En el siguiente documento puedes encontrar un manual completo de como realizar esto tanto en Windows como en Linux. </br> </br>

          .. image:: img/Practicas_DNS.pdf
              :width: 400 px
              :alt: Tutorial configuración servidores DNS
              :align: center

    .. raw:: html

        </br>
        <div style="text-align: justify; color: orange; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
        <u><b>PRÁCTICA 1</b></u></br>
        Realiza la práctica 1 del Tema 3 del aula virtual, vas a crear tu sistema de servidores DNS.
        </div>


Juntando todo(DDNS)
-------------------

.. raw:: html

        <p>
          El <b>DNS dinámico(Dynamic DNS)</b> es un servicio que puede ser de gran utilidad en la mayoría de ocasiones en aplicaciones reales. 
          El DNS dinámico garantiza que los usuarios puedan seguir accediendo al dispositivo o servicio mediante el nombre de dominio. No necesitan rastrear ni actualizar la dirección IP manualmente.<sup id="fnref:note3"><a class="footnote-ref" href="#fn:note3" role="doc-noteref">3</a></sup>. 
        </p>



.. image:: img/DDNS.png
    :width: 900 px
    :alt: conf. DNS Linux GUI
    :align: center


**¿Se te pueden ocurrir situaciones en lo que esto sea de utilidad?¿Qué ventajas podría tener?**

Puedes encontrar multitud de recursos en la web para poder orientarte en la configuración de esta característica para nuestros servidores DNS. Por ejemplo puedes 
`acceder al siguiente enlace <https://medium.com/marcsanchezg/instalar-y-configurar-un-servidor-ddns-dhcp-dns-790cbc34e53d>`_ y realizar las tareas correspondientes en tu
servidor.

    
.. raw:: html

   </br>
   <div class="footnotes">
       <hr />
       <ol>
           <li class="footnote" id="fn:note1">
               <p>
                   <b>Fuente:</b> Podemos optar por utilizar el <a href="https://docs.microsoft.com/en-us/powershell/module/dnsserver/?view=win10-ps" target="_blank">Módulo DnsServer PowerShell</a> o aprovoechar la sencillez del
                   <a href="https://docs.microsoft.com/es-es/windows-server/administration/windows-commands/dnscmd" target="_blank">Comando DNSCMD</a>
                   <a class="footnote-backref" rev="footnote" href="#fnref:note1">&#8617;</a>
               </p>
           </li>
           <li class="footnote" id="fn:note2">
               <p>
                   <b>Ayuda:</b> Puedes encontrar un manual muy completo sobre DNS y BIND <a href="https://www.fpgenred.es/DNS/instalacin_de_bind_versin_9.html" target="_blank">el siguiente enlace</a><a class="footnote-backref" rev="footnote" href="#fnref:note2">&#8617;</a>
               </p>
           </li>
           <li class="footnote" id="fn:note3">
               <p>
                   <b>Fuente:</b> Puedes encontrar una explicación muy buena en la <a href="https://aws.amazon.com/es/what-is/dynamic-dns/" target="_blank">documentación de AWS sobre DDNS</a><a class="footnote-backref" rev="footnote" href="#fnref:note3">&#8617;</a>
               </p>
           </li>
       </ol>
   </div>
