---
title: Integrar AEM Forms con Adobe Analytics
seo-title: Learn how to integrate AEM Forms with Adobe Analytics.
exl-id: 0730432e-75b8-4b35-a377-ae4a2bee6c9f
hidefromtoc: true
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1757'
ht-degree: 81%

---

# Integración de AEM Forms con [!DNL Adobe Analytics] {#integrate-aem-forms-with-adobe-analytics}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html) |
| AEM as a Cloud Service | Este artículo |

<span class="preview"> Este documento describe el procedimiento manual para habilitar Adobe Analytics en un formulario adaptable. Sin embargo, el Adobe recomienda utilizar la variable [Habilitar Adobe Analytics para un formulario adaptable mediante la automatización de la configuración de Experience Cloud](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md). </span>

AEM Forms se integra con [Adobe Analytics](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=es) para permitirle capturar y rastrear las métricas de rendimiento de sus formularios publicados. El objetivo detrás del análisis de estas métricas es permitir que los usuarios empresariales obtengan información sobre el comportamiento del usuario final y optimizar la experiencia de captura de datos. Puede capturar y hacer un seguimiento del comportamiento de los usuarios que iniciaron sesión y no los que iniciaron sesión (anónimos) mediante Adobe Analytics para Forms adaptable.

Después de realizar las acciones mencionadas en este artículo, puede configurar y ver los informes en [!DNL Adobe Analytics], como se muestra en el siguiente vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/337262)

Puede usar [!DNL Adobe Analytics] para descubrir patrones de interacción y problemas que los usuarios afrontan al utilizar los formularios adaptables. De forma predeterminada, [!DNL Adobe Analytics] rastrea y almacena información sobre los siguientes eventos:

* **Procesar**: Número de veces que se abre un formulario.

* **Enviar**: Número de veces que se envía un formulario.

* **Abandonar**: Número de veces que los usuarios se van sin completar el formulario.

* **Error**: Número de errores identificados en el panel y en los campos del panel.

* **Ayuda**: Número de veces que un usuario abre la ayuda de un panel y los campos del panel.

* **Visita al campo**: Número de veces que un usuario visita un campo del formulario.

* **Guardar**: Número de veces que los usuarios guardan un formulario en el Portal de Forms.

Además de estos eventos predeterminados, puede definir eventos personalizados en formularios adaptables mediante un editor de reglas y asignar esos eventos a eventos en [!DNL Adobe Analytics]

La siguiente imagen ilustra las acciones que debe realizar antes de ver los informes en [!DNL Adobe Analytics]:

![Información general de Analytics](assets/analytics-workflow.png)

## 1. Configurar [!DNL Adobe Analytics] {#Configure-adobe-analytics}

Antes de configurar [!DNL Adobe Analytics], cree lo siguiente:

* Un Adobe ID para iniciar sesión en [Adobe Experience Cloud](https://experience.adobe.com/#/home).
* Un [grupo de informes](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=es).


### Instalar AEM Forms y extensiones de [!DNL Adobe Analytics] {#install-extensions}

Siga estos pasos para configurar AEM Forms y las extensiones de [Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=es):

1. Inicie sesión en Adobe Experience Cloud y seleccione un nombre adecuado para la empresa.

1. Pulse **[!UICONTROL Launch/Recopilación de datos]** y pulse **[!UICONTROL Ir a Launch/Recopilación de datos]**.

1. Pulse **[!UICONTROL Nueva propiedad]** y especifique un nombre para la configuración.

1. Especifique un nombre de dominio y pulse **[!UICONTROL Guardar]** para guardar la propiedad.

1. Pulse el nombre de configuración disponible en la lista de Propiedades de la etiqueta.

1. En la sección **[!UICONTROL Creación]**, pulse **[!UICONTROL Extensiones]**.

1. Pulse **[!UICONTROL Catálogo]** y pulse **[!UICONTROL Instalar]** para la extensión **[!UICONTROL Adobe Experience Manager Forms]**. **[!UICONTROL Adobe Experience Manager Forms]** se muestra en la lista de extensiones instaladas disponibles en la pestaña **Instalado**.

1. Pulse **[!UICONTROL Instalar]** para la extensión **[!UICONTROL Adobe Analytics]**.
1. Seleccione el nombre del grupo de informes en las listas desplegables **[!UICONTROL Grupos de informes de desarrollo]**, **[!UICONTROL Grupos de informes de pruebas]** y **[!UICONTROL Grupos de informes de producto]** y pulse **[!UICONTROL Guardar]** para guardar la extensión.

### Configurar elementos de datos {#configure-data-elements}

Puede seleccionar cualquiera de los elementos de datos configurados en una regla creada para un evento. Cuando se produce un evento en un formulario adaptable, AEM Forms envía estos elementos de datos a [!DNL Adobe Analytics].

Tras instalar la extensión **[!UICONTROL Adobe Experience Manager Forms]**, puede crear los siguientes elementos de datos:

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
   <td>PageURL<br /> </td>
   <td>PanelTitle<br /> </td>
   <td>TimeSpent</td>
  </tr>
 </tbody>
</table>

Realice los siguientes pasos para configurar los elementos de datos:

1. En la sección **[!UICONTROL Creación]**, pulse **[!UICONTROL Elementos de datos]**.

1. Pulse **[!UICONTROL Crear nuevo elemento de datos]**.

1. Especifique un nombre para el elemento de datos. Por ejemplo, título de formulario para el tipo de elemento de datos FormTitle.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como el nombre de la extensión.

1. Seleccione el **[!UICONTROL Tipo de elemento de datos]**.

1. Pulse **[!UICONTROL Guardar]** para guardar el elemento de datos.

   >[!VIDEO](https://video.tv.adobe.com/v/337472)

### Configurar reglas {#configure-rules}

Realice los siguientes pasos para crear reglas basadas en la extensión **[!UICONTROL Adobe Experience Manager Forms]**:

1. En la sección **[!UICONTROL Creación]**, pulse **[!UICONTROL Reglas]**.

1. Pulse **[!UICONTROL Crear nueva regla]**.

1. Especifique un nombre para la regla. Por ejemplo, Envío del formulario para registrar los envíos de formularios.

1. En la sección **[!UICONTROL Eventos]**, pulse **[!UICONTROL Añadir]**.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como el nombre de la extensión.

1. Seleccione el tipo de evento. La entrada para el campo **[!UICONTROL Nombre]** se rellena automáticamente en función del tipo de evento seleccionado.

1. Pulse **[!UICONTROL Conservar cambios]** para guardar el evento.

1. En la sección **[!UICONTROL Acciones]**, pulse **[!UICONTROL Añadir]**.

1. Especifique **[!UICONTROL Adobe Analytics]** como el nombre de la extensión.

1. Seleccione **[!UICONTROL Establecer variables]** como tipo de acción. Las opciones disponibles en la lista desplegable incluyen las siguientes:

   * **[!UICONTROL Establecer variables]**: Utilice este tipo de acción para definir el tipo de evento para el que se envían los elementos de datos seleccionados de AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Enviar señalización]**: Utilice este tipo de acción para enviar datos de AEM Forms a [!DNL Adobe Analytics].

   * **[!UICONTROL Borrar variables]**: Utilice este tipo de acción para borrar la pista de datos de modo que el evento se registre solo una vez en [!DNL Adobe Analytics].

     El método recomendado es usar la acción **[!UICONTROL Establecer variables]** para configurar el evento y los elementos de datos y, a continuación, utilizar **[!UICONTROL Enviar señalización]** para enviar datos y, luego, usar **[!UICONTROL Borrar variables]** para borrar la pista de datos.

1. En la sección **[!UICONTROL Props]**, asigne las opciones del grupo de informes disponibles en la lista desplegable con los elementos de datos definidos mediante [Configurar elementos de datos](#configure-data-elements).

   Por ejemplo, para enviar el elemento de datos **FormTitle** de AEM Forms a [!DNL Adobe Analytics] al enviar un formulario:
   1. En la sección **[!UICONTROL Props]**, seleccione una propiedad para el título de formulario disponible en el grupo de informes y, a continuación, pulse ![Icono de la base de datos](assets/database-icon.svg) para asignarlo al título del formulario creado en [Configurar elementos de datos](#configure-data-elements).

      ![define-props](assets/define-props.png)

   1. Pulse **[!UICONTROL Agregar otro]** para agregar más elementos de datos a la lista.

1. En la sección **[!UICONTROL Eventos]**, seleccione un evento de las opciones disponibles en el grupo de informes y pulse **[!UICONTROL Conservar cambios]**.

1. En la sección **[!UICONTROL Acciones]**, pulse + y especifique **[!UICONTROL Adobe Analytics]** como el nombre de la extensión.

1. Seleccione **[!UICONTROL Enviar señalización]** como tipo de acción. En el panel derecho, seleccione **[!UICONTROL s.t()]** para enviar datos a [!DNL Adobe Analytics] y tratarla como una vista de página o **[!UICONTROL s.tl()]** para enviar datos a [!DNL Adobe Analytics] y que no lo trate como una vista de página. Pulse **[!UICONTROL Conservar cambios]**.

1. En la sección **[!UICONTROL Acciones]**, pulse + y especifique **[!UICONTROL Adobe Analytics]** como el nombre de la extensión.

1. Seleccione **[!UICONTROL Borrar variables]** como tipo de acción. Pulse **[!UICONTROL Conservar cambios]**. Después de realizar estos pasos, la sección **[!UICONTROL Acciones]** se muestra de la siguiente forma:
   ![Configuración de acciones](assets/actions-config.png)

   Personalice la sección **[!UICONTROL Acciones]** según sus necesidades. Por ejemplo, puede definir dos **Send Beacon** pasos en un flujo de acción para enviar datos a [!DNL Adobe Analytics] y tratarla como una vista de página en un solo paso y enviar datos a [!DNL Adobe Analytics] y no la trate como una vista de página en el segundo paso.

   ![Configuración de acciones](assets/actions-config-2.png)

1. Pulse **[!UICONTROL Guardar]** para guardar la regla.

   Puede crear reglas para todos los tipos de eventos, como Abandonar, Error, Visita de campo, Ayuda, Procesar, Guardar y Enviar.

   >[!VIDEO](https://video.tv.adobe.com/v/337425)


### Flujos de publicación {#publish-flow}

Tras crear los elementos de datos y utilizarlos en las reglas, publique la configuración para recopilar datos de formulario en [!DNL Adobe Analytics].

Siga estos pasos para publicar la configuración:

1. En la sección **[!UICONTROL Publicación]**, pulse **[!UICONTROL Flujo de publicación]**.

1. Pulse **[!UICONTROL Añadir biblioteca]**, especifique un nombre y seleccione el entorno de la biblioteca.

1. Pulse **[!UICONTROL Añadir todos los recursos modificados]** y, a continuación, pulse **[!UICONTROL Guardar y generar en desarrollo]**.

1. En la sección **[!UICONTROL Desarrollo]**, pulse ![Más opciones](assets/more-options-icon.svg) y, luego, **[!UICONTROL Aprobar y publicar en producción]**.

1. Confirme que los cambios y el flujo de publicación se mostrarán pronto en la **[!UICONTROL Publicado]** sección.

![Flujo de publicación](assets/publish-flow.png)

## 2. Configurar AEM Forms {#configure-aem-forms}

Antes de crear una configuración de Launch de Adobe, cree una [Configuración de IMS de Adobe mediante Adobe Launch como solución de nube](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html?lang=es).

### Crear configuración de Adobe Launch {#create-adobe-launch-configuration}

Realice los siguientes pasos para crear una configuración de Adobe Launch:

1. En la instancia de autor de AEM Forms, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuraciones de Adobe Launch]**.

1. Seleccione una carpeta para crear la configuración y pulse **[!UICONTROL Crear]**.

1. Especifique un título para la configuración en el campo **[!UICONTROL Título]**.

1. Seleccione la [configuración de Adobe IMS asociada](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-launch/connect-aem-launch-adobe-io.html?lang=es).

1. Seleccione el nombre de la empresa utilizada mientras [configura Adobe Analytics](#Configure-adobe-analytics).

1. Seleccione el nombre de la propiedad creada mientras [configura Adobe Analytics](#install-extensions).

1. Pulse **[!UICONTROL Guardar y cerrar]**.

1. Publique la configuración.

### Habilitar [!DNL Adobe Analytics] para un formulario adaptable {#enable-analytics-adaptive-form}

Para usar la variable [!DNL Adobe Launch] en un formulario adaptable existente:

1. En la instancia de autor de AEM Forms, vaya a **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Formularios]** > **[!UICONTROL Formularios y documentos]**.
1. Seleccione el formulario adaptable y pulse **[!UICONTROL Propiedades]**.
1. En la pestaña **[!UICONTROL Básico]**, seleccione el [contenedor de configuración](#create-adobe-launch-configuration) utilizado al crear la configuración de Adobe Launch.
1. Pulse **[!UICONTROL Guardar y cerrar]**. El formulario adaptable está habilitado para [!DNL Adobe Analytics].
1. Publicar el formulario.

Tras habilitar [!DNL Adobe Analytics] para un formulario adaptable, puede [validar](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/analytics.html?lang=es#validate-the-page-view-beacon) si hay un flujo de eventos de datos adecuado entre AEM Forms y [!DNL Adobe Analytics]. La integración de AEM Forms con Adobe Analytics ha finalizado. Ahora puede [configurar y ver informes en Adobe Analytics](#view-reports-adobe-analytics).

### Crear reglas para capturar eventos personalizados (opcional) {#capture-custom-events}

Cree reglas sobre campos específicos de un formulario adaptable mediante un editor de reglas para enviar datos de Analytics de un formulario adaptable a [!DNL Adobe Analytics].

En un proceso de dos fases, usted define una regla en un campo de un formulario adaptable. La regla envía un evento. El nombre del evento se asigna a un evento de captura personalizado en Adobe Launch.

Para crear reglas utilizando un editor de reglas en un formulario adaptable:

1. Pulse el campo y seleccione ![Editor de reglas](assets/rule-editor-icon.svg) para abrir la página del editor de reglas.
1. Defina una condición en la sección [!UICONTROL Cuándo] de la regla.
1. En la sección [!UICONTROL Entonces] de la regla, seleccione **[!UICONTROL Evento de envío]** de la lista desplegable **[!UICONTROL Seleccionar acción]**.
1. Especifique el nombre del evento en el campo **[!UICONTROL Nombre del tipo de evento]**.

Por ejemplo, si la fecha de nacimiento es anterior a una fecha determinada, AEM Forms envía el evento **Seguridad**.

![Evento de envío](assets/security-event.png)

Para asignar el evento a un evento de captura personalizado en [!DNL Adobe Analytics]:

1. [Cree una regla](#configure-rules).

1. En la sección **[!UICONTROL Eventos]**, pulse **[!UICONTROL Añadir]**.

1. Especifique **[!UICONTROL Adobe Experience Manager Forms]** como el nombre de la extensión.

1. Seleccione **[!UICONTROL Capturar evento personalizado]** de la lista desplegable **[!UICONTROL Tipo de evento]**.

1. Especifique el nombre del evento que indicó en el paso 4 al crear una regla con el editor de reglas.

1. Pulse **Conservar cambios** y realice el resto de las acciones especificadas en [Configurar reglas](#configure-rules).

## 3. Configurar y ver informes en [!DNL Adobe Analytics] {#view-reports-adobe-analytics}

Después de configurar un formulario adaptable para enviar datos de evento a [!DNL Adobe Analytics], puede comenzar a ver los informes en [!DNL Adobe Analytics]:

1. Pulse ![Seleccionar producto](assets/select-analytics.png) y seleccione **[!UICONTROL Analytics]**.

1. Pulse **[!UICONTROL Crear proyecto]** y seleccione **[!UICONTROL Proyecto en blanco]**.

1. Seleccione el nombre del grupo de informes en la lista desplegable de la parte superior derecha de la forma libre.

1. Especifique **Título del formulario** en el texto **[!UICONTROL Buscar elementos de dimensión]** para ver todos los títulos de los formularios.

1. Coloque el título del formulario adaptable en el cuadro de texto **[!UICONTROL Colocar un segmento aquí (o cualquier otro componente)]**.

1. En la sección **[!UICONTROL Métricas]**, suelte los eventos que desea rastrear en el cuadro de texto **[!UICONTROL Colocar una métrica aquí (o cualquier otro componente)]**.

1. Pulse ![Visualizaciones](assets/visualization-icon.svg) y suelte un tipo de gráfico en la sección de la forma libre. Del mismo modo, puede agregar varios tipos de gráficos a la sección de la forma libre.

1. Pulse las teclas Ctrl + S y especifique un nombre para guardar el proyecto.

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

>[!MORELIKETHIS]
>
>*[Habilitar Adobe Analytics en un formulario adaptable](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)