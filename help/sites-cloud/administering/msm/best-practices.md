---
title: Prácticas recomendadas de MSM
description: Conozca las prácticas recomendadas recopiladas por los equipos de consultoría e ingeniería de Adobe para ayudarle a poner en marcha el Administrador de varios sitios AEM.
feature: Multi Site Manager
role: Admin
exl-id: 61b8ded8-3b9e-423f-85a9-7280e1a721cc
source-git-commit: 47910a27118a11a8add6cbcba6a614c6314ffe2a
workflow-type: tm+mt
source-wordcount: '1434'
ht-degree: 100%

---

# Prácticas recomendadas de MSM {#msm-best-practices}

## General {#general}

MSM es un marco de trabajo configurable para automatizar la implementación de contenido. Las implementaciones suelen incluir partes importantes de un sitio web y abarcan organizaciones y áreas geográficas. Por lo tanto, es muy recomendable planificar las implementaciones de MSM con el cuidado con que planifica el sitio web:

* Planifique con cuidado la **estructura y los flujos de contenido** antes de iniciar la implementación.
* **Personalice tanto como sea necesario, pero tan poco como sea posible.** Aunque MSM admite un alto grado de personalización (p. ej., configuraciones de despliegue), la práctica recomendada normalmente para el rendimiento, la fiabilidad y la actualización de su sitio web es minimizar la personalización.
* Establezca un modelo de **gobernanza** desde el principio, y capacite a los usuarios debidamente para garantizar el éxito. Una práctica recomendada desde el punto de vista de la gobernanza es **minimizar la autoridad que tienen los productores de contenido local** para asignar o conectar contenido a otros usuarios locales y a sus respectivas Live Copies. Esto se debe a que las herencias encadenadas no gobernadas pueden aumentar significativamente la complejidad de una estructura de MSM y comprometer su rendimiento y fiabilidad.
* Una vez que existe un plan para la estructura, los flujos de contenido, la automatización y la gobernanza, **haga un prototipo y compruebe exhaustivamente su sistema** antes de iniciar una implementación activa.
* Tenga en cuenta que la **consultoría de Adobe y los integradores de sistemas líderes** tienen una amplia experiencia en la planificación e implementación de la automatización de contenido con MSM, por lo que pueden ayudarle a empezar su proyecto MSM y a lo largo de toda su implementación.

## Fuentes de Live Copy y configuraciones de modelo {#live-copy-sources-and-blueprint-configurations}

