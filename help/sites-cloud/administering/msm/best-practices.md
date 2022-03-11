---
title: Prácticas recomendadas de MSM
description: Conozca las prácticas recomendadas recopiladas por los equipos de consultoría e ingeniería de Adobe para ayudarle a poner en marcha el administrador de varios sitios de AEM.
feature: Multi Site Manager
role: Admin
exl-id: 61b8ded8-3b9e-423f-85a9-7280e1a721cc
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 1%

---

# Prácticas recomendadas de MSM {#msm-best-practices}

## General {#general}

MSM es un marco configurable para automatizar la implementación de contenido. Implementations often involve major portions of a website and span organizations and geographies. Por lo tanto, es muy recomendable planificar las implementaciones de MSM con el cuidado con que planifica el sitio web:

* Carefully **plan structure and content flows** before starting implementation.
* **Personalice tanto como sea necesario, pero tan poco como sea posible.** While MSM supports a high degree of customization (e.g. rollout configurations), typically the best practice for the performance, reliability and upgradeability of your website is to minimize customization.
* Establezca un **gobierno** de forma temprana, y capacite a los usuarios en consecuencia para garantizar el éxito. Una práctica recomendada desde el punto de vista de la gobernanza es **minimizar la autoridad que tienen los productores de contenido local** para asignar o conectar contenido a otros usuarios locales y sus Live Copies respectivos. Esto se debe a que las herencias encadenadas y no gobernadas pueden aumentar significativamente la complejidad de una estructura de MSM y comprometer su rendimiento y fiabilidad.
* Una vez que existe un plan para su estructura, flujos de contenido, automatización y control, **prototipo y prueba exhaustivamente su sistema** antes de iniciar una implementación activa.
* Tenga en cuenta que **Consultoría de Adobe e integradores de sistemas líderes** tienen una amplia experiencia en la planificación e implementación de la automatización de contenido con MSM, por lo que pueden ayudarle a empezar con su proyecto MSM y a lo largo de toda su implementación.

## Fuentes de Live Copy y configuraciones de modelo {#live-copy-sources-and-blueprint-configurations}

