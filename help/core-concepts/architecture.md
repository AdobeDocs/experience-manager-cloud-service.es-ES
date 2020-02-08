---
title: Introducción a la arquitectura de Adobe Experience Manager como servicio de nube
description: 'Introducción a la arquitectura de Adobe Experience Manager como servicio de nube. '
translation-type: tm+mt
source-git-commit: 5a846d34ee094e7d2f7fc71dbeef65f3fa58e86c

---


# Introducción a la arquitectura de Adobe Experience Manager como servicio de nube {#an-introduction-to-the-architecture-adobe-experience-manager-as-a-cloud-service}

Adobe Experience Manager (AEM) como servicio de nube ha producido cambios en la arquitectura.

## Escala {#scaling}

AEM como servicio de nube ahora tiene:

* Arquitectura dinámica con un número variable de imágenes de AEM.

![Arquitectura dinámica](assets/concepts-01.png "Arquitectura dinámica")

Esta arquitectura:

* Se escala en función del tráfico *real* y la actividad *real* .

* Tiene instancias individuales que solo se ejecutan cuando es necesario.

* Utiliza aplicaciones modulares.

* Tiene un clúster de creación como predeterminado; esto evita el tiempo de inactividad para tareas de mantenimiento.

Esto permite escalar automáticamente en distintos patrones de uso:

![Escala automática para](assets/concepts-02.png "patrones de uso variablesEscala automática para patrones de uso variables")

Para conseguirlo, se crean todas las instancias de AEM como un servicio en la nube iguales, cada una con las mismas características de tamaño predeterminadas en cuanto al número de nodos, la memoria asignada y la capacidad informática asignada.

AEM como servicio de nube se basa en el uso de un motor de orquestación que:

* Controla constantemente el estado del servicio.

* Escala dinámicamente cada una de las instancias de servicio según las necesidades reales; tanto la escala hacia arriba como hacia abajo, según corresponda.

Esto:

* Se aplica al número de nodos, la cantidad de memoria y la capacidad de CPU asignada en cada nodo.

* Permite que AEM como servicio de nube ajuste los patrones de tráfico a medida que cambian.

La escala de las instancias de cada inquilino del servicio puede ser automática o manual, en los dos ejes:

* Vertical: la memoria asignada y la capacidad de CPU se pueden aumentar o reducir para un número fijo de nodos.

* Horizontal: el número de nodos de un servicio determinado se puede aumentar o reducir.

## Entornos {#environments}

