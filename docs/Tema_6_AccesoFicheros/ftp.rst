FTP
===
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
---------
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
-----------
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
      * Usuari@s virtuales
      * Autorizar acceso anónimo
  * Enjaular a l@s usuari@s.
  * Soporte para conexiones seguras mediante SSL(instalación de certificados).

**SERVIDOR FTP EN LINUX**

Utilizaremos VsFTP (`manual en la web <https://comoinstalar.me/como-instalar-ftp-en-ubuntu-20-04-lts/>`_), teniendo en cuenta lo siguiente:

  * # apt-get install vsftpd
  * 1 solo fichero de configuración
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
