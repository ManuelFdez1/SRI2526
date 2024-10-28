El Espacio de Nombres de Dominio
================================

El servicio DNS es una base de datos en la que se almacenan las asociaciones de nombres de dominios y direcciones IP. Está clasificada por nombres de dominio, **como en un árbol invertido llamado espacio de nombres de dominio**.
  1. El árbol comienza en el **nodo raíz(.)**, situado en el nivel superior. Por debajo, puede existir un número indeterminado de nodos.
  2. El siguiente nivel se denomina **TLD (Top Level Domain)**, como *com, org, edu, es...*
  3. El nombre de un nodo está formado por el conjunto de nombres que forman el itinerario desde ese nodo hasta la raíz. Los nombres se separan con un punto.
  4. Un nombre de dominio correcto se denomina **FQDN (Fully Qualified Domain Name)**, como por ejemplo *www.ejemplo.com. (incluyendo el punto final)*

.. raw:: html

    <div style="text-align:center;">
    <a title="derivative work: Asdepikas (talk) Dns-raum.svg: / CC BY-SA (https://creativecommons.org/licenses/by-sa/2.5)" href="https://es.wikipedia.org/wiki/Sistema_de_nombres_de_dominio#Jerarqu%C3%ADa_DNS"><img width="512" alt="DNS arbol" src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1f/DNS_arbol.svg/512px-DNS_arbol.svg.png"></a>
    </div>


Estructura
------------

La cantidad de información que incluye este espacio de nombres de dominio es demasiado grande para almacenarla de manera centralizada, además la velocidad del sistema sería mucho menor. Por ello la estructura de DNS se basa en dos conceptos:
  1. Delegación.
  2. Jerarquización

**¿DÓNDE SE GUARDA LA INFORMACIÓN?**
Cada servidor DNS tiene un **FICHERO DE ZONA** en el que almacena toda la información de el/los dominio/s sobre los que está autorizado y no ha sub-delegado. En estructuras denominadas **Registros de Recursos(RR)**

**¿QUIEN SE ENCARGA DEL NIVEL RAIZ Y DE LOS TLD?**
Una organización denominada `ICANN <https://www.icann.org/es>`_, que a su vez delega los dominios de siguientes niveles en otras autoridades-servidores DNS. (p. ej: en españa `RED.es <https://red.es/redes/es/quienes-somos/redes?qt-view__pagina_corporativa__block_3=2#qt-view__pagina_corporativa__block_3>`_ se encarga del dominio .es)

.. image:: img/espacioDNStld.png
        :width: 300 px
        :alt: Espacio de nombres DNS
        :align: center


Dominios y zonas
-----------------

Una zona se inicia como una base de datos de almacenamiento para un único nombre de dominio DNS. Si se agregan otros **dominios inferiores (subdominios)**, éstos pueden formar parte de la misma zona o pertenecer a otra zona. Después de agregar un subdominio, se puede:

  * **Administrarlo** e incluirlo como parte de los registros de la zona original.
  * **Delegarlo** a otra zona creada para admitir el subdominio.

En la siguiente imagen se muestra el dominio *microsoft.com*, inicialmente, se configura como una zona única para todos los espacios de nombres DNS de Microsoft. Sin embargo, si añadimos subdominios podemos encontrar diferentes situaciones:

    .. image:: img/dominiosyzonas.png
        :width: 400 px
        :alt: Espacio de nombres DNS
        :align: center


    1. **ejemplo.microsoft.com** muestra un subdominio nuevo, **este dominio es delegado fuera de la zona** microsoft.com y administrado en su propia zona, por otro servidor DNS. En la configuración de zona de microsoft.com debe haber algún parametro que índique las zonas delegadas.
    2. **dev.microsoft.com** NO utiliza la delegación en un subdominio, los datos del subdominio continúan formando parte de la zona microsoft.com, por lo que los administra el servidor DNS principal.

.. raw:: html

    <div style="text-align: left; color: BLUE; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
    <u>¿Sabrías?</u></br>
    Explicar la diferencia entre HOSTING y REGISTRO DE DOMINIO, encontrando alguna tarifa en la web y explicando la diferencia de precio entre ambas.
    </div></br>
