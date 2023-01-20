---
title: Cómo integrar Adobe Sign con AEM Forms
description: Obtenga información sobre cómo configurar Adobe Sign para  [!DNL AEM Forms]  as a Cloud Service.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 609c3072-1c3d-43fa-898a-b4e62db8483b
source-git-commit: 72c53bf69c36c265d25d136c0d2887cac2fe98fc
workflow-type: ht
source-wordcount: '1028'
ht-degree: 100%

---

# Integrar [!DNL Adobe Sign] con [!DNL AEM Forms] as a Cloud Service  {#integrate-adobe-sign-with-aem-forms}

[!DNL Adobe Sign] activa los flujos de trabajo de firma electrónica para formularios adaptables. Las firmas electrónicas mejoran los flujos de trabajo para procesar documentos para el área legal, ventas, nóminas, administración de recursos humanos y muchas más.

Cuando se trabaja con [!DNL Adobe Sign] y los formularios adaptables, normalmente los usuarios rellenan un formulario adaptable para solicitar un servicio. Por ejemplo, una solicitud de tarjeta de crédito y un formulario de solicitud para una prestación. Cuando un usuario rellena, envía y firma el formulario de solicitud, este se envía al proveedor de servicios para que realice más acciones. El proveedor de servicios revisa la solicitud y utiliza [!DNL Adobe Sign] para marcarla como aprobada. Para habilitar flujos de trabajo de firma electrónica similares, puede integrar [!DNL Adobe Sign] con [!DNL AEM Forms].

Para usar [!DNL Adobe Sign] con [!DNL AEM Forms], configure [!DNL Adobe Sign] en AEM Cloud Services:

## Requisitos previos {#prerequisites}

Para integrar [!DNL Adobe Sign] con [!DNL AEM Forms], necesita lo siguiente:

