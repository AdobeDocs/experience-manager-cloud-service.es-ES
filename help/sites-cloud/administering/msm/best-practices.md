---
title: Prácticas recomendadas de MSM
description: Conozca las prácticas recomendadas recopiladas por los equipos de consultoría e ingeniería de Adobe para ayudarle a poner en marcha el administrador de varios sitios de AEM.
feature: Administrador de varios sitios
role: Administrator
exl-id: 61b8ded8-3b9e-423f-85a9-7280e1a721cc
translation-type: tm+mt
source-git-commit: 184de9c1391ade3abbf2c6d73f09a324e6fa7e3e
workflow-type: tm+mt
source-wordcount: '1436'
ht-degree: 0%

---

# Prácticas recomendadas de MSM {#msm-best-practices}

## General {#general}

MSM es un marco configurable para automatizar la implementación de contenido. Las implementaciones suelen incluir partes importantes de un sitio web y abarcan organizaciones y zonas geográficas. Por lo tanto, es muy recomendable planificar las implementaciones de MSM con el cuidado con que planifica el sitio web:

* **estructura del plan y flujos de contenido** cuidadosamente antes de iniciar la implementación.
* **Personalice tanto como sea necesario, pero tan poco como sea posible.** Aunque MSM admite un alto grado de personalización (p. ej., configuraciones de implementación), la práctica recomendada para el rendimiento, la fiabilidad y la actualización del sitio web es minimizar la personalización.
* Establezca un modelo de **administración** antes y capacite a los usuarios en consecuencia para garantizar el éxito. Una práctica recomendada desde el punto de vista del gobierno es **minimizar la autoridad que los productores de contenido local tienen** para asignar/conectar contenido a otros usuarios locales y sus respectivas Live Copies. Esto se debe a que las herencias encadenadas y no gobernadas pueden aumentar significativamente la complejidad de una estructura de MSM y comprometer su rendimiento y fiabilidad.
* Una vez que existe un plan para su estructura, flujos de contenido, automatización y administración, **prototipo y pruebe a fondo su sistema** antes de iniciar una implementación activa.
* Tenga en cuenta que los **asesores de Adobe y los integradores de sistemas líderes** tienen una planificación profunda de la experiencia e implementan la automatización de contenido con MSM, de modo que pueden ayudarle a empezar con su proyecto MSM y a lo largo de toda su implementación.

## Configuraciones de fuentes y modelos de Live Copy {#live-copy-sources-and-blueprint-configurations}

