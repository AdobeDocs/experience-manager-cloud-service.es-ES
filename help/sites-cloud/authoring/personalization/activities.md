---
title: Administración de actividades
description: La consola Actividades permite crear, organizar y administrar las actividades de marketing de las marcas
exl-id: e7cab16d-7678-472d-b75f-7f67b303ba8d
source-git-commit: 56a7f214a4a1a3a58c56f1e06e3a98532054ffee
workflow-type: tm+mt
source-wordcount: '2019'
ht-degree: 99%

---

# Administración de actividades {#managing-activities}

La consola Actividades permite crear, organizar y administrar las [actividades](/help/sites-cloud/authoring/personalization/overview.md#activities) de marketing de las marcas.

* Añadir marcas
* Añadir y configurar las actividades de cada marca
* Administrar actividades

>[!TIP]
>
>Si utiliza Adobe Target como motor de segmentación, también puede [ver los datos de rendimiento de las actividades](#viewing-performance-and-converting-winning-experiences-a-b-test). Si utiliza la prueba A/B, puede [convertir los ganadores](#viewing-performance-and-converting-winning-experiences-a-b-test).

En la consola de actividades, las actividades se organizan según la marca. Puede utilizar marcas y carpetas para estructurar la organización de las actividades. Vaya a la consola de actividades; para ello, pulse o haga clic en **Personalización** y pulse o haga clic en **Actividades**.

Las actividades están disponibles en el modo Segmentación del [contenido de destino de creación](/help/sites-cloud/authoring/personalization/targeted-content.md), donde también puede crear actividades. Las actividades que cree en el modo Segmentación aparecerán en la consola de actividades.

Las actividades se muestran con una etiqueta que describe qué tipo de actividad se define:

* XT: segmentación de la experiencia de Adobe Target
* A/B: prueba de A/B de Adobe Target
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

## Crear una marca mediante la consola de actividades {#creating-a-brand-using-the-activities-console}

Cree una marca para la que quiera administrar actividades de marketing.

Cuando cree una marca mediante la consola Actividades, esta también aparecerá en la [consola Ofertas](/help/sites-cloud/authoring/personalization/offers.md), donde podrá crear ofertas para las experiencias de las actividades.

1. En la consola de navegación, haga clic o pulse **Personalización**. Haga clic o pulse **Actividades**.

   ![Navegación a actividades](/help/sites-cloud/authoring/assets/activities-navigation.png)

1. En la consola de actividades, haga clic o pulse **Crear** y, a continuación, **Crear marca**.
1. Seleccione la plantilla de marca y haga clic o pulse **Siguiente**.
1. Escriba un título para la marca tal y como desea que aparezca en las consolas de actividades y de ofertas. De forma opcional, escriba o seleccione una o más etiquetas para asociarlas a la marca.
1. Haga clic o pulse **Crear**. La marca aparece en la consola de actividades.

## Añadir/editar una actividad mediante la consola de actividades {#adding-editing-an-activity-using-the-activities-console}

Añada una actividad o edite una actividad existente para centrar sus esfuerzos de marketing en audiencias más específicas. Cuando cree o edite una actividad, deberá indicar la siguiente información:

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
>Para poder hacer lo siguiente **Seleccionar una configuración de destino** debe estar en el **Autores de actividades de Target** grupo.

>[!NOTE]
>
>Es necesario *crear* nuevas actividades de Adobe Target en el editor de contenido segmentado, no en la consola **Actividades**, ya que la sincronización con Adobe Target fallará.
>
>Sin embargo, puede editar las actividades existentes de Adobe Target en la consola.

Para añadir una actividad:

1. Pulse o haga clic en la marca para la que está creando la actividad y, a continuación, pulse o haga clic en **Crear**. Después, seleccione **Crear actividad**. Si está editando, seleccione la actividad en la pantalla Área maestra y pulse o haga clic en **Editar actividad**.
1. Proporcione la información siguiente y, a continuación, haga clic o pulse **Siguiente**:
   * El nombre de la actividad.
   * El motor de búsqueda de segmentación que se va a usar. ContextHub (AEM) está seleccionada de forma predeterminada. Si necesita utilizar Adobe Target, cree la actividad en el editor de contenido de destino.
   * Si seleccionó Adobe Target como motor de segmentación, seleccione o edite la configuración de la nube que se utiliza para conectar con Adobe Target. (Procure no seleccionar un marco que haya creado para la configuración de la nube).
   * (Opcional) El objetivo o una descripción de la actividad.
   * Seleccione el tipo de actividad.
1. Agregue una o varias experiencias a la actividad. Pulse o haga clic en **Agregar experiencia**.
1. Si utiliza la segmentación AEM o la segmentación por experiencia de Adobe Target:
   1. Haga clic o pulse en **Seleccionar audiencia** y escoja el segmento de destino de la experiencia.
   1. Haga clic o pulse **Añadir experiencia**, escriba un nombre y haga clic o pulse **Aceptar**.
   1. Haga clic o pulse **Siguiente**.
Si utiliza la prueba A/B de Adobe Target:
   1. Haga clic o pulse el lápiz en el cuadro de audiencias para seleccionar una audiencia.
   1. Haga clic o pulse **Añadir experiencia**, escriba un nombre y haga clic o pulse **Aceptar**.
   1. Especifique el porcentaje de tráfico que muestra cada experiencia.
   1. Haga clic o pulse **Siguiente**.
1. Para especificar el momento en que la actividad comenzará, use el menú desplegable **Inicio** para seleccionar uno de los siguientes valores:
   * **Cuando se activa:** la actividad se inicia cuando se active la página que contiene el contenido de destino.
   * **Fecha y hora especificadas:** una hora específica. Cuando seleccione esta opción, pulse o haga clic en el icono de calendario, seleccione una fecha y especifique la hora a la que desea iniciar la actividad.
1. Para especificar cuándo finaliza la actividad, utilice el menú desplegable final para seleccionar uno de los siguientes valores:
   * **Cuando se desactiva:** la actividad finaliza cuando la página que tiene el contenido de destino se desactiva.
   * **Fecha y hora especificadas**: una hora determinada. Al seleccionar esta opción, toque o haga clic en el icono de calendario, seleccione una fecha y especifique la hora de finalización de la actividad.
1. Para especificar una prioridad de la actividad, utilice el regulador para seleccionar cualquier valor: **Baja**, **Normal** o **Alta**.
1. Si utiliza Adobe Target como motor de segmentación, seleccione qué desea medir con esta actividad. Consulte [Configuración de la actividad y definición de objetivos](/help/sites-cloud/authoring/personalization/targeted-content.md) para obtener más información acerca de las métricas de éxito disponibles. Debe seleccionar por lo menos un objetivo.
1. Haga clic o pulse **Guardar**.

   >[!NOTE]
   >
   >Después de crear una actividad, debe publicarla de forma que esté disponible.

## Publicar y cancelar la publicación de actividades {#publishing-and-unpublishing-activities}

Debe publicar actividades para que puedan estar disponibles. Por el contrario, es posible que no quiera que las actividades estén disponibles al cancelar su publicación.

>[!NOTE]
>
>Al cancelar la publicación de una actividad, el estado de la actividad no cambia a menos que actualice la página.

Para publicar o cancelar la publicación de actividades:

1. Haga clic o pulse la marca y, a continuación, el área que contiene la actividad que quiera publicar o de la cual quiera cancelar la publicación.
1. Haga clic o pulse el icono junto a la actividad o actividades que desee publicar o cuya publicación quiera cancelar.

   ![Publicación desde la consola de actividades](/help/sites-cloud/authoring/assets/activities-console.png)

1. Para publicar, pulse o haga clic en **Publicar**. Para cancelar la publicación, pulse o haga clic en **Cancelar publicación**. La actividad o actividades se publicarán (o no), y su estado cambiará en la consola de actividades (es posible que sea necesaria una actualización).

## Actividades en las instancias de Publicación y Autor {#activities-on-author-and-publish-instances}

Cuando se activa una actividad que utiliza el motor de segmentación de Adobe Target, una segunda actividad se crea en la instancia de publicación:

* La actividad en la instancia de autor realiza el seguimiento de la actividad de la instancia de autor y resulta útil para simular la experiencia de los visitantes. El análisis que se grabó para esta actividad refleja únicamente lo que ocurre en la instancia de autor.
* La actividad de la instancia refleja y responde a la actividad en el servidor de publicación. Esta es la actividad que se ejecuta en el sitio web público. Publicar únicamente la actividad es importante si se quiere hacer el seguimiento y analizar el uso real del sitio público.

## Visualizar el rendimiento y convertir experiencias ganadoras (pruebas A/B) {#viewing-performance-and-converting-winning-experiences-a-b-test}

Puede ver el rendimiento de cualquier actividad de Adobe Target (XT o A/B). Si utiliza la prueba A/B también puede convertir la experiencia ganadora, que a su vez se convertirá en la experiencia predeterminada.

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

   Una experiencia ganadora es la que más crece en los informes, y está basada en la tasa de conversión.

1. Haga clic o pulse **Sí** para confirmar que desea convertir el ganador, deshabilitar la experiencia actual y reemplazarla por el contenido de experiencia ganadora.

## Sincronizar actividades con Adobe Target {#synchronizing-activities-with-adobe-target}

Las actividades que utilizan el motor de segmentación de Adobe Target se sincronizan con las campañas de Adobe Target. Una actividad se sincroniza automáticamente con Adobe Target cuando se cumplen las siguientes condiciones:

* La actividad contiene al menos una experiencia.
* Por lo menos una experiencia contiene un segmento asignado y una oferta.
* Cada experiencia de la actividad debe tener el mismo número de ofertas.

Estas condiciones se aplican a las actividades de las instancias de publicación y autor.

Cuando se sincroniza una actividad, se crea la campaña correspondiente en Adobe Target:

* Las actividades de la instancia de publicación tienen el mismo nombre que la campaña de Adobe Target correspondiente.
* Las actividades de la instancia de creación se corresponden con las campañas de Target que tienen el mismo nombre con el sufijo `_author`.

![Sincronización con Adobe Target](/help/sites-cloud/authoring/assets/activities-synch.png)

Las actividades de creación se sincronizan inmediatamente cuando se modifica la actividad. La sincronización inmediata permite la simulación de actividades con ContextHub.

La publicación de actividades se sincroniza cuando la actividad está publicada en una instancia de publicación de AEM.

## Solución de problemas con la sincronización de la actividad {#troubleshooting-activity-synchronization}

Cuando AEM sincroniza una actividad con Adobe Target, incluye una propiedad de la actividad denominada `thirdPartyId`. El valor de esta propiedad se basa en la ruta de acceso de la actividad del repositorio de AEM. Dos campañas de Adobe Target no pueden tener el mismo valor para la propiedad `thirdPartyId`. Por lo tanto, una actividad no se podrá sincronizar si una campaña existente (de un tipo AB o XT diferente) en Adobe Target utiliza el mismo valor para `thirdPartyId`.

Este problema también puede ocurrir en las siguientes circunstancias:

1. Una actividad se crea y se sincroniza con Adobe Target.
1. En otra instancia AEM, se crea una actividad según la misma marca y utiliza el mismo nombre. Se produce un error al intentar sincronizar esta actividad.

Este problema también puede ocurrir en las siguientes circunstancias:

1. Una actividad se crea y se sincroniza con Adobe Target. La actividad se eliminará de AEM.
1. Una actividad se crea según la misma marca y se usa el mismo nombre que el de la actividad eliminada. Se produce un error al intentar sincronizar esta actividad.

Para evitar problemas de sincronización, use siempre nombres únicos para las actividades. Si una actividad no se sincroniza, puede eliminar la campaña en Adobe Target que utilice el mismo nombre si dicha campaña no se está utilizando.

>[!NOTE]
>
>Al crear una campaña en Adobe Target, se asigna una propiedad denominada `thirdPartyId` a cada campaña. Cuando elimine una campaña en Adobe Target, la propiedad `thirdPartyId` no se eliminará. No puede volver a utilizar `thirdPartyId` para las campañas de distintos tipos (AB, XT) y no se puede quitar manualmente. Para evitar este problema, asigne a cada campaña un nombre único; por tanto, los nombres de campaña no se pueden reutilizar en tipos de campaña diferentes.
>
>Si utiliza el mismo nombre en el mismo tipo de campaña, sobrescribirá la campaña existente.
>
>Si al sincronizar se muestra el mensaje de error “Se ha producido un error en la solicitud. `thirdPartyId` ya existe”, cambie el nombre de la campaña y vuelva a sincronizar.
