Virtualización
==============

El funcionamiento de los servidores hoy día no tiene nada que ver con lo que sucedía hace unos pocos años. Se ha pasado de un alojamiento en máquinas reales, las cuales incluso albergaban varios servicios, a trabajar con máquinas simuladas que ofrecen unicámente un servicio. Estas técnicas reciben el nombre de *Virtualización*. La virtualización de sistemas es una potente **técnica de abstracción mediante la cual podemos crear una capa intermedia que se encarga de posibilitar la comunicación entre una máquina física (anfitrión o host) y el sistema o sistemas huésped (guest) virtuales**.

![arquitectura de contenedores](img/arquitectura-v1.png)

**VENTAJAS**
+ Reducción de costes y mejor gestión de los recursos hardware. Cada máquina física puede usarse para varios propósitos a la vez, con los recursos adecuados.
+ Sustitución de ordenadores por un fondo de MV (pool) que puedan ser creadas, clonadas y destruidas a demanda.
+ Posibilidad de vender capacidad de cálculo a otras empresas
(Virtual Private Servers).
+ Simplificación de los sistemas de copia de seguridad.
Entornos para aprendizaje y pruebas. Se simplifica el montaje y experimentación de otros sistemas operativos y software distinto al que usamos habitualmente. Ideal para estudiantes.
+ Compatibilidad de programas. Posibilidad de usar programas que no ofrezcan versiones para nuestro sistema habitual.
+ Entornos controlados. Se pueden probar programas en los que no confiamos,
+ Fácil migración de unos ordenadores a otros.

**INCONVENIENTES**
+ Un único punto de fallo para todas las máquinas virtuales que se ejecuten en un único servidor físico. Para solucionarlo se deben utilizar **servidores con un alto nivel de redundancia** de discos, memoria, red, fuente de alimentación, y demás componentes (algo bastante más fácil de conseguir si trabajamos en entornos virtualizados)


  **Actualmente se asocia un único servicio a cada servidor, con el fin de limitar el alcance de un hipotético fallo**


### Tipos de Virtualización.

