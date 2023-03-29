---
title: Administración de actividades
description: La consola Actividades permite crear, organizar y administrar las actividades de marketing de las marcas
exl-id: e7cab16d-7678-472d-b75f-7f67b303ba8d
source-git-commit: 56a7f214a4a1a3a58c56f1e06e3a98532054ffee
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 47%

---

# Administración de actividades {#managing-activities}

La consola Actividades permite crear, organizar y administrar el marketing [actividades](/help/sites-cloud/authoring/personalization/overview.md#activities) de sus marcas:

* Añadir marcas
* Añadir y configurar las actividades de cada marca
* Administrar actividades

>[!TIP]
>
>Si usa Adobe Target como motor de targeting, también puede [ver datos de rendimiento de sus actividades](#viewing-performance-and-converting-winning-experiences-a-b-test). Si utiliza la prueba A/B, puede [convertir ganadores](#viewing-performance-and-converting-winning-experiences-a-b-test).

En la consola Actividades , las actividades se organizan por marca. Puede utilizar marcas y carpetas para estructurar la organización de las actividades. Para desplazarse a la consola Actividades , toque o haga clic en **Personalización** y pulsando/haciendo clic **Actividades**.

Las actividades están disponibles en el modo Segmentación del [contenido de destino de creación](/help/sites-cloud/authoring/personalization/targeted-content.md), donde también puede crear actividades. Las actividades que crea en el modo Segmentación aparecen en la consola Actividades .

Las actividades se muestran con una etiqueta que describe qué tipo de actividad se define:

* XT: segmentación de experiencias de Adobe Target
* A/B: prueba A/B de Adobe Target
* AEM: segmentación en Adobe Experience Manager (es decir, conducida por ContextHub)

![Tipos de actividades](/help/sites-cloud/authoring/assets/activities-types.png)

>[!NOTE]
>
>Los tipos de actividades estarán disponibles dependiendo de lo siguiente:
>
>* Si la opción `xt_only` está habilitada en el inquilino de Adobe Target (clientcode) que se utiliza en AEM para conectarse a Adobe Target, puede crear **solo** actividades XT en AEM.
>
>* Si la `xt_only` opción **no está** activada en el inquilino de Adobe Target (clientcode), puede crear actividades **** XT o A/B en AEM.
>
>**Nota adicional:** La `xt_only` opción es una configuración aplicada a un determinado inquilino de Target (clientcode) y solo se puede modificar directamente en Adobe Target. No puede activar ni desactivar esta opción en AEM.

>[!CAUTION]
>
>Debe asegurar el nodo de configuración de actividades `cq:ActivitySettings` de la instancia de publicación, para que los usuarios normales no puedan obtener acceso a él. El nodo de configuración de la actividad solo debe ser accesible para el servicio que administra la sincronización de actividades en Adobe Target.
>
>Consulte Requisitos previos para la integración con Adobe Target para obtener información detallada.
<!--
>See [Prerequisites for Integrating with Adobe Target](/help/sites-administering/target-requirements.md#securingtheactivitysettings) for detailed information.
-->

## Creación de una marca mediante la consola de actividades {#creating-a-brand-using-the-activities-console}

Cree una marca para la que quiera administrar actividades de marketing.

Cuando cree una marca mediante la consola Actividades, esta también aparecerá en la [consola Ofertas](/help/sites-cloud/authoring/personalization/offers.md), donde podrá crear ofertas para las experiencias de las actividades.

1. En la consola de navegación, haga clic o pulse **Personalización**. Toque o haga clic en **Actividades**.

   ![Navegación a actividades](/help/sites-cloud/authoring/assets/activities-navigation.png)

1. En la consola Actividades , toque o haga clic en **Crear** then **Crear marca**.
1. Seleccione la plantilla de marca y toque o haga clic en **Siguiente**.
1. Escriba un título para la marca tal como desea que aparezca en las consolas Actividades y Ofertas . De forma opcional, escriba o seleccione una o varias etiquetas para asociarlas a la marca.
1. Haga clic o pulse **Crear**. La marca aparece en la consola Actividades .

## Adición/edición de una actividad mediante la consola Actividades {#adding-editing-an-activity-using-the-activities-console}

Añada una actividad o edite una actividad existente para centrar sus esfuerzos de marketing en audiencias específicas. Al crear o editar una actividad, debe especificar la siguiente información:

* **Nombre:** Nombre de la actividad.
* **Motor de segmentación:** [AEM](/help/sites-cloud/authoring/personalization/overview.md#aem) o [Adobe Target](/help/sites-cloud/authoring/personalization/overview.md#adobe-target) como motor del contenido segmentado.
* **Seleccione una configuración de Target:** (Solo Adobe Target) La configuración de nube que esta actividad debe utilizar para conectarse a Adobe Target. Esta opción solo aparece cuando Adobe Target está seleccionado como motor de segmentación.
* **Tipo de actividad**: el tipo de actividad; prueba A/B o segmentación de experiencias
* **Objetivo:** (Opcional) Una descripción de la actividad.
* **Experiencias:** Asignaciones entre los nombres de audiencia y los segmentos de marketing a los que está dirigiendo.
* **Porcentajes de tráfico:** Si se selecciona la prueba A/B, puede cambiar el tráfico (en porcentaje) que se destina a cada experiencia.
* **Duración:** Período de tiempo en el que se aplica la actividad.
* **Prioridad:** Prioridad relativa de la actividad. Cuando las actividades proporcionan contenido para los mismos segmentos de usuario, la actividad de la prioridad mayor prevalece por encima de la otra.
* **Métrica de objetivo:** Si Adobe Target está seleccionado como motor de determinación de objetivos, puede agregar métricas de éxito a la actividad. Se requiere una métrica de éxito.

>[!NOTE]
>
>Para poder **seleccionar una configuración de destino** debe estar en el grupo **Autores de actividades de Target**.

>[!NOTE]
>
>Es necesario *crear* nuevas actividades de Adobe Target en el editor de contenido segmentado, no en la consola **Actividades**, ya que la sincronización con Adobe Target fallará.
>
>Sin embargo, puede editar las actividades de Adobe Target existentes en la consola.

Para añadir una actividad:

1. Pulse o haga clic en la marca para la que está creando la actividad y, a continuación, pulse o haga clic en **Crear**. Después, seleccione **Crear actividad**. Si está editando, seleccione la actividad en la pantalla Área maestra y pulse o haga clic en **Editar actividad**.
1. Proporcione la siguiente información y, a continuación, toque o haga clic en **Siguiente**:
   * Un nombre para la actividad.
   * Motor de segmentación que se va a usar. ContextHub (AEM) está seleccionado de forma predeterminada. Si necesita utilizar Adobe Target, cree la actividad en el editor de contenido de destino.
   * Si ha seleccionado Adobe Target como motor de orientación, seleccione o edite la configuración de nube que desea utilizar para conectarse a Adobe Target. (Tenga cuidado de no seleccionar un marco que haya creado para la configuración de nube).
   * (Opcional) El objetivo o una descripción de la actividad.
   * Seleccione el Tipo de actividad.
1. Agregue una o varias experiencias a la actividad. Pulse o haga clic en **Agregar experiencia**.
1. Si está utilizando AEM segmentación o la segmentación de experiencias de Adobe Target:
   1. Haga clic o pulse en **Seleccionar audiencia** y escoja el segmento de destino de la experiencia.
   1. Haga clic o pulse **Añadir experiencia**, escriba un nombre y haga clic o pulse **Aceptar**.
   1. Haga clic o pulse **Siguiente**.
Si utiliza la prueba A/B de Adobe Target:
   1. Toque o haga clic en el lápiz del cuadro de audiencias para seleccionar una audiencia.
   1. Haga clic o pulse **Añadir experiencia**, escriba un nombre y haga clic o pulse **Aceptar**.
   1. Introduzca el porcentaje de tráfico que muestra cada experiencia.
   1. Haga clic o pulse **Siguiente**.
1. Para especificar cuándo se inicia la actividad, utilice el **Inicio** menú desplegable para seleccionar uno de los siguientes valores:
   * **Cuando se activa:** La actividad se inicia cuando se activa la página que contiene el contenido de destino.
   * **Fecha y hora especificadas:** Una hora específica. Cuando seleccione esta opción, pulse o haga clic en el icono de calendario, seleccione una fecha y especifique la hora a la que desea iniciar la actividad.
1. Para especificar cuándo termina la actividad, utilice el menú desplegable Final para seleccionar uno de los siguientes valores:
   * **Cuando está desactivado**: La actividad finaliza cuando la página que contiene el contenido de destino se desactiva.
   * **Fecha y hora especificadas**: una hora determinada. Cuando seleccione esta opción, toque o haga clic en el icono de calendario, seleccione una fecha y especifique la hora a la que desea finalizar la actividad.
1. Para especificar una prioridad para la actividad, utilice el control deslizante para seleccionar **Bajo**, **Normal** o **Alto**.
1. Si utiliza Adobe Target como motor de determinación de objetivos, seleccione qué desea medir con esta actividad. Consulte [Configuración de la actividad y definición de objetivos](/help/sites-cloud/authoring/personalization/targeted-content.md) para obtener más información acerca de las métricas de éxito disponibles. Debe seleccionar al menos un objetivo.
1. Toque o haga clic en **Guardar**.

   >[!NOTE]
   >
   >Después de crear una actividad, debe publicarla para que esté disponible.

## Publicación y cancelación de la publicación de actividades {#publishing-and-unpublishing-activities}

Debe publicar actividades para que estén disponibles. Por el contrario, es posible que quiera que las actividades no estén disponibles cancelando la publicación.

>[!NOTE]
>
>Al cancelar la publicación de una actividad, el estado de la actividad no cambia a menos que actualice la página.

Para publicar o cancelar la publicación de actividades:

1. Toque o haga clic en la marca y, a continuación, en el área que contiene la actividad que desea publicar o cuya publicación desea cancelar.
1. Toque o haga clic en el icono situado junto a la actividad o actividades que desea publicar o cuya publicación desea cancelar.

   ![Publicación desde la consola de actividades](/help/sites-cloud/authoring/assets/activities-console.png)

1. Para publicar, toque o haga clic en **Publicación**. Para cancelar la publicación, toque o haga clic en **Cancelar la publicación**. La actividad o actividades se publican o dejan de publicarse y su estado cambia en la consola Actividades (puede que sea necesario actualizarlas).

## Actividades en instancias de autor y publicación {#activities-on-author-and-publish-instances}

Cuando se activa una actividad que utiliza el motor de destino de Adobe Target, se crea una segunda actividad en la instancia de publicación:

* La actividad en la instancia de autor realiza el seguimiento de la actividad en la instancia de autor y resulta útil para simular la experiencia del visitante. Los análisis registrados para esta actividad solo reflejan lo que ocurre en la instancia de autor.
* La actividad en la instancia de publicación refleja y responde a la actividad en el servidor de publicación. Esta es la actividad que se ejecuta en el sitio web público. Solo la actividad de publicación es relevante para rastrear y analizar el uso del sitio público real.

## Visualización del rendimiento y conversión de experiencias ganadoras (prueba A/B) {#viewing-performance-and-converting-winning-experiences-a-b-test}

Puede ver el rendimiento de cualquier actividad de Adobe Target (XT o A/B). Si utiliza la prueba A/B, también puede convertir la experiencia ganadora, que a su vez será la experiencia predeterminada.

Para ver el rendimiento de las actividades y convertirlas en experiencias ganadoras:

1. En **Personalización**, haga clic o pulse en **Actividades** para ir a la consola **Actividades**.
1. Haga clic o pulse la marca de la cual quiera ver actividades.
1. Seleccione la actividad y pulse o haga clic en **Ver propiedades**, seleccione la pestaña **Informes** y haga clic en la actividad para la que desee ver el rendimiento o convertir las experiencias ganadoras. Se muestran los datos de rendimiento.

   ![Comprobación del rendimiento de la actividad](/help/sites-cloud/authoring/assets/activities-performance.png)

1. Haga clic o pulse en el vínculo **Ganador de push** para que esa experiencia sea la experiencia predeterminada.

   Convertir al ganador hace lo siguiente:

   * Desactiva la actividad actual
   * Modifica todas las páginas y reemplaza el contenido de destino con el contenido real de la experiencia ganadora. El contenido de la experiencia ganadora pasa a formar parte de la página normal **sin** segmentación.

   ![Conversión del ganador](/help/sites-cloud/authoring/assets/activities-reports.png)

   Una experiencia ganadora es la que genera más alza en los informes, que se basa en la tasa de conversión.

1. Toque o haga clic en **Sí** para confirmar que desea convertir el ganador, deshabilitando la experiencia actual y sustituyéndola por el contenido de la experiencia ganadora.

## Sincronización de actividades con Adobe Target {#synchronizing-activities-with-adobe-target}

Las actividades que utilizan el motor de targeting de Adobe Target se sincronizan con las campañas de Adobe Target. Una actividad se sincroniza automáticamente con Adobe Target cuando se cumplen las siguientes condiciones:

* La actividad contiene al menos una experiencia.
* Al menos una experiencia contiene un segmento asignado y una oferta.
* Cada experiencia de la actividad debe tener el mismo número de ofertas.

Estas condiciones se aplican a las actividades en instancias de autor y publicación.

Cuando se sincroniza una actividad, se crea una campaña correspondiente en Adobe Target:

* Las actividades de la instancia de publicación tienen el mismo nombre que la campaña de Adobe Target correspondiente.
* Las actividades de la instancia de creación se corresponden con las campañas de Target que tienen el mismo nombre con el sufijo `_author`.

![Sincronización con Adobe Target](/help/sites-cloud/authoring/assets/activities-synch.png)

Las actividades de creación se sincronizan inmediatamente cuando se modifica la actividad. La sincronización inmediata permite la simulación de actividades con ContextHub.

Las actividades de publicación se sincronizan cuando la actividad se publica en la instancia de publicación de AEM.

## Resolución de problemas de sincronización de actividades {#troubleshooting-activity-synchronization}

Cuando AEM sincroniza una actividad con Adobe Target, incluye una propiedad de la actividad denominada `thirdPartyId`. El valor de esta propiedad se basa en la ruta de acceso de la actividad del repositorio de AEM. Dos campañas de Adobe Target no pueden tener el mismo valor para la propiedad `thirdPartyId`. Por lo tanto, una actividad no se podrá sincronizar si una campaña existente (de un tipo AB o XT diferente) en Adobe Target utiliza el mismo valor para `thirdPartyId`.

Esta situación puede ocurrir en las siguientes circunstancias:

1. Se crea y sincroniza una actividad con Adobe Target.
1. En otra instancia de AEM, se crea una actividad con la misma marca y con el mismo nombre. La sincronización de esta actividad falla cuando se intenta.

Esta situación también puede ocurrir en las siguientes circunstancias:

1. Se crea y sincroniza una actividad con Adobe Target. A continuación, la actividad se elimina en AEM.
1. Una actividad se crea con la misma marca y con el mismo nombre que la actividad eliminada. La sincronización de esta actividad falla cuando se intenta.

Para evitar problemas de sincronización, use siempre nombres únicos para las actividades. Si una actividad no se sincroniza, puede eliminar la campaña en Adobe Target que utilice el mismo nombre si dicha campaña no se está utilizando.

>[!NOTE]
>
>Al crear una campaña en Adobe Target, se asigna una propiedad denominada `thirdPartyId` a cada campaña. Cuando elimine una campaña en Adobe Target, la propiedad `thirdPartyId` no se eliminará. No puede volver a utilizar `thirdPartyId` para las campañas de distintos tipos (AB, XT) y no se puede quitar manualmente. Para evitar este problema, asigne a cada campaña un nombre único; por tanto, los nombres de campaña no se pueden reutilizar en tipos de campaña diferentes.
>
>Si utiliza el mismo nombre en el mismo tipo de campaña, sobrescribirá la campaña existente.
>
>Si al sincronizar se muestra el mensaje de error “Se ha producido un error en la solicitud. `thirdPartyId` ya existe”, cambie el nombre de la campaña y vuelva a sincronizar.
