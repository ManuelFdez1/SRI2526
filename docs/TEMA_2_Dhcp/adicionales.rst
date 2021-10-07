Configuraciones adicionales
=============================

En determinadas situaciones (empresas más grandes, con mayores requisitos de funcionamiento...) la funcionalidad de DHCP puede ampliarse con dos configuraciones muy interesantes:

  1. DHCP Relay
  2. DHCP Failover

DHCP Relay
-----------

.. raw:: html

    <p>
    Esta configuración consiste básicamente en la puesta en marcha de un <b>AGENTE</b> que básicamente lo que permite es actuar como un intermediario(proxy) del servicio DHCP, recibiendo peticiones al levantar máquinas, y delegando a un servidor DHCP real la tarea de asignar la configuración IP de los clientes de distintas redes, en un esquema similar a la siguiente imagen <sup id="fnref:note1"><a class="footnote-ref" href="#fn:note1" role="doc-noteref">1</a></sup>:
    </p>


.. raw:: html

      <div style="text-align:center;">
      <a title="Rel" href="https://bytelearning.blogspot.com/2016/08/como-crear-un-dhcp-relay-en-linux.html"><img width="512" alt="DHCP Relay" src="https://4.bp.blogspot.com/-rA3kiCPJBMk/V578DoqT5rI/AAAAAAAAGXc/sXiD6rSCUzIgyfzppzpTf7KfcGNhGu98gCLcB/s1600/Diagrama.png"></a>
      </div>


En el siguiente documento puedes encontrar, paso a paso, como montar un agente DHCP Relay en Ubuntu. Debes tener en cuenta varias cosas:

* Necesitarás varias MV en marcha (hasta 3)
* Deberás realizar alguna modificación en la configuración de red (en concreto la **creación de rutas**)
* Aunque el documento hable de Ubuntu Server puedes utilizar otras distribuciones, no será muy diferente a lo expuesto en él.
* Puedes combinar MV Windows/Linux según tus necesidades para que actúen tanto como servidor DHCP o como Relay.

          .. raw:: html

              <p style="text-align: justify;"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/42/Pdf-2127829.png/480px-Pdf-2127829.png" alt="Perfil" width="50" style="vertical-align: middle; float:left;"/>  En el siguiente documento puedes encontrar un manual completo de como realizar esto tanto en Windows como en Linux. </br> </br>

          .. image:: img/Practica_Dhcp_RELAY_UbuntuServer.pdf
              :width: 400 px
              :alt: Tutorial configuración DHCP Relay Linux
              :align: center

DHCP Failover
--------------

DHCP es un servicio crítico, en caso de fallo nuestra red estaría inoperativa para la mayoría de usari@s y dispositivos. En el caso de GRANDES organizaciones podría interesar tener algún método de redundancia, el cual posibilite la distribución de la carga, y la disponibilidad del servicio en caso de fallo. El protocolo DHCP FAILOVER **permite la sincronización de dos servidores DHCP, gestionando el mismo ámbito**.

    .. image:: img/dhcpFailover.png
              :width: 600 px
              :alt: Esquema DHCP Failover
              :align: center

En el siguiente enlace https://www.fpgenred.es/DHCP/protocolo_dhcp_failover.html puedes encontrar una completa referencia a los parámetros que pueden incluirse, además de un ejemplo de configuración completo en Linux. también
te puede servir de ayuda el siguiente video elaborado por un alumno de Ciclos Formativos:

.. raw:: html

        <iframe width="250" style="display:block; margin-left:auto; margin-right:auto;"src="https://www.youtube.com/embed/RmYv8ssRL7E" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></br>


El protoco DHCP FAILOVER puedes encontrarlo en cualquiera de los sistemas operativos actuales. Si hasta ahora unicámente nos hemos referido a Linux(Ubuntu), su configuración no es muy distinta en Windows.

  * Windws SRV con GUI: `Blog con tutorial paso a paso <https://www.solvetic.com/tutoriales/article/3364-como-configurar-dhcp-failover-en-windows-server-2016//>`_
  * PowerShell: `Doc. oficial de Microsoft <https://docs.microsoft.com/en-us/powershell/module/dhcpserver/add-dhcpserverv4failover?view=windowsserver2019-ps/>`_


.. raw:: html

        <div style="text-align: justify; color: orange; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
        <b>PRÁCTICA 4</b></br></br>
        Accede al aula virtual del módulo y completa la última práctica del tema. Vas a montar un sistema de alta disponibilidad sobre el servicio DHCP.
        </div>
        </br>


.. raw:: html

   <div class="footnotes">
       <hr />
       <ol>
           <li class="footnote" id="fn:note1">
               <p>
                   <b>Fuente:</b> <a href="https://bytelearning.blogspot.com/2016/08/como-crear-un-dhcp-relay-en-linux.html" target="_blank">Cómo crear un DHCP relay en Linux </a> <a class="footnote-backref" rev="footnote" href="#fnref:note1">&#8617;</a>
               </p>
           </li>
       </ol>
   </div>
