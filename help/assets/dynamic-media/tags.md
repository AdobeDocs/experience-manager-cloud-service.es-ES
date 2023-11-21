---
title: Integración de visualizadores de Dynamic Media con etiquetas de Analytics y Adobe Experience Platform
description: Obtenga información acerca de la extensión de visores de Dynamic Media para Experience Platform y visores de Dynamic Media 5.13. Permite a los clientes de etiquetas de Adobe Analytics y Platform utilizar eventos y datos específicos para los visores de Dynamic Media en la configuración de etiquetas de Experience Platform.
contentOwner: Rick Brough
feature: Asset Reports
role: Admin,User
exl-id: a71fef45-c9a4-4091-8af1-c3c173324b7a
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '6661'
ht-degree: 7%

---

# Integración de visualizadores de Dynamic Media con etiquetas de Analytics y Adobe Experience Platform {#integrating-dynamic-media-viewers-with-adobe-analytics-and-adobe-launch}

## ¿Qué es la integración de visores de Dynamic Media con etiquetas de Experience Platform y Adobe Analytics? {#what-is-dynamic-media-viewers-integration-with-adobe-analytics-and-adobe-launch}

<!-- Leave this hidden path here; it points to the topic source from Sasha https://wiki.corp.adobe.com/pages/viewpage.action?spaceKey=~oufimtse&title=Dynamic+Media+Viewers+integration+with+Adobe+Launch 

name used to be Experience Platform Launch. Changed to Experience Platform Data Collection-->

*Visores de Dynamic Media* para Experience Platform Tags y Dynamic Media Viewers 5.13, permite a los clientes de Adobe Analytics y Experience Platform Tags utilizar eventos y datos específicos para Dynamic Media Viewers en su configuración de etiquetas de Experience Platform.

Esta integración significa que puede rastrear el uso de los visualizadores de Dynamic Media en su sitio web con Adobe Analytics. Al mismo tiempo, puede utilizar los eventos y los datos expuestos por los visualizadores con cualquier otra extensión de etiquetas de Experience Platform que provenga del Adobe o de un tercero.

Para obtener más información sobre las extensiones de Adobe o las extensiones de terceros, consulte [extensiones de Adobe](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) en la Guía del usuario de etiquetas de Experience Platform.

**Este tema está diseñado para lo siguiente:** Administradores de sitio, desarrolladores del programa Adobe Experience Manager y personas de Operaciones.

### Limitaciones de la integración {#limitations-of-the-integration}

