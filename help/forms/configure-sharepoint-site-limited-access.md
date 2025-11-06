---
title: ¿Cómo configurar un sitio de SharePoint con acceso limitado mediante el ámbito de autorización?
description: Obtenga información sobre cómo configurar el sitio de SharePoint con acceso limitado mediante el ámbito de autorización.
keywords: Configuración del sitio de SharePoint con acceso limitado?, Configuración de SharePoint con acceso limitado, Uso del ámbito de autorización para limitar el acceso al sitio de SharePoint.
feature: Adaptive Forms, Core Components
role: User, Developer
exl-id: 3230bab2-c1aa-409d-9f01-c42cf88b1135
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 24%

---

# Configuración del sitio de SharePoint con acceso limitado mediante el ámbito de autorización

<span class="preview">: la característica está disponible en el programa de usuarios que la adoptaron por primera vez. Puede enviar un correo electrónico a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa para primeros usuarios y solicitar acceso a esta funcionalidad. </span>

El propósito del acceso limitado o restringido es mejorar la administración de la seguridad, ya que permite a los administradores controlar el acceso de los usuarios a un sitio de SharePoint en particular o a un grupo de sitios de SharePoint. El nivel de permiso es útil cuando necesita conceder a un usuario o grupo acceso a un sitio específico sin permitirle ver ningún otro sitio de SharePoint no permitido.

## Ventajas para configurar el sitio de SharePoint con acceso limitado

Ventajas para proporcionar acceso limitado al sitio de SharePoint:

* **Seguridad mejorada**: Al limitar el acceso, puede asegurarse de que sólo el personal autorizado tenga la capacidad de ver o manipular información confidencial, lo que reduce el riesgo de acceso no autorizado.

* **Principio del menor privilegio**: proporciona a los usuarios los niveles mínimos de acceso (o permisos) necesarios para realizar sus funciones de trabajo. Esto minimiza la exposición de cada usuario a partes sensibles de la red, que pueden protegerse contra posibles amenazas internas.

* **Protección de datos**: El acceso restringido ayuda a proteger los datos esenciales contra la exposición. Garantiza que solo los usuarios que necesiten ver los datos puedan acceder a ellos, lo que es esencial para cumplir con las regulaciones de protección de datos.

* **Prevención accidental de pérdida de datos**: al haber menos personas capaces de modificar el contenido, las posibilidades de eliminaciones accidentales o alteraciones de datos importantes se reducen significativamente.

* **Flujo de datos controlado**: ayuda a controlar el flujo de información dentro y fuera de la organización, asegurándose de que los datos no terminen en las manos equivocadas.

## Configuración de SharePoint con acceso limitado mediante el ámbito de autorización

Siga los pasos a continuación para configurar SharePoint Sites con acceso limitado mediante ámbitos de autorización:

