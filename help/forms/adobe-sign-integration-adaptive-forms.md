---
title: ¿Cómo se integra Adobe Sign con AEM Forms?
description: Obtenga información sobre cómo configurar Adobe Sign para [!DNL AEM Forms] ¿as a Cloud Service?
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 72c53bf69c36c265d25d136c0d2887cac2fe98fc
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 1%

---

# Integrar [!DNL Adobe Sign] con [!DNL AEM Forms] as a Cloud Service  {#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] activa los flujos de trabajo de firma electrónica para Adaptive Forms. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para áreas legales, de ventas, de nómina, de gestión de recursos humanos y muchas otras áreas.

En un [!DNL Adobe Sign] y Forms adaptable, un usuario rellena un Formulario adaptable para solicitar un servicio. Por ejemplo, una solicitud de tarjeta de crédito y un formulario de beneficios para los ciudadanos. Cuando un usuario rellena, envía y firma el formulario de solicitud, este se envía al proveedor de servicios para que realice más acciones. El proveedor de servicios revisa la aplicación y utiliza [!DNL Adobe Sign] para marcar la solicitud aprobada. Para habilitar flujos de trabajo de firma electrónica similares, puede integrar [!DNL Adobe Sign] con [!DNL AEM Forms].

Para usar [!DNL Adobe Sign] con [!DNL AEM Forms], configure [!DNL Adobe Sign] en AEM Cloud Services:

## Requisitos previos {#prerequisites}

Debe integrar lo siguiente [!DNL Adobe Sign] con [!DNL AEM Forms]:

