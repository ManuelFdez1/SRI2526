Servicios de acceso a ficheros
===============================

Servicios LAN
--------------

Si hablamos de redes locales (LAN) y compartir ficheros y recursos, tenemos varios protocolos destacados:
    * Network File System (**NFS**): Sistemas UNIX-Linux.
    * Server Message Block (**SMB/CIFS**):​ Protocolo para compartir archivos, impresoras... entre sistemas Windows. Aunque es un protocolo propiedad de Microsoft, tiene
      algunas implementaciones libres, por ejemplo SAMBA en versiones Linux.
    * Linux incluye algunos comandos muy útiles de gestión remota de ficheros (**rsync, scp...**).

.. image:: img/samba.png
      :width: 200 px
      :alt: Compartir recursos en red Windows Linux
      :align: center

.. Warning::
   ¿Pueden/Deben usarse estos servicios más allá de una LAN?¿Sabrías decir que habría que configurar para poder hacerlo?

SAMBA es una opción bastante sencilla para poder compartir recursos entre máquinas Windows y Linux. No importa que SO sea el servidor y que SO actúe de cliente.

.. raw:: html

      <iframe width="300" style="display:block; margin-left:auto; margin-right:auto;" src="https://www.youtube.com/embed/LjvFmSHAS3M" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></br>

.. Important::
   Sería un ejercicio interesante que compartieras ficheros entre MV Linux y Windows. Podrías incluso ubicar esos recursos compartidos en discos distintos al SO.

FTP
----
FTP (**File Transfer Protocol**, 'Protocolo de Transferencia de Archivos'), es un protocolo para la transferencia de archivos entre sistemas conectados a una red. Desde un
equipo cliente se puede conectar a un servidor para descargar archivos desde él o para enviarle archivos, independientemente del sistema operativo utilizado en
cada equipo. FTP está pensado para ofrecer la máxima velocidad en la conexión, pero no seguridad, ya que todo el intercambio de información, se realiza en texto
plano.

.. image:: img/protocoloftp.png
    :width: 200 px
    :alt: Protocolo FTP
    :align: center

Para solucionar este problema son de gran utilidad aplicaciones como scp y sftp, incluidas en el paquete SSH, o dotar de seguridad al propio servidor ftp con una
capa SSL similar a la utilizada en HTTPS, alternativas que permiten transferir archivos pero cifrando todo el tráfico.

    * `SFTP <https://es.wikipedia.org/wiki/SSH_File_Transfer_Protocol>`_.
    * `FTPS <https://es.wikipedia.org/wiki/FTPS>`_.

.. Warning::
   El servicio FTP puede trabajar de dos maneras (puedes encontrar una `información más detallada en la Wikipedia <https://es.wikipedia.org/wiki/Protocolo_de_transferencia_de_archivos#Modos_de_conexi%C3%B3n_del_cliente_FTP>`_):

      * ACTIVO
      * PASIVO

   Es importante conocer las características de cada una, ya que podemos encontrarnos problemas de funcionamiento dependiendo de las características de seguridad de
   la red bajo la que estemos trabajando.

Clientes
~~~~~~~~
Un cliente FTP emplea el protocolo FTP para conectarse a un servidor FTP para transferir archivos, independientemente del SO del propio cliente o del servidor.
Podemos encontrar clientes de varios tipos:

    1. LINEA DE COMANDOS: Algunos clientes de FTP/SFPT básicos vienen integrados en los sistemas operativos(Windows,Linux). Ofrecen un acceso rápido y sin necesidad de
    instalación de ningún paquete. Las instrucciones de estos comandos son universales, independientes del SO.

            .. image:: img/ejemploftpcomando.png
                :width: 300 px
                :alt: Ejemplo conexión comando FTP
                :align: center

        .. Tip::
           Puedes encontrar servidores públicos de FTP donde probar los comandos, incluso de subida de ficheros (en **speedtest.tele2.net** puedes encontrar un servidor que admite
           acceso anónimo).


    2. INTEGRADOS EN EL NAVEGADOR: Muchos navegadores llevan integrados clientes FTP o permiten la instalación de *plugins*.

            .. image:: img/ejemploftpnavegador.png
                :width: 300 px
                :alt: Ejemplo conexión comando FTP
                :align: center

    3. PROGRAMAS ESPECÍFICOS: Hay disponibles clientes con **más funcionalidades y opciones**, tanto para Windows como para Unix/Linux o Mac. Algunos ejemplos podrían ser:

        * `FileZilla Client <https://filezilla-project.org/download.php?type=client>`_.
        * `WinSCP <https://winscp.net/eng/index.php>`_.
        * `Transmit <https://panic.com/transmit/>`_.


