==========================
Resolución de nombres. DNS
==========================

En una red TCP/IP, las máquinas se identifican mediante su dirección IP. Para las personas resulta más sencillo recordar un nombre que se asocia a una máquina concreta. Este se denomina DOMINIO O NOMBRE DE DOMINIO y está relacionado con la red LOCAL donde esté el dispositivo. Es más fiable, ya que la dirección IP puede cambiar, pero no el nombre. Es necesario un mecanismo que traduzca los nombres de dominio de las máquinas a direcciones IP.

    * INICIALMENTE → archivo HOSTS
    * El crecimiento de la red causó que el sistema de nombres en el archivo hosts no resultara práctico. Por lo que surgió el **Servicio DNS (Domain Name System - Sistema de nombres de dominio)**
    * El DNS es una **base de datos distribuida y jerárquica** que almacena información asociada a nombres de dominio en redes como Internet .

.. raw:: html

    <div style="text-align: center; color: BLUE; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
    La mayoría de los SSOO actuales siguen leyendo en primer lugar de los ficheros hosts para realizar las traducciones de nombre/IP. ¿Sabrías encontrar su ubicación tanto en Windows como en Linux?
    </div></br>


Para estudiar este servicio, uno de los más importantes del WWW, vamos a analizar estos apartados:

.. toctree::
   :maxdepth: 2

   espacio
   tipos
   ficherozona
   configuracion
   comprobaciones
   adicionales