* Un activo [Cuenta de desarrollador de Adobe Sign](https://acrobat.adobe.com/us/en/sign/developer-form.html).
* Un [aplicación de API de Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md).
* Credenciales (ID de cliente y Secreto de cliente) de [!DNL Adobe Sign] aplicación API.
* Uso [clave criptográfica idéntica](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=en#make-sure-you-properly-replicate-encryption-keys-when-needed) para instancias de autor y publicación.
* (Solo para la autenticación basada en el ID del gobierno) [Habilitar el método de autenticación](https://helpx.adobe.com/sign/using/adobesign-authentication-government-id.html#AuditReport) para la autenticación de ID de gobierno.

## Configuración de [!DNL Adobe Sign] con [!DNL AEM Forms] {#configure-adobe-sign-with-aem-forms}

Una vez cumplidos los requisitos previos, realice los siguientes pasos para configurar [!DNL Adobe Sign] con [!DNL AEM Forms] en las instancias de Autor.

1. En la instancia de autor de AEM Forms, vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Explorador de configuración]**.
1. En el **[!UICONTROL Explorador de configuración]** página, toque **[!UICONTROL Crear]**.
1. En el **[!UICONTROL Crear configuración]** , especifique un **[!UICONTROL Título]** para la configuración, habilite **[!UICONTROL Configuraciones de nube]** y toque **[!UICONTROL Crear]**. Crea un contenedor de configuración para almacenar Cloud Services. Asegúrese de que el nombre de la carpeta no contenga ningún espacio.
1. Vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** y abra el contenedor de configuración que creó en el paso anterior.

   >[!NOTE]
   >
   >Cuando cree un formulario adaptable, especifique el nombre del contenedor en la variable **[!UICONTROL Contenedor de configuración]** campo .

1. En la página de configuración, pulse **[!UICONTROL Crear]** para crear [!DNL Adobe Sign] en AEM Forms.
1. En el **[!UICONTROL General]** de la pestaña **[!UICONTROL Crear configuración de Adobe Sign]** página, especifique un **[!UICONTROL Nombre]** para la configuración y pulse **[!UICONTROL Siguiente]**. Si lo desea, puede especificar un **[!UICONTROL Título]** y busque para seleccionar un **[!UICONTROL Miniatura]** para la configuración.

1. Copie la dirección URL de la ventana actual del explorador en un bloc de notas. La dirección URL es necesaria para configurar [!DNL Adobe Sign] aplicación con [!DNL AEM Forms] en un paso posterior. Toque **[!UICONTROL Siguiente]**.

1. En el **[!UICONTROL Configuración]** , la pestaña **[!UICONTROL URL de OAuth]** contiene la dirección URL predeterminada. El formato de la dirección URL es:

   `https://<shard>/public/oAuth/v2`

   Por ejemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   dónde:

   **na1** hace referencia al uso compartido predeterminado de la base de datos. Puede modificar el valor del compartido de la base de datos. Asegúrese de que la variable [!DNL  Adobe Sign] Las configuraciones de nube apuntan al [Compartimiento correcto](https://helpx.adobe.com/sign/using/identify-account-shard.html).

   Si crea otro [!DNL Adobe Sign] para una función o componente de Adobe Experience Manager, asegúrese de que todas las [!DNL Adobe Sign] Las configuraciones de nube apuntan al mismo uso compartido.

   >[!NOTE]
   >
   > Mantenga el **Crear configuración de Adobe Sign** página abierta. No lo cierre. Puede recuperar **ID de cliente** y **Secreto del cliente** después de configurar la configuración de OAuth para [!DNL Adobe Sign] como se describe en los pasos siguientes.


1. Configure las opciones de OAuth para la variable [!DNL Adobe Sign] aplicación:

   1. Abra una ventana del explorador e inicie sesión en [!DNL Adobe Sign] cuenta de desarrollador.
   1. Seleccione la aplicación configurada para [!DNL AEM Forms]y toque **[!UICONTROL Configuración de OAuth para aplicación]**.
   1. En el **[!UICONTROL Dirección URL de redireccionamiento]** , añada la URL copiada en un paso anterior (paso 7) y haga clic en **[!UICONTROL Guardar]**.
   1. Active el siguiente ámbito para la variable [!DNL Adobe Sign] aplicación y haga clic en **[!UICONTROL Guardar]**.
   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   Para obtener información paso a paso sobre cómo configurar las opciones de OAuth para un [!DNL Adobe Sign] y obtenga las claves, consulte [Configuración de oAuth para la aplicación](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md) documentación para desarrolladores.

   ![Configuración de OAuth](assets/oauthconfig_new.png)

1. Vuelva a la **[!UICONTROL Crear configuración de Adobe Sign]** página. En el **[!UICONTROL Configuración]** especifique el **[!UICONTROL ID de cliente]** (también denominado ID de aplicación) y **[!UICONTROL Secreto del cliente]**]. Utilice la variable [ID de cliente y Secreto de cliente de la aplicación Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) creado en el paso anterior.

1. Seleccione el **[!UICONTROL Habilitar Adobe Sign para archivos adjuntos]** para anexar archivos adjuntos a un formulario adaptable al correspondiente [!DNL Adobe Sign] documento enviado para firma.

1. Toque **[!UICONTROL Conectarse a Adobe Sign]**. Cuando se le soliciten credenciales, proporcione el nombre de usuario y la contraseña de la cuenta utilizada al crear [!DNL Adobe Sign] aplicación. Cuando se le pida que confirme el acceso para `your developer account`, haga clic en **[!UICONTROL Permitir acceso]**. Si las credenciales son correctas y se permite [!DNL AEM Forms] para acceder a su [!DNL Adobe Sign] cuenta de desarrollador, aparece un mensaje de éxito similar al siguiente.

   ![Correcto Configuración de Adobe Sign Cloud](assets/adobe-sign-cloud-configuration-success.png)

1. Toque **[!UICONTROL Crear]** para crear la variable [!DNL Adobe Sign] configuración.

1. Seleccione la configuración y haga clic en **[!UICONTROL Publicación]**, seleccione la configuración y haga clic en **[!UICONTROL Publicación]**. Duplica la configuración en los entornos de publicación correspondientes.

1. Repita todos los pasos anteriores en las instancias de desarrollador, etapa y producción (la que se quede) para completar la configuración [!DNL Adobe Sign] con [!DNL AEM Forms] para su entorno.

Ahora, puede [agregar campos de Adobe Sign a un formulario adaptable](working-with-adobe-sign.md). Asegúrese de agregar el contenedor de configuración utilizado para el Cloud Service a todos los Forms adaptables habilitados para [!DNL Adobe Sign]. Puede especificar un contenedor de configuración desde las propiedades de un formulario adaptable.

## (Solo para AEM flujos de trabajo) Configure [!DNL Adobe Sign] planificador para sincronizar el estado de firma {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Cuando utilice [!DNL Adobe Sign] Paso del flujo de trabajo para firmar un formulario adaptable, el formulario se puede pasar de un firmante a otro o se puede enviar a todos los firmantes simultáneamente, en función de la configuración del paso del flujo de trabajo. [!DNL Adobe Sign] Forms adaptable activado se envía al servidor de Experience Manager Forms solo después de que todos los firmantes hayan completado el proceso de firma.

De forma predeterminada, la variable [!DNL Adobe Sign] Scheduler Services comprueba (encuestas) la respuesta del firmante cada 24 horas. Puede cambiar el intervalo predeterminado para su entorno.

Para cambiar el intervalo predeterminado, especifique un [expresión cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) para el **sign.status.exp** propiedad de la variable **Servicio de configuración de Adobe Sign** configuración.

Por ejemplo, para ejecutar el servicio de configuración diariamente a las 00:00 a. m., establezca la variable **sign.status.exp** propiedad de la variable **Servicio de configuración de Adobe Sign** configuración para especificar `0 0 0 1/1 * ? *`. El siguiente archivo JSON muestra el ejemplo para ejecutar el servicio de configuración diariamente a las 00:00 a.m.:

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

Para establecer los valores de una configuración, [Generación de configuraciones de OSGi mediante el SDK de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart)y [implementar la configuración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) a su instancia de Cloud Service.

<!-- , perform the following steps:

1. Log in to [!DNL AEM Forms] Server with admin credentials and navigate to **[!UICONTROL Tools]** &gt;**[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   You can also open the following URL in a browser window:
   `https://server/system/console/configMgr`

1. Locate and open the **[!UICONTROL Adobe Sign Configuration Service]** option. Specify a [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression) in the **Status Update Scheduler Expression** field and click **Save**. For example, to run the configuration service daily at 00:00 am, specify `0 0 0 1/1 * ? *` in the **Status Update Scheduler Expression** field.

Default interval to sync status of [!DNL Adobe Sign] is now changed. -->

## Artículos relacionados {#related-articles}

* [Uso de Adobe Sign en un formulario adaptable](working-with-adobe-sign.md)

* [Prácticas recomendadas para utilizar Adobe Sign con Adaptive Forms](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
