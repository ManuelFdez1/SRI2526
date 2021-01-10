Alta disponibilidad
====================

Un siguiente nivel para mejorar el rendimiento sería la **ALTA DISPONIBILIDAD** mediante **REDUNDANCIA** de servidores. En estos casos tenemos un
servidor intermedio(proxy inverso) que puede actuar, por ejemplo, como:

    1. Balanceador de carga.
    2. Proxy cache

.. image:: img/balanceoCarga.png
                :width: 400 px
                :alt: Balanceo de carga web
                :align: center

Tenemos diferentes alternativas si queremos configurar un escenario de redundancia (La mayoría de las webs que visitamos en realidad trabajan con estos esquemas)

    * **Apache** pueden configurarse para actuar como servidor intermedio (`documentación oficial <https://httpd.apache.org/docs/2.4/howto/reverse_proxy.html>`_).
    * En el caso de **NginX**, es uno de los puntos fuertes del programa (`guía en la documentación oficial <https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/>`_).


¿Te atreverías a montar un balanceo de carga con Apache? Deberías manejar concetpos como:
Proxy inverso
Balanceo de carga
Contenedores
