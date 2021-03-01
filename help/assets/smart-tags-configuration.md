---
title: Etiquetas inteligentes mejoradas
description: Aplique etiquetas comerciales contextuales y descriptivas mediante el servicio AI y ML de Adobe Sensei para mejorar la detección de recursos y la velocidad de contenido.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a1213a1694a50d174b4ad1e7e4ba7c71944b861a
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 83%

---


# Configurar [!DNL Experience Manager] para el etiquetado inteligente de recursos {#configure-aem-for-smart-tagging}

El etiquetado de recursos con vocabulario controlado por taxonomía garantiza que los recursos se puedan identificar y recuperar fácilmente mediante búsquedas basadas en etiquetas. Adobe proporciona etiquetas inteligentes que utilizan inteligencia artificial y algoritmos de aprendizaje automático para formar imágenes. Las etiquetas inteligentes utilizan un marco de inteligencia artificial de [Adobe Sensei](https://www.adobe.com/sensei/experience-cloud-artificial-intelligence.html) para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial.

La funcionalidad Etiquetas inteligentes está disponible para su compra como complemento de [!DNL Experience Manager]. Después de realizar la compra, se envía un correo electrónico al administrador de la organización con un vínculo a Adobe Developer Console. El administrador accede al vínculo para integrar las etiquetas inteligentes con [!DNL Experience Manager] Adobe Developer Console.

<!-- TBD: 
1. Can a similar flowchart be created about how training works in CS? ![flowchart](assets/flowchart.gif)
2. Is there a link to buy SCS or initiate a sales call.
3. Keystroke all steps and check all screenshots.
-->

>[!IMPORTANT]
>
>Si las implementaciones de [!DNL Experience Manager Assets] se crearon después de la [versión de agosto de 2020](/help/release-notes/release-notes-cloud/2020/release-notes-2020-8-0.md#assets), [!DNL Adobe Developer Console] se integra de forma predeterminada. Ayuda a configurar la funcionalidad de las etiquetas inteligentes más rápido. En las implementaciones anteriores, los administradores pueden configurar manualmente la integración con las instrucciones siguientes.

## Integración con Adobe Developer Console {#aio-integration}

Para poder etiquetar las imágenes mediante SCS, integre [!DNL Adobe Experience Manager] el servicio de etiquetas inteligentes con Adobe Developer Console. En el back-end, el [!DNL Experience Manager] servidor autentica las credenciales del servicio con la puerta de enlace de Adobe Developer Console antes de reenviar la solicitud al servicio.

* Cree una configuración en [!DNL Experience Manager] para generar una clave pública. [Obtenga un certificado público para la integración de OAuth.](#obtain-public-certificate)
* [Cree una integración en Adobe Developer Console y cargue la clave pública generada.](#create-aio-integration)
* [Configure las etiquetas inteligentes](#configure-smart-content-service) en su [!DNL Experience Manager] instancia utilizando la clave de API y otras credenciales de Adobe Developer Console.
* [Compruebe la configuración](#validate-the-configuration).
* [Vuelva a configurar una vez caducado ](#certrenew)el certificado.

### Requisitos previos para la integración de Adobe Developer Console {#prerequisite-for-aio-integration}

Antes de utilizar las etiquetas inteligentes, asegúrese de lo siguiente para crear una integración en Adobe Developer Console:

* Cuenta de Adobe ID que tiene privilegios de administrador para la organización.
* Las etiquetas inteligentes están activadas para su organización.

### Obtención de un certificado público {#obtain-public-certificate}

El certificado público permite autenticar el perfil en Adobe Developer Console. Puede crear un certificado desde [!DNL Experience Manager].

1. En la [!DNL Experience Manager] interfaz de usuario, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**.

1. En la página [!UICONTROL Configuraciones de IMS de Adobe], haga clic en **[!UICONTROL Crear]**. En el menú **[!UICONTROL Solución de Cloud,]** seleccione **[!UICONTROL Etiquetas inteligentes]**.

1. Seleccione **[!UICONTROL Crear nuevo certificado]**. Proporcione un nombre y haga clic en **[!UICONTROL Crear certificado]**. Haga clic en **[!UICONTROL Aceptar]**.

1. Haga clic en **[!UICONTROL Descargar clave pública]**.

   ![[!DNL Experience Manager] Etiquetas inteligentes crear clave pública](assets/aem_smarttags-config1.png)

### Creación de una integración {#create-aio-integration}

Para utilizar etiquetas inteligentes, cree una integración en Adobe Developer Console para generar clave de API, ID de cuenta técnica, ID de organización y Secreto de cliente.

1. Acceda a [https://console.adobe.io](https://console.adobe.io/) en el explorador. Seleccione la cuenta adecuada y compruebe que la función de organización asociada sea administrador del sistema.
1. Cree un proyecto con el nombre que desee. Haga clic en **[!UICONTROL Añadir API]**.
1. En la página **[!UICONTROL Add an API]**, seleccione **[!UICONTROL Experience Cloud]** y, a continuación, **[!UICONTROL Smart Content]**. Haga clic en **[!UICONTROL Siguiente]**. 
1. Seleccione **[!UICONTROL Cargar la clave pública]**. Proporcione el archivo de certificado descargado de [!DNL Experience Manager]. Se muestra un mensaje con las [!UICONTROL claves públicas cargadas correctamente]. Haga clic en **[!UICONTROL Siguiente]**. 
1. [!UICONTROL La página de ] credenciales Crear una nueva cuenta de servicio (JWT) muestra la clave pública de la cuenta de servicio. Haga clic en **[!UICONTROL Siguiente]**. 
1. En la página **[!UICONTROL Seleccionar perfiles de producto]**, seleccione **[!UICONTROL Servicios de contenido inteligente]**. Haga clic en **[!UICONTROL Guardar API configurada]**. La página muestra más información sobre la configuración. Mantenga esta página abierta para copiar y añadir estos valores en [!DNL Experience Manager] al configurar las etiquetas inteligentes en [!DNL Experience Manager].

   ![En la pestaña Información general, puede revisar la información proporcionada para la integración.](assets/integration_details.png)

### Configuración de las etiquetas inteligentes {#configure-smart-content-service}

Para configurar la integración, utilice los valores de los campos Carga útil, Secreto del cliente, Servidor de autorización y Clave de API de la integración de Adobe Developer Console.

1. En la [!DNL Experience Manager] interfaz de usuario, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**.
1. Acceda a la página **[!UICONTROL Configuración de cuenta técnica de Adobe IMS]** y proporcione el **[!UICONTROL título]**.
1. En el campo **[!UICONTROL Servidor de autorización]**, proporcione `https://ims-na1.adobelogin.com` la dirección URL.
1. En el campo **[!UICONTROL Clave de API,]** especifique el **[!UICONTROL ID de cliente]** desde el [!DNL Adobe Developer Console].
1. En el campo **[!UICONTROL Secreto del cliente,]** proporcione el **[!UICONTROL Secreto del cliente]** desde el [!DNL Adobe Developer Console]. Haga clic en la opción **[!UICONTROL Recuperar secreto de cliente]** para verlo.
1. En [!DNL Adobe Developer Console], en el proyecto, haga clic en **[!UICONTROL Cuenta de servicio (JWT)]** desde el margen izquierdo. Haga clic en la pestaña **[!UICONTROL Generar JWT]**. Haga clic en **[!UICONTROL Copiar]** para copiar la **[!UICONTROL carga útil JWT]** mostrada. Proporcione este valor en el campo **[!UICONTROL Carga útil]** de [!DNL Experience Manager]. Haga clic en **[!UICONTROL Crear]**.

### Validación de la configuración {#validate-the-configuration}

Después de completar la configuración, siga estos pasos para validarla.

1. En la [!DNL Experience Manager] interfaz de usuario, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**.

1. Seleccione la configuración de Etiquetas inteligentes. Haga clic en **[!UICONTROL Comprobar estado]** en la barra de herramientas. Haga clic en **[!UICONTROL Comprobar]**. El cuadro de diálogo con el mensaje de [!UICONTROL Configuración correcta] confirma que la configuración está funcionando.

![Validación de la configuración de etiquetas inteligentes](assets/smart-tag-config-validation.png)

### Volver a configurar si un certificado caduca {#certrenew}

Cuando caduca el certificado, ya no es de confianza. Para agregar un certificado, siga estos pasos. No puede renovar un certificado caducado.

1. Inicie sesión en la implementación [!DNL Experience Manager] como administrador. Haga clic en **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Usuarios]**.

1. Busque y haga clic en el usuario **[!UICONTROL dam-update-service]**. Haga clic en la pestaña **[!UICONTROL Almacén de claves]**.
1. Elimine el almacén de claves **[!UICONTROL similaritysearch]** y el certificado caducado. Haga clic en **[!UICONTROL Guardar y cerrar]**.

   ![Eliminar la entrada de búsqueda por similitudes existente en el almacén de claves para agregar un nuevo certificado de seguridad](assets/smarttags_delete_similaritysearch_keystore.png)

   *Figura: Elimine la  `similaritysearch` entrada existente en el almacén de claves para agregar un certificado de seguridad.*

1. En la [!DNL Experience Manager] interfaz de usuario, acceda a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**. Abra la configuración de etiquetas inteligentes disponible. Para descargar un certificado público, haga clic en **[!UICONTROL Descargar certificado público]**.

1. Acceda a [https://console.adobe.io](https://console.adobe.io) y vaya al servicio existente en el proyecto. Cargue el nuevo certificado y configúrelo. Para obtener más información sobre la configuración, consulte las instrucciones de [Creación de la integración de Adobe Developer Console.](#create-aio-integration)

## Habilitar el etiquetado automático cuando se cargan recursos (opcional) {#enable-smart-tagging-for-uploaded-assets}

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Herramientas > Flujo de trabajo > Modelos]**.
1. En la página **[!UICONTROL Modelos de flujo de trabajo]**, seleccione el modelo de flujo de trabajo de **[!UICONTROL recursos de actualización de DAM]**.
1. Haga clic en **[!UICONTROL Editar]** en la barra de herramientas.
1. Expanda el panel lateral para mostrar los pasos. Arrastre el paso **[!UICONTROL Recurso de etiqueta inteligente]** que está disponible en la sección Flujo de trabajo de DAM y colóquelo después del paso **[!UICONTROL Miniaturas del proceso]**.

   ![Añada el paso del recurso de etiquetas inteligentes después del paso de miniaturas de proceso en el flujo de trabajo de recursos de actualización de DAM](assets/chlimage_1-105.png)

   *Imagen: Añada el paso del recurso de etiquetas inteligentes después del paso de miniaturas de proceso en el flujo de trabajo de recursos de actualización de DAM*

1. Abra el paso que desee configurar. En **[!UICONTROL Configuración avanzada]**, compruebe que la opción **[!UICONTROL Avance del controlador]** está seleccionada.

   ![Configuración del controlador para avanzar al siguiente paso del flujo de trabajo.](assets/smart-tags-workflow-handler-setting.png)

1. En la pestaña **[!UICONTROL Argumentos]**, seleccione **[!UICONTROL Omitir errores]** si desea que el flujo de trabajo ignore errores al predecir etiquetas. Para etiquetar recursos al cargarlos, independientemente de si el etiquetado inteligente está activado en las carpetas, seleccione **[!UICONTROL Omitir indicador de etiqueta inteligente]**.

1. Haga clic en **[!UICONTROL Aceptar]**. Cierra el paso del proceso. Guarde el flujo de trabajo. Haga clic en **[!UICONTROL Sincronizar]**.

>[!MORELIKETHIS]
>
>* [Etiquetado de recursos mediante un servicio inteligente](smart-tags.md)

