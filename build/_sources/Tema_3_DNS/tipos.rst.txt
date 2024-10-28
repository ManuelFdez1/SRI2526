Tipos de servidores, resoluciones y búsquedas
==============================================

En todo lo relacionado con DNS podemos encontrar diferentes clasificaciones que deben aclararse para poder trabajar correctamente con el servicio.

Tipos de servidores
--------------------

    .. raw:: html

        <p>
        En cuanto al <b>modo de funcionamiento</b> de un servicio DNS, podemos clasificarlos en los siguientes tipos:<sup id="fnref:note1"><a class="footnote-ref" href="#fn:note1" role="doc-noteref">1</a></sup>:
        </p>

    1. **Servidor primario (maestro)**: en él se llevan a cabo todas las modificaciones sobre una o varias zonas. Almacena la **copia original de la BD de la zona** y se le denomina **autorizado**.
    2. **Servidor secundario (esclavo)**: contiene una **copia de solo lectura de los archivos de zona** que obtiene del servidor maestro (**transferencia** de zona), también es **autorizado**.

          .. image:: img/srvslave.png
                  :width: 400 px
                  :alt: Servidor esclavo DNS
                  :align: center
    3. **Servidor caché**: No contiene información acerca de la zona y se utiliza para acelerar las consultas, almacenando las últimas realizadas.

          .. image:: img/srvcache.png
                  :width: 400 px
                  :alt: Servidor cache DNS
                  :align: center
    4. **Servidor reenviador (forwarder)**: Cuando un servidor DNS no tiene la respuesta a una consulta, puede acudir a este tipo de servidores que se utilizan para reducir el tráfico y las consultas DNS, ya que resuelven completamente la consulta y se comparte su caché.
    5. **Servidor solo autorizado**: Se trata de servidores que están autorizado en una o varias zonas, como primario o secundario, pero no preguntan a otros servidores para resolver la petición.
    6. **Servidores raíz (root servers)**: En Internet existen un conjunto de servidores DNS autorizados para el dominio raíz «.», conocidos como servidores raíz (root servers). Contienen el fichero de la zona «.» que contiene información sobre los servidores DNS autorizados para cada uno de los dominios TLD.

          .. image:: img/rootservers.png
                  :width: 400 px
                  :alt: Servidor cache DNS
                  :align: center


Tipos de resoluciones
----------------------

    1. resolución **RECURSIVA**: El servidor local se encargará de dar una respuesta COMPLETA al cliente y consultará a los servidores DNS intermedios que necesite en su nombre.

          .. image:: img/recursiva.png
                  :width: 400 px
                  :alt: Servidor cache DNS
                  :align: center
    2. resolución **ITERATIVA**: El servidor DNS local devuelve la mejor respuesta que puede ofrecer al cliente. Si no dispone de la información solicitada, indicará la IP del siguiente servidor de nombres autorizado

          .. image:: img/iterativa.png
                  :width: 400 px
                  :alt: Servidor cache DNS
                  :align: center

Tipos de búsquedas
--------------------

Según el tipo búsqueda que se realice sobre nuestro/s servidor/es, tenemos:


    1. **BÚSQUEDA DIRECTA**: En la **mayor parte de las búsquedas DNS**, los clientes normalmente realizan una búsqueda directa, que es la que se basa en el nombre DNS de otro equipo según se almacenó en un registro de recursos de dirección (A). Este tipo de consulta espera una dirección IP como datos de recurso para la respuesta a la consulta.
    2. **BÚSQUEDA INVERSA**: DNS proporciona un proceso de búsqueda inversa, que permite a los clientes utilizar una dirección IP conocida durante la búsqueda de un nombre y busca un nombre de equipo en función de su dirección.

      Tiene forma de pregunta, como *"¿Puede decirme el nombre DNS del equipo que utiliza la dirección IP 192.168.1.20?"*. De la misma forma que los nombres de dominio se resuelven efectuando consultas para cada componente de derecha a izquierda, las direcciones IP siguen el mismo sistema apoyándose en el dominio **in-addr.arpa**.

      Este tipo de búsquedas suele utilizarse por **seguridad para comprobar la identidad del cliente** (por ejemplo intervienen en el envío de correos electrónicos), de hecho **todo servidor autorizado en una zona debe definir una zona de búsqueda inversa por seguridad**, para poder hacer comprobaciones de este tipo.

          .. raw:: html

              <div style="text-align: justify;  background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
              <b>EJEMPLO</b></br>
              <u>Para la IP 192.168.8.100:</u></br>
              <ol>
              <li>El servidor buscara la zona <i>arpa</i> luego pasara a la zona *in-addr.arpa*</li>
              <li>Continua con la zona <i>192.in-addr.arpa</i></li>
              <li>Después <i>168.192.in-addr.arpa</i></li>
              <li>Seguriá con la zona <i>8.168.192.in-addr.arpa</i></li>
              <li>Finaliza encontrando el registro buscado <i>100.8.168.192.in-addr.arpa</i></li>
              </ol>
              </div>


.. raw:: html

   <div class="footnotes">
       <hr />
       <ol>
           <li class="footnote" id="fn:note1">
               <p>
                   <b>Fuente:</b> <a href="https://www.zeppelinux.es/servidores-de-nombres-sus-tipos-y-zonas/#an_n36" target="_blank">Servidores de nombres, tipos </a> <a class="footnote-backref" rev="footnote" href="#fnref:note1">&#8617;</a>
               </p>
           </li>
       </ol>
   </div>
