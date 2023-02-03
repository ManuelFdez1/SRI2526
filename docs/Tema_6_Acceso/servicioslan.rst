Servicios LAN
==============

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
