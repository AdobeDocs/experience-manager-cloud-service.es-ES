---
title: Etiquetas inteligentes mejoradas
description: Aplique etiquetas comerciales contextuales y descriptivas mediante el servicio AI y ML de Adobe Sensei para mejorar la detección de recursos y la velocidad de contenido.
contentOwner: AG
translation-type: tm+mt
source-git-commit: bf7bb91dd488f39181a08adc592971d6314817de
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 12%

---


# Configuración de Experience Manager para el etiquetado inteligente de recursos {#configure-aem-for-smart-tagging}

El etiquetado de recursos con vocabulario controlado por taxonomía garantiza que los recursos se puedan identificar y recuperar fácilmente mediante búsquedas basadas en etiquetas. Adobe proporciona etiquetas inteligentes que utilizan inteligencia artificial y algoritmos de aprendizaje automático para formar imágenes. Smart Tags utiliza un marco de inteligencia artificial de [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial.

La funcionalidad Etiquetas inteligentes está disponible para su compra como complemento de [!DNL Experience Manager]. Después de realizar la compra, se envía un correo electrónico al administrador de la organización con un vínculo a Adobe I/O. El administrador accede al vínculo para integrar las etiquetas inteligentes con [!DNL Experience Manager] Adobe I/O.

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
4. Post-GA, if time permits, create a video.
-->

## Integración con Adobe I/O {#aio-integration}

Para poder etiquetar las imágenes con SCS, integre [!DNL Adobe Experience Manager] el servicio de etiquetas inteligentes con Adobe I/O. En el back-end, el [!DNL Experience Manager] servidor autentica las credenciales de servicio con la puerta de enlace de Adobe I/O antes de reenviar la solicitud al servicio.

* Cree una configuración en [!DNL Experience Manager] para generar una clave pública. Obtenga un certificado público para la integración de OAuth.
* Cree una integración en Adobe I/O y cargue la clave pública generada.
* Configure la [!DNL Experience Manager] instancia mediante la clave de API y otras credenciales de Adobe I/O.
* De forma opcional, habilite el etiquetado automático en la carga de recursos.

### Requisitos previos para la integración de Adobe I/O {#prerequisite-for-aio-integration}

Antes de utilizar las etiquetas inteligentes, asegúrese de lo siguiente para crear una integración en Adobe I/O:

* Una cuenta de Adobe ID que tiene privilegios de administrador para la organización.
* Las etiquetas inteligentes están activadas para su organización.

### Obtain a public certificate {#obtain-public-certificate}

Un certificado público le permite autenticar su perfil en Adobe I/O.

1. En la interfaz [!DNL Experience Manager] de usuario, acceda a **[!UICONTROL Herramientas]** > Servicios **[!UICONTROL de]** nube > Servicios **[!UICONTROL de nube]** heredados.

1. On the Cloud Services page, click **[!UICONTROL Configure Now]** under **[!UICONTROL Assets Smart Tags]**.

1. En el cuadro de diálogo **[!UICONTROL Crear configuración]** , especifique un título y un nombre para la configuración de etiquetas inteligentes. Haga clic en **[!UICONTROL Crear]**.

1. En el cuadro de diálogo **[!UICONTROL AEM Smart Content Service]** , utilice los valores siguientes:

   **[!UICONTROL URL de servicio]**: `https://mc.adobe.io/marketingcloud/smartcontent`

   **[!UICONTROL Servidor de autorización]**: `https://ims-na1.adobelogin.com`

   Deje el resto de campos en blanco por ahora (se proporcionará más tarde). Haga clic en **[!UICONTROL Aceptar]**.

   ![Cuadro de diálogo del servicio de contenido inteligente de Experience Manager para proporcionar la URL del servicio de contenido](assets/aem_scs.png)

1. Haga clic en **[!UICONTROL Descargar certificado público para la integración]** de OAuth y descargue el archivo de certificado público `AEM-SmartTags.crt`.

   ![Configuración creada para el servicio de etiquetado inteligente](assets/download_link.png)

### Volver a configurar si un certificado caduca {#certrenew}

Cuando caduca el certificado, ya no es de confianza. Para agregar un nuevo certificado, siga estos pasos. No puede renovar un certificado caducado.

1. Log in your [!DNL Experience Manager] deployment as an administrator. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.

1. Busque y haga clic en **[!UICONTROL dam-update-service]** user. Haga clic en la ficha **[!UICONTROL Almacén]** de claves.
1. Elimine la **[!UICONTROL similitud existente en el almacén de claves de búsqueda]** con el certificado caducado. Click **[!UICONTROL Save &amp; Close]**.

   ![Eliminar la entrada de búsqueda por similitudes existente en Keystore para agregar un nuevo certificado de seguridad](assets/smarttags_delete_similaritysearch_keystore.png)

   *Figura: Elimine la`similaritysearch`entrada existente en Keystore para agregar un nuevo certificado de seguridad.*

1. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Servicios de nube heredados]**. Haga clic en **[!UICONTROL Etiquetas inteligentes de recursos]** > **[!UICONTROL Mostrar configuración]** > **[!UICONTROL Configuraciones disponibles]**. Haga clic en la configuración requerida.

1. Para descargar un certificado público, haga clic en **[!UICONTROL Descargar certificado público para la integración]** de OAuth.

