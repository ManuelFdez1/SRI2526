Configuración del servicio
=============================

Vamos aprender a configurar tanto los clientes (las interfaces de red que solicitan una configuración dinámica) como los servidores. En ambos casos trabajaremos con sistemas operativos Windows y Linux, con GUI y sin ella.

Configuración clientes
----------------------

Windows
^^^^^^^

**GUI**

En las propiedades de la interfaz (tarjeta) de red correspondiente:

    .. image:: img/confClienteWindowsGui.png
        :width: 400 px
        :alt: NAS Diagram
        :align: center

**Línea de comandos**

En PowerShell, a través del comando `Set-NetIPInterface <https://docs.microsoft.com/en-us/powershell/module/nettcpip/set-netipinterface?view=win10-ps>`_ (debemos asegurarnos de borrar las posibles direcciones estáticas que se hayan asignado a la interfaz)

.. code-block:: shell-session

              PS C:\>Set-NetIPInterface -InterfaceIndex 5 -Dhcp Enabled

Linux
^^^^^^^
`Netplan <https://netplan.io/>`_ es el sistema de gestión de la red, sustituyendo al antiguo gestor. Puede trabajar de dos maneras (renderers):
  * **NetworkManager (GUI)**
  * **Systemd-networkd (CLI)**

**GUI**

Debemos asociar las tarjetas al gestor gráfico (**en netplan, renderer: NetworkManager**). Desde ese momento ya tenemos la gestión gráfica. Para desactivarla hay que parar el servicio network-manager.

La imagen siguiente es orientativa, la interfaz cambiará en función de la distro de Linux y de la versión de la misma.

    .. image:: img/confLinuxGUI.png
        :width: 400 px
        :alt: NAS Diagram
        :align: center

.. raw:: html

    <div style="text-align: center; color: BLUE; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
    Se debe optar por una de los dos modos de configuración(interfaz gráfica / ficheros de configuración)
    </div></br>


**Línea de comandos**

Para la configuración (a través del fichero yaml ubicado en **/etc/netplan**) de las tarjetas, puedes `encontrar en la web <https://netplan.io/examples/>`_ muchos ejemplos de ello.
Para la consulta, el up/down y  la actualización de las tarjetas tenemos comandos como:


        * Recargar la configuración (después de una modificación en el fichero netplan)
            .. code-block:: shell-session

              $sudo netplan apply
        * Volver a solicitar la concesión de configuración al srv. DHCP
            .. code-block:: shell-session

              $sudo dhclient
        * Comprobar las direcciones de las interfaces
            .. code-block:: shell-session

              $ip a
        * Comprobar la dirección de una interfaz en concreto.
            .. code-block:: shell-session

              $ip a show eth0
              $ip a list eth0
              $ip a show dev eth0
        * Mostrar únicamente interfaces en funcionamiento
            .. code-block:: shell-session

              $ip link ls up
        * Cambiar el estado de una interfaz (a veces nos ayudará a actualizar la configuración tras modificaciones en el fichero netplan)
            .. code-block:: shell-session

              #ip link set dev {DEVICE} {up|down}


.. image:: img/confminimanetplan.png
        :width: 200 px
        :alt: NAS Diagram
        :align: center


Configuración servidor
----------------------

Windows
^^^^^^^

.. raw:: html

    <p>
      <b>GUI </b><sup id="fnref:note1"><a class="footnote-ref" href="#fn:note1" role="doc-noteref">1</a></sup>
    </p>

De manera visual a traves de la interfaz gráfica que ofrece Windows 2012/2016 Server y la instalación de roles y características.
    .. image:: img/confSrvWindowsGui.png
        :width: 400 px
        :alt: NAS Diagram
        :align: center

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

              Add-DhcpServerv4Scope -name "RedAula2" -StartRange 10.0.0.1 -EndRange 10.0.0.254 -SubnetMask 255.255.255.0 -State Active
              Add-DhcpServerv4ExclusionRange -ScopeID 10.0.0.0 -StartRange 10.0.0.1 -EndRange 10.0.0.15
              Set-DhcpServerv4OptionValue -OptionID 3 -Value 10.0.0.1 -ScopeID 10.0.0.0 -ComputerName DHCP1.corp.contoso.com
              Set-DhcpServerv4OptionValue -DnsDomain corp.contoso.com -DnsServer 10.0.0.2

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
