Fichero de zona DNS
======================

.. raw:: html

    <p>
    Ya sabemos que DNS gestiona una base de datos distribuida entre múltiples servidores que almacenan ficheros de zona con información sobre nombre de dominio. Los Archivos de zona contienen información sobre un espacio de nombres particular y son almacenados en los servidores autorizados. Los ficheros de zona contienen básicamente dos cosas <sup id="fnref:note1"><a class="footnote-ref" href="#fn:note1" role="doc-noteref">1</a></sup>:
    </p>

1. **DIRECTIVAS**: Parámetros y configuraciones especiales a la zona.
2. **REGISTROS DE RECURSOS (RR)**: Elementos integrantes de la zona.

        .. image:: img/ficherozona.png
                  :width: 400 px
                  :alt: Ejemplo fichero de zona
                  :align: center

Todas las directivas y registros de recursos deberían ir en sus propias líneas individuales. Los comentarios se pueden colocar después de los punto y comas (;).

Directivas
------------

Las directivas comienzan con el símbolo **$** seguido del nombre de la directiva. Usualmente aparecen en la parte superior del archivo de zona. Lo siguiente son usadas a menudo:

* **$INCLUDE**: Incluye el contenido de otro archivo en el fichero de zona donde se usa la directiva. Sirve para separar la configuración del servidor en distintos ficheros (La configuración de Ubuntu, de hecho, lo hace así).
* **$ORIGIN**: ES el nombre del dominio acabado en punto. Se anexa a registros no completamente especificados (acabados en punto ".").

  Pueden haber varios en un mismo fichero de zona, por ejemplo para delegar subdominios.

  Si no se indica ninguna directiva de este tipo se tomará como valor de ORIGIN el nombre de la zona.

        .. code-block:: shell-session

              $ORIGIN botet.es.
              ...     ; a partir de aquí se añade .botet.es. a los nombres relativos
              ...
              $ORIGIN informatica.botet.es.
              ...     ; a partir de aquí se añade .informatica.botet.es. a los nombres relativos
              ...
* **$TTL**: Ajusta el valor *Time to Live (TTL)* predeterminado para la zona. Este es el tiempo, en segundos, que un RR es válido. Cada recurso puede contener su propio valor TTL, el cual ignora esta directiva..

Registros de recursos(RR)
-------------------------

El componente principal de un archivo de zona es su registro de recursos. El formato de representación dentro del fichero de zona suele ser:

        .. image:: img/rrdns.png
                  :width: 400 px
                  :alt: Estructura registro de recurso
                  :align: center


1. **TTL (Time to life)**: Es opcional a  nivel de recurso, ya que se puede definir a nivel global para toda la zona.
2. El campo **Clase** indica la arquitectura de protocolos utilizada (habitualmente TCP/IP cuyo identificador es **IN**)
3. El campo **Tipo** puede tener multitud de valores, dependiendo del tipo de recurso al que haga referencia.
      * SOA – INICIO DE AUTORIDAD
      * A – HOST
      * CNAME – ALIAS
      * PTR – PUNTERO(Resolucion inversa)
      * NS – SERVIDOR DE NOMBRES
      * MX – SERVIDOR DE CORREO
      * SRV – OTROS SERVIDORES.


Ejemplo Fichero de zona
-------------------------

      .. code-block:: shell-session

        $ORIGIN example.com.
        $TTL 86400
        @	SOA	dns1.example.com.	hostmaster.example.com. (
        2001062501 ; serial
        21600      ; refresh after 6 hours
        3600       ; retry after 1 hour
        604800     ; expire after 1 week
        86400 )    ; minimum TTL of 1 day
        ;
        ;
        NS	dns1.example.com.
        NS	dns2.example.com.
        dns1	A	10.0.1.1
              AAAA	aaaa:bbbb::1
        dns2	A	10.0.1.2
              AAAA	aaaa:bbbb::2
        ;
        ;
        @	MX	10	mail.example.com.
          MX	20	mail2.example.com.
        mail	A	10.0.1.5
              AAAA	aaaa:bbbb::5
        mail2	A	10.0.1.6
              AAAA	aaaa:bbbb::6
        ;
        ;
        ; This sample zone file illustrates sharing the same IP addresses for multiple services:
        ;
        services	A	10.0.1.10
                  AAAA	aaaa:bbbb::10
                  A	10.0.1.11
                  AAAA	aaaa:bbbb::11

        ftp	CNAME	services.example.com.
        www	CNAME	services.example.com.
        ;
        ;
              ...

.. raw:: html

   <div class="footnotes">
       <hr />
       <ol>
           <li class="footnote" id="fn:note1">
               <p>
                   <b>Fuente:</b> <a href="https://www.fpgenred.es/DNS/ficheros_de_zona_y_registros_de_recursos.html" target="_blank">Ficheros de zona y registros de recursos</a> <a class="footnote-backref" rev="footnote" href="#fnref:note1">&#8617;</a>
               </p>
           </li>
       </ol>
   </div>
