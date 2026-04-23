---
title: Reutilización de fragmentos de contenido mediante MSM y Live Copies
description: Obtenga información acerca del uso de la funcionalidad Live Copy de MSM para utilizar el mismo contenido de fragmento de contenido, o similar, en varias ubicaciones, mientras se sincroniza con el contenido de origen.
badgeSaas: label="AEM Sites" type="Positive" tooltip="(Se aplica a AEM Sites)."
feature: Content Fragments
role: User
solution: Experience Manager Sites
hide: true
hidefromtoc: true
index: false
source-git-commit: 85b72909597a95531aea51719c841bc5db9c1a21
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 3%

---

# Reutilización de fragmentos de contenido mediante MSM {#reuse-content-fragments-using-msm}

El Administrador de varios sitios (MSM) y la funcionalidad de Live Copy le permiten utilizar el mismo contenido en varias ubicaciones y, al mismo tiempo, sincronizarse con el contenido de origen.

<!-- CQDOC-23473 - feature is currently beta so page is hidden, see metadata -->
<!-- CQDOC-23473 - screenshots -->
<!-- CQDOC-23473 - only mentioned once in ToC, add entries -->
<!-- CQDOC-23473 - will work on folders -->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!CAUTION]
>
>MSM desde la consola Fragmento de contenido es actualmente la funcionalidad de Beta y solo está disponible para clientes específicos.
>
>MSM para fragmentos de contenido también está disponible al usar fragmentos de contenido a través de la consola **Assets**.

* Con Live Copies de MSM puede:
   * Crear contenido una vez
   * Reutilice este contenido en otras áreas del mismo sitio, en otros sitios o en aplicaciones.
* A continuación, MSM mantiene las relaciones activas entre el contenido de origen y sus Live Copies para lo siguiente:
   * Al cambiar el contenido de origen, se sincronizan el origen y las Live Copies.
   * Puede realizar ajustes solo en el contenido de las Live Copies desconectando la relación activa para subfragmentos o componentes individuales.

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

Para obtener una descripción detallada de los conceptos de MSM, consulte Reutilización del contenido: administrador de varios sitios y Live Copy.

<!--
For a detailed overview of MSM concepts see [Reusing Content: Multi Site Manager and Live Copy](/help/sites-cloud/administering/msm/overview.md).
-->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>La funcionalidad Administrador de varios sitios (MSM) de Adobe Experience Manager permite a los usuarios reutilizar contenido creado una vez y reutilizado en varias ubicaciones web.

<!--
>[!NOTE]
>
>[Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md) functionality in Adobe Experience Manager enables users to reuse content that is authored once and then reused across multiple web-locations. 
-->

Con MSM para fragmentos de contenido puede:

* Cree fragmentos de contenido una vez y luego realice copias (vinculadas) de estos fragmentos para reutilizarlos en otras áreas del sitio o la aplicación.
* Mantenga varias copias sincronizadas actualizando la copia de origen una vez y, a continuación, inserte los cambios en las copias (activas).
* Realice cambios locales suspendiendo temporal o permanentemente el vínculo entre los fragmentos principales y secundarios, ya sea por completo o para sus variaciones o campos.

MSM para fragmentos de contenido, combinado con la funcionalidad dentro del Editor de fragmentos de contenido, le permite romper y restablecer la herencia en el nivel de campo.

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>Esta página cubre la funcionalidad de MSM al usar la consola **Fragmentos de contenido**.
>
>MSM para fragmentos de contenido también está disponible al usar fragmentos de contenido a través de la consola **Assets**.

<!--
>[!NOTE]
>
>This page covers MSM functionality when using the **Content Fragments** console.
>
>MSM for Content Fragments is also available when using [Content Fragments via the **Assets** console](/help/assets/content-fragments/content-fragments-msm.md). 
-->

## Crear una Live Copy {#create-a-live-copy}

<!-- CQDOC-23473 - exclude children or referenced content fragments? -->

Para crear una Live Copy del fragmento de contenido:

1. En la consola Fragmento de contenido vaya a la ubicación del fragmento.
1. Seleccione el fragmento.
1. Seleccione **Crear Live Copy** en la barra de herramientas superior.
1. En el cuadro de diálogo que se abre, especifique el destino y continúe con **Siguiente**.
1. Especifique las propiedades. Puede especificar el título, el nombre y si la Live Copy debe excluir los elementos secundarios (fragmentos anidados).
1. Continuar con **Siguiente**.
1. Seleccione si desea que la Live Copy se cree inmediatamente (**Ahora**) o en una fecha y hora **Más tarde**.
1. Confirme con **Crear Live Copy**.

   <!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

   >[!CAUTION]
   >
   >Si desea utilizar MSM para crear copias de fragmentos de contenido), cualquier restricción **Única** debe eliminarse de cualquier tipo de datos utilizado en los respectivos modelos de fragmentos de contenido.

   <!--
   >[!CAUTION]
   >
   >If you want to use MSM to create copies of Content Fragments), then any **Unique** constraints should be removed from any Data Types used in the respective [Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md).
   -->