Tenga en cuenta que se puede crear una Live Copy mediante una de las acciones siguientes: [páginas regulares](creating-live-copies.md#creating-a-live-copy-of-a-page) o [configuración de modelo](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Ambos son casos de uso válidos.

Los beneficios adicionales de utilizar una configuración de modelo son que:

* Permiten que el autor use la opción de **Despliegue** en un modelo para insertar explícitamente modificaciones a Live Copies que heredan de este modelo.
* Permiten que el autor utilice **Crear sitio** para seleccionar idiomas fácilmente y configurar la estructura de la Live Copy.
* Definen una configuración de despliegue predeterminada para Live Copies que tengan una relación con el modelo.

En caso de que no se haga referencia a una configuración de modelo, los despliegues solo se pueden iniciar desde las propias Live Copies, lo que básicamente extrae contenido de la fuente.

Al crear un nuevo sitio con Live Copy, resulta ventajoso crear configuraciones de modelo para garantizar la disponibilidad del conjunto completo de funciones MSM.

>[!NOTE]
>
> Tenga en cuenta que los CUG de la pestaña Permisos no se pueden desplegar en Live Copies desde modelos. Tenga en cuenta esto al configurar Live Copy.

## Sincronización de componentes y contenedores {#components-and-container-synchronization}

En general, la regla de despliegue en MSM con respecto a la sincronización de componentes es:

* Los componentes se despliegan sincronizando cualquier recurso contenido en el modelo.
* Los contenedores solo sincronizan el recurso actual.

Esto significa que los componentes se tratan como un acumulado y, en un despliegue, el componente en sí y todos sus elementos secundarios se sustituyen por los de los modelos. Esto significa que si se agrega un recurso a un componente de este tipo localmente, se reemplazará por el contenido del modelo al desplegarse.

Para admitir el anidado de componentes de modo que los componentes añadidos localmente se mantengan en un despliegue, el componente debe declararse como contenedor.

>[!NOTE]
>
>Añada la propiedad `cq:isContainer` al componente para designarlo como contenedor.

## Crear sitio {#create-site}

Tenga en cuenta que AEM tiene dos enfoques principales para crear Live Copies:

* Al [crear una Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page): este enfoque puede considerarse más genérico y le permite crear Live Copies desde cualquier página. La estructura de contenido de una Live Copy coincide exactamente con el origen.

* Al [crear un sitio](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration): se trata de un enfoque más especializado, principalmente para crear sitios web con una estructura multilingüe.

A continuación se indican algunas consideraciones que se deben tener en cuenta al crear un sitio:

* Para crear un nuevo sitio, necesita una [configuración de modelo](creating-live-copies.md#managing-blueprint-configurations).
* Para permitir la selección de rutas de idioma a crear en un sitio nuevo, las raíces de idioma correspondientes deben existir en el modelo (fuente).
* Una vez [se ha creado un nuevo sitio como Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (mediante **Crear**, luego **Sitio**), los dos primeros niveles de esta Live Copy son *superficiales*. Los elementos secundarios de la página no pertenecen a la relación dinámica, pero se desplegará si se encuentra una relación dinámica que coincida con el activador.

Es útil evitar lo siguiente:

* Añadir manualmente idiomas en el modelo (por debajo del primer nivel).
* Añadir manualmente contenido directamente debajo de la raíz del idioma, ya que esto no provoca que se transfiera automáticamente este nuevo contenido a Live Copy en el despliegue.

## MSM y sitios web multilingües {#msm-and-multilingual-websites}

MSM puede ayudar en la creación de sitios web multilingües de dos maneras:

Al crear maestros de idiomas, tenga en cuenta lo siguiente:

* Mientras que MSM en sí **no proporciona traducción de contenido**, se puede integrar con conectores de traducción de terceros que sí lo hagan. Tenga en cuenta lo siguiente:
   * MSM le permite cancelar la herencia en el nivel de página o componente. Esto evita sobrescribir el contenido traducido (de una Live Copy, con contenido aún no traducido de un modelo) en el próximo despliegue.
      * Algunos conectores de traducción de terceros automatizan esta administración de las herencias de MSM.
      * Consulte a su proveedor de servicios de traducción para obtener más información.
      * Un enfoque alternativo para crear y traducir maestros de idiomas es usar copias de idiomas junto con el marco de trabajo de integración de traducción listo para usar de AEM.

Para obtener más información, consulte [Traducción de contenido para sitios multilingües](/help/sites-cloud/administering/translation/overview.md) y [Prácticas recomendadas de traducción.](/help/sites-cloud/administering/translation/best-practices.md)

## Cambios y despliegues de la estructura {#structure-changes-and-rollouts}

Las modificaciones en la estructura de contenido de un modelo o árbol de fuentes se reflejan de forma diferente en una Live Copy. Esto depende del tipo de modificación:

* **La creación** de páginas nuevas en un modelo hará que las páginas correspondientes se creen en Live Copies después del despliegue con la configuración de despliegue estándar.
* **La eliminación** de páginas en un modelo hará que las páginas correspondientes se eliminen de las Live Copies después del despliegue con la configuración de despliegue estándar.
* **Mover** páginas a un modelo **no** hará que las páginas correspondientes se muevan a Live Copies después del despliegue con la configuración de despliegue estándar:
   * El motivo de este comportamiento es que mover una página incluye implícitamente eliminar una página. Esto podría provocar un comportamiento inesperado al publicar, ya que al eliminar páginas en el autor se desactiva automáticamente el contenido correspondiente al publicar. Esto también puede tener un efecto adicional en elementos relacionados, como vínculos, marcadores, etc.
      * La herencia de contenido en las respectivas páginas de Live Copy se actualiza para reflejar la nueva ubicación de sus fuentes en el modelo.
      * Para mover por completo una página de un modelo a Live Copies, tenga en cuenta las [prácticas recomendadas para mover páginas.](#page-move)

### Prácticas recomendadas para mover páginas {#page-move}

Cuando considere la posibilidad de mover páginas a una Live Copy, tenga en cuenta la siguiente práctica recomendada.

>[!NOTE]
>
>Lo siguiente solo funcionará con el [Activador de despliegue](live-copy-sync-config.md#rollout-triggers).

1. Cree una configuración de despliegue personalizada.
   * Esta nueva configuración debe incluir la acción `PageMoveAction`.
   * No agregue otras acciones a esta configuración.
1. Coloque la nueva configuración.
   * Para desplegar completamente la página, mueva mientras elimina las páginas respectivas en su antigua ubicación en Live Copy:
      * Coloque la configuración recién creada antes de la configuración de despliegue estándar. La configuración de despliegue estándar se encargará de eliminar las páginas en sus ubicaciones antiguas.
      * Para desplegar la página, mueva las páginas mientras mantiene las respectivas en sus antiguas ubicaciones en Live Copies (básicamente duplicando el contenido):
         * Coloque la configuración recién creada después de la configuración de despliegue estándar. Esto garantizará que no se elimine contenido en la Live Copy ni se desactive de la publicación.

## Personalización de despliegues {#customizing-rollouts}

Las configuraciones de despliegue de MSM son altamente personalizables. Debe tener en cuenta que la automatización de los despliegues puede tener consecuencias de gran alcance. Como práctica recomendada, debe planificar con mucho cuidado antes de realizar las siguientes actividades:

* Automatización de despliegues como [activadores onModify](#onmodify)
* Personalización de [tipos de nodo/propiedades](#node-types-properties)
* Inicio de flujos de trabajo subsiguientes
* Activación de contenido como parte de despliegues

### onModify {#onmodify}

Al usar el [activador de despliegue](live-copy-sync-config.md#rollout-triggers) `onModify` debe tener en cuenta lo siguiente:

* Automatizar despliegues con activadores `onModify` puede tener un impacto negativo en el rendimiento de la creación, ya que activan despliegues después de cada modificación de la página.
* El resultado del despliegue puede diferir del esperado, ya que:
   * No se puede especificar el orden de los eventos de modificación resultantes.
   * La arquitectura basada en eventos no puede garantizar la secuencia de eventos transferidos al administrador de despliegue.
* El uso de una configuración de despliegue de este tipo podría provocar conflictos de confirmación si se producen actualizaciones simultáneas del mismo recurso.

Por lo tanto, se recomienda usar únicamente activadores `onModify` si los beneficios del inicio del despliegue automático superan cualquier problema de rendimiento potencial.

### Tipos de nodo/Propiedades {#node-types-properties}

Además de personalizar las acciones de despliegue, MSM también le permite personalizar las propiedades de los nodos que se están desplegando. La [configuración OSGi de MSM le permite excluir tipos de nodos](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) de copiarse de la fuente a Live Copy.

## Información adicional {#further-information}

Consulte los siguientes artículos para obtener más información sobre MSM y Live Copy.

* [Creación y sincronización de Live Copies](creating-live-copies.md)
* [Información general de Live Copy](live-copy-overview.md)
* [Configuración de la sincronización de Live Copy](live-copy-sync-config.md)
* [Conflictos de despliegue de MSM](rollout-conflicts.md)
