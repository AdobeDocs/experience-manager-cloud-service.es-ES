---
title: ¿Cómo se integra AEM Forms con Adobe Analytics?
seo-title: Learn how to integrate AEM Forms with Adobe Analytics.
exl-id: 0730432e-75b8-4b35-a377-ae4a2bee6c9f
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1687'
ht-degree: 0%

---

# Integrar con [!DNL Adobe Analytics] {#integrate-aem-forms-with-adobe-analytics}

AEM Forms se integra con [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=en) para que pueda capturar y rastrear las métricas de rendimiento de los formularios publicados. El objetivo detrás del análisis de estas métricas es permitir que los usuarios empresariales obtengan perspectivas sobre el comportamiento del usuario final y optimizar la experiencia de captura de datos. Puede capturar y rastrear el comportamiento de los usuarios que iniciaron sesión y no los que iniciaron sesión (anónimos) a través de Adobe Analytics para Adaptive Forms.

Después de realizar las acciones mencionadas en este artículo, puede configurar y ver los informes en [!DNL Adobe Analytics], como se muestra en el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

Puede usar [!DNL Adobe Analytics] para descubrir patrones de interacción y problemas que los usuarios afrontan al utilizar formularios adaptables. Fuera de la caja, [!DNL Adobe Analytics] rastrea y almacena información sobre los siguientes eventos:

* **Renderización**: Número de veces que se abre un formulario.

* **Submit**: Número de veces que se envía un formulario.

* **Abandono**: Número de veces que los usuarios se van sin completar el formulario.

* **Error**: Número de errores encontrados en el panel y en los campos del panel.

* **Ayuda**: Número de veces que un usuario abre la ayuda de un panel y los campos del panel.

* **Visita al campo**: Número de veces que un usuario visita un campo del formulario.

* **Guardar**: Número de veces que los usuarios guardan un formulario en Forms Portal.

Además de estos eventos predeterminados, puede definir eventos personalizados en formularios adaptables mediante el editor de reglas y asignar esos eventos a eventos en [!DNL Adobe Analytics]

La siguiente ilustración ilustra las acciones que debe realizar antes de ver los informes en [!DNL Adobe Analytics]:

![Información general de Analytics](assets/analytics-workflow.png)

## 1. Configurar [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Antes de configurar [!DNL Adobe Analytics], crear:

