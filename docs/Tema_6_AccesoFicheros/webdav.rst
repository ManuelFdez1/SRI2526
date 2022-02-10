WebDAV(HTTP/S)
==============
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
------------------------

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
------------------------

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