* La integración de etiquetas de Experience Platform para los visualizadores de Dynamic Media no funciona en el nodo de creación de Experience Manager. No puede ver ningún seguimiento desde una página WCM hasta que se publique.
* La integración de etiquetas de Experience Platform para los visualizadores de Dynamic Media no es compatible con el modo de operación &quot;emergente&quot;, en el que la URL del visualizador se obtiene mediante el botón &quot;URL&quot; en la página Detalles del recurso.
* La integración de etiquetas de Experience Platform no se puede usar de forma simultánea con la integración de visores heredados de Analytics (mediante el `config2=` parámetro).
* La compatibilidad con el seguimiento de vídeo se limita únicamente al seguimiento de reproducción principal, tal como se describe en [Resumen de seguimiento](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-av-playback/track-core-overview.html?lang=en#player-events). En particular, no se admite QoS, anuncios, capítulos o segmentos ni el seguimiento de errores.
* La configuración de duración del almacenamiento para elementos de datos no es compatible con elementos de datos que utilizan el *Visores de Dynamic Media* extensión. La duración del almacenamiento debe establecerse en **[!UICONTROL Ninguno]**.

### Casos de uso para la integración {#use-cases-for-the-integration}

El caso de uso principal para la integración con etiquetas de Experience Platform son los clientes que utilizan Experience Manager Assets y Experience Manager Sites. En estos casos, puede configurar una integración estándar entre el nodo de creación de Experience Manager y las etiquetas de Experience Platform y, a continuación, asociar la instancia de Sites con la propiedad Etiquetas de Experience Platform. Después, cualquier componente WCM de Dynamic Media agregado a una página de Sites realizará un seguimiento de los datos y eventos de los visualizadores.

Consulte [Seguimiento de visualizadores de Dynamic Media en Experience Manager Sites](#tracking-dynamic-media-viewers-in-aem-sites).

Un caso de uso secundario que admite la integración son los clientes que solo utilizan Experience Manager Assets o Dynamic Media Classic. En estos casos, se obtiene el código incrustado del visor y se agrega a la página del sitio web. A continuación, obtenga la URL de producción de la biblioteca de etiquetas de Experience Platform desde Etiquetas de Experience Platform y agréguela manualmente al código de la página web.

Consulte [Seguimiento de visualizadores de Dynamic Media mediante código incrustado](#tracking-dynamic-media-viewers-using-embed-code).

## Funcionamiento de los datos y el seguimiento de eventos en la integración {#how-data-and-event-tracking-works-in-the-integration}

La integración aprovecha dos tipos independientes y separados de seguimiento de visualizadores de Dynamic Media: *Adobe Analytics* y *Adobe Analytics para audio y vídeo*.

### Acerca del seguimiento con Adobe Analytics  {#about-tracking-using-adobe-analytics}

Adobe Analytics permite rastrear las acciones que realiza el usuario cuando interactúa con los visualizadores de Dynamic Media en el sitio web. Adobe Analytics también le permite hacer un seguimiento de datos específicos del visor. Por ejemplo, puede rastrear y registrar eventos de carga de vista junto con el nombre del recurso, cualquier acción de zoom que se haya producido y las acciones de reproducción de vídeo.

En Etiquetas de Experience Platform, los conceptos de *Elementos de datos* y *Reglas* trabajen juntos para habilitar el seguimiento de Adobe Analytics.

#### Acerca de los elementos de datos en las etiquetas de Experience Platform {#about-data-elements-in-adobe-launch}

Un elemento de datos en las etiquetas de Experience Platform es una propiedad con nombre cuyo valor se define estáticamente o se calcula dinámicamente en función del estado de una página web o de los datos de los visualizadores de Dynamic Media.

Las opciones disponibles para una definición de elemento de datos dependen de la lista de extensiones instaladas en la propiedad de etiquetas de Experience Platform. La extensión &quot;Core&quot; está preinstalada y disponible de forma predeterminada en cualquier configuración. Esta extensión &quot;Core&quot; permite definir un elemento de datos cuyo valor proviene de una cookie, un código JavaScript, una cadena de consulta y muchas otras fuentes.

Para el seguimiento de Adobe Analytics, se deben instalar otras extensiones, como se describe en [Instalación y configuración de extensiones](#installing-and-setup-of-extensions). La extensión de visualizadores de Dynamic Media agrega la capacidad de definir un elemento de datos cuyo valor es un argumento del evento de visualizador dinámico. Por ejemplo, es posible hacer referencia al tipo de visor o al nombre del recurso notificado por el visor al cargar, al nivel de zoom notificado cuando el usuario final amplía o reduce la imagen y mucho más.

La extensión del visor de Dynamic Media mantiene automáticamente los valores de sus elementos de datos actualizados.

Una vez definido, se puede utilizar un elemento de datos en otros lugares de la interfaz de usuario de etiquetas de Experience Platform mediante el widget selector de elementos de datos. En particular, se hace referencia a los elementos de datos definidos para los fines del seguimiento de visualizadores de Dynamic Media mediante la acción Establecer variables de la extensión Adobe Analytics en Regla (a continuación).

Consulte [Elementos de datos](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html) en la Guía del usuario de etiquetas de Experience Platform.

#### Acerca de las reglas en etiquetas de Experience Platform {#about-rules-in-adobe-launch}

Una regla en Etiquetas de Experience Platform es una configuración agnóstica que define tres áreas que conforman una regla: *Eventos*, *Condiciones*, y *Acciones*:

* *Eventos* (if) indique a Experience Platform Tags cuándo almacenar en déclencheur una regla.
* *Condiciones* (if) indique a las etiquetas de Experience Platform qué otras restricciones permitir o no permitir al activar una regla.
* *Acciones* (entonces) indique al Experience Platform de etiquetas qué debe hacer cuando se activa una regla.

Las opciones disponibles en las secciones Eventos, Condiciones y Acciones dependen de las extensiones instaladas en la propiedad Etiquetas de Experience Platform. El *Núcleo* La extensión de está preinstalada y disponible de forma predeterminada en cualquier configuración. La extensión proporciona varias opciones para Eventos, como acciones básicas a nivel de explorador que incluyen cambios de enfoque, pulsaciones de teclas y envíos de formularios. También incluye opciones para Condiciones, como valor de la cookie, tipo de explorador y más. Para las acciones, solo está disponible la opción Código personalizado.

Para el seguimiento de Adobe Analytics, se deben instalar otras extensiones, como se describe en [Instalación y configuración de extensiones](#installing-and-setup-of-extensions). Específicamente:

* La extensión de visores de Dynamic Media amplía la lista de eventos admitidos a eventos específicos de los visores de Dynamic Media, como la carga del visor, el intercambio de recursos, el acercamiento y la reproducción de vídeo.
* La extensión de Adobe Analytics amplía la lista de acciones admitidas con dos acciones necesarias para enviar datos a los servidores de seguimiento: *Establecer variables* y *Send Beacon*.

Para rastrear visualizadores de Dynamic Media, es posible utilizar cualquier tipo de lo siguiente:

* Eventos de la extensión Visualizadores de Dynamic Media, la extensión principal o cualquier otra extensión.
* Condiciones en la definición de regla. O bien, puede dejar vacía el área de condiciones.

En la sección Acciones, es necesario que tenga un *Establecer variables* acción. Esta acción le indica a Adobe Analytics cómo rellenar variables de seguimiento con datos. Al mismo tiempo, la variable *Establecer variables* La acción no envía nada al servidor de seguimiento.

El *Establecer variables* la acción debe ir seguida de una *Send Beacon* acción. El *Send Beacon* esta acción realmente envía datos al servidor de seguimiento de analytics. Ambas acciones, *Establecer variables* y *Send Beacon*, proceden de la extensión de Adobe Analytics.

Consulte [Reglas](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html) en la Guía del usuario de etiquetas de Experience Platform.

#### Configuración de muestra {#sample-configuration}

La siguiente configuración de ejemplo en Etiquetas de Experience Platform muestra cómo rastrear un nombre de recurso en la carga del visor.

1. Desde el **[!UICONTROL Elementos de datos]** pestaña, definir un elemento de datos `AssetName` que hace referencia a `asset` parámetro del `LOAD` de la extensión Visualizadores de Dynamic Media.

   ![image2019-11](assets/image2019-11.png)

1. Desde el **[!UICONTROL Reglas]** pestaña, definir una regla *TrackAssetOnLoad*.

   En esta regla, la variable **[!UICONTROL Evento]** El campo utiliza el **[!UICONTROL CARGAR]** de la extensión Visualizadores de Dynamic Media.

   ![image2019-22](assets/image2019-22.png)

1. La configuración de acción tiene dos tipos de acción de la extensión de Adobe Analytics:

   *Establecer variables*, que asignan una variable de análisis de su elección al valor de `AssetName` Elemento de datos.

   *Send Beacon*, que envía información de seguimiento a Adobe Analytics.

   ![image2019-3](assets/image2019-3.png)

1. La configuración de regla resultante aparece de la siguiente manera:

   ![image2019-4](assets/image2019-4.png)

### Acerca de Adobe Analytics para audio y vídeo {#about-adobe-analytics-for-audio-and-video}

Cuando se suscribe una cuenta de Experience Cloud para utilizar Adobe Analytics para audio y vídeo, basta con habilitar el seguimiento de vídeo en la *Visores de Dynamic Media* configuración de extensión. Las métricas de vídeo están disponibles en Adobe Analytics. El seguimiento de vídeos depende de la presencia de la extensión de Adobe Medium Analytics para audio y vídeo.

Consulte [Instalación y configuración de extensiones](#installing-and-setup-of-extensions).

Actualmente, la compatibilidad con el seguimiento de vídeo se limita solo al seguimiento de &quot;reproducción principal&quot;, tal como se describe en [Resumen de seguimiento](https://experienceleague.adobe.com/docs/media-analytics/using/tracking/track-av-playback/track-core-overview.html?lang=en#player-events). En particular, no se admite QoS, anuncios, capítulos o segmentos ni el seguimiento de errores.

## Uso de la extensión Visualizadores de Dynamic Media {#using-the-dynamic-media-viewers-extension}

Como se menciona en [Casos de uso para la integración](#use-cases-for-the-integration)Sin embargo, es posible rastrear los visualizadores de Dynamic Media con la nueva integración de Experience Platform Tags en Experience Manager Sites y utilizando el código incrustado.

### Seguimiento de visualizadores de Dynamic Media en Experience Manager Sites {#tracking-dynamic-media-viewers-in-aem-sites}

Para realizar un seguimiento de los visualizadores de Dynamic Media en Experience Manager Sites, siga todos los pasos que se enumeran en la sección [Configurar todas las piezas de integración](#configuring-all-the-integration-pieces) se debe realizar la sección. Específicamente, debe crear la configuración de IMS y la configuración de nube de etiquetas de Experience Platform.

Tras la configuración adecuada, cualquier visor de Dynamic Media que agregue a una página de Sites mediante un componente WCM compatible con Dynamic Media, realiza un seguimiento automático de los datos en Adobe Analytics, Adobe Analytics para vídeo o ambos.

Consulte [Agregar recursos de Dynamic Media a páginas que utilizan sitios de Adobe](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

### Seguimiento de visualizadores de Dynamic Media mediante código incrustado {#tracking-dynamic-media-viewers-using-embed-code}

Los clientes que no utilicen Experience Manager Sites o que incrusten visores de Dynamic Media en páginas web fuera de Experience Manager Sites, o en ambas, pueden seguir utilizando la integración de etiquetas de Experience Platform.

Complete los pasos de configuración desde el [Configuración de Adobe Analytics](#configuring-adobe-analytics-for-the-integration) y [Configuración de etiquetas de Experience Platform](#configuring-adobe-launch-for-the-integration) secciones. Sin embargo, no es necesario realizar pasos de configuración relacionados con el Experience Manager.

Después de la configuración adecuada, puede agregar compatibilidad con Etiquetas de Experience Platform a una página web con un visor de Dynamic Media.

Consulte [Añadir el código de incrustación de etiquetas de Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-embed-code.html) para obtener más información sobre cómo utilizar el código incrustado de la biblioteca de etiquetas de Experience Platform.

Para obtener más información sobre cómo utilizar la función de código incrustado de Experience Manager Dynamic Media, consulte [Incrustación del visualizador de imágenes o vídeos en una página web](/help/assets/dynamic-media/embed-code.md).

**Seguimiento de visualizadores de Dynamic Media mediante el código incrustado:**

1. Tenga una página web lista para incrustar un visor de Dynamic Media.
1. Obtenga el código incrustado de la biblioteca de etiquetas de Experience Platform iniciando sesión primero en Etiquetas de Experience Platform (consulte ) [Configuración de etiquetas de Experience Platform](#configuring-adobe-launch-for-the-integration)).
1. Seleccionar **[!UICONTROL Propiedad]**, luego seleccione la **[!UICONTROL Entornos]** pestaña.
1. Elija el Nivel de entorno que sea relevante para el entorno de la página web. A continuación, en la **[!UICONTROL Instalar]** , seleccione el icono del cuadro.
1. **[!UICONTROL En las instrucciones de instalación web]** , copie el código incrustado completo de la biblioteca de etiquetas de Experience Platform, junto con el código que lo rodea `<script/>` etiquetas.

## Guía de referencia para la extensión Visualizadores de Dynamic Media {#reference-guide-for-the-dynamic-media-viewers-extension}

### Acerca de la configuración de visores de Dynamic Media {#about-the-dynamic-media-viewers-configuration}

La extensión del visor de Dynamic Media se integra automáticamente con la biblioteca de etiquetas de Experience Platform si se cumplen las siguientes condiciones:

* Objeto global de biblioteca de etiquetas de Experience Platform ( `_satellite`) está presente en la página.
* Función de extensión de visores de Dynamic Media `_dmviewers_v001()` se define en `_satellite`.

* `config2=` No se ha especificado el parámetro del visor, lo que significa que el visor no utiliza la integración heredada de Analytics.

Además, existe la opción de deshabilitar explícitamente la integración de etiquetas de Experience Platform en el visor especificando lo siguiente `launch=0` en la configuración del visor. El valor predeterminado de este parámetro es `1`.

### Configuración de la extensión Visualizadores de Dynamic Media {#configuring-the-dynamic-media-viewers-extension}

La única opción de configuración para la extensión Visualizadores de Dynamic Media es **[!UICONTROL Habilitar Adobe Medium Analytics para audio y vídeo]**.

Al marcar (habilitar) esta opción y al instalar y configurar la extensión de Adobe Medium Analytics para audio y vídeo, las métricas de reproducción de vídeo se envían a la solución Adobe Analytics para audio y vídeo. Al deshabilitar esta opción, se desactiva el seguimiento de vídeo.

Si activa esta opción *sin* Con la extensión de Adobe Medium Analytics para audio y vídeo instalada, la opción no tiene ningún efecto.

![image2019-7-22_12-4-23](assets/image2019-7-22_12-4-23.png)

### Acerca de los elementos de datos en la extensión Visualizadores de Dynamic Media {#about-data-elements-in-the-dynamic-media-viewers-extension}

El único tipo de elemento de datos que proporciona la extensión Visualizadores de Dynamic Media es el **[!UICONTROL Evento de visualizador]** de la lista desplegable **[!UICONTROL Tipo de elemento de datos]**.

Cuando se selecciona, el editor de elementos de datos procesa un formulario con dos campos:

* **[!UICONTROL Tipo de datos de evento de visualizadores de DM]**: Una lista desplegable que identifica todos los eventos de visualizador admitidos por la extensión de visualizadores de Dynamic Media que tienen argumentos, además de un elemento especial **[!UICONTROL COMÚN]**. Un elemento **[!UICONTROL COMÚN]** representa una lista de parámetros de evento que son comunes a todos los tipos de eventos enviados por los visualizadores.
* **[!UICONTROL Parámetro de seguimiento]** : un argumento del evento de visor de Dynamic Media seleccionado.

![image2019-7-22_12-5-46](assets/image2019-7-22_12-5-46.png)

Consulte la [Guía de referencia de visores de Dynamic Media](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers.html) para obtener la lista de eventos admitidos por cada tipo de visor; vaya a la sección específica del visor y, a continuación, seleccione la subsección Compatibilidad con el seguimiento de Adobe Analytics. Actualmente, la guía de referencia de visores de Dynamic Media no documenta argumentos de evento.

Veamos ahora el ciclo de vida de los visualizadores de Dynamic Media *Elemento de datos*. El valor de este elemento de datos se rellena después de que el evento de visualizador de Dynamic Media correspondiente se produzca en la página. Por ejemplo, supongamos que el elemento de datos apunta a la variable **[!UICONTROL CARGAR]** y su argumento &quot;asset&quot;. El valor de este elemento de datos recibe datos válidos después de que el visor ejecute el evento LOAD por primera vez. Si el elemento de datos apunta a la variable **[!UICONTROL ZOOM]** y su argumento &quot;scale&quot;, el valor de dicho elemento de datos permanece vacío hasta que el visor envía un **[!UICONTROL ZOOM]** por primera vez.

Del mismo modo, los valores de los elementos de datos se actualizan automáticamente cuando el visor envía un evento correspondiente a la página. La actualización de valor se produce incluso si el evento concreto no se especifica en la configuración de regla. Por ejemplo, supongamos que hay un elemento de datos **[!UICONTROL ZoomScale]** se define para el parámetro &quot;scale&quot; del evento ZOOM. Sin embargo, la única regla presente en la configuración de regla se activa mediante la variable **[!UICONTROL CARGAR]** evento. El valor de **[!UICONTROL ZoomScale]** se actualiza cada vez que un usuario ejecuta zoom dentro del visor.

Cualquier visualizador de Dynamic Media tiene un identificador único en la página web. El elemento de datos realiza un seguimiento del valor mismo y del visualizador que lo ha rellenado. Por ejemplo, supongamos que hay varios visualizadores en la misma página y un **[!UICONTROL AssetName]** Elemento de datos que apunta a **[!UICONTROL CARGAR]** y su argumento &quot;asset&quot;. El **[!UICONTROL AssetName]** Data Element mantiene una colección de nombres de recursos asociados a cada visor cargado en la página.

El valor exacto devuelto por el elemento de datos depende del contexto. Si el elemento de datos se solicita en una regla activada por un evento de visualizador de Dynamic Media, se devuelve el valor del elemento de datos para el visualizador que inició la regla. Además, el elemento de datos se solicita en una regla activada por un evento de otra extensión de etiquetas de Experience Platform. En este punto, el valor del elemento de datos proviene del visor que actualizó por última vez este elemento de datos.

**Tenga en cuenta la siguiente configuración de ejemplo:**

* Una página web que tiene dos visores de zoom de Dynamic Media: *visor1* y *visor2*.

* **[!UICONTROL ZoomScale]** El elemento de datos apunta a **[!UICONTROL ZOOM]** y su argumento &quot;scale&quot;.
* **[!UICONTROL TrackPan]** Regla con lo siguiente:

   * Utiliza el visor de Dynamic Media **[!UICONTROL PANORÁMICA]** evento como déclencheur.
   * Envía el valor de **[!UICONTROL ZoomScale]** Elemento de datos a Adobe Analytics.

* **[!UICONTROL TrackKey]** Regla con lo siguiente:

   * Utiliza el evento de pulsación de teclas de la extensión de etiquetas de Experience Platform principal como déclencheur.
   * Envía el valor de **[!UICONTROL ZoomScale]** Elemento de datos a Adobe Analytics.

Ahora, supongamos que el usuario carga la página web con los dos visores. Entrada *visor1*, se acercan a una escala del 50 %; a continuación, en *visor2*, se acercan a una escala del 25%. Entrada *visor1*, recorren la imagen y finalmente presionan una tecla en el teclado.

La actividad del usuario provoca que se realicen las dos llamadas de seguimiento siguientes a Adobe Analytics:

* La primera llamada se produce porque **[!UICONTROL TrackPan]** La regla se activa cuando el usuario entra en pánico *visor1*. Esa llamada envía el 50 % como valor de **[!UICONTROL ZoomScale]** Elemento de datos porque el elemento de datos sabe que la regla se activa por *visor1* y obtiene el valor de escala correspondiente;
* La segunda llamada se produce porque **[!UICONTROL TrackKey]** La regla se activa cuando el usuario presiona una tecla del teclado. Esa llamada envía el 25 % como valor de **[!UICONTROL ZoomScale]** Elemento de datos porque el visor no activó la regla. Como tal, el elemento de datos devuelve el valor más actualizado.

El ejemplo configurado anteriormente también afecta a la duración del valor del elemento de datos. El valor del elemento de datos administrado por el visor de Dynamic Media se almacena en el código de biblioteca de etiquetas de Experience Platform incluso después de que el propio visor se haya eliminado de la página web. Esta funcionalidad significa que si hay una regla activada por una extensión que no sea Dynamic Media Viewer y que haga referencia a dicho elemento de datos, el elemento de datos devolverá el último valor conocido. Incluso si el visualizador ya no está presente en la página web.

En cualquier caso, los valores de los elementos de datos impulsados por los visualizadores de Dynamic Media no se almacenan en el almacenamiento local ni en el servidor; en su lugar, solo se guardan en la biblioteca de etiquetas de Experience Platform del lado del cliente. Los valores de este elemento de datos desaparecen cuando se vuelve a cargar la página web.

Generalmente, el editor de elementos de datos admite [selección de duración de almacenamiento](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/data-elements.html#create-a-data-element). Sin embargo, los elementos de datos que utilizan la extensión Visualizadores de Dynamic Media solo admiten la opción de duración del almacenamiento de **[!UICONTROL Ninguno]**. Es posible configurar cualquier otro valor en la interfaz de usuario, pero el comportamiento del elemento de datos no está definido en este caso. La extensión administra el valor del elemento de datos por su cuenta: el elemento de datos que mantiene el valor del argumento de evento del visor durante todo el ciclo de vida del visor.

### Acerca de las reglas en la extensión Visualizadores de Dynamic Media {#about-rules-in-the-dynamic-media-viewers-extension}

En el Editor de reglas, la extensión agrega nuevas opciones de configuración para el Editor de eventos. Además, el editor proporciona una opción para hacer referencia manualmente a los parámetros de evento en el editor de acciones como una opción abreviada en lugar de utilizar elementos de datos preconfigurados.

#### Acerca del editor de eventos {#about-the-events-editor}

En el Editor de eventos, la extensión Visualizadores de Dynamic Media agrega una **[!UICONTROL Tipo de evento]** llamado **[!UICONTROL Evento de visor]**.

Cuando se selecciona, el Editor de eventos procesa la lista desplegable **[!UICONTROL Eventos de visor de Dynamic Media]**, donde se enumeran todos los eventos disponibles compatibles con los visualizadores de Dynamic Media.

![image2019-8-2_15-13-1](assets/image2019-8-2_15-13-1.png)

#### Acerca del editor de acciones {#about-the-actions-editor}

La extensión Visualizadores de Dynamic Media permite utilizar parámetros de evento de visualizadores de Dynamic Media para asignarlos a variables de análisis en el editor de Establecer variables de la extensión de Adobe Analytics.

El método más sencillo es completar el siguiente proceso en dos pasos:

* En primer lugar, defina uno o varios elementos de datos, donde cada elemento de datos representa un parámetro de un evento de visualizador de Dynamic Media.
* Finalmente, en el editor Set Variables de la extensión de Adobe Analytics, seleccione el icono selector de elementos de datos (tres discos apilados) para abrir el cuadro de diálogo Seleccionar elemento de datos y, a continuación, seleccione un elemento de datos de él.

![image2019-7-10_20-41-52](assets/image2019-7-10_20-41-52.png)

Sin embargo, es posible utilizar un enfoque alternativo y evitar la creación de elementos de datos. Puede hacer referencia directamente a un argumento desde un evento de visualizador de Dynamic Media. Introduzca el nombre completo del argumento de evento en la variable **[!UICONTROL valor]** campo de entrada de la asignación de variables de Analytics. Asegúrese de rodear con signos de porcentaje (%). Por ejemplo,

`%event.detail.dm.LOAD.asset%`

![image2019-7-12_19-2-35](assets/image2019-7-12_19-2-35.png)

Hay una diferencia importante entre el uso de elementos de datos y la referencia de argumentos de evento directo. Para el elemento de datos, no importa qué déclencheur de evento provoquen la acción Establecer variables. El evento que déclencheur la regla puede no estar relacionado con el visualizador dinámico (como seleccionar la página web de la extensión principal). Sin embargo, al utilizar una referencia de argumento directo es importante asegurarse de que el evento que déclencheur la regla corresponda al argumento de evento al que hace referencia.

Por ejemplo, la referencia `%event.detail.dm.LOAD.asset%` devuelve el nombre de recurso correcto si la regla se activa mediante el evento **[!UICONTROL LOAD]** de la extensión del visualizador de Dynamic Media. Sin embargo, devuelve un valor vacío para cualquier otro evento.

En la tabla siguiente se enumeran los eventos de visualizador de Dynamic Media y sus argumentos admitidos:

<table>
 <tbody>
  <tr>
   <td>Nombre del evento del visor</td>
   <td>Referencia de argumento</td>
  </tr>
  <tr>
   <td><code>COMMON</code></td>
   <td><code>%event.detail.dm.objID%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.compClass%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.instName%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.timeStamp%</code></td>
  </tr>
  <tr>
   <td><code>BANNER</code><br /> </td>
   <td><code>%event.detail.dm.BANNER.asset%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.BANNER.label%</code></td>
  </tr>
  <tr>
   <td><code>HREF</code></td>
   <td><code>%event.detail.dm.HREF.rollover%</code></td>
  </tr>
  <tr>
   <td><code>ITEM</code></td>
   <td><code>%event.detail.dm.ITEM.rollover%</code></td>
  </tr>
  <tr>
   <td><code>LOAD</code></td>
   <td><code>%event.detail.dm.LOAD.applicationname%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.asset%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.company%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.sdkversion%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewertype%</code></td>
  </tr>
  <tr>
   <td><strong> </strong></td>
   <td><code>%event.detail.dm.LOAD.viewerversion%</code></td>
  </tr>
  <tr>
   <td><code>METADATA</code></td>
   <td><code>%event.detail.dm.METADATA.length%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.METADATA.type%</code></td>
  </tr>
  <tr>
   <td><code>MILESTONE</code></td>
   <td><code>%event.detail.dm.MILESTONE.milestone%</code></td>
  </tr>
  <tr>
   <td><code>PAGE</code></td>
   <td><code>%event.detail.dm.PAGE.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.PAGE.label%</code></td>
  </tr>
  <tr>
   <td><code>PAUSE</code></td>
   <td><code>%event.detail.dm.PAUSE.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>PLAY</code></td>
   <td><code>%event.detail.dm.PLAY.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SPIN</code></td>
   <td><code>%event.detail.dm.SPIN.framenumber%</code></td>
  </tr>
  <tr>
   <td><code>STOP</code></td>
   <td><code>%event.detail.dm.STOP.timestamp%</code></td>
  </tr>
  <tr>
   <td><code>SWAP</code></td>
   <td><code>%event.detail.dm.SWAP.asset%</code></td>
  </tr>
  <tr>
   <td><code>SWATCH</code></td>
   <td><code>%event.detail.dm.SWATCH.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.SWATCH.label%</code></td>
  </tr>
  <tr>
   <td><code>TARG</code></td>
   <td><code>%event.detail.dm.TARG.frame%</code></td>
  </tr>
  <tr>
   <td> </td>
   <td><code>%event.detail.dm.TARG.label%</code></td>
  </tr>
  <tr>
   <td><code>ZOOM</code></td>
   <td><code>%event.detail.dm.ZOOM.scale%</code></td>
  </tr>
 </tbody>
</table>

## Configurar todas las piezas de integración {#configuring-all-the-integration-pieces}

**ANTES DE COMENZAR**

El Adobe recomienda revisar toda la documentación antes de esta sección para comprender la integración completa.

En esta sección se explican los pasos de configuración necesarios para integrar los visualizadores de Dynamic Media con Adobe Analytics y Adobe Analytics para audio y vídeo. Aunque el uso de la extensión de visores de Dynamic Media para otros fines en etiquetas de Experience Platform es posible, estos escenarios no se tratan en esta documentación.

Va a utilizar los siguientes productos de Adobe para configurar su integración:

* Adobe Analytics: se utiliza para configurar variables e informes de seguimiento.
* Etiquetas de Experience Platform: se utilizan para definir una propiedad, una o más reglas y uno o más elementos de datos para habilitar el seguimiento del visor.

Además, si esta solución de integración se utiliza con Experience Manager Sites, se debe realizar la siguiente configuración:

* [Consola de Adobe Developer](https://developer.adobe.com/console/home) : la integración se crea para las etiquetas de Experience Platform.
* Nodo de creación de Experience Manager: configuración de IMS y configuración de nube de etiquetas de Experience Platform.

Como parte de la configuración de, asegúrese de que tiene acceso a una empresa de Adobe Experience Cloud que ya tiene habilitadas las etiquetas de Adobe Analytics y Experience Platform.

## Configuración de Adobe Analytics para la integración {#configuring-adobe-analytics-for-the-integration}

Después de configurar Adobe Analytics, se configura lo siguiente para la integración:

* Se establece un grupo de informes y se selecciona.
* Las variables de Analytics están disponibles para recibir datos de seguimiento.
* Los informes están disponibles para ver los datos recopilados dentro de Adobe Analytics.

Consulte también [Guía de implementación de Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html).

**Para configurar Adobe Analytics para la integración:**

1. Comience accediendo a Adobe Analytics desde el Experience Cloud [página principal](https://experience.adobe.com/#/home). En la barra de menús, seleccione el icono Soluciones (una tabla de tres por tres puntos) cerca de la esquina superior derecha de la página y, a continuación, seleccione **[!UICONTROL Analytics]**.

   ![2019-07-22_18-08-47](assets/2019-07-22_18-08-47.png)

   Ahora seleccione un grupo de informes.

### Selección de un grupo de informes {#selecting-a-report-suite}

1. Cerca de la esquina superior derecha de la página Adobe Analytics, a la derecha del campo **[!UICONTROL Buscar informes]**, seleccione el grupo de informes correcto en la lista desplegable. Si hay varios grupos de informes disponibles y no está seguro de cuál usar, póngase en contacto con el administrador de Adobe Analytics, que le ayudará a seleccionar qué grupo de informes utilizar.

   En el ejemplo siguiente, un usuario creó un grupo de informes denominado *DynamicMediaViewersExtensionDoc* y lo seleccionó en la lista desplegable. El nombre del grupo de informes es solo un ejemplo. El nombre del grupo de informes que seleccione en última instancia depende de usted.

   Si no hay ningún grupo de informes disponible, usted o el administrador de Adobe Analytics deben crear uno para poder continuar con la configuración.

   Consulte [Informes y grupos de informes](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/report-suites-admin.html) y [Crear un grupo de informes](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite.html).

   En Adobe Analytics, los grupos de informes se administran en **[!UICONTROL Administrador]** > **[!UICONTROL Grupos de informes]**.

   ![2019-07-22_18-09-49](assets/2019-07-22_18-09-49.png)

   Ahora configure las variables de Adobe Analytics.

### Configuración de variables de Adobe Analytics {#setting-up-adobe-analytics-variables}

1. Designe una o más variables de Adobe Analytics que desee utilizar para realizar un seguimiento del comportamiento de los visualizadores de Dynamic Media en la página web.

   Es posible utilizar cualquier tipo de variable admitida por Adobe Analytics. La decisión sobre el tipo de variable (como Tráfico personalizado) [props], Conversión [eVar]) depende de las necesidades específicas de su implementación de Analytics.

   Consulte [Información general sobre props y eVars](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/evar.html#vars).

   A los efectos de esta documentación, solo se utiliza una variable de tráfico personalizado (props) porque está disponible en un informe de Analytics pocos minutos después de que se produzca una acción en una página web.

   Para habilitar una nueva variable Tráfico personalizado, en Adobe Analytics, en la barra de herramientas, vaya a **[!UICONTROL Administrador]** > **[!UICONTROL Grupos de informes]**.

1. En el **[!UICONTROL Administrador de grupos de informes]** , seleccione el informe correcto y, en la barra de herramientas, vaya a **[!UICONTROL Editar configuración]** > **[!UICONTROL Tráfico]** > **[!UICONTROL Variables de tráfico]**.
1. Elija una variable no utilizada, asígnele un nombre descriptivo ( **[!UICONTROL Recurso del visor (prop 30)]**) y, a continuación, cambie el cuadro combinado a &quot;Habilitado&quot; en la columna Habilitado.

   La siguiente captura de pantalla es un ejemplo de una variable de Tráfico personalizado ( **[!UICONTROL prop30]**) para rastrear un nombre de recurso utilizado por el visor:

   ![image2019-6-26_23-6-59](/help/assets/dynamic-media/assets/image2019-6-26_23-6-59.png)

1. En la parte inferior de la lista de variables, seleccione **[!UICONTROL Guardar]**.

### Configuración de un informe {#setting-up-a-report}

1. Por lo general, la configuración de un informe en Adobe Analytics depende de las necesidades específicas del proyecto. Como tal, la configuración detallada de los informes está fuera del ámbito de esta integración.

   Sin embargo, basta con saber que los informes Tráfico personalizado están disponibles automáticamente en Adobe Analytics después de configurar variables de Tráfico personalizado en **[Configuración de variables de Adobe Analytics](#setting-up-adobe-analytics-variables)**.

   Por ejemplo, el informe de **[!UICONTROL Recurso del visor (prop 30)]** está disponible en el menú Informes en **[!UICONTROL Tráfico personalizado]** > **[!UICONTROL Tráfico personalizado 21-30]** > **[!UICONTROL Recurso del visor (prop 30)]**.

   Al visitar este informe justo después de la creación de **[!UICONTROL Recursos del visualizador (prop 30)]**, no se muestra ningún dato; esto se espera en este punto de la integración.

   ![image2019-6-26_23-12-49](/help/assets/dynamic-media/assets/image2019-6-26_23-12-49.png)

## Configuración de etiquetas de Experience Platform para la integración {#configuring-adobe-launch-for-the-integration}

Después de configurar las etiquetas de Experience Platform, se configura lo siguiente para la integración:

* La creación de una nueva propiedad para mantener todas las configuraciones juntas.
* Instalación y configuración de extensiones. El código del lado del cliente de todas las extensiones instaladas en la propiedad se compila junto en una biblioteca. La página web utiliza esta biblioteca más adelante.
* Configuración de elementos de datos y reglas. Esta configuración define qué datos adquirir de los visualizadores de Dynamic Media, cuándo almacenar en déclencheur la lógica de seguimiento y dónde enviar los datos del visualizador en Adobe Analytics.
* Publicación de la biblioteca.

**Para configurar las etiquetas de Experience Platform para la integración:**

1. Comience por acceder a las etiquetas de Experience Platform desde el Experience Cloud [página principal](https://experience.adobe.com/#/home). En la barra de menús, seleccione el icono Soluciones (tres por tres tablas de puntos) cerca de la esquina superior derecha de la página, y luego seleccione **[!UICONTROL Etiquetas]**.

   También puede [abrir etiquetas de Experience Platform directamente](https://launch.adobe.com/).

   ![image2019-7-8_15-38-44](assets/image2019-7-8_15-38-44.png)

### Creación de una propiedad en Etiquetas de Experience Platform {#creating-a-property-in-adobe-launch}

Una propiedad de Etiquetas de Experience Platform es una configuración con nombre que mantiene todos los ajustes juntos. Se genera y publica una biblioteca de las opciones de configuración en diferentes niveles de entorno (desarrollo, ensayo y producción).

Consulte también [Configurar una propiedad de toque](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/initial-configuration/configure-tags.html).

**Para crear una propiedad en Etiquetas de Experience Platform:**

1. En Etiquetas de Experience Platform, seleccione **[!UICONTROL Nueva propiedad]**.
1. En el cuadro de diálogo **[!UICONTROL Crear propiedad]**, dentro del campo **[!UICONTROL Nombre]**, escriba un nombre descriptivo, como el título del sitio web. Por ejemplo, `DynamicMediaViewersProp.`
1. En el **[!UICONTROL Domains]** , introduzca el dominio del sitio web.
1. En la lista desplegable **[!UICONTROL Opciones avanzadas]**, habilite **[!UICONTROL Configurar para el desarrollo de extensiones (no se puede modificar posteriormente)]** siempre que la extensión que desee utilizar (en este caso, los *visualizadores de Dynamic Media*) aún no se haya publicado.

   ![image2019-7-8_16-3-47](assets/image2019-7-8_16-3-47.png)

1. Seleccione **[!UICONTROL Guardar]**.

   Seleccione la propiedad creada y continúe a *Instalación y configuración de extensiones*.

### Instalación y configuración de extensiones {#installing-and-setup-of-extensions}

Todas las extensiones disponibles en etiquetas de Experience Platform se enumeran en la **[!UICONTROL Extensiones]** > **[!UICONTROL Catálogo]**.

Para instalar una extensión, seleccione **[!UICONTROL Instalar]**. Si es necesario, realice una configuración de extensión única y seleccione **[!UICONTROL Guardar]**.

Cuando sea necesario, se deben instalar y configurar las siguientes extensiones:

* (Obligatorio) *Servicio de ID de Experience Cloud* extensión

No se necesita ninguna configuración adicional, acepte para los valores propuestos. Cuando haya terminado, asegúrese de seleccionar **[!UICONTROL Guardar]**.

Consulte [Extensión del servicio de ID de Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/id-service/overview.html).

* (Obligatorio) *Adobe Analytics* extensión

Para configurar esta extensión, necesita la ID del grupo de informes que se encuentra en Adobe Analytics, en **[!UICONTROL Administrador]** > **[!UICONTROL Grupo de informes]**, en **[!UICONTROL ID del grupo de informes]** encabezado de columna.

(Solo con fines de demostración, el ID del grupo de informes del **[!UICONTROL DynamicMediaViewersExtensionDoc]** El grupo de informes se utiliza en las siguientes capturas de pantalla. Este ID se creó y utilizó en [Selección de un grupo](#selecting-a-report-suite) de informes anteriormente).

![image2019-7-8_16-45-34](assets/image2019-7-8_16-45-34.png)

En la página Instalar extensión, introduzca la ID del grupo de informes en el campo **[!UICONTROL Grupos de informes de desarrollo]**, en el campo **[!UICONTROL Grupos de informes de ensayo]** y en el campo **[!UICONTROL Grupos de informes de producción]**.

![image2019-7-8_16-47-40](assets/image2019-7-8_16-47-40.png)

*Configure el siguiente elemento solo si desea utilizar el seguimiento de vídeo:*

En el **[!UICONTROL Instalar extensión]** página, expandir **[!UICONTROL General]** y, a continuación, especifique el Servidor de seguimiento. El servidor de seguimiento sigue la plantilla `<trackingNamespace>.sc.omtrdc.net`, donde `<trackingNamespace>` es la información obtenida en el correo electrónico de aprovisionamiento.

Seleccione **[!UICONTROL Guardar]**.

Consulte [Extensión de Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/analytics/overview.html).

* (Opcional. (obligatorio solo si se necesita seguimiento de vídeo) *Adobe Medium Analytics para audio y vídeo* extensión

Rellene el campo del servidor de seguimiento. El servidor de seguimiento para *Adobe Medium Analytics para audio y vídeo* La extensión de es diferente del servidor de seguimiento utilizado para Adobe Analytics. Sigue a la plantilla `<trackingNamespace>.hb.omtrdc.net`, donde `<trackingNamespace>` es la información del correo electrónico de aprovisionamiento.

El resto de campos son opcionales.

Consulte [Extensión de Adobe Medium Analytics para audio y vídeo](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/media-analytics/overview.html).

* (Obligatorio) *Visores de Dynamic Media* extensión

Seleccione **[!UICONTROL habilitar Adobe Analytics para vídeo]** para activar el seguimiento de Video Heartbeat.

En el momento de escribir este artículo, *Visores de Dynamic Media* La extensión de solo está disponible si la propiedad Etiquetas de Experience Platform se crea para el desarrollo.

Consulte [Creación de una propiedad en Etiquetas de Experience Platform](#creating-a-property-in-adobe-launch).

Una vez instaladas y configuradas las extensiones, se enumerarán las cinco extensiones siguientes (cuatro si no realiza el seguimiento de vídeo) en el área Extensiones > Instaladas.

![image2019-7-22_12-7-36](assets/image2019-7-22_12-7-36.png)

### Configuración de elementos de datos y reglas {#setting-up-data-elements-and-rules}

En Etiquetas de Experience Platform, cree los elementos de datos y las reglas necesarios para realizar el seguimiento de los visualizadores de Dynamic Media.

Consulte [Funcionamiento de los datos y el seguimiento de eventos en la integración](#how-data-and-event-tracking-works-in-the-integration) para obtener una descripción general del seguimiento con etiquetas de Experience Platform.

Consulte [Configuración de muestra](#sample-configuration) para obtener una configuración de ejemplo en Etiquetas de Experience Platform que muestra cómo rastrear un nombre de recurso durante la carga del visor.

Consulte [Configuración de la extensión Visualizadores de Dynamic Media](#configuring-the-dynamic-media-viewers-extension) para obtener información detallada sobre las funcionalidades de la extensión.

### Publicar una biblioteca {#publishing-a-library}

Para cambiar la configuración de las etiquetas de Experience Platform (incluidas las propiedades, las extensiones, las reglas y los elementos de datos configurados), debe *publicar* dichos cambios. La publicación en etiquetas de Experience Platform se realiza desde la pestaña Publicación en la configuración de la propiedad.

Las etiquetas de Experience Platform pueden tener varios entornos de desarrollo, un entorno de ensayo y un entorno de producción. De forma predeterminada, la Configuración en la nube de etiquetas de Experience Platform de Experience Manager señala el nodo de creación de etiquetas de Experience Manager al entorno de ensayo de las etiquetas de Platform. El nodo Publicación de Experience Manager apunta al entorno de producción de Etiquetas de Experience Platform. Esta disposición significa que, con la configuración predeterminada del Experience Manager, es necesario publicar la biblioteca de etiquetas de Experience Platform en el entorno de ensayo. Al hacerlo, puede utilizarlo en el autor del Experience Manager. A continuación, puede publicarlo en el entorno de producción para que se pueda utilizar en la publicación de Experience Manager.

Consulte [Entornos](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html?lang=es) para obtener más información sobre los entornos de Etiquetas de Experience Platform.

La publicación de una biblioteca implica los dos pasos siguientes:

* Añadir y crear una nueva biblioteca incluyendo todos los cambios necesarios (nuevos y actualizaciones) en la biblioteca.
* Desplazar la biblioteca a través de los diferentes niveles de entorno (desde Desarrollo hasta Ensayo y Producción).

#### Añadir y crear una nueva biblioteca {#adding-and-building-a-new-library}

1. La primera vez que abre la pestaña Publicación en Etiquetas de Experience Platform, la lista de la biblioteca estará vacía.

   En la columna izquierda, seleccione **[!UICONTROL Añadir nueva biblioteca]**.

   ![image2019-7-15_14-43-17](assets/image2019-7-15_14-43-17.png)

1. En la página Crear nueva biblioteca, en **[!UICONTROL Nombre]** , introduzca un nombre descriptivo para la nueva biblioteca. Por ejemplo,

   *DynamicMediaViewersLib*

   En la lista desplegable Entorno, elija el Nivel de entorno. Inicialmente, solo está disponible el nivel de desarrollo para la selección. Cerca de la parte inferior izquierda de la página, seleccione **[!UICONTROL Añadir todos los recursos modificados]**.

   ![image2019-7-15_14-49-41](assets/image2019-7-15_14-49-41.png)

1. Cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar y generar para desarrollo]**.

   En unos minutos, la biblioteca se crea y está lista para usarse.

   ![image2019-7-15_15-3-34](assets/image2019-7-15_15-3-34.png)

   >[!NOTE]
   >
   >La próxima vez que cambie la configuración de Etiquetas de Experience Platform, vaya a **[!UICONTROL Publicación]** debajo de la pestaña **[!UICONTROL Propiedad]** , luego seleccione la biblioteca creada anteriormente.
   >
   >
   >En la pantalla de publicación de la biblioteca, seleccione **[!UICONTROL Añadir todos los recursos modificados]**, luego seleccione **[!UICONTROL Guardar y generar para desarrollo]**.

#### Subir una biblioteca por los niveles de entorno {#moving-a-library-up-through-environment-levels}

1. Después de agregar una nueva biblioteca, se encuentra en el entorno de desarrollo. Para moverlo al nivel del entorno de ensayo (que corresponde a la columna Enviado), en el menú desplegable de la biblioteca, seleccione **[!UICONTROL Enviar para aprobación]**.

   ![image2019-7-15_15-52-37](assets/image2019-7-15_15-52-37.png)

1. En el cuadro de diálogo de confirmación, seleccione **[!UICONTROL Enviar]**.

   Una vez que la biblioteca se haya movido a la columna Submitted, en el menú desplegable de la biblioteca, seleccione **[!UICONTROL Generar para ensayo]**.

   ![image2019-7-15_15-54-37](assets/image2019-7-15_15-54-37.png)

1. Para mover la biblioteca del entorno de ensayo al entorno de producción (que es la columna Publicado), siga un proceso similar.

   Primero, en el menú desplegable, seleccione **[!UICONTROL Aprobar para publicación]**.

   ![image2019-7-15_16-7-39](assets/image2019-7-15_16-7-39.png)

1. En el menú desplegable, seleccione **[!UICONTROL Generar y publicar en producción]**.

   ![image2019-7-15_16-8-9](assets/image2019-7-15_16-8-9.png)

   Consulte [Publicación](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html) para obtener más información sobre el proceso de publicación en Etiquetas de Experience Platform.

## Configuración de Adobe Experience Manager para la integración {#configuring-adobe-experience-manager-for-the-integration}

<!-- Prerequisites list below should be verified by Sasha -->

Requisitos previos:

* Experience Manager ejecuta las instancias Author y Publish.
* El nodo de creación del Experience Manager está configurado en Dynamic Media. <!-- Scene7 run mode (dynamicmedia_s7) -->
* Los componentes de Dynamic Media WCM están habilitados en Experience Manager Sites.

La configuración del Experience Manager consta de los dos pasos principales siguientes:

* Configuración del IMS del Experience Manager.
* Configuración de Experience Platform Tags Cloud.

### Configuración de IMS de Experience Manager {#configuring-aem-ims}

1. En Experience Manager author, seleccione el icono Herramientas (martillo) y vaya a **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**.

   ![2019-07-25_11-52-58](assets/2019-07-25_11-52-58.png)

1. En la página Configuración de IMC de Adobe, cerca de la esquina superior izquierda, seleccione **[!UICONTROL Crear]**.
1. En el **[!UICONTROL Configuración de cuenta técnica de IMS de Adobe]** , en la **[!UICONTROL Solución de nube]** , seleccione la opción **[!UICONTROL Recopilación de datos de Experience Platform]**.
1. Activar **[!UICONTROL Crear nuevo certificado]**, luego, en el campo de texto, introduzca cualquier valor significativo para el certificado. Por ejemplo, *AdobeLaunchIMSCert*. Seleccionar **[!UICONTROL Crear certificado]**.

   Se muestra el siguiente mensaje de información:

   *Para recuperar un token de acceso válido, se debe añadir la clave pública del nuevo certificado a la cuenta técnica de Adobe Developer.*

   Para cerrar el cuadro de diálogo Información, seleccione **[!UICONTROL OK]**.

   ![2019-07-25_12-09-24](assets/2019-07-25_12-09-24.png)

1. Seleccionar **[!UICONTROL Descargar clave pública]** para descargar un archivo de clave pública (`*.crt`) a su sistema local.

   >[!NOTE]
   >
   >En este punto, ***dejar abierto*** el **[!UICONTROL Configuración de cuenta técnica de IMS de Adobe]** página; ***no*** cierre la página y ***no*** select **[!UICONTROL Siguiente]**. Va a volver a esta página más adelante en los pasos.

   ![2019-07-25_12-52-24](assets/2019-07-25_12-52-24.png)

1. En una nueva pestaña del explorador, vaya a [Consola de Adobe Developer](https://developer.adobe.com/console/integrations).

1. Desde el **[!UICONTROL Integraciones de consola de Adobe I/O]** página, cerca de la esquina superior derecha, seleccione **[!UICONTROL Nueva integración]**.
1. En el **[!UICONTROL Creación de una nueva integración]** , asegúrese de que **[!UICONTROL Acceso a una API]** el botón de opción está seleccionado y, a continuación, seleccione **[!UICONTROL Continuar]**.

![2019-07-25_13-04-20](assets/2019-07-25_13-04-20.png)

1. En el segundo **[!UICONTROL Creación de una nueva integración]** página, activar (activar) la **[!UICONTROL API de etiquetas de Experience Platform]** botón de opción. En la esquina inferior derecha de la página, seleccione **[!UICONTROL Continuar]**.

   ![2019-07-25_13-13-54](assets/2019-07-25_13-13-54.png)

1. En la tercera **[!UICONTROL Creación de una nueva integración]** , haga lo siguiente:

   * En el **[!UICONTROL Nombre]** , introduzca un nombre descriptivo. Por ejemplo, *DynamicMediaViewersIO*.

   * En el **[!UICONTROL Descripción]** , introduzca una descripción para la integración.

   * En el **[!UICONTROL Certificados de clave pública]** , cargue su archivo de clave pública (`*.crt`) que descargó anteriormente en estos pasos.

   * En el **[!UICONTROL Seleccione una función para la API de etiquetas de Experience Platform]** encabezado, seleccione **[!UICONTROL Administrador]**.

   * En el **[!UICONTROL Seleccione uno o varios perfiles de producto para la API de etiquetas de Experience Platform]** encabezado, seleccione el perfil de producto denominado **[!UICONTROL Etiquetas - &lt;your_company_name>]**.

   ![2019-07-25_13-49-18](assets/2019-07-25_13-49-18.png)

1. Seleccionar **[!UICONTROL Crear integración]**.
1. En el **[!UICONTROL Integración creada]** página, seleccione **[!UICONTROL Continuar con los detalles de integración]**.

   ![2019-07-25_14-16-33](assets/2019-07-25_14-16-33.png)

1. Aparecerá la página de detalles Integraciones, similar a la siguiente:

   >[!NOTE]
   >
   >***Deje abierta esta página de detalles de integración***. Va a necesitar varios fragmentos de información de la **[!UICONTROL Información general]** y **[!UICONTROL JWT]** pestañas en un momento.

   ![2019-07-25_14-35-30](assets/2019-07-25_14-35-30.png)
   *Página de detalles de integración*

1. Vuelva a la página **[!UICONTROL Configuración de cuenta técnica de Adobe IMS]** que dejó abierta anteriormente. En la esquina superior derecha de la página, seleccione **[!UICONTROL Siguiente]** para abrir **[!UICONTROL Cuenta]** página en la **[!UICONTROL Configuración de cuenta técnica de IMS de Adobe]** ventana.

   (Si ha cerrado la página anteriormente, regrese a Experience Manager Author y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**. Seleccione **[!UICONTROL Crear]**. En el **[!UICONTROL Solución de nube]** , seleccione la opción **[!UICONTROL Etiquetas de Experience Platform]**. En la lista desplegable **[!UICONTROL Certificado]**, seleccione el nombre del certificado creado anteriormente.

   ![2019-07-25_20-57-50](assets/2019-07-25_20-57-50.png)
   *Configuración de cuenta técnica de IMS de Adobe: página de certificado*

1. El **[!UICONTROL Cuenta]** tiene cinco campos que debe rellenar con información de la página Detalles de integración del paso anterior.

   ![2019-07-25_20-42-45](assets/2019-07-25_20-42-45.png)
   *Configuración de cuenta técnica de IMS de Adobe: página Cuenta*

1. En el **[!UICONTROL Cuenta]** , rellene los campos siguientes:

   * **[!UICONTROL Título]** : introduzca un título descriptivo para la cuenta.
   * **[!UICONTROL Servidor de autorización]** - Vuelva a la página de detalles de integración que abrió anteriormente. Seleccione el **[!UICONTROL JWT]** pestaña. Copie el nombre del servidor, sin la ruta, como se indica a continuación.

   Vuelva a la página **[!UICONTROL Cuenta]** y, a continuación, pegue el nombre en el campo correspondiente.
Por ejemplo, `https://ims-na1.adobelogin.com/`
(el nombre del servidor de ejemplo es solo para fines explicativos)

   ![2019-07-25_15-01-53](assets/2019-07-25_15-01-53.png)
   *Página de detalles de la integración: pestaña JWT*

1. **[!UICONTROL Clave de API]**: Vuelva a la página de detalles de la integración. Seleccione el **[!UICONTROL Información general]** , a la derecha de la pestaña **[!UICONTROL Clave de API (ID de cliente)]** , seleccione **[!UICONTROL Copiar]**.

   Vuelva a la página **[!UICONTROL Cuenta]** y pegue la clave en el campo correspondiente.

   ![2019-07-25_14-35-333](assets/2019-07-25_14-35-333.png)
   *Página de detalles de integración*

1. **[!UICONTROL Secreto del cliente]**: Regrese a la página de detalles de la integración. Desde el **[!UICONTROL Información general]** pestaña, seleccione **[!UICONTROL Recuperar secreto de cliente]**. A la derecha del **[!UICONTROL Secreto de cliente]** , seleccione **[!UICONTROL Copiar]**.

   Vuelva a la página **[!UICONTROL Cuenta]** y pegue la clave en el campo correspondiente.

1. **[!UICONTROL Carga útil]** - Vuelva a la página de detalles de la integración. Desde el **[!UICONTROL JWT]** pestaña, en el campo Carga útil JWT, copie todo el código de objeto JSON.

   Vuelva a la página **[!UICONTROL Cuenta]** y pegue el código en el campo correspondiente.

   ![2019-07-25_21-59-12](assets/2019-07-25_21-59-12.png)
   *Página de detalles de la integración: pestaña JWT*

   La página Cuenta, con todos los campos rellenados, aparece de forma similar a la siguiente:

   ![2019-07-25_22-08-30](assets/2019-07-25_22-08-30.png)

1. Cerca de la esquina superior derecha de la **[!UICONTROL Cuenta]** página, seleccione **[!UICONTROL Crear]**.

   Con el Experience Manager IMS configurado, ahora tiene una nueva cuenta IMSA en **[!UICONTROL Configuraciones de IMS de Adobe]**.

   ![image2019-7-15_14-17-54](assets/image2019-7-15_14-17-54.png)

## Configuración de Experience Platform Tags Cloud para la integración {#configuring-adobe-launch-cloud-for-the-integration}

1. En Experience Manager Author, cerca de la esquina superior izquierda, seleccione el icono Herramientas (martillo) y, a continuación, vaya a **[!UICONTROL Cloud Service]** > **[!UICONTROL Configuraciones de etiquetas de Experience Platform]**.

   ![2019-07-26_12-10-38](assets/2019-07-26_12-10-38.png)

1. En el **[!UICONTROL Configuraciones de etiquetas de Experience Platform]** , en el panel izquierdo, seleccione un sitio de Experience Manager al que desee aplicar la configuración de etiquetas de Experience Platform.

   Solo con fines de ejemplo, la variable **`We.Retail`** El sitio está seleccionado en la captura de pantalla siguiente.

   ![2019-07-26_12-20-06](assets/2019-07-26_12-20-06.png)

1. Cerca de la esquina superior izquierda de la página, seleccione **[!UICONTROL Crear]**.
1. En el **[!UICONTROL General]** página (1/3 páginas) del **[!UICONTROL Configuración de Crear etiquetas de Experience Platform]** , rellene los campos siguientes:

   * **[!UICONTROL Título]** : introduzca un título de configuración descriptivo. Por ejemplo, `We.Retail Tags cloud configuration`.

   * **[!UICONTROL Configuración de Adobe IMS asociada]** - Seleccione la configuración de IMS que creó anteriormente en [Configuración de IMS de Experience Manager](#configuring-aem-ims).

   * **[!UICONTROL Compañía]** - Desde el **[!UICONTROL Compañía]** , seleccione su empresa de Experience Cloud. La lista se rellena automáticamente.

   * **[!UICONTROL Propiedad]** : En la lista desplegable Propiedad, seleccione la propiedad Etiquetas de Experience Platform que creó anteriormente. La lista se rellena automáticamente.

Después de completar todos los campos, su **[!UICONTROL General]** La página será similar a la siguiente:

![image2019-7-15_14-34-23](assets/image2019-7-15_14-34-23.png)

1. Cerca de la esquina superior izquierda, seleccione **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Ensayo]** página (2/3 páginas) del **[!UICONTROL Configuración de Crear etiquetas de Experience Platform]** , rellene el siguiente campo:

   En el **[!UICONTROL URI de biblioteca]** (Identificador de recurso uniforme), compruebe la ubicación de la versión de ensayo de la biblioteca de etiquetas de Experience Platform. El Experience Manager rellena este campo automáticamente.

   Solo con fines explicativos, este paso utiliza bibliotecas de etiquetas de Experience Platform implementadas en CDN de Adobe.

   >[!NOTE]
   >
   >Asegúrese de que el URI de biblioteca (Identificador uniforme de recursos) rellenado automáticamente no tenga un formato incorrecto. Si es necesario, corríjalo de modo que el URI represente un URI relativo al protocolo. Es decir, comienza desde una barra diagonal doble.
   >
   >
   >Por ejemplo: `//assets.adobetm.com/launch-xxxx`.

   Su **[!UICONTROL Ensayo]** es probable que la página tenga un aspecto similar al siguiente. El **[!UICONTROL Archivar]** y **[!UICONTROL Cargar biblioteca asincrónicamente]** Las opciones son ***no*** set:

   ![image2019-7-15_15-21-8](assets/image2019-7-15_15-21-8.png)

1. Cerca de la esquina superior derecha, seleccione **[!UICONTROL Siguiente]**.
1. En el **[!UICONTROL Producción]** página (3/3 páginas) del **[!UICONTROL Configuración de Crear etiquetas de Experience Platform]** , si es necesario, corrija el URI de producción rellenado automáticamente de forma similar a como se hizo en el **[!UICONTROL Ensayo]** página.
1. Cerca de la esquina superior derecha, seleccione **[!UICONTROL Crear]**.

   La nueva configuración de nube de etiquetas de Experience Platform se ha creado y se muestra junto al sitio web.

1. Seleccione la nueva configuración de nube de etiquetas de Experience Platform (aparece una marca de verificación a la izquierda del título de la configuración cuando se selecciona). En la barra de herramientas, seleccione **[!UICONTROL Publish]**.

   ![image2019-7-15_15-47-6](assets/image2019-7-15_15-47-6.png)

Actualmente, Experience Manager Author no admite la integración de visores de Dynamic Media con etiquetas de Experience Platform.

Sin embargo, se admite en el nodo de publicación del Experience Manager. Al utilizar la configuración predeterminada de Configuración de nube de etiquetas de Experience Platform, la publicación de Experience Manager utiliza el entorno de producción de Etiquetas de Experience Platform. Como tal, es necesario insertar las actualizaciones de la biblioteca de etiquetas de Experience Platform de Desarrollo al entorno de producción cada vez durante la prueba.

Es posible solucionar esta limitación. Especifique la URL de desarrollo o ensayo de la biblioteca de etiquetas de Experience Platform en la configuración de nube de etiquetas de Experience Platform para la publicación de Experience Manager anterior. Al hacerlo, el nodo de publicación del Experience Manager utiliza la versión de desarrollo o ensayo de la biblioteca de etiquetas del Experience Platform.

Consulte [Integración de etiquetas de Experience Platform y Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/overview.html#integrations) para obtener más información sobre la configuración de la nube de etiquetas de Experience Platform.