* Un Adobe ID para iniciar sesión en [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* A [grupo de informes](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).


### Instalación de AEM Forms y [!DNL Adobe Analytics] extensiones {#install-extensions}

Siga estos pasos para configurar AEM Forms y [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html) extensiones:

1. Inicie sesión en Adobe Experience Cloud y seleccione un nombre adecuado para la empresa.

1. Toque **[!UICONTROL Inicio/Recopilación de datos]** y toque **[!UICONTROL Vaya a Launch/Recopilación de datos]**.

1. Toque **[!UICONTROL Nueva propiedad]** y especifique un nombre para la configuración.

1. Especifique un nombre de dominio y toque **[!UICONTROL Guardar]** para guardar la propiedad.

1. Pulse el nombre de configuración disponible en la lista de Propiedades de la etiqueta.

1. En el **[!UICONTROL Creación]** sección, toque **[!UICONTROL Extensiones]**.

1. Toque **[!UICONTROL Catálogo]** y toque **[!UICONTROL Instalar]** para el **[!UICONTROL Adobe Experience Manager Forms]** extensión. **[!UICONTROL Adobe Experience Manager Forms]** se muestra en la lista de extensiones instaladas disponibles en la **Installed** pestaña .

1. Toque **[!UICONTROL Instalar]** para el **[!UICONTROL Adobe Analytics]** extensión.
1. Seleccione el nombre del grupo de informes en la **[!UICONTROL Grupos de informes de desarrollo]**, **[!UICONTROL Ensayo de grupos de informes]** y **[!UICONTROL Grupos de informes de producto]** toque y listas desplegables **[!UICONTROL Guardar]** para guardar la extensión.

### Configuración de elementos de datos {#configure-data-elements}

Puede seleccionar cualquiera de los elementos de datos configurados en una regla creada para un evento. Cuando se produce un evento en un formulario adaptable, AEM Forms envía estos elementos de datos a [!DNL Adobe Analytics].

Después de instalar el **[!UICONTROL Adobe Experience Manager Forms]** , puede crear los siguientes elementos de datos:

<table>
 <tbody>
  <tr>
   <td>FieldName</th>
   <td>FieldTitle</th>
   <td>FormInstance</th>
  </tr>
  <tr>
   <td>FormName<br /> </td>
   <td>FormTitle<br /> </td>
   <td>PageName</td>
  </tr>
  <tr>
   <td>Dirección URL de la página<br /> </td>
   <td>Título del panel<br /> </td>
   <td>Tiempo empleado</td>
  </tr>
 </tbody>
</table>

Siga estos pasos para configurar los elementos de datos:

1. En el **[!UICONTROL Creación]** sección, toque **[!UICONTROL Elementos de datos]**.

1. Toque **[!UICONTROL Crear nuevo elemento de datos]**.

1. Especifique un nombre para el elemento de datos. Por ejemplo, Título de formulario para el tipo de elemento de datos Título de formulario .

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como el nombre de la extensión.

1. Seleccione el **[!UICONTROL Tipo de elemento de datos]**.

1. Toque **[!UICONTROL Guardar]** para guardar el elemento de datos.

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### Configuración de reglas {#configure-rules}

Realice los siguientes pasos para crear reglas basadas en la variable **[!UICONTROL Adobe Experience Manager Forms]** extensión:

1. En el **[!UICONTROL Creación]** sección, toque **[!UICONTROL Reglas]**.

1. Toque **[!UICONTROL Crear nueva regla]**.

1. Especifique un nombre para la regla. Por ejemplo, Formulario enviado para registrar los envíos de formularios.

1. En el **[!UICONTROL Eventos]** sección, toque **[!UICONTROL Agregar]**.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como el nombre de la extensión.

1. Seleccione el tipo de evento. La entrada para el **[!UICONTROL Nombre]** se rellena automáticamente en función del tipo de evento seleccionado.

1. Toque **[!UICONTROL Conservar cambios]** para guardar el evento.

1. En el **[!UICONTROL Acciones]** sección, toque **[!UICONTROL Agregar]**.

1. Especifique **[!UICONTROL Adobe Analytics]** como el nombre de la extensión.

1. Select **[!UICONTROL Establecer variables]** como Tipo de acción. Las opciones disponibles en la lista desplegable incluyen:

   * **[!UICONTROL Establecer variables]**: Utilice este tipo de acción para definir el tipo de evento para el que se envían los elementos de datos seleccionados de AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Send Beacon]**: Utilice este tipo de acción para enviar datos de AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Borrar variables]**: Utilice este tipo de acción para borrar la pista de datos de modo que el evento se registre solo una vez en [!DNL Adobe Analytics].

      El método recomendado es usar la variable **[!UICONTROL Establecer variables]** tipo de acción para configurar el evento y los elementos de datos y, a continuación, utilizar **[!UICONTROL Send Beacon]** para enviar datos y, a continuación, utilizar **[!UICONTROL Borrar variables]** para borrar la pista de datos.