Tenga en cuenta que se puede crear una Live Copy mediante una de las acciones siguientes: [páginas regulares](creating-live-copies.md#creating-a-live-copy-of-a-page) o [configuración de modelo](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Ambos son casos de uso válidos.

Los beneficios adicionales de utilizar una configuración de modelo son que:

* Permita que el autor use el **Despliegue** en un modelo para insertar explícitamente modificaciones en Live Copies que heredan de este modelo.
* Permita que el autor utilice **Crear sitio** para seleccionar idiomas fácilmente y configurar la estructura de Live Copy.
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
>Añadir la propiedad `cq:isContainer` al componente para designarlo como contenedor.

## Crear sitio {#create-site}

Tenga en cuenta que AEM tiene dos enfoques principales para crear Live Copies:

* When [creación de una Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-page) : este enfoque puede considerarse más genérico y le permite crear Live Copies desde cualquier página. La estructura de contenido de una Live Copy coincide exactamente con el origen.

* When [creación de un sitio](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) - Se trata de un enfoque más especializado, principalmente para crear sitios web con una estructura multilingüe.

A continuación se indican algunas consideraciones que se deben tener en cuenta al crear un sitio:

* Para crear un nuevo sitio, necesita una [configuración de modelo](creating-live-copies.md#managing-blueprint-configurations).
* Para permitir la selección de rutas de idioma para crear en un sitio nuevo, las raíces de idioma correspondientes deben existir en el modelo (fuente).
* Una vez [se ha creado un nuevo sitio como Live Copy](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (mediante **Crear**, luego **Sitio**), los dos primeros niveles de esta Live Copy son *superficial*. Los elementos secundarios de la página no pertenecen a la relación de vida, pero se seguirá desplegando si se encuentra una relación de vida que coincida con el déclencheur.

Es útil evitar:

* Adición manual de idiomas en el modelo (por debajo del primer nivel).
* Manually adding content directly below the language root, as this does not result in automatically carrying this new content over to the Live Copy on rollout.

## MSM y sitios web multilingües {#msm-and-multilingual-websites}

MSM puede ayudar en la creación de sitios web multilingües de dos maneras:

Al crear maestros de idiomas, tenga en cuenta lo siguiente:

* Mientras que MSM en sí **no proporciona traducción de contenido**, se puede integrar con conectores de traducción de terceros que sí lo hagan. Please note that:
   * MSM le permite cancelar la herencia en el nivel de página o componente. Esto ayuda a evitar sobrescribir el contenido traducido (de una Live Copy, con contenido aún no traducido de un modelo) en la próxima implementación.
      * Algunos conectores de traducción de terceros automatizan esta administración de las heredaciones de MSM.
      * Consulte a su proveedor de servicios de traducción para obtener más información.
      * Un enfoque alternativo para crear y traducir maestros de idiomas es usar copias de idiomas junto con AEM marco de integración de traducción listo para usar.

Para obtener más información, consulte [Traducción de contenido para sitios multilingües](/help/sites-cloud/administering/translation/overview.md) y [Prácticas recomendadas de traducción.](/help/sites-cloud/administering/translation/best-practices.md)

## Cambios y lanzamientos de la estructura {#structure-changes-and-rollouts}

Las modificaciones en la estructura de contenido de un modelo o árbol de origen se reflejan de forma diferente en una Live Copy. This is dependent on the modification type:

* **Creación** las páginas nuevas de un modelo harán que las páginas correspondientes se creen en Live Copies después de la implementación con la configuración de lanzamiento estándar.
* **Deleting** pages in a blueprint will result in corresponding pages being deleted from Live Copies after rollout with standard rollout configuration.
* **Mover** páginas en un modelo **not** como resultado, las páginas correspondientes se mueven en Live Copies después de la implementación con la configuración de lanzamiento estándar:
   * El motivo de este comportamiento es que un movimiento de página incluye implícitamente una eliminación de página. This could potentially lead to unexpected behavior on publish, as deleting pages on author automatically deactivates corresponding content on publish. Esto también puede tener un efecto adicional en elementos relacionados, como vínculos, marcadores, etc.
      * Content inheritance in the respective Live Copy pages is updated to reflect the new location of their sources in the blueprint.
      * To fully realize a page move from a blueprint to Live Copies, consider the [page move best practices.](#page-move)

### Page Move Best Practices {#page-move}

Cuando considere la posibilidad de mover páginas en una Live Copy, considere la siguiente práctica recomendada.

>[!NOTE]
>
>The following will work only with the [On Rollout trigger](live-copy-sync-config.md#rollout-triggers).

1. Cree una configuración de lanzamiento personalizada.
   * Esta nueva configuración debe incluir la acción `PageMoveAction`.
   * No agregue otras acciones a esta configuración.
1. Coloque la nueva configuración.
   * To fully roll out the page move while deleting respective pages at their old location in the Live Copy:
      * Coloque la configuración recién creada antes de la configuración de lanzamiento estándar. The standard rollout configuration will take care of deleting the pages in their old locations.
      * Para desplegar la página, mueva mientras mantiene las páginas respectivas en sus antiguas ubicaciones en Live Copies (básicamente duplicando el contenido):
         * Coloque la configuración recién creada después de la configuración de lanzamiento estándar. Esto garantizará que no se elimine contenido en Live Copy ni se desactive de la publicación.

## Personalización de lanzamientos {#customizing-rollouts}

Las configuraciones de implementación de MSM son altamente personalizables. Debe tener en cuenta que la automatización de las implementaciones puede tener consecuencias de gran alcance. Como práctica recomendada, debe planificar con mucho cuidado antes de realizar las siguientes actividades:

* Automatización de lanzamientos como con [déclencheur onModify](#onmodify)
* Personalización [tipos de nodo/propiedades](#node-types-properties)
* Inicio de flujos de trabajo subsiguientes
* Activación de contenido como parte de lanzamientos

### onModify {#onmodify}

Al usar la variable [déclencheur de implementación](live-copy-sync-config.md#rollout-triggers) `onModify` debe tener en cuenta que:

* Automatización de lanzamientos con `onModify` Los déclencheur pueden tener un impacto negativo en el rendimiento de la creación, ya que déclencheur los lanzamientos después de cada modificación de página.
* El resultado de la implementación puede diferir del esperado, ya que:
   * No se puede especificar el orden de los eventos de modificación resultantes.
   * La arquitectura basada en eventos no puede garantizar la secuencia de eventos pasados al administrador de implementación.
* El uso de una configuración de lanzamiento de este tipo podría provocar conflictos de confirmación si se producen actualizaciones simultáneas del mismo recurso.

Por lo tanto, se recomienda usar únicamente `onModify` déclencheur si los beneficios del inicio automático de la implementación superan cualquier problema de rendimiento potencial.

### Tipos de nodo/Propiedades {#node-types-properties}

Además de personalizar las acciones de implementación, MSM también le permite personalizar las propiedades de los nodos que se están implementando. La variable [La configuración OSGi de MSM le permite excluir tipos de nodos](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) de copiarse del origen a Live Copy.

## Información adicional {#further-information}

Consulte los siguientes artículos para obtener más información sobre MSM y Live Copy.

* [Creación y sincronización de Live Copies](creating-live-copies.md)
* [Información general de Live Copy](live-copy-overview.md)
* [Configuración de la sincronización de Live Copy](live-copy-sync-config.md)
* [Conflictos de implementación de MSM](rollout-conflicts.md)