* una [cuenta de desarrollador de Adobe Sign](https://acrobat.adobe.com/es/es/sign/developer-form.html) activa;
* un [aplicación API de Adobe Sign](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/create_app.md);
* las credenciales (ID de cliente y Secreto de cliente) de la aplicación API de [!DNL Adobe Sign];
* usar una [clave criptográfica idéntica](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html?lang=es#make-sure-you-properly-replicate-encryption-keys-when-needed) para las instancias de autor y publicación;
* (solo para la autenticación basada en documentos de identidad oficiales) [Habilitar el método de autenticación](https://helpx.adobe.com/es/sign/using/adobesign-authentication-government-id.html#AuditReport) para la autenticación de documentos de identidad oficiales.

## Configuración de [!DNL Adobe Sign] con [!DNL AEM Forms] {#configure-adobe-sign-with-aem-forms}

Una vez cumplidos los requisitos previos, realice los siguientes pasos para configurar [!DNL Adobe Sign] con [!DNL AEM Forms] en las instancias de autor.

1. En la instancia de autor de AEM Forms, vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL General]** > **[!UICONTROL Explorador de configuración]**.
1. En la página **[!UICONTROL Explorador de configuración]**, pulse **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Crear configuración]**, especifique un **[!UICONTROL Título]** para la configuración, habilite **[!UICONTROL Configuraciones de nube]** y pulse **[!UICONTROL Crear]**. Crea un contenedor de configuración para almacenar servicios en la nube. Asegúrese de que el nombre de la carpeta no contenga ningún espacio.
1. Vaya a **[!UICONTROL Herramientas]** ![martillo](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]** y abra el contenedor de configuración que creó en el paso anterior.

   >[!NOTE]
   >
   >Cuando cree un formulario adaptable, especifique el nombre del contenedor en el campo **[!UICONTROL Contenedor de configuración]**.

1. En la página de configuración, pulse **[!UICONTROL Crear]** para crear una configuración de [!DNL Adobe Sign] en AEM Forms.
1. En la pestaña **[!UICONTROL General]** de la página **[!UICONTROL Crear configuración de Adobe Sign]**, especifique un **[!UICONTROL Nombre]** para la configuración y pulse **[!UICONTROL Siguiente]**. Si lo desea, puede especificar un **[!UICONTROL Título]** y examinar los archivos para seleccionar una **[!UICONTROL miniatura]** para la configuración.

1. Copie la URL de la ventana actual del explorador en un bloc de notas. La URL es necesaria para configurar la aplicación [!DNL Adobe Sign] con [!DNL AEM Forms] en un paso posterior. Pulse **[!UICONTROL Siguiente]**.

1. En la pestaña **[!UICONTROL Configuración]**, el campo **[!UICONTROL URL de OAuth]** contiene la URL predeterminada. El formato del URL es el siguiente:

   `https://<shard>/public/oAuth/v2`

   Por ejemplo:
   `https://secure.na1.echosign.com/public/oauth/v2`

   donde:

   **na1** hace referencia a la partición predeterminada de la base de datos. Puede modificar el valor de la partición de la base de datos. Asegúrese de que las configuraciones en la nube de [!DNL  Adobe Sign] apuntan a la [partición correcta](https://helpx.adobe.com/es/sign/using/identify-account-shard.html).

   Si crea otra configuración de [!DNL Adobe Sign] para una función o componente de Adobe Experience Manager, asegúrese de que todas las configuraciones en la nube de [!DNL Adobe Sign] apuntan a la misma partición.

   >[!NOTE]
   >
   > Mantenga la página **Crear la configuración de Adobe Sign** abierta. No la cierre. Puede recuperar la **ID de cliente** y el **Secreto de cliente** después de configurar OAuth para la aplicación [!DNL Adobe Sign] como se describe en los pasos siguientes.


1. Configure OAuth para la aplicación [!DNL Adobe Sign]:

   1. Abra una ventana del explorador e inicie sesión en su cuenta de desarrollador de [!DNL Adobe Sign].
   1. Seleccione la aplicación configurada para [!DNL AEM Forms] y pulse **[!UICONTROL Configurar OAuth para aplicación]**.
   1. En el cuadro **[!UICONTROL URL de redireccionamiento]**, añada la URL copiada en el paso anterior (Paso 7) y haga clic en **[!UICONTROL Guardar]**.
   1. Habilite el siguiente ámbito para la aplicación [!DNL Adobe Sign] y haga clic en **[!UICONTROL Guardar]**.
   * [!DNL aggrement_read]
   * [!DNL aggrement_write]
   * [!DNL aggrement_send]
   * [!DNL widget_read]
   * [!DNL widget_write]
   * [!DNL workflow_read]

   Para obtener información paso a paso sobre cómo configurar OAuth para una aplicación [!DNL Adobe Sign] y obtener las claves, consulte la documentación para desarrolladores [Configurar OAuth para la aplicación](https://www.adobe.io/apis/documentcloud/sign/docs.html#!adobedocs/adobe-sign/master/gstarted/configure_oauth.md).

   ![Configuración de OAuth](assets/oauthconfig_new.png)

1. Vuelva a la página **[!UICONTROL Crear configuración de Adobe Sign]**. En la pestaña **[!UICONTROL Configuración]**, especifique la [**[!UICONTROL ID de cliente]** (también denominada como ID de aplicación) y el **[!UICONTROL Secreto de cliente]**]. Utilice el [ID de cliente y el Secreto de cliente de la aplicación Adobe Sign](https://opensource.adobe.com/acrobat-sign/developer_guide/helloworld.html#get-the-app-id-and-secret) que creó en el paso anterior.

1. Seleccione la opción **[!UICONTROL Habilitar Adobe Sign para archivos adjuntos]** para anexar los archivos adjuntos a un formulario adaptable al documento de [!DNL Adobe Sign]correspondiente enviado para su firma.

1. Pulse **[!UICONTROL Conectar con Adobe Sign]**. Cuando se le soliciten credenciales, indique el nombre de usuario y la contraseña de la cuenta utilizada al crear la aplicación [!DNL Adobe Sign]. Cuando se le pida que confirme el acceso de `your developer account`, haga clic en **[!UICONTROL Permitir acceso]**. Si las credenciales son correctas y permite a [!DNL AEM Forms] acceder a su cuenta de desarrollador de [!DNL Adobe Sign], aparecerá un mensaje de éxito similar al siguiente.

   ![La configuración en la nube de Adobe Sign se ha completado correctamente](assets/adobe-sign-cloud-configuration-success.png)

1. Pulse **[!UICONTROL Crear]** para crear la configuración de [!DNL Adobe Sign].

1. Seleccione la configuración y haga clic en **[!UICONTROL Publicar]**, seleccione la configuración y haga clic en **[!UICONTROL Publicar]**. Esto replicará la configuración en los entornos de publicación correspondientes.

1. Repita todos los pasos anteriores en las instancias de desarrollador, fase y producción (cualquiera de las restantes) para completar la configuración de [!DNL Adobe Sign] con [!DNL AEM Forms] para su entorno.

Ahora puede [usar Agregar campos de Adobe Sign a un formulario adaptable](working-with-adobe-sign.md). Asegúrese de agregar el contenedor de configuración utilizado para Cloud Service a todos los formularios adaptables habilitados para [!DNL Adobe Sign]. Puede especificar un contenedor de configuración desde las propiedades de un formulario adaptable.

## (Solo para flujos de trabajo de AEM) Configure el planificador de [!DNL Adobe Sign] para sincronizar el estado de firma. {#configure-adobe-sign-scheduler-to-sync-the-signing-status}

Cuando utilice el paso del flujo de trabajo [!DNL Adobe Sign] para firmar un formulario adaptable, el formulario se puede pasar de un firmante a otro o se puede enviar a todos los firmantes simultáneamente, en función de la configuración del paso del flujo de trabajo. Los formularios adaptables habilitados para [!DNL Adobe Sign] se envían al servidor de Experience Manager Forms solo después de que todos los firmantes completen el proceso de firma.

De forma predeterminada, los servicios del planificador [!DNL Adobe Sign] comprueban (sondean) la respuesta de los firmantes cada 24 horas. Puede cambiar el intervalo predeterminado para su entorno.

Para cambiar el intervalo predeterminado, especifique una [expresión Cron](https://en.wikipedia.org/wiki/Cron#CRON_expression) para la propiedad **sign.status.exp** de la configuración del **servicio de configuración de Adobe Sign**.

Por ejemplo, para ejecutar el servicio de configuración diariamente a las 00:00 a. m., establezca la propiedad **sign.status.exp** de la configuración del **servicio de configuración de Adobe Sign** para especificar `0 0 0 1/1 * ? *`. El siguiente archivo JSON muestra el ejemplo para ejecutar el servicio de configuración diariamente a las 00:00 a. m.:

```json
{
  "sign.status.exp":"0 0 0 1/1 * ? *"
}
```

Para establecer los valores de una configuración, [Generar configuraciones OSGi mediante el SDK de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=es#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [implemente la configuración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=es#deployment-process) a su instancia de Cloud Service.

<!-- , perform the following steps:

1. Log in to [!DNL AEM Forms] Server with admin credentials and navigate to **[!UICONTROL Tools]** &gt;**[!UICONTROL Operations]** &gt; **[!UICONTROL Web Console]**.

   You can also open the following URL in a browser window:
   `https://server/system/console/configMgr`

1. Locate and open the **[!UICONTROL Adobe Sign Configuration Service]** option. Specify a [cron expression](https://en.wikipedia.org/wiki/Cron#CRON_expression) in the **Status Update Scheduler Expression** field and click **Save**. For example, to run the configuration service daily at 00:00 am, specify `0 0 0 1/1 * ? *` in the **Status Update Scheduler Expression** field.

Default interval to sync status of [!DNL Adobe Sign] is now changed. -->

## Artículos relacionados {#related-articles}

* [Usar Adobe Sign en un formulario adaptable](working-with-adobe-sign.md)

* [Prácticas recomendadas para utilizar Adobe Sign con formularios adaptables](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