1. En el **[!UICONTROL Props]** , asigne las opciones del grupo de informes disponibles en la lista desplegable con los elementos de datos definidos mediante [Configuración de elementos de datos](#configure-data-elements).

   Por ejemplo, para enviar **Título del formulario** elemento de datos de AEM Forms a [!DNL Adobe Analytics] al enviar un formulario:
   1. En el **[!UICONTROL Props]** , seleccione una prop para Título de formulario disponible en el grupo de informes y, a continuación, pulse ![Icono de base de datos](assets/database-icon.svg) para asignarlo al título del formulario creado en [Configuración de elementos de datos](#configure-data-elements).

      ![define-props](assets/define-props.png)

   1. Toque **[!UICONTROL Añadir otro]** para agregar más elementos de datos a la lista.

1. En el **[!UICONTROL Eventos]** seleccione un evento de las opciones disponibles en el grupo de informes y pulse **[!UICONTROL Conservar cambios]**.

1. En el **[!UICONTROL Acciones]** , pulse + y especifique **[!UICONTROL Adobe Analytics]** como el nombre de la extensión.

1. Select **[!UICONTROL Send Beacon]** como Tipo de acción. En el panel derecho, seleccione **[!UICONTROL s.t()]** para enviar datos a [!DNL Adobe Analytics] y tratarla como una vista de página o **[!UICONTROL s.tl()]** para enviar datos a [!DNL Adobe Analytics] y no lo trate como una vista de página. Toque **[!UICONTROL Conservar cambios]**.

1. En el **[!UICONTROL Acciones]** , pulse + y especifique **[!UICONTROL Adobe Analytics]** como el nombre de la extensión.

1. Select **[!UICONTROL Borrar variables]** como Tipo de acción. Toque **[!UICONTROL Conservar cambios]**. Después de realizar estos pasos, la variable **[!UICONTROL Acciones]** se muestra como:
   ![Configuración de acciones](assets/actions-config.png)

   Personalice el **[!UICONTROL Acciones]** según sus necesidades. Por ejemplo, puede definir dos **Send Beacon** pasos de un flujo de acciones para enviar datos a [!DNL Adobe Analytics] y tratarla como una vista de página en un paso y enviar datos a [!DNL Adobe Analytics] y no lo trate como una vista de página en el segundo paso.

   ![Configuración de acciones](assets/actions-config-2.png)

1. Toque **[!UICONTROL Guardar]** para guardar la regla.

   Puede crear reglas para todos los tipos de eventos, como Abandono, Error, Visita de campo, Ayuda, Procesamiento, Guardar y Enviar.

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Flujos de publicación {#publish-flow}

Después de crear los elementos de datos y utilizarlos en las reglas, publique la configuración para recopilar datos de formulario en [!DNL Adobe Analytics].

Siga estos pasos para publicar la configuración:

1. En el **[!UICONTROL Publicación]** sección, toque **[!UICONTROL Flujo de publicación]**.

1. Toque **[!UICONTROL Agregar biblioteca]** y especifique un nombre y seleccione el entorno de la biblioteca.

1. Toque **[!UICONTROL Agregar todos los recursos modificados]** y, a continuación, toque **[!UICONTROL Guardar y crear en desarrollo]**.

1. En el **[!UICONTROL Desarrollo]** sección, toque ![Más opciones](assets/more-options-icon.svg) y, a continuación, toque **[!UICONTROL Aprobar y publicar en producción]**.

1. Confirme los cambios y el flujo de publicación se mostrará pronto en la **[!UICONTROL Publicado]** para obtener más información.

![Flujo de publicación](assets/publish-flow.png)

## 2. Configurar AEM Forms {#configure-aem-forms}

Antes de crear la configuración de Launch de Adobe, cree un [Configuración de Adobe IMS mediante Adobe Launch as the Cloud Solution](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

### Crear configuración de Adobe Launch {#create-adobe-launch-configuration}

Realice los siguientes pasos para crear una configuración de Launch de Adobe:

1. En la instancia de autor de AEM Forms, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuraciones de Launch de Adobe]**.

1. Seleccione una carpeta para crear la configuración y pulse **[!UICONTROL Crear]**.

1. Especifique un título para la configuración en la **[!UICONTROL Título]** campo .

1. Seleccione el [configuración de Adobe IMS asociada](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html).

1. Seleccione el nombre de la empresa utilizada mientras [configuración de Adobe Analytics](#Configure-adobe-analytics).

1. Seleccione el nombre de la propiedad creada mientras [configuración de Adobe Analytics](#install-extensions).

1. Toque **[!UICONTROL Guardar y cerrar]**.

1. Publique la configuración.

### Habilitar [!DNL Adobe Analytics] para un formulario adaptable {#enable-analytics-adaptive-form}

Para usar [!DNL Adobe Launch] configuración en un formulario adaptable existente:

1. En la instancia de autor de AEM Forms, vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms y documentos]**.
1. Seleccione el formulario adaptable y pulse **[!UICONTROL Propiedades]**.
1. En el **[!UICONTROL Básico]** , seleccione [contenedor de configuración](#create-adobe-launch-configuration) se utiliza al crear la configuración de Launch de Adobe.
1. Toque **[!UICONTROL Guardar y cerrar]**. El formulario adaptable está habilitado para [!DNL Adobe Analytics].
1. Publicar el formulario.

Después de habilitar [!DNL Adobe Analytics] para un formulario adaptable, puede [validate](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=en#validate-the-page-view-beacon) si hay un flujo de eventos de datos adecuado entre AEM Forms y [!DNL Adobe Analytics]. La integración de AEM Forms con Adobe Analytics ha finalizado. Ahora puede [configurar y ver informes en Adobe Analytics](#view-reports-adobe-analytics).

### Crear reglas para capturar eventos personalizados (opcional) {#capture-custom-events}

Cree reglas sobre campos específicos de un formulario adaptable mediante el editor de reglas para enviar datos de Analytics de un formulario adaptable a [!DNL Adobe Analytics].

En un proceso de dos etapas, se define una regla en un campo de forma adaptativa. La regla envía un evento. El nombre del evento se asigna a un evento de captura personalizado en Launch de Adobe.

Para crear reglas utilizando el editor de reglas en un formulario adaptable:

1. Pulse el campo y seleccione ![Editor de reglas](assets/rule-editor-icon.svg) para abrir la página del editor de reglas.
1. Defina una condición en la variable [!UICONTROL When] de la regla.
1. En el [!UICONTROL Entonces] de la regla, seleccione **[!UICONTROL Evento de envío]** de la variable **[!UICONTROL Seleccionar acción]** lista desplegable.
1. Especifique el nombre del evento en la variable **[!UICONTROL Nombre del evento de tipo]** campo .

Por ejemplo, si la fecha de nacimiento es anterior a una fecha determinada, AEM Forms envía la variable **Seguridad** evento.

![Evento de envío](assets/security-event.png)

Para asignar el evento a un evento de captura personalizado en [!DNL Adobe Analytics]:

1. [Crear una regla](#configure-rules).

1. En el **[!UICONTROL Eventos]** sección, toque **[!UICONTROL Agregar]**.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como el nombre de la extensión.

1. Select **[!UICONTROL Capturar evento personalizado]** de la variable **[!UICONTROL Tipo de evento]** lista desplegable.

1. Especifique el nombre del evento que especificó en el paso 4 al crear una regla con el editor de reglas.

1. Toque **Conservar cambios** y realizar el resto de las acciones especificadas en [Configurar reglas](#configure-rules).

## 3. Configure y vea los informes en [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

Después de configurar un formulario adaptable para enviar datos de evento a [!DNL Adobe Analytics], puede empezar a ver los informes en [!DNL Adobe Analytics]:

1. Toque ![Seleccionar producto](assets/select-analytics.png) y seleccione **[!UICONTROL Analytics]**.

1. Toque **[!UICONTROL Crear proyecto]** y seleccione **[!UICONTROL Proyecto en blanco]**.

1. Seleccione el nombre del grupo de informes en la lista desplegable de la parte superior derecha de la forma libre.

1. Especifique **Título del formulario** en el **[!UICONTROL Buscar elementos de dimensión]** para ver todos los títulos de los formularios.

1. Coloque el título del formulario adaptable en el **[!UICONTROL Coloque un segmento aquí (o cualquier otro componente)]** cuadro de texto.

1. En el **[!UICONTROL Métricas]** , suelte los eventos a los que realizar el seguimiento **[!UICONTROL Coloque una métrica aquí (o cualquier otro componente)]** cuadro de texto.

1. Toque ![Visualizaciones](assets/visualization-icon.svg) y suelte un tipo de gráfico en la sección Forma libre . Del mismo modo, puede agregar varios tipos de gráficos a la sección Forma libre.

1. Pulse Ctrl + S y especifique un nombre para guardar el proyecto.

<!--

## Add AEM Forms and Adobe Analytics integration specific rules to Dispatcher {#forms-specific-rules-to-dispatcher}

Add AEM Forms and Adobe Analytics integration specific rules to filter the data traffic that is sent to the backend.

Perform the following steps to add AEM Forms and Adobe Analytics integration specific rules to Dispatcher for Experience Manager Forms as a Cloud Service:

1. Open your AEM Project and navigate to `\src\conf.dispatcher.d\filters`.
1. Open `filters.any` file for editing and add the following rule at the end of the file:

     ```json
     /00XX { /type "allow" /path "/content/forms/af/*" /method "POST" /selectors '(analyticsconfigparser)' /extension '(jsp|json)' }
     ```

1. Save and close the file.
1. Compile and deploy the project to your [!DNL AEM Forms] as a Cloud Service environment.



## Limitations {#limitations}

* Adobe Analytics can track form metrics only for authenticated users.

-->
