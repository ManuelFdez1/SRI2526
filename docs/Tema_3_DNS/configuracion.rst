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

El fichero sobre el que trabajan la mayoria de las distribuciones es /etc/resolv.conf(actualmente en muchos sistemas esto no es tan simple, y lo gestiona el demonio systemd) que guarda las direcciones IP de los servidores DNS. En nuestras distros ya sabemos que esta configuración se realiza en el fichero .yaml de netplan

                .. code-block:: shell-session

                    nameservers:
                        addresses: [10.10.10.1, 1.1.1.1]


Configuración servidor
----------------------

Windows
^^^^^^^

**GUI**

De manera visual a traves de la interfaz gráfica que ofrece Windows 2012/2016/2019 Server y la instalación de roles y características.

Puedes encontrar un ejemplo de configuración paso a paso en el siguiente video:

.. raw:: html

        <iframe width="250" style="display:block; margin-left:auto; margin-right:auto;"src="https://www.youtube.com/embed/5AMMCAcw3js" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></br>

        <div style="text-align: justify; color: orange; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
        <b>PRÁCTICA 1</b></br></br>
        Accede al aula virtual del módulo y completa la primera práctica del Tema2. Envía un <b>documento pdf</b> con los pantallazos y características de los equipos, aportando las explicaciones que consideres oportunas.
        </div>
        </br>

.. raw:: html

    <p>
      <b>Línea de comandos </b><sup id="fnref:note2"><a class="footnote-ref" href="#fn:note2" role="doc-noteref">2</a></sup>
    </p>


* Instalación
            .. code-block:: shell-session

              Install-WindowsFeature DHCP -IncludeManagementTools
* Configuración de un ámbito y sus opciones. Un ejemplo podría ser:
            .. code-block:: shell-session

              Add-DhcpServerv4Scope -name "RedAula2" -StartRange 192.168.200.11 -EndRange 192.168.200.254 -SubnetMask 255.255.255.0 -State Active
              Set-DhcpServerv4OptionValue  -ComputerName win-ts9g7n11dbe -ScopeId 192.168.100.0 -DnsServer 192.168.100.254 -Router 192.168.100.254 -Force

* Exportar/Importar configuración DHCP server a fichero de texto.
            .. code-block:: shell-session

              PS C:\> Export-DhcpServer -ComputerName "dhcpserver.contoso.com" -File "C:\exportdir\dhcpexport.xml" [-ScopeId 10.10.10.0,10.20.20.0]
              PS C:\> Import-DhcpServer -ComputerName "dhcpserver.contoso.com" -File "C:\exports\dhcpexport.xml" -BackupPath "C:\dhcpbackup\" [-ScopeId 10.10.10.0,10.20.20.0]

.. raw:: html

        <div style="text-align: justify; color: orange; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
        <b>PRÁCTICA 2</b></br></br>
        Accede al aula virtual del módulo y completa la segunda práctica del Tema2, en la que crearás el ámbito DHCP con PowerShell. Envía <b>la secuencia de comandos de PowerShell</b> que has utilizado para solucionar la práctica.
        </div>
        </br>


Linux
^^^^^^^

Se suele configurar directamente con el fichero de configuración correspondiente, pero existen programas denominados **paneles** que nos permiten configurar los servidores a través de un **entorno web** (uno de los muchos ejemplos que existen puede ser `Webmin <https://www.webmin.com/>`_ ).

En Ubuntu srv 18.04/20.04 el servidor que viene en sus repositorios es **isc-dchp-server**, en el que destacan 2 Ficheros de configuración a tener en cuenta:

  1. **/etc/default/isc-dhcp-server** → Interfaces donde trabaja el srv dhcp
  2. **/etc/dhcp/dhcpd.conf** → Configuración y def. De ámbitos

Un ejemplo sencillo de configuración de un ámbito (**subnet en el fichero dhcpd.conf**) podría ser:

    .. image:: img/ejemploConfUbuntu.png
        :width: 400 px
        :alt: NAS Diagram
        :align: center

Además de gestiónar el servicio con los siguiente comandos (podemos elegir entre las dos opciones):


            .. code-block:: shell-session

              $sudo service isc-dhcp-server [restart|start|stop|status]
              $sudo systemctl [restart|start|stop|status] isc-dhcp-server.service

Puedes encontrar un ejemplo de configuración paso a paso en el siguiente video:

.. raw:: html

        <iframe width="250" style="display:block; margin-left:auto; margin-right:auto;"src="https://www.youtube.com/embed/eWwasdFtIzM" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></br>
        <div style="text-align: justify; color: orange; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
        <b>PRÁCTICA 3</b></br></br>
        Accede al aula virtual del módulo y completa la tercera práctica del Tema2, configurando un srv DHCP en Ubuntu. Envía <b>el fichero /etc/dhcpd/dhpd.conf</b> como solución a la práctica.
        </div>
        </br>

.. raw:: html

    <div style="text-align: justify; color: BLUE; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
    <u>¿Sabrías?</u></br>
    En todos los servidores DHCP tenemos la opción de incluir <b>RESERVAS</b>, las cuales son muy útiles para configurar equipos especiales de nuestra red, tales como:
    <ul>
      <li>Impresoras</li>
      <li>Servidores</li>
      <li>...........</li>
    </ul>
    ¿Podrías configurar alguna reserva en tus servidores DHCP?
    </div></br>


.. raw:: html

   </br>
   <div class="footnotes">
       <hr />
       <ol>
           <li class="footnote" id="fn:note1">
               <p>
                   <b>Inst. y configuración servidor DHCP Windows(GUI):</b> <a href="https://social.technet.microsoft.com/wiki/contents/articles/51170.microsoft-windows-server-2016-dhcp-server-installation-configuration.aspx" target="_blank">Doc. oficial de Microsoft</a> <a class="footnote-backref" rev="footnote" href="#fnref:note1">&#8617;</a>
               </p>
           </li>
           <li class="footnote" id="fn:note2">
               <p>
                   <b>Inst. y configuración servidor DHCP Windows(PowerShell):</b> <a href="https://docs.microsoft.com/en-us/windows-server/networking/technologies/dhcp/dhcp-deploy-wps" target="_blank">Doc. oficial de Microsoft</a> / <b>comandos DHCP PowerShell:</b> <a href="https://docs.microsoft.com/en-us/powershell/module/dhcpserver/?view=win10-ps" target="_blank">Doc. oficial de Microsoft</a> <a class="footnote-backref" rev="footnote" href="#fnref:note2">&#8617;</a>
               </p>
           </li>
       </ol>
   </div>
