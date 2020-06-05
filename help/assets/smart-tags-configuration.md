---
title: Etiquetas inteligentes mejoradas
description: Aplique etiquetas comerciales contextuales y descriptivas mediante el servicio AI y ML de Adobe Sensei para mejorar la detección de recursos y la velocidad de contenido.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 41684858f1fe516046b9601c1d869fff180320e0
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 7%

---


# Configuración de Experience Manager para el etiquetado inteligente de recursos {#configure-aem-for-smart-tagging}

El etiquetado de recursos con vocabulario controlado por taxonomía garantiza que los recursos se puedan identificar y recuperar fácilmente mediante búsquedas basadas en etiquetas. Adobe proporciona etiquetas inteligentes que utilizan inteligencia artificial y algoritmos de aprendizaje automático para formar imágenes. Smart Tags utiliza un marco de inteligencia artificial de [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial.

La funcionalidad Etiquetas inteligentes está disponible para su compra como complemento de [!DNL Experience Manager]. Después de realizar la compra, se envía un correo electrónico al administrador de la organización con un vínculo a Adobe Developer Console. El administrador accede al vínculo para integrar las etiquetas inteligentes con [!DNL Experience Manager] Adobe Developer Console.

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
4. Post-GA, if time permits, create a video.
-->

## Integración con Adobe Developer Console {#aio-integration}

Para poder etiquetar las imágenes mediante SCS, integre [!DNL Adobe Experience Manager] el servicio de etiquetas inteligentes con Adobe Developer Console. En el back-end, el [!DNL Experience Manager] servidor autentica las credenciales del servicio con la puerta de enlace de Adobe Developer Console antes de reenviar la solicitud al servicio.

* Cree una configuración en [!DNL Experience Manager] para generar una clave pública. Obtenga un certificado público para la integración de OAuth.
* Cree una integración en Adobe Developer Console y cargue la clave pública generada.
* Configure la [!DNL Experience Manager] instancia utilizando la clave de API y otras credenciales de Adobe Developer Console.
* De forma opcional, habilite el etiquetado automático en la carga de recursos.

### Requisitos previos para la integración de Adobe Developer Console {#prerequisite-for-aio-integration}

Antes de utilizar las etiquetas inteligentes, asegúrese de lo siguiente para crear una integración en Adobe Developer Console:

* Una cuenta de Adobe ID que tiene privilegios de administrador para la organización.
* Las etiquetas inteligentes están activadas para su organización.

### Obtain a public certificate {#obtain-public-certificate}

Un certificado público le permite autenticar su perfil en Adobe Developer Console. Puede crear un certificado desde dentro [!DNL Experience Manager].

1. En la interfaz [!DNL Experience Manager] de usuario, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > Configuraciones de IMS de **[!UICONTROL Adobe]**.

1. En la página Configuraciones [!UICONTROL de IMS de] Adobe, haga clic en **[!UICONTROL Crear]**. En el menú Solución **[!UICONTROL de]** Cloud, seleccione Etiquetas **[!UICONTROL inteligentes]**.

1. Seleccione **[!UICONTROL Crear nuevo certificado]**. Proporcione un nombre y haga clic en **[!UICONTROL Crear certificado]**. Haga clic en **[!UICONTROL Aceptar]**.

1. Haga clic en **[!UICONTROL Descargar clave]** pública.

   ![Las etiquetas inteligentes de Experience Manager crean una clave pública](assets/aem_smarttags-config1.png)

### Volver a configurar si un certificado caduca {#certrenew}

Cuando caduca el certificado, ya no es de confianza. Para agregar un nuevo certificado, siga estos pasos. No puede renovar un certificado caducado.

1. Log in your [!DNL Experience Manager] deployment as an administrator. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.

1. Busque y haga clic en **[!UICONTROL dam-update-service]** user. Haga clic en la ficha **[!UICONTROL Almacén]** de claves.
1. Elimine la **[!UICONTROL similitud existente en el almacén de claves de búsqueda]** con el certificado caducado. Click **[!UICONTROL Save &amp; Close]**.

   ![Eliminar la entrada de búsqueda por similitudes existente en Keystore para agregar un nuevo certificado de seguridad](assets/smarttags_delete_similaritysearch_keystore.png)

   *Figura: Elimine la`similaritysearch`entrada existente en Keystore para agregar un nuevo certificado de seguridad.*

1. En la interfaz [!DNL Experience Manager] de usuario, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > Configuraciones de IMS de **[!UICONTROL Adobe]**. Abra la configuración de etiquetas inteligentes disponible. Para descargar un certificado público, haga clic en **[!UICONTROL Descargar certificado]** público.

1. Acceda a [https://console.adobe.io](https://console.adobe.io) y vaya al servicio existente en el proyecto. Cargue el nuevo certificado y configúrelo. Para obtener más información sobre la configuración, consulte las instrucciones de [Creación de la integración](#create-aio-integration)de Adobe Developer Console.

### Creación de una integración {#create-aio-integration}

Para utilizar etiquetas inteligentes, cree una integración en Adobe Developer Console para generar clave de API, ID de cuenta técnica, ID de organización y Secreto de cliente.

1. Acceda a [https://console.adobe.io](https://console.adobe.io/) en un navegador. Seleccione la cuenta adecuada y compruebe que la función de organización asociada sea administrador del sistema.
1. Cree un proyecto con el nombre que desee. Haga clic en **[!UICONTROL Añadir API]**.
1. En la página **[!UICONTROL Añadir una API]** , seleccione **[!UICONTROL Experience Cloud]** y seleccione Contenido **** inteligente. Haga clic en **[!UICONTROL Siguiente]**. 
1. Seleccione **[!UICONTROL Cargar la clave]** pública. Proporcione el archivo de certificado descargado de [!DNL Experience Manager]. Se muestra un mensaje con las claves [!UICONTROL públicas cargadas correctamente] . Haga clic en **[!UICONTROL Siguiente]**. 
1. [!UICONTROL Crear una nueva página de credenciales] de cuenta de servicio (JWT) muestra la clave pública de la cuenta de servicio que se acaba de configurar. Haga clic en **[!UICONTROL Siguiente]**. 
1. En la página **[!UICONTROL Seleccionar perfiles]** de producto, seleccione Servicios de contenido **[!UICONTROL inteligente]**. Haga clic en **[!UICONTROL Guardar API]** configurada. Una página muestra más información sobre la configuración. Mantenga esta página abierta para copiar y agregar estos valores en Experience Manager al configurar las etiquetas inteligentes en [!DNL Experience Manager].

   ![En la ficha Información general, puede revisar la información proporcionada para la integración.](assets/integration_details.png)

### Configurar etiquetas inteligentes {#configure-smart-content-service}

Para configurar la integración, utilice los valores de los campos Carga útil, Secreto del cliente, Servidor de autorización y Clave de API de la integración de Adobe Developer Console.

1. En la interfaz [!DNL Experience Manager] de usuario, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > Configuraciones de IMS de **[!UICONTROL Adobe]**.
1. Acceda a la página Configuración **[!UICONTROL de cuenta técnica de]** Adobe IMS y proporcione un **[!UICONTROL título]**.
1. En el campo **[!UICONTROL Servidor]** de autorización, proporcione `https://ims-na1.adobelogin.com` la dirección URL.
1. En el campo Clave **** de API, especifique el ID **[!UICONTROL de]** cliente desde el [!DNL Adobe Developer Console].
1. En el campo Secreto **[!UICONTROL del]** cliente, proporcione el Secreto **[!UICONTROL del]** cliente desde el [!DNL Adobe Developer Console]. Haga clic en la opción **[!UICONTROL Recuperar secreto]** de cliente para verlo.
1. En [!DNL Adobe Developer Console], en el proyecto, haga clic en Cuenta **[!UICONTROL de servicio (JWT)]** desde el margen izquierdo. Haga clic en la ficha **[!UICONTROL Generar JWT]** . Haga clic en **[!UICONTROL Copiar]** para copiar la carga útil **** JWT mostrada. Proporcione este valor en el campo **[!UICONTROL Carga útil]** de [!DNL Experience Manager]. Haga clic en **[!UICONTROL Crear]**.

### Validar la configuración {#validate-the-configuration}

Después de completar la configuración, siga estos pasos para validar la configuración.

1. En la interfaz [!DNL Experience Manager] de usuario, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > Configuraciones de IMS de **[!UICONTROL Adobe]**.

1. Seleccione la configuración de Etiquetas inteligentes. Haga clic en **[!UICONTROL Comprobar estado]** en la barra de herramientas. Haga clic en **[!UICONTROL Comprobar]**. Un cuadro de diálogo con el mensaje de configuración  Sana confirma que la configuración está funcionando.

![Validación de la configuración de etiquetas inteligentes](assets/smart-tag-config-validation.png)

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