1. Acceda a [https://console.adobe.io](https://console.adobe.io) y vaya al servicio existente en el proyecto. Cargue el nuevo certificado. Para obtener más información, consulte las instrucciones de [Creación de la integración](#create-aio-integration)de Adobe I/O.

### Creación de una integración {#create-aio-integration}

Para utilizar las API de etiquetas inteligentes, cree una integración en Adobe I/O para generar la clave de API, el ID de cuenta técnica, el ID de organización y el Secreto de cliente.

1. Acceda a [https://console.adobe.io](https://console.adobe.io/).
1. Seleccione la cuenta adecuada y compruebe que la función de organización asociada sea administrador del sistema. Cree un proyecto o abra un proyecto existente. En la página del proyecto, haga clic en **[!UICONTROL Añadir API]**.
1. En la página **[!UICONTROL Añadir una API]** , seleccione **[!UICONTROL Experience Cloud]** y seleccione Contenido **** inteligente. Haga clic en **[!UICONTROL Continuar]**.
1. En la página siguiente, seleccione **[!UICONTROL Nueva integración]**. Haga clic en **[!UICONTROL Continuar]**.
1. En la página Detalles **[!UICONTROL de la]** integración, especifique un nombre para la puerta de enlace de integración y agregue una descripción.
1. En los certificados **[!UICONTROL de claves]** públicas, cargue el `AEM-SmartTags.crt` archivo que descargó anteriormente.
1. Haga clic en **[!UICONTROL Crear integración]**.
1. Para vista de la información de la integración, haga clic en **[!UICONTROL Continuar a los detalles]** de la integración.

   ![En la ficha Información general, puede revisar la información proporcionada para la integración.](assets/integration_details.png)

### Configurar etiquetas inteligentes {#configure-smart-content-service}

Para configurar la integración, utilice los valores de los campos de ID de cuenta técnica, ID de organización, Secreto de cliente, Servidor de autorización y clave de API de la integración de Adobe I/O. La creación de una configuración de nube de etiquetas inteligentes permite la autenticación de solicitudes de API desde la [!DNL Experience Manager] instancia.

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas > Servicio de nube > Servicios]** de nube heredados para abrir la consola de [!UICONTROL Cloud Services] .
1. En Etiquetas **[!UICONTROL inteligentes de]** recursos, abra la configuración creada anteriormente. En la página de configuración del servicio, haga clic en **[!UICONTROL Editar]**.
1. En el cuadro de diálogo **[!UICONTROL AEM Smart Content Service]**, utilice los valores predefinidos para los campos **[!UICONTROL URL de servicio]** y **[!UICONTROL Servidor de autorización]**.
1. Para los campos **[!UICONTROL Clave de API]**, **[!UICONTROL Id de cuenta técnica]**, **[!UICONTROL Id de organización]** y **[!UICONTROL Secreto de cliente]**, utilice los valores generados anteriormente.

### Validar la configuración {#validate-the-configuration}

Después de completar la configuración, puede utilizar un MBean de JMX para validar la configuración. Para validar, siga estos pasos.

1. Acceda a su [!DNL Experience Manager] servidor en `https://[aem_server]:[port]`.

1. Vaya a **[!UICONTROL Herramientas > Operaciones > Consola]** Web para abrir la consola OSGi. Haga clic en **[!UICONTROL Principal > JMX]**.
1. Haga clic en **[!UICONTROL com.day.cq.dam.similaritysearch.internal.impl]**. Abre **[!UICONTROL SimilitudBuscar Tareas diversas.]**.
1. Haga clic en **[!UICONTROL validateConfigs()]**. En el cuadro de diálogo **[!UICONTROL Validar configuraciones]** , haga clic en **[!UICONTROL Invocar]**.

   El resultado de validación se muestra en el mismo cuadro de diálogo.

## Habilitar el etiquetado inteligente para los recursos recientemente cargados (opcional) {#enable-smart-tagging-for-uploaded-assets}

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas > Flujo de trabajo > Modelos]**.
1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el modelo de flujo de trabajo de **[!UICONTROL recursos de actualización de DAM]**.
1. Haga clic en **[!UICONTROL Editar]** en la barra de herramientas.
1. Expanda el panel lateral para mostrar los pasos. Arrastre el paso **[!UICONTROL Recurso de etiqueta inteligente]** que está disponible en la sección Flujo de trabajo de DAM y colóquelo después del paso **[!UICONTROL Miniaturas del proceso]**.

   ![Añada el paso del recurso de etiquetas inteligentes después del paso de miniaturas de proceso en el flujo de trabajo de recursos de actualización de DAM](assets/chlimage_1-105.png)

   *Figura: Añada el paso del recurso de etiquetas inteligentes después del paso de la miniatura del proceso en el flujo de trabajo de recursos de actualización de DAM.*

1. Abra el paso que desee configurar. En **[!UICONTROL Configuración avanzada]**, compruebe que la opción **[!UICONTROL Avance del controlador]** está seleccionada.

   ![Configuración del controlador para avanzar al siguiente paso del flujo de trabajo.](assets/smart-tags-workflow-handler-setting.png)

1. En la ficha **[!UICONTROL Argumentos]** , seleccione **[!UICONTROL Omitir errores]** si desea que el flujo de trabajo ignore errores al predecir etiquetas. Para etiquetar recursos al cargarlos, independientemente de si el etiquetado inteligente está activado en las carpetas, seleccione **[!UICONTROL Omitir marca]** de etiqueta inteligente.

1. Haga clic en **[!UICONTROL Aceptar]** para cerrar el paso del proceso y, a continuación, guarde el flujo de trabajo. Haga clic en **[!UICONTROL Sincronizar]**.

>[!MORELIKETHIS]
>
>* [Etiquetado de recursos mediante un servicio inteligente](smart-tags.md)