Servidores
~~~~~~~~~~
En este servicio debemos prestar atención a los siguientes elementos o propiedades:
  * Instalación y configuración del servicio sobre el SO correspondiente.
  * Crear los directorios donde se ubicarán los sitios FTP, con los PERMISOS ADECUADOS.
  * Creación de grupos y de directorios públicos asociados.
  * Parámetros de conexión
      * Nº máximo de conexiones.
      * Limitar anchos de banda.
      * Limitar acceso por IP/ Hora..
  * Tipos de usuari@/autenticación.
      * Usuari@s locales
      * Usuari@s virtuales. Varias posibilidades.
          * Ficheros generados con el paquete db-util (https://www.linuxcloudvps.com/blog/setup-virtual-users-in-vsftpd/)
          * Ficheros generados con htpasswd.
          * Bases de datos (MySql..)
          * Servicios de directorio (LDAP)
      * Autorizar acceso anónimo
  * Enjaular a l@s usuari@s (**CHROOT**).
  * Soporte para conexiones seguras mediante SSL(instalación de certificados).

**SERVIDOR FTP EN LINUX**

Utilizaremos VsFTP (`manual en la web <https://web.mit.edu/rhel-doc/4/RH-DOCS/rhel-rg-es-4/s1-ftp-vsftpd-conf.html>`_ o también
la `documentación oficial <https://security.appspot.com/vsftpd/vsftpd_conf.html>`_  ), teniendo en cuenta lo siguiente:

  * # apt-get install vsftpd
  * La configuración bastante sencilla
  * Permite **servidores virtuales** (por IP)
  * Puede incluirse **cifrado** (FTP seguro)
  * **Enjaular usuarios** (*atención writeable chroot*)

  Por defecto los usuarios del servicio FTP se encuentran vinculados a los usuarios del sistema en Linux pero existen otras maneras de gestionar la identificación de usuarios
  como por ejemplo con una base de datos MySQL(USUARIOS VIRTUALES).

  .. raw:: html

        <p style="text-align: justify;"><img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/42/Pdf-2127829.png/480px-Pdf-2127829.png" alt="Perfil" width="50" style="vertical-align: middle; float:left;"/>  <b>En el siguiente documento puedes encontrar un manual completo de como realizar la configuración básica un servidor FTP con sus usuari@s incluidos en una BD MySQL.</b></br>

  .. image:: img/usuariosvirtuales.pdf
        :width: 400 px
        :alt: Usuarios virtuales(VSFTP+MYSQL+PAM)
        :align: center

.. raw:: html

        </br>
        <div style="text-align: justify; color: orange; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
        <u><b>PRÁCTICA 1</b></u></br>
        Servidor FTP seguro en Ubuntu Server.
        </div>
        </br>


WebDAV(HTTP/S)
--------------
A través de los protocolos HTTP/HTTPS podemos configurar el acceso remoto a sistemas de ficheros en nuestro/s servidor/es, con protocolos más modernos que FTP.
`WebDAV(Web Distributed Authoring and Versioning) <https://es.wikipedia.org/wiki/SSH_File_Transfer_Protocol>`_.

.. image:: img/introwebdav.png
    :width: 300 px
    :alt: WebDAV
    :align: center

Tal y como dice la `documentación oficial de Apache <https://httpd.apache.org/docs/2.4/mod/mod_dav.html>`_, el objetivo de este protocolo (o más concretamente EXTENSIÓN DE PROTOCOLO) es conseguir que la web (http/https) permita el acceso con permisos de escritura a recursos publicados.
Con él podemos hacer accesibles partes de nuestro sitio web como  un directorio remoto.

.. Warning::
   ¿Sabrías deducir para que resultaría de utilidad este tipo de característica instalada y configurada en nuestros servidores web?

Configuración en Apache
~~~~~~~~~~~~~~~~~~~~~~~

Los pasos a realizar, `extraídos del siguiente manual <https://www.digitalocean.com/community/tutorials/how-to-configure-webdav-access-with-apache-on-ubuntu-14-04>`_, son:

    1. Activar los módulos correspondientes.

    .. code-block:: shell-session

                    # a2enmod dav dav_fs

    2. Añadir en nuestra configuración de Apache el módulo (sobre  un directorio/location) →  DAV On

        .. image:: img/webdav_1.png
            :width: 400 px
            :alt: WebDAV
            :align: center

    3. Añadir algún método de autenticación
        * ¿basic/digest?
        * ¿IP?
        * Sin autenticación Acceso libre

    4. Atención a permisos/propietario

        .. image:: img/webdav_2.png
            :width: 400 px
            :alt: WebDAV
            :align: center

    5. Reiniciar apache
    6. Probar la conexión con un cliente(Linux|Windows|MAC).

        .. image:: img/webdav_3.png
            :width: 400 px
            :alt: WebDAV
            :align: center


Configuración en NginX
~~~~~~~~~~~~~~~~~~~~~~~

Los pasos a realizar en este caso puedes encontrarlos en la `documentación oficial <http://nginx.org/en/docs/http/ngx_http_dav_module.html>`_, son:

    1. Instalar los paquetes correspondientes.

    .. code-block:: shell-session

                    # apt -y install nginx-extras libnginx-mod-http-dav-ext

    2. Añadir en nuestra configuración de las opciones correspondientes:

        .. image:: img/webdav_4.png
            :width: 400 px
            :alt: WebDAV
            :align: center

    3. El resto de aspectos a tener en cuenta son muy similares a Apache.

.. Warning::
   La directiva `DirectoryIndex <https://httpd.apache.org/docs/2.4/mod/mod_dir.html#directoryindex>`_ en Apache o `Autoindex <http://nginx.org/en/docs/http/ngx_http_autoindex_module.html>`_ en NginX para listar el contenido de un directorio del servidor suele ser una fuente de errores en combinación con WebDAV.
   **La recomendación general es desactivar esa directiva para poder utilizar los módulos dav**

.. raw:: html

        </br>
        <div style="text-align: justify; color: orange; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
        <u><b>PRÁCTICA 2</b></u></br>
        Realiza la práctica de configuración de WebDAV
        </div>
        </br>

.. Important::
   ¿Sabrías deducir que puertos utiliza WebDAV?