## Ver propiedades y estado {#view-properties-and-status}

Para ver las propiedades y el estado del origen y de la Live Copy:

1. En la consola Fragmento de contenido vaya a la ubicación del fragmento.
1. Seleccione el fragmento.
1. Seleccione el icono de información (i) en la columna **Título** del fragmento.
Se abrirá el panel de información derecho.
1. Seleccione la ficha para **Detalles de Live Copy**.

   ![Información sobre una Live Copy](/help/sites-cloud/administering/content-fragments/assets/cf-msm-information.png)

## Propagación de modificaciones {#propagate-modifications}

Para propagar modificaciones entre el origen y la Live Copy.

### Sincronizar {#synchronize}

Para almacenar en déclencheur una sincronización que extrae las actualizaciones de contenido de su Live Copy al origen:

1. En la consola Fragmento de contenido vaya a la ubicación del origen del fragmento.
1. Seleccione el fragmento.
1. En la barra de herramientas, seleccione **Sincronizar**.
1. Confirme **Sincronizar** en el cuadro de diálogo.

### Despliegue {#rollout}

Para almacenar en déclencheur un despliegue que inserte las actualizaciones de origen en Live Copy:

1. En la consola Fragmento de contenido vaya a la ubicación de la Live Copy del fragmento.
1. Seleccione el fragmento.
1. Seleccione **Despliegue** en la barra de herramientas. Se abrirá el asistente para guiarle a través del proceso.
1. Seleccione las Live Copies que se incluirán en el despliegue y **Continuar**.
1. Programe el despliegue inmediatamente (**Ahora**) o **Más tarde**.
1. **Continuar** según corresponda.

<!-- CQDOC-23473 - feature is beta, is in authoring so remove here when GA -->

## Cancele y vuelva a la herencia en el editor {#cancel-and-revert-to-inheritance-in-the-editor}

La herencia es el mecanismo por el que el contenido se puede insertar automáticamente de un fragmento a otro. Los campos heredados y las variaciones pueden ser el producto de Multi-Site Management.

Puede cancelar (y luego revertir) la herencia en el editor de fragmentos de contenido. Según el contexto, esto puede estar disponible para una variación o un campo individual, si el fragmento forma parte de una Live Copy.

Por ejemplo:

* Cancelar herencia

  ![Icono Cancelar herencia](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-cancel-inheritance.png)

* Revertir a herencia (si la herencia ya se ha cancelado)

  ![Icono Revertir a herencia](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-revert-to-inheritance.png)

<!-- CQDOC-23473 - feature is currently beta reinstate Note for GA -->

<!--
## Cancel, and revert to, inheritance {#cancel-and-reinstate-inheritance}

Inheritance is the mechanism where content can be automatically pushed from one fragment to another. Inherited fields, and variations, can be the product of Multi-Site Management.

You can cancel (then revert) the inheritance. Depending on the context, this can be available for a variation, or an individual field, if the fragment is part of a live copy.
-->

<!--
>[!NOTE]
>
>For more details see [Cancel, and revert to, inheritance in the editor](/help/sites-cloud/administering/content-fragments/authoring.md#cancel-and-revert-to-inheritance).
-->

## Comparar MSM para fragmentos de contenido y páginas de sitios {#compare-msm-for-content-fragments-and-sites-pages}

<!-- CQDOC-23473 - needs a detailed review -->

En la mayoría de los casos, MSM para fragmentos de contenido coincide con el comportamiento de MSM para la funcionalidad de páginas de sitios. Algunas diferencias clave que hay que tener en cuenta son:

* El modelo en MSM para páginas de Sites se denomina fuente de Live Copy en MSM para fragmentos de contenido.
* En el caso de las páginas de Sites, puede comparar un modelo y su Live Copy, pero los fragmentos de contenido no pueden comparar un origen con su Live Copy.
* No puede editar una Live Copy en la consola Fragmentos de contenido.
* Las páginas de Sites generalmente tienen elementos secundarios, pero los fragmentos de contenido no, aunque pueden tener fragmentos a los que se hace referencia. La opción para incluir o excluir elementos secundarios hace referencia a estos fragmentos a los que se hace referencia.
* La eliminación del paso de capítulos del asistente para crear sitios no se admite en MSM para fragmentos de contenido.
* La configuración de bloqueos MSM en propiedades de página no es compatible con MSM para fragmentos de contenido.
* Para MSM para fragmentos de contenido, use solamente la **configuración de despliegue estándar**. Otras configuraciones de despliegue no están disponibles para MSM para fragmentos de contenido.

>[!NOTE]
>
>Recuerde que los MSM para fragmentos de contenido a los que se accede a través de la consola Fragmentos de contenido se basan en la funcionalidad de Assets; esto se debe a que se almacenan como Assets (aunque se consideran una función de Sites).

## Limitaciones {#limitations}

* Los déclencheur al modificar y la configuración de despliegue asociada no existen para los fragmentos de contenido.
