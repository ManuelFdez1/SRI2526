Entorno de trabajo
===================
Para el módulo de Servicios de Red e Internet el escenario más típico a configurar en nuestros servidores virtualizados (en los SSOO correspondientes), serán los siguientes:
* Una tarjeta de red conectada a la red real del aula. Esta será la **IP pública** de ’nuestra red’ virtualizada.
* El resto de tarjetas de red configuradas de manera que solo sean visibles en nuestro equipo, y en la **red privada** correspondiente.

Para probar el funcionamiento de nuestros servidores, crearemos MV que actúen como clientes, teniendo una única interfaz de red, la cual se conectará a la red privada .

![](img/escenario.png "Entorno de trabajo típico")

En algunos apartados del módulo (especialmente en el servicio web) podremos encontrarnos con escenarios donde ejecutemos múltiples instancias de contenedores para simular un entorno de alta disponibilidad<b><sup id="fnref:note1"><a class="footnote-ref" href="#fn:note1" role="doc-noteref">1</a></sup></b>.

![](img/escenarioDockermultiple.jpg "Entorno de trabajo con múltiples contenedores")

<div style="text-align: left; color: BLUE; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
<u>TAREA</u></br>
<ul>
<li>Añade a las MV que creaste para la primera práctica una tarjeta interna, a la cual darás dirección estática(la que quieras) la tarjeta externa se contectará a la red real y se configurará por DHCP.</li>
<li>A cada MV se conectará un cliente interno, el cual también configuraras de manera manual, y podrá verse con el servidor únicamente (mediante un ping)</li>
<li>Realiza esto para los tres servidores virtualizados que creaste.</li>
</ul>
</div>



<div class="footnotes">
       <hr />
       <ol>
           <li class="footnote" id="fn:note1">
               <p>
                   <b>En la imagen el símbolo <span style="font-size:28px;">?</span> es un balacenador de carga:</b>
                   <a href="https://httpd.apache.org/docs/2.4/howto/reverse_proxy.html" target="_blank">apache</a> o <a href="https://nginx.org/en/docs/http/load_balancing.html" target="_blank">NginX</a>
                    <a class="footnote-backref" rev="footnote" href="#fnref:note1">&#8617;</a>
               </p>
           </li>
       </ol>
   </div>