Tenga en cuenta que se puede crear una Live Copy utilizando [páginas normales](creating-live-copies.md#creating-a-live-copy-of-a-page) o una [configuración de modelo](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Ambos son casos de uso válidos.

Los beneficios adicionales de utilizar una configuración de modelo son que:

* Permita que el autor utilice la opción **Rollout** en un modelo para insertar explícitamente modificaciones en Live Copies que heredan de este modelo.
* Permita que el autor utilice **Crear sitio** para poder seleccionar idiomas fácilmente y configurar la estructura de Live Copy.
* Defina una configuración de lanzamiento predeterminada para Live Copies que tengan una relación con el modelo.

En caso de que no se haga referencia a una configuración de modelo, las implementaciones solo se pueden iniciar desde las propias Live Copies, lo que básicamente elimina el contenido del origen.

Al crear un nuevo sitio con Live Copy, resulta ventajoso crear configuraciones de modelo para garantizar la disponibilidad del conjunto de funciones MSM completo.

>[!NOTE]
>
> Tenga en cuenta que los CUG de la ficha Permisos no se pueden desplegar en Live Copies desde modelos. Planee esto al configurar Live Copy.

## Sincronización de componentes y contenedores {#components-and-container-synchronization}

En general, la regla de implementación en MSM con respecto a la sincronización de componentes es:

* Los componentes se implementan sincronizando cualquier recurso contenido en el modelo.
* Los contenedores solo sincronizan el recurso actual.

Esto significa que los componentes se tratan como un agregado y, en un despliegue, el componente en sí y todos sus elementos secundarios se sustituyen por los de los modelos. Esto significa que si se agrega un recurso a un componente de este tipo localmente, se perderá por el contenido del modelo al implementarse.

Para admitir el anidado de componentes de modo que los componentes añadidos localmente se mantengan en un despliegue, el componente debe declararse como contenedor.

>[!NOTE]
>
>Agregue la propiedad `cq:isContainer` al componente para designarlo como contenedor.

## Crear sitio {#create-site}

Tenga en cuenta que AEM tiene dos enfoques principales para crear Live Copies:

* Al [crear una Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page): este enfoque puede considerarse más genérico, ya que le permite crear Live Copies desde cualquier página. La estructura de contenido de una Live Copy coincide exactamente con el origen.

* Al [crear un sitio](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) : se trata de un enfoque más especializado, principalmente para crear sitios web con una estructura multilingüe.

A continuación se indican algunas consideraciones que se deben tener en cuenta al crear un sitio:

* Para crear un nuevo sitio, necesita una [configuración de modelo](creating-live-copies.md#managing-blueprint-configurations).
* Para permitir la selección de rutas de idioma para crear en un sitio nuevo, las raíces de idioma correspondientes deben existir en el modelo (fuente).
* Una vez que se ha creado un [nuevo sitio como Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (con **Crear** y, a continuación, **Sitio**), los dos primeros niveles de esta Live Copy son *superficial*. Los elementos secundarios de la página no pertenecen a la relación de vida, pero se seguirá desplegando si se encuentra una relación de vida que coincida con el déclencheur.

Es útil evitar:

* Adición manual de idiomas en el modelo (por debajo del primer nivel).
* Añadir contenido manualmente directamente debajo de la raíz del idioma, ya que esto no provoca que se transfiera automáticamente este nuevo contenido a Live Copy en el despliegue.

## MSM y sitios web multilingües {#msm-and-multilingual-websites}

MSM puede ayudar en la creación de sitios web multilingües de dos maneras:

Al crear maestros de idiomas, tenga en cuenta lo siguiente:

* Aunque el propio MSM **no proporciona traducción de contenido**, se puede integrar con conectores de traducción de terceros que sí proporcionan. Tenga en cuenta que:
   * MSM le permite cancelar la herencia en el nivel de página o componente. Esto ayuda a evitar sobrescribir el contenido traducido (de una Live Copy, con contenido aún no traducido de un modelo) en la próxima implementación.
      * Algunos conectores de traducción de terceros automatizan esta administración de las heredaciones de MSM.
      * Consulte a su proveedor de servicios de traducción para obtener más información.
      * Un enfoque alternativo para crear y traducir maestros de idiomas es usar copias de idiomas junto con AEM marco de integración de traducción listo para usar.

Para obtener más información, consulte [Traducción de contenido para sitios multilingües](/help/sites-cloud/administering/translation/overview.md) y las [Prácticas recomendadas de traducción.](/help/sites-cloud/administering/translation/best-practices.md)

## Cambios de estructura y lanzamientos {#structure-changes-and-rollouts}

Las modificaciones en la estructura de contenido de un modelo o árbol de origen se reflejan de forma diferente en una Live Copy. Esto depende del tipo de modificación:

* **** Al crear páginas nuevas en un modelo, las páginas correspondientes se crearán en Live Copies después de la implementación con la configuración de lanzamiento estándar.
* **** Al eliminar páginas en un modelo, las páginas correspondientes se eliminarán de Live Copies después de la implementación con la configuración de lanzamiento estándar.
* **** Al mover páginas en un modelo, las páginas correspondientes  **** no se moverán en Live Copies después de la implementación con la configuración de lanzamiento estándar:
   * El motivo de este comportamiento es que un movimiento de página incluye implícitamente una eliminación de página. Esto podría provocar un comportamiento inesperado al publicar, ya que al eliminar páginas en el autor se desactiva automáticamente el contenido correspondiente al publicar. Esto también puede tener un efecto adicional en elementos relacionados, como vínculos, marcadores, etc.
      * La herencia de contenido en las respectivas páginas de Live Copy se actualiza para reflejar la nueva ubicación de sus orígenes en el modelo.
      * Para realizar el paso completo de una página de un modelo a Live Copies, considere las [prácticas recomendadas de movimiento de página.](#page-move)

### Prácticas recomendadas para mover páginas {#page-move}

Cuando considere la posibilidad de mover páginas en una Live Copy, considere la siguiente práctica recomendada.

>[!NOTE]
>
>Lo siguiente solo funcionará con el [déclencheur de lanzamiento de activación](live-copy-sync-config.md#rollout-triggers).

1. Cree una configuración de lanzamiento personalizada.
   * Esta nueva configuración debe incluir la acción `PageMoveAction`.
   * No agregue otras acciones a esta configuración.
1. Coloque la nueva configuración.
   * Para desplegar completamente la página, mueva mientras elimina las páginas respectivas en su antigua ubicación en Live Copy:
      * Coloque la configuración recién creada antes de la configuración de lanzamiento estándar. La configuración de lanzamiento estándar se encargará de eliminar las páginas en sus ubicaciones antiguas.
      * Para desplegar la página, mueva mientras mantiene las páginas respectivas en sus antiguas ubicaciones en Live Copies (básicamente duplicando el contenido):
         * Coloque la configuración recién creada después de la configuración de lanzamiento estándar. Esto garantizará que no se elimine contenido en Live Copy ni se desactive de la publicación.

## Personalización de lanzamientos {#customizing-rollouts}

Las configuraciones de implementación de MSM son altamente personalizables. Debe tener en cuenta que la automatización de las implementaciones puede tener consecuencias de gran alcance. Como práctica recomendada, debe planificar con mucho cuidado antes de realizar las siguientes actividades:

* Automatización de lanzamientos como con [déclencheur onModify](#onmodify)
* Personalización de [tipos de nodo/propiedades](#node-types-properties)
* Inicio de flujos de trabajo subsiguientes
* Activación de contenido como parte de lanzamientos

### onModify {#onmodify}

Al utilizar el [déclencheur de implementación](live-copy-sync-config.md#rollout-triggers) `onModify` debe tener en cuenta que:

* La automatización de los lanzamientos con déclencheur `onModify` puede tener un impacto negativo en el rendimiento de la creación, ya que déclencheur los lanzamientos después de cada modificación de página.
* El resultado de la implementación puede diferir del esperado, ya que:
   * No se puede especificar el orden de los eventos de modificación resultantes.
   * La arquitectura basada en eventos no puede garantizar la secuencia de eventos pasados al administrador de implementación.
* El uso de una configuración de lanzamiento de este tipo podría provocar conflictos de confirmación si se producen actualizaciones simultáneas del mismo recurso.

Por lo tanto, se recomienda utilizar únicamente déclencheur `onModify` si los beneficios del inicio automático de la implementación superan cualquier posible problema de rendimiento.

### Tipos de nodo/Propiedades {#node-types-properties}

Además de personalizar las acciones de implementación, MSM también le permite personalizar las propiedades de los nodos que se están implementando. La configuración [MSM OSGi permite excluir tipos de nodos](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) de la copia desde el origen a Live Copy.

## Información adicional {#further-information}

Consulte los siguientes artículos para obtener más información sobre MSM y Live Copy.

* [Creación y sincronización de Live Copies](creating-live-copies.md)
* [Consola de información general de Live Copy](live-copy-overview.md)
* [Configuración de la sincronización de Live Copy](live-copy-sync-config.md)
* [Conflictos de implementación de MSM](rollout-conflicts.md)
