Sistemas Operativos NAS
========================

En este apartado nos referimos a distribuciones Linux diseñadas para almacenamiento conectado a la red **NAS, siglas de Almacenamiento Conectado en
Red (Network Attached Storage)**. Muchos de estos SSOO tienen un carácter gratuito, open-source y software libre (basado en licencia BSD) y nos
permiten administrar soportes de almacenamiento accesible desde red, por ejemplo para almacenamientos masivos de información, música, backups, etc.
Dos ejemplos:

    * FreeNAS: https://www.freenas.org/
        .. image:: img/Freenas.png
            :width: 400 px
            :alt: Ejemplo freenas
            :align: center
    * OpenMediaVault (necesita menos recursos para funcionar): https://www.openmediavault.org/
        .. image:: img/OpenMediaVault.png
            :width: 400 px
            :alt: Ejemplo openmediavault
            :align: center


Para poder practicar con estas distribuciones podemos hacer uso de la virtualización. Vamos a simular nuestro NAS, como si hubiéramos comprado uno. Para ello
debemos dar los siguientes pasos:

    1 Crearemos una MV
       * OpenMediaVault/FreeNAS ISO
       * Atentos-as a los requisitos y al tipo de la MV
    2 Añadimos disco/s duro/s a nuestra configuración (nuestro NAS)
       * Podemos añadir los que queramos y darle estructura de RAID
    3 Configuramos la red de la MV para hacerlo pública
    4 Primeras tareas
       * Crear pool
       * Usuarios/grupos
       * Configuramos el/los servicios que queramos proporcionar
          * SMB
          * WebDAV
          * ....

.. Important::
   Configurar tu propio NAS y 'juega' con las opciones de servicios, uso y seguridad que te ofrecen.