**TIPO 1:** Denominada **nativa/unhosted**, es software que se ejecuta directamente sobre el hardware, para ofrecer la funcionalidad. El hipervisor es un SO cuya única misión es gestionar conjuntos de clusters, Máq. Virtuales, unidades de almacenamiento, etc... Un ejemplo de este tipo de virtualización [lo puedes encontrar en el siguiente video](https://youtu.be/ERb_X20UKqU), en el que muestran una instalación real de un hipervisor denominado [Proxmox](https://www.proxmox.com/en/).

![](img/virtTipo_1.png)

**Ejemplos**
* Proxmox
* PowerVM (IBM)
* ESXi (VmWare)
*  Xen
*  OpenVZ

**TIPO 2:** denominada **hosted o paravirtualización**, es software que se ejecuta **sobre un SO** para ofrecer la funcionalidad(con la consiguiente penlización en rendimiento). Es la virtualización que has usado hasta ahora.

![](img/virtTipo_2.png)

**Ejemplos**
* Parallels (Windows/Mac/Linux)
* VMware (Windows / Linux)
* VirtualBox (Windows/Mac/Linux, Gratis)
* QEMU(Linux, Gratis)
* Windows Virtual PC (Windows, Gratis)

**CONTENEDORES:** Es una alternativa más de virtualización, que persigue mejorar el rendimiento y permitiendo el diseño de infraestructuras de trabajo más dinámicas.
Posibilidad de aplicaciones de gestión automática(Kubernetes..)

![](img/arquitecturaContenedores.png)

**Ejemplos**
* Docker
* LXC/LXD
* Windows servers containers

**CLOUD virtualization:**   Virtualización en sistemas remotos, con todas la ventajas del cloud computing (Azure, AWS, GoogleCloud..)

<a title="Tondashell / CC BY-SA (https://creativecommons.org/licenses/by-sa/4.0)" href="https://commons.wikimedia.org/wiki/File:OpenQRMEnterprise-Datacenter-Cloud-Model-2017.jpg"><img width="512" alt="OpenQRMEnterprise-Datacenter-Cloud-Model-2017" src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/OpenQRMEnterprise-Datacenter-Cloud-Model-2017.jpg/512px-OpenQRMEnterprise-Datacenter-Cloud-Model-2017.jpg"></a>

**Ejemplos**
* Azure
*  Amazon Web Services.
* Google Cloud
* ……

> **Puedes encontrar un interesante artículo de las diferencias entre MV y contenedor, y la evolución de estas tecnologías en los últimos años en el [siguiente blog](https://www.xataka.com/otros/docker-a-kubernetes-entendiendo-que-contenedores-que-mayores-revoluciones-industria-desarrollo)**.

### Gestión de la virtualización.

A la hora de virtualizar SO, debemos tener varios elementos y parametros de configuracion en cuenta. En concreto, **utilizando VirtualBox** debemos prestar especial atención a:

* **Requisitos del SO a virtualizar** → En el apartado de **Configuración** de VBox (Memoria, procesador..)
* **Medios virtuales** → Para incluir el/los discos duros necesarios para nuestro sistema, además de vinular la ISO del SO que queremos instalar.
* **Configuracion de red en las MV** → Uno de los apdos. más importantes. Debemos tener claro los distintos tipos de red en VBox y la utilidad de cada uno. Puedes encontrar una buena aclaración en el [apartado correspondiente del manual oficial de VirtualBox](https://www.virtualbox.org/manual/ch06.html#networkingmodes).
* **Dispositivos USB** → Extension Pack (se instala en la consola de administración de VBox)
* **Carpetas compartidas** → GuestAdditions (Se deben instalar en cada MV por separado. ¿Sabrías hacerlo en una MV sin interfaz gráfica(GUI)?). Puedes encontrar guías de como hacerlo en la web:
  * [Sistemas Linux](https://www.techrepublic.com/article/how-to-install-virtualbox-guest-additions-on-a-gui-less-ubuntu-server-host/).
  * [Sistemas Windows](http://somebooks.es/instalar-guest-additions-windows-server-2016-sin-escritorio-virtualizado-virtualbox/)


<div style="text-align: justify; color: orange; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
<b>PRÁCTICA 1</b></br></br>
Accede al aula virtual del módulo y completa la primera práctica, siguiendo lo indicado en el enunciado. Envía un <b>documento pdf</b> con los pantallazos y características de los equipos, aportadndo las explicaciones que consideres oportunas.
</div>


### Contenedores

Los contenedores(containers) son el siguiente paso en la evolución de la virtualización de sistemas operativos, su objetivo principal es OPTIMIZAR el uso de los recursos de la máquina anfitrión(host). Se puede entender como una virtualización a nivel de sistema operativo.
Se evita la sobrecarga asociada con tener a cada huésped ejecutando un sistema operativo completamente instalado. Una desventaja de la virtualización basada en contenedores, sin embargo, es que cada invitado debe utilizar el mismo sistema operativo que utiliza el host, además de tener un menor nivel de aislamiento.

<div style="text-align:center;">
<a title="Containers diagram" href="https://hackernoon.com/how-container-tech-like-docker-and-business-service-automation-will-monetize-the-cloud-5cbc5a85fe59"><img width="512" alt="Containers diagram" src="https://hackernoon.com/hn-images/1*xef4b78LWTh-raeSkIssvA.png"></a>
</div>


**Docker**

Se ha impuesto como sistema de virtualización de aplicaciones mediante contenedores. Podemos encontrar muchos tutoriales y formaciones en la web <b><sup id="fnref:note1"><a class="footnote-ref" href="#fn:note1" role="doc-noteref">1</a></sup></b>. Varios aspectos destacan:
* Inicialmente creada para GNU/Linux. Actualmente también existe como aplicación para Windows 2010/2016/2019 Srv
* Los contenedores ofrecen un mejor rendimiento que las MV.
* Pueden crearse redes virtuales privadas de contenedores
* Existen herramientas para la gestión de grupos de contenedores(clusters..).
  * [Kubernetes](https://kubernetes.io/es/docs/home/).
  * [Docker Swarm](https://docs.docker.com/engine/swarm/key-concepts).
* El núcleo es el Docker Engine, pero existen opciones para gestionar contenedores.
  * [Docker Compose](https://docs.docker.com/compose/).
  * [Docker Machine](https://www.josedomingo.org/pledin/2016/05/creando-servidores-docker-con-docker-machine/).

Para poder ejecutar docker, debemos instalarlo previamente en nuestro SO (preferiblemente una MV Linux Server, donde ya viene incluido en los repositorios por defecto), teniendo en cuenta varias cosas:

* Docker autocompleta los comandos.
* En caso de duda
    ```console
      $docker --help
    ```
* Para instalar docker
    ```console
      #apt install docker docker.io
    ```
* Para ejectuar docker sin privilegios de administración(sin sudo)
    ```console
      #usermod -a -G docker usuario
    ```
* Estado de Docker, imágenes y contenedores:
    ```console
      $docker system info
      $docker [image|container] [ls|rm|prune|load..] [-a]
    ```
* Arrancar|parar un contenedor:
    ```console
      $docker [container] [run|start|pause|kill|restart...]
    ```
* Gestíon de las **redes**([doc oficial](https://docs.docker.com/network/)) en nuestros entornos(similar a lo que ofrecen las MV):
    ```console
      $docker network [ls|connect|create|rm|prune]
    ```
* Administración de **volúmenes**([doc oficial](https://docs.docker.com/storage/)). Es importante entender la diferencia entre **Volúmenes vs Dir. Enlazado**
    ```console
      $docker volume [create|inspect|ls|prune|rm]
    ```
* Ejecución de comandos contra los contenedores.
    ```console
      $docker exec -it apache-2 /bin/bash
      $docker cp index.html apache:/opt/bitnami/apache/htdocs/index.html
    ```

Como ejemplo, un comando típico de docker, en el que publicamos el puerto 80 del contenedor en el 8080 del host, puede ser:
  ```console
      $docker run -d -p 8080:80 --name=XX --mount type=bind, source=dirHost, target=dirContainer DockerImg
  ```

___
> **¿SABRÍAS?...**
1. Instalar *docker y docker-compose* en una máquina virtual Ubuntu Server
2. Conseguir ejecutar comandos de docker sin necesidad de sudo.
3. **Descargar** la imagen Hello-world del repoitorio oficial de docker.
4. Listar las imágenes y contenedores existentes en tu MV, ejecutar la imagen anterior, comprobar su estado y finalmente borrar la imagen de tu MV.
5. Ejecutar el contenedor **[httpd](https://hub.docker.com/_/httpd/)**  poniéndole como nombre *web* y redirigiendo al puerto 8080 del host(tu MV) el puerto 80 del contenedor. Prueba el acceso a la web.
6. Ejecutar el ejemplo de docker-compose incluido en el pie de página con éxito.
___

**Más cosas sobre Docker/Contenedores**

Si quisiéramos organizar la ejecución de dos contenedores relacionados de alguna manera (por ejemplo un servidor http y un servidor de BD que trabajan en conjunto para servir una página web) tendríamos la opción de usar **Docker-compose**<b><sup id="fnref:note2"><a class="footnote-ref" href="#fn:note2" role="doc-noteref">2</a></sup></b>. Previamente debemos haber instalado el paquete.

En los contenedores en general y en Docker en particular se manejan varios conceptos que debemos conocer para aprovechar todas sus posibilidades:

  * **Imágenes**: Plantillas a partir de las cuales lanzamos los contenedores. Pueden estar en [repositorios públicos](https://hub.docker.com/search?q=&type=image) o privados (creados por nosotr@s mism@s)
    - <a href="https://gitlab.com/mtgimenez.prof/servicios/-/raw/master/docs/TEMA_1_Introduccion/Docker/05_Imagenes.pdf" target="_blank">Tutorial</a>
    - <a href="https://gitlab.com/mtgimenez.prof/servicios/-/raw/master/docs/TEMA_1_Introduccion/Docker/05_Imagenes-Soluciones.pdf" target="_blank">Ejemplos</a>
  * **Contenedores**: Se ejecutan a partir de las imágenes.
    - <a href="https://gitlab.com/mtgimenez.prof/servicios/-/raw/master/docs/TEMA_1_Introduccion/Docker/04_Contenedores.pdf" target="_blank">Tutorial</a>
    - <a href="https://gitlab.com/mtgimenez.prof/servicios/-/raw/master/docs/TEMA_1_Introduccion/Docker/04_Contenedores-Soluciones.pdf" target="_blank">Ejemplos</a>
  * **Volúmenes**: herramienta para conseguir la **persistencia** de los datos en la ejecución de contenedores.
    - <a href="https://gitlab.com/mtgimenez.prof/servicios/-/raw/master/docs/TEMA_1_Introduccion/Docker/06_Almacenamiento.pdf" target="_blank">Tutorial</a>
    - <a href="https://gitlab.com/mtgimenez.prof/servicios/-/raw/master/docs/TEMA_1_Introduccion/Docker/06_Almacenamiento-Soluciones.pdf" target="_blank">Ejemplos</a>
  * **Redes**: Docker permite la gestión de las redes a distintos niveles y características. Esto proporciona opciones muy útiles para crear distintos escenarios.
    - <a href="https://gitlab.com/mtgimenez.prof/servicios/-/raw/master/docs/TEMA_1_Introduccion/Docker/07_Redes.pdf" target="_blank">Tutorial</a>

**En el aula virtual de la asignatura tienes una sección *RECURSOS* con un tutorial completo de Docker que puede resultarte de utilidad**


<div style="text-align: justify; color: orange; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
<b>PRÁCTICA 2</b></br></br>
Accede al aula virtual del módulo y completa la segunda práctica sobre contenedores siguiendo lo indicado en el enunciado. Envía un <b>documento pdf</b> con los pantallazos y características de los equipos, aportando las explicaciones que consideres oportunas.
</div>
</br>

**En el aula virtual del módulo puedes encontrar una sección *RECURSOS* con un completo manual de Docker con todos las herramientas comentadas más desarrolladas y ejemplos de utilización de las mismas.**

### Automatización

La **ORQUESTACIÓN O AUTOMATIZACIÓN** de los servicios consiste en la organización de los sistemas, configuración, gestión y coordinación automatizadas de los sistemas informáticos, las aplicaciones y los servicios. Ayuda a la TI a gestionar con mayor facilidad las tareas complejas y los flujos de trabajo, ya que éstos suelen ser **variables**(piensa en el ejemplo de una web como Amazon en determinadas fechas del año como navidades, Black Friday...) <b><sup id="fnref:note1"><a class="footnote-ref" href="#fn:note3" role="doc-noteref">3</a></sup></b>. Con las herramientas que vamos a ver conseguimos cosas como:

  1. Mejorar el funcionamiento de nuestros servicios, ya que se adaptan a las necesidades en cada momento.
  2. Optimizamos el uso de nuestros recursos, ya que los asignamos de manera coherente.
  3. Reducimos la presencia de errores al limitar la intervención humana.
  4. Ahorro de costes.

  ![orquestación de servicios](http://www.jtech.ua.es/j2ee/publico/servc-web-2012-13/imagenes/sesion5/orquestacion.gif)

Tenemos multitud de herramientas disponibles para configurar entornos de orquestación/automatización a distintos niveles:

  - **Máquinas virtuales:** <a href="https://desarrolloweb.com/articulos/trabajar-con-vagrant.html" target="_blank">Vagrant</a> y <a href="https://openwebinars.net/blog/que-es-ansible/" target="_blank">Ansible</a>. Puedes encontrar un ejemplo en
  - **Contenedores:** <a href="https://kubernetes.io/es/docs/concepts/overview/what-is-kubernetes/" target="_blank"> Kubernetes</a> o <a href="https://docs.docker.com/engine/swarm/swarm-tutorial/" target="_blank">Docker Swarm</a>.
  - **En la nube**(cloud computing): Cada empresa ofrece distintas herramientas, si nos fijamos en AWS, y <a href="https://aws.amazon.com/es/containers/" target="_blank">según su propia documentación</a>: Para obtener control completo sobre el entorno de informática, elija ejecutar los contenedores en *Amazon Elastic Compute Cloud (EC2)*. Para los orquestadores de contenedores, puede elegir *Amazon Elastic Container Service (ECS)* o *Amazon Elastic Kubernetes Service (EKS)*.


<div style="text-align: left; color: BLUE; background-color: #e0e0e0; border-radius: 25px; padding-top: 20px;padding-right: 30px;padding-bottom: 20px; padding-left: 30px;">
<u>EJEMPLO</u></br>
Siguiendo el siguiente tutorial (<a href="https://www.middlewareinventory.com/blog/vagrant-ansible-example/#Ansible_playbook_and_its_artifacts" target="_blank"> https://www.middlewareinventory.com</a>) y con alguna corrección, prueba a ejecutar un primer escenario de automatización con Ansible y Vagrant en una <b>máquina real</b> (tu portátil o si arrancas tu SO anfitrión desde un DD externo).
</div>


Una vez ejecutado este ejemplo, piensa las posibilidades que te ofrecen estas herramientas:

- Arranque/parada en remoto de varias MV.
- Configuración de las características de esas MV.
- Automatización de instalaciones, comprobaciones, etc...
- ++++++++++++++++++++++++

<div class="footnotes">
       <hr />
       <ol>
           <li class="footnote" id="fn:note1">
               <p>
                   <b>Más ayuda en:</b> <a class="footnote-backref" rev="footnote" href="#fnref:note1">&#8617;</a>
                   <ul>
                   <li><a href="https://www.mclibre.org/consultar/webapps/lecciones/docker.html" target="_blank">mclibre</a></li>
                   <li><a href="https://www.josedomingo.org/pledin/2016/02/primeros-pasos-con-docker/" target="_blank">pledin 3.0</a></li>
                   </ul>
               </p>
           </li>
           <li class="footnote" id="fn:note2">
               <p>
                   <b>Ejemplo: </b><a href="https://blog.dinahosting.com/servicio-web-con-docker-y-docker-compose/" target="_blank">Como levantar un srv con docker-compose</a> <a class="footnote-backref" rev="footnote" href="#fnref:note2">&#8617;</a>
               </p>
           </li>
           <li class="footnote" id="fn:note3">
               <p>
                   <b>Ejemplo: </b><a href="https://www.redhat.com/es/topics/automation/what-is-orchestration" target="_blank">Tutoriales de RedHat</a> <a class="footnote-backref" rev="footnote" href="#fnref:note3">&#8617;</a>
               </p>
           </li>
       </ol>

   </div>
