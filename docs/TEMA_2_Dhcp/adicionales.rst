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

      <span style="text-align:center;">
      <a title="Rel" href="https://bytelearning.blogspot.com/2016/08/como-crear-un-dhcp-relay-en-linux.html"><img width="512" alt="DHCP Relay" src="https://4.bp.blogspot.com/-rA3kiCPJBMk/V578DoqT5rI/AAAAAAAAGXc/sXiD6rSCUzIgyfzppzpTf7KfcGNhGu98gCLcB/s1600/Diagrama.png"></a>
      </span>

DHCP Failover
--------------

DHCP es un servicio crítico, en caso de fallo nuestra red estaría inoperativa para la mayoría de usari@s y dispositivos. En el caso de GRANDES organizaciones podría interesar tener algún método de redundancia, el cual posibilite la distribución de la carga, y la disponibilidad del servicio en caso de fallo. El protocolo DHCP FAILOVER **permite la sincronización de dos servidores DHCP, gestionando el mismo ámbito**.

    .. image:: img/dhcpFailover.png
              :width: 600 px
              :alt: Esquema DHCP Failover
              :align: center

Puedes encontrar ayuda, en el siguiente video elaborado por una alumno de Ciclos Formativos:

.. raw:: html

        <iframe width="250" style="display:block; margin-left:auto; margin-right:auto;"src="https://www.youtube.com/embed/RmYv8ssRL7E" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></br>


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