1. [Cree una aplicación con ](#create-an-application-with-the-limited-permission-in-the-azure-portal)
1. [Definir el ámbito de autorización en la instancia de AEM](#set-the-authorization-scope-at-aem-instance)

### Crear una aplicación con el permiso limitado en el portal de Azure

Cree una aplicación en [Microsoft Azure Portal](https://portal.azure.com/#home) con el ámbito de permiso `Sites.Selected` en la API de Microsoft Graph.

![Sitio seleccionado de SharePoint](/help/forms/assets/sharepoint-selected-site.png)

Para obtener información sobre cómo recuperar `Client ID`, `Client Secret` y `Tenant ID` para `OAuth URL`, consulte la [documentación de Microsoft®](https://learn.microsoft.com/es-es/graph/auth-register-app-v2).

* En el portal de Microsoft® Azure, añada el URI de redireccionamiento como `https://[author-instance]/libs/cq/sharepoint/content/configurations/wizard.html`. Reemplace `[author-instance]` por la URL de su instancia de autor.
* Agregue el ámbito de permisos `offline_access` y `Sites.Selected` en la API de Graph de Microsoft para proporcionar acceso restringido a los sitios.
* Para la URL de OAuth: `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Reemplace `<tenant-id>` por el `tenant-id` de su aplicación desde el portal de Microsoft® Azure.

Para usar el permiso de API `Sites.Selected` se requiere una aplicación registrada en Azure Portal con los permisos adecuados establecidos para SharePoint Online Sites. Esta configuración garantiza que la aplicación tenga la autorización necesaria para interactuar con el sitio de SharePoint dentro del ámbito definido, lo que proporciona el acceso limitado requerido.

Consulte el [artículo del blog - Desarrollar aplicaciones que usan Sites.Permisos seleccionados para sitios de SPO](https://techcommunity.microsoft.com/t5/microsoft-sharepoint-blog/develop-applications-that-use-sites-selected-permissions-for-spo/ba-p/3790476) para obtener instrucciones sobre el desarrollo de aplicaciones que usan permisos de `Sites.Selected` para sitios de SharePoint Online.

### Definir el ámbito de autorización en la instancia de AEM

Para proporcionar acceso limitado a un sitio SharePoint de Microsoft, es esencial establecer correctamente el ámbito de autorización. Para establecer el ámbito de autorización y conectar AEM Forms a su almacenamiento de Microsoft® SharePoint:

1. Vaya a su instancia de **AEM Forms Author** > **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** >  **[!UICONTROL Microsoft® SharePoint]**.
1. Una vez seleccionada la variable **[!UICONTROL Microsoft® SharePoint]**, se le redirigirá a **[!UICONTROL Explorador SharePoint]**.
1. Seleccione un **Contenedor de configuración**. La configuración se almacena en el contenedor de configuración seleccionado.
1. Haga clic en **[!UICONTROL Crear]** > **[!UICONTROL Biblioteca de documentos de SharePoint]** en la lista desplegable. Aparecerá el asistente de configuración de SharePoint.

   ![Acceso limitado al sitio de SharePoint](/help/forms/assets/sharepoint-doc-library-limited-scopes.png)

1. Especifique **[!UICONTROL Title]**, **[!UICONTROL ID de cliente]** y **[!UICONTROL Secreto de cliente]**. Para obtener información sobre cómo recuperar el ID de cliente y el secreto de cliente, consulte [Documentación de Microsoft®](https://learn.microsoft.com/es-es/graph/auth-register-app-v2).

1. Usar URL de OAuth como `https://login.microsoftonline.com/tenant-id/oauth2/v2.0/authorize`. Reemplace `<tenant-id>` por el `tenant-id` de su aplicación desde el portal de Microsoft® Azure.

   >[!NOTE]
   >
   > El campo **secreto de cliente** es obligatorio u opcional dependiendo de su configuración de la aplicación de Azure Active Directory. Si la aplicación está configurada para utilizar un secreto de cliente, es obligatorio proporcionar dicho secreto.

1. Agregue `offline_access Sites.Selected` en el campo `Authorization Scope`. Cuando agrega el ámbito `offline_access Sites.Selected` en el campo de cuadro de texto `Authorization Scope`, el cuadro de texto `SharePoint Site ID` se vuelve visible en la pantalla.

1. Especifique el ID del sitio de SharePoint. Para obtener información sobre cómo recuperar el ID del sitio de SharePoint, consulte la sección [Bytes adicionales](#extra-bytes).

1. Haga clic en **[!UICONTROL Comprobar conexión al sitio]**. Si la conexión se realiza correctamente, aparece el mensaje `Connection Successful`.

1. Ahora, seleccione **Sitio de SharePoint** > **Biblioteca de documentos** > **Carpeta de SharePoint**, para guardar los datos.

   >[!NOTE]
   >
   >* De forma predeterminada, `forms-ootb-storage-adaptive-forms-submission` está presente en el sitio de SharePoint seleccionado.
   >* Cree una carpeta como `forms-ootb-storage-adaptive-forms-submission` si no está presente en la biblioteca `Documents` del sitio de SharePoint seleccionado haciendo clic en **Crear carpeta**.

Ahora puede usar esta configuración de [SharePoint Sites para la acción de envío en un formulario adaptable](/help/forms/configure-submit-action-sharepoint.md#use-sharepoint-document-library-configuration-in-an-adaptive-form-use-sharepoint-configuartion-in-af).

## Bytes adicionales

Para recuperar el valor de `SharePoint Site ID`:

1. Vaya a las [API de Microsoft Graph Explorer](https://developer.microsoft.com/en-us/graph/graph-explorer).
1. En el panel izquierdo, debajo de las API `SharePoint Sites`, haga clic en `Search for a SharePoint site by keyword`.
1. Reemplace el marcador de posición `contoso` por el nombre real del sitio de SharePoint para recuperar el ID de sitio correspondiente.

   ![ID. de biblioteca de documentos de SharePoint](/help/forms/assets/sharepoint-site-id.png)

Al hacer clic en el botón `Run Query`, el ID del sitio se muestra en la pantalla.