>[!NOTE]
>
> Para obtener más información, consulte [Implementación - Modos de ejecución](/help/implementing/deploying/overview.md#runmodes)

AEM como servicio de nube está disponible como instancias individuales y cada instancia representa un entorno AEM completo. Existen cuatro tipos de entornos disponibles con AEM como servicio de nube:

* **Entorno** de producción: aloja las aplicaciones para los profesionales del negocio.

* **Entorno** de etapa: siempre se asocia a un único entorno de producción en una relación 1:1. El entorno de etapa se utiliza para varias pruebas de rendimiento y calidad antes de que los cambios en la aplicación se inserten en el entorno de producción.

* **Entorno** de desarrollo: permite a los desarrolladores implementar aplicaciones AEM en las mismas condiciones de tiempo de ejecución que los entornos de fase y producción.

* **Entorno** de demostración: puede utilizarse con fines de evaluación, demostración, creación de prototipos y capacitación.

Los entornos de desarrollo y demostración suelen denominarse entornos *no productivos* .

## Programas {#programs}

Cualquier nuevo proyecto de AEM siempre está enlazado a exactamente un código base específico, donde puede almacenar tanto la configuración como el código personalizado para su proyecto. Esta información se almacena en un repositorio de código, al que se puede acceder a través de los clientes Git habituales, y que está disponible en el momento de crear los nuevos programas.

Un programa de AEM es el contenedor que incluye:

|  Elemento de programa |  Número |
|--- |--- |
| Repositorio de códigos (Git) |  1 |
| Imagen de línea de base (Sitios o recursos) |  1 |
| Conjunto de entorno de fase y producción (1:1) | 0 o 1. |
| Entornos que no son de producción (desarrollo o demostración) | 0 a N |
| Canalización para cada entorno | 0 o 1. |

Inicialmente, AEM dispone de dos tipos de programas como servicio de nube:

* Servicio Sitios de AEM Cloud

* Servicio AEM Cloud Assets

Ambos permiten el acceso a una serie de funciones y características. La capa de creación contendrá todas las funciones Sitios y Recursos para todos los programas, pero los programas de Recursos no tendrán una capa de publicación de forma predeterminada.

## Arquitectura de tiempo de ejecución {#runtime-architecture}

Hay varios componentes principales de esta nueva arquitectura:

<!--- needs reworking -->

![AEM como servicio de nube -](assets/concepts-03.png "Arquitectura del tiempo de ejecuciónAEM como servicio de nube - Arquitectura del tiempo de ejecución")

* Para AEM Sites como servicio de nube:

   * Sigue existiendo el concepto de una capa de creación y una capa de publicación para cada entorno (de alto nivel).

   * El nivel de autor está formado por dos o más nodos dentro de un único clúster de creación. Escala automáticamente, según la actividad de creación.

      * Los creadores y autores de contenido inician sesión en el nivel de creación de AEM para crear, editar y administrar contenido.

      * El inicio de sesión en el nivel de autor se administra mediante Adobe Identity Management Services (IMS).

      * La integración y el procesamiento de recursos utilizan un servicio de cómputo de Assets dedicado.
   * El nivel de publicación consta de dos o más nodos dentro de un único conjunto de servidores de publicación: pueden operar de forma independiente entre sí. Cada nodo consta de un editor de AEM y un servidor web equipado con el módulo Dispatcher de AEM. Escala automáticamente según las necesidades de tráfico del sitio.

      * Los usuarios finales, o los visitantes del sitio, visitan el sitio web a través del servicio de publicación de AEM.


* Para AEM Assets como servicio de nube:

   * La arquitectura solo incluye un entorno de creación.

* Tanto el nivel de creación como el de publicación leen y conservan el contenido desde/hacia un servicio de repositorio de contenido.

   * El nivel de publicación solo lee contenido de la capa de persistencia.

   * El nivel de autor lee y escribe contenido desde y hacia la capa de persistencia.

   * El almacenamiento de blobs se comparte en el nivel de publicación y autor; los archivos no se *mueven*.

   * Cuando el contenido se aprueba desde el nivel de autor, esto indica que se puede activar, por lo que se envía a la capa de persistencia del nivel de publicación. Esto sucede a través del servicio de replicación, un conducto de middleware. Esta canalización recibe el nuevo contenido y los nodos de servicio de publicación individuales se suscriben al contenido insertado en la canalización.

      >[!NOTE]
      >
      >For more details see [Replication](/help/operations/replication.md).

   * Los desarrolladores y administradores administran AEM como una aplicación de servicio en la nube mediante un servicio de integración continua/entrega continua (CI/CD), disponible mediante [Cloud Manager](/help/overview/what-is-new-and-different.md#cloud-manager). Esto incluye implementaciones de código y configuración mediante el canalizador CI/CD del Administrador de nube. Cualquier cosa relacionada con la supervisión, el mantenimiento y la solución de problemas (por ejemplo, archivos de registro) se expone a los clientes dentro de Cloud Manager.

   * El acceso a los niveles de creación y publicación siempre se produce mediante un equilibrador de carga. Esto siempre está actualizado con los nodos activos de cada uno de los niveles.

   * Para el nivel de publicación, también está disponible un servicio de red de entrega continua (CDN) como primer punto de entrada.

* En el caso de instancias de demostración de AEM como servicio de nube, la arquitectura se simplifica a un solo nodo de creación. Por lo tanto, no presenta todas las características del desarrollo, la fase o el entorno de producción estándar. Esto también significa que puede haber cierto tiempo de inactividad y que no hay soporte para operaciones de backup y restore.

## Arquitectura de implementación {#deployment-architecture}

Cloud Manager administra todas las actualizaciones de las instancias de AEM como un servicio de nube. Es obligatorio, ya que es la única manera de crear, probar e implementar la aplicación del cliente, tanto para el autor como para los niveles de publicación. Estas actualizaciones las puede activar Adobe, cuando hay una nueva versión del servicio de nube de AEM lista, o el cliente, cuando hay una nueva versión de su aplicación lista.

Técnicamente, esto se lleva a cabo debido al concepto de una tubería de implementación, junto con cada entorno dentro de un programa. Cuando se está ejecutando una canalización de Cloud Manager, se crea una nueva versión de la aplicación del cliente, tanto para el autor como para los niveles de publicación. Esto se logra combinando los últimos paquetes de clientes con la última imagen básica de Adobe. Cuando las nuevas imágenes se crean y prueban correctamente, Cloud Manager automatiza completamente el cambio a la última versión de la imagen mediante la actualización de todos los nodos de servicio mediante un patrón de actualización móvil. Esto no provoca downtime ni para el autor ni para el servicio de publicación.

<!--- needs reworking -->

![AEM como servicio de nube -](assets/concepts-04.png "Arquitectura de implementaciónAEM como servicio de nube - Arquitectura de implementación")

## Distribución de contenido {#content-distribution}

Adobe Experience Manager como servicio de nube ha modificado la forma en que funciona la publicación de contenido. Con AEM como servicio de nube, el marco de replicación de versiones anteriores de AEM ya no se utiliza para publicar páginas (se mueven los cambios de la instancia de autor a las instancias de publicación).

AEM como servicio de nube ahora utiliza la función [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html) para mover el contenido adecuado. Utiliza un servicio de canalización que se ejecuta en Adobe I/O, que está fuera del tiempo de ejecución de AEM.

La configuración es automatizada, incluida la autoconfiguración automática cuando se agregan, eliminan o reciclan nodos de publicación durante el tiempo de ejecución.

Una sola solicitud de publicación o cancelación de publicación puede incluir varios recursos, pero devolverá un solo estado aplicado a todos; se realizará correctamente con todos los recursos del servicio de publicación de AEM o se producirá un error en todos los casos. Esto garantiza que los recursos del servicio de publicación de AEM nunca estarán en un estado incoherente.

**Diagrama de la Arquitectura de Distribución de Contenido de Alto Nivel**

![Diagrama](assets/architecture-diagram.png "de Arquitectura de Distribución de Contenido de Alto Nivel Diagrama de Arquitectura de Distribución de Contenido de Alto Nivel")

## Evoluciones clave {#key-evolutions}

La nueva arquitectura de AEM como servicio de nube presenta algunos cambios e innovaciones fundamentales en comparación con las generaciones anteriores:

* Todos los archivos (blobs) se cargan directamente y se sirven desde un almacén de datos en la nube. El flujo de bits asociado nunca pasa por el JVM de los servicios AEM Author y Publish. Como resultado, los nodos de los servicios de creación y publicación de AEM pueden tener un tamaño menor y ser más compatibles con la expectativa de una escala automática rápida. Para los profesionales del sector empresarial, esto resulta en una experiencia más rápida al cargar y descargar imágenes, vídeos, etc.

* Todas las operaciones consistentes en publicar contenido ahora implican una canalización siguiendo un patrón de suscripción. El contenido publicado se inserta en varias colas de la canalización, a las que se suscriben todos los nodos del servicio de publicación. Como resultado, el nivel de autor no necesita tener en cuenta el número de nodos en el servicio de publicación; esto permite aplicar una escala automática rápida al nivel de publicación.

* Se introdujo el concepto de maestro dorado para automatizar el ciclo de vida de los nodos de publicación. El maestro dorado es un nodo de publicación especializado, al que ningún usuario final tiene acceso y desde el que se crean todos los nodos del servicio de publicación. Las operaciones de mantenimiento, como la compactación, se realizan en el repositorio de contenido adjunto al maestro dorado. Los nodos de publicación se reciclan diariamente y no requieren ningún tipo de mantenimiento rutinario; en el pasado, dicho mantenimiento requería cierto tiempo de inactividad, especialmente para la instancia de creación.

* La arquitectura separa completamente el contenido de la aplicación del código de la aplicación y la configuración. Todo el código y la configuración son prácticamente inmutables y se codifican en la imagen de línea de base utilizada para crear los distintos nodos del autor y los servicios de publicación. Como resultado, existe una garantía absoluta de que cada nodo es idéntico, y los cambios en el código y la configuración sólo se pueden realizar de forma global mediante la ejecución de una canalización de Cloud Manager.
