---
title: Administrar  [!DNL Adobe Stock] recursos en [!DNL Assets].
description: Busque, recupere, conceda licencias y administre  [!DNL Adobe Stock] recursos desde  [!DNL Adobe Experience Manager]. Utilice los recursos con licencia como cualquier otro recurso digital.
contentOwner: AG
feature: Search,Adobe Stock
role: Admin,User
exl-id: 13f21d79-2a8d-4cb1-959e-c10cc44950ea
source-git-commit: 034899c2a717fafdc50cc269d6db3feb77d907c5
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 5%

---

# Usar [!DNL Adobe Stock] recursos en [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

Las organizaciones pueden integrar su [!DNL Adobe Stock] plan empresarial con [!DNL Experience Manager Assets] para garantizar que los recursos con licencia estén disponibles en general para sus proyectos creativos y de marketing, con las potentes capacidades de administración de recursos de [!DNL Experience Manager].

[!DNL Adobe Stock]El servicio proporciona a diseñadores y empresas acceso a millones de fotos, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, verificados y libres de derechos de autor para todos sus proyectos creativos. [!DNL Experience Manager] los usuarios pueden encontrar, obtener una vista previa y obtener licencias rápidamente de los  [!DNL Adobe Stock] recursos guardados en  [!DNL Experience Manager], sin salir de la  [!DNL Experience Manager] interfaz.

## Integrar [!DNL Experience Manager] y [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

Para establecer la comunicación entre [!DNL Experience Manager] y [!DNL Adobe Stock], cree una configuración de IMS y una configuración [!DNL Adobe Stock] en [!DNL Experience Manager].

>[!NOTE]
>
>Solo los [!DNL Experience Manager] administradores y [!DNL Admin Console] administradores de una organización pueden realizar la integración, ya que requiere privilegios de administrador.

### Crear una configuración de IMS {#create-an-ims-configuration}

1. En la interfaz de usuario de [!DNL Experience Manager], vaya a **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Haga clic en **[!UICONTROL Crear]** y seleccione **[!UICONTROL Solución de nube]** > **[!UICONTROL Adobe Stock]**.
1. Vuelva a utilizar un certificado existente o seleccione **[!UICONTROL Crear nuevo certificado]**.
1. Haga clic en **[!UICONTROL Crear certificado]**. Una vez creada, descargue la clave pública. Haga clic en **[!UICONTROL Siguiente]**. Deje abierta la pantalla [!UICONTROL Configuración de cuenta técnica de Adobe IMS] para proporcionar los valores necesarios en breve.
1. Acceda a [Consola de desarrollador de Adobe](https://console.adobe.io). Asegúrese de que su cuenta tiene permisos de administrador para la organización para la que se requiere la integración.
1. Haga clic en **[!UICONTROL Crear nuevo proyecto]** y en **[!UICONTROL Agregar API]**. Seleccione **[!UICONTROL Adobe Stock]** de la lista de API disponibles. Seleccione [!UICONTROL OAUTH 2.0 Web].
1. Proporcione valores **[!UICONTROL de URI de redireccionamiento predeterminado]** y **[!UICONTROL Patrón de URI de redireccionamiento]**. Haga clic en **[!UICONTROL Guardar API configurada]**. Copie el ID y el secreto generados.
1. En la pantalla [!UICONTROL Configuración de cuenta técnica de Adobe IMS] , proporcione los valores en los cuadros titulados **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]** y **[!UICONTROL Payload]**. Para obtener información detallada sobre estos valores, consulte [Inicio rápido de la autenticación JWT](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

### Crear la configuración [!DNL Adobe Stock] en [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. En [!DNL Experience Manager], vaya a **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Haga clic en **[!UICONTROL Crear]** para crear una configuración y asociarla a la configuración de IMS existente. Seleccione `PROD` como parámetro de entorno.
1. En el campo **[!UICONTROL Ruta de recursos con licencia]** , deje una ubicación tal cual. No cambie la ubicación donde desea almacenar los activos [!DNL Adobe Stock].
1. Complete la creación añadiendo todas las propiedades necesarias. Haga clic en **[!UICONTROL Guardar y cerrar]**.
1. Agregue [!DNL Experience Manager] usuarios o grupos que puedan obtener una licencia de los recursos.

>[!NOTE]
>
>Si hay varias configuraciones [!DNL Adobe Stock], seleccione la configuración que desee en el panel Preferencias de usuario. Para acceder al panel desde la página de inicio del Experience Manager, haga clic en el icono de usuario y, a continuación, haga clic en **[!UICONTROL Preferencias de usuario]** > **[!UICONTROL Configuración de stock]**.

## Usar y administrar [!DNL Adobe Stock] recursos en [!DNL Experience Manager] {#usemanage}

Con esta capacidad, las organizaciones en las que los usuarios pueden trabajar utilizan [!DNL Adobe Stock] recursos en [!DNL Experience Manager Assets]. Desde la interfaz de usuario [!DNL Experience Manager], los usuarios pueden buscar [!DNL Adobe Stock] recursos y obtener una licencia para los recursos necesarios.

Una vez que un recurso [!DNL Adobe Stock] tiene licencia en [!DNL Experience Manager], se puede utilizar y administrar como un recurso típico. En [!DNL Experience Manager], los usuarios pueden buscar y previsualizar los recursos; copiar y publicar los recursos; compartir los recursos en [!DNL Brand Portal]; acceda a los recursos y utilícelos a través de la aplicación de escritorio [!DNL Experience Manager]; y así sucesivamente.

<!--  ![Search for Adobe Stock assets and filter results from your Adobe Experience Manager workspace](assets/adobe-stock-search-results-workspace.png)

*Figure: Search for [!DNL Adobe Stock] assets and filter results from your [!DNL Experience Manager] interface.*

**A.** Search assets similar to the assets whose [!DNL Adobe Stock] ID is provided. **B.** Search assets that match your selection of shape or orientation. **C.** Search for one of more supported asset types **D.** Open or collapse the filters pane **E.** License and save the selected asset in [!DNL Experience Manager] **F.** Save the asset in [!DNL Experience Manager] with watermark **G.** Explore assets on [!DNL Adobe Stock] website that are similar to the selected asset **H.** View the selected assets on [!DNL Adobe Stock] website **I.** Number of selected assets from the search results **J.** Switch between Card view and List view -->

### Buscar recursos {#find-assets}

Los usuarios de [!DNL Experience Manager] pueden buscar recursos tanto en [!DNL Experience Manager] como en [!DNL Adobe Stock]. Cuando la ubicación de búsqueda no está limitada a [!DNL Adobe Stock], se muestran los resultados de búsqueda de [!DNL Experience Manager] y [!DNL Adobe Stock].

* Para buscar [!DNL Adobe Stock] recursos, haga clic en **[!UICONTROL Navegación]** > **[!UICONTROL Recursos]** > **[!UICONTROL Buscar en Adobe Stock]**.

* Para buscar recursos en [!DNL Adobe Stock] y [!DNL Experience Manager Assets], haga clic en buscar ![buscar](assets/do-not-localize/search_icon.png).

También puede empezar a escribir `Location: Adobe Stock` en la barra de búsqueda para seleccionar [!DNL Adobe Stock] recursos. [!DNL Experience Manager] ofrece funciones de filtrado avanzadas en los recursos buscados, lo que permite a los usuarios centrarse rápidamente en los recursos necesarios mediante filtros, como tipos de recursos admitidos, orientación de imagen y estado con licencia.

>[!NOTE]
>
>Los recursos que se buscan desde [!DNL Adobe Stock] solo se muestran en [!DNL Experience Manager]. [!DNL Adobe Stock] los recursos se recuperan y se almacenan en el  [!DNL Experience Manager] repositorio solo después de que un usuario  [guarde una ](/help/assets/aem-assets-adobe-stock.md#saveassets) licencia de  [recurso y guarde un recurso](/help/assets/aem-assets-adobe-stock.md#licenseassets). Los recursos que ya están almacenados en [!DNL Experience Manager] se muestran y resaltan para facilitar la referencia y el acceso. Además, los activos [!DNL Stock] se guardan con algunos metadatos adicionales para indicar el origen como [!DNL Stock].

![Filtros de búsqueda en el Experience Manager y recursos de Adobe Stock resaltados en los resultados de búsqueda](assets/aem-search-filters2.jpg)

*Figura: Filtros de búsqueda  [!DNL Experience Manager] y  [!DNL Adobe Stock] recursos resaltados en los resultados de búsqueda.*

### Guarde y vea los recursos necesarios {#saveassets}

Seleccione un recurso que desee guardar en [!DNL Experience Manager]. Haga clic en [!UICONTROL Guardar] en la barra de herramientas de la parte superior y proporcione el nombre y la ubicación del recurso. Los recursos sin licencia se guardan localmente con una marca de agua.

La próxima vez que busque recursos, los recursos guardados se resaltarán con un distintivo para indicar que dichos recursos están disponibles en [!DNL Experience Manager Assets].

>[!NOTE]
>
>Los recursos añadidos recientemente muestran un distintivo Nuevo en lugar de un distintivo Con licencia .

### Recursos de licencia {#licenseassets}

Los usuarios pueden obtener licencias de [!DNL Adobe Stock] recursos mediante la cuota de su [!DNL Adobe Stock] plan empresarial. Al conceder una licencia a un recurso, este se guarda sin marca de agua y está disponible para su búsqueda y uso en [!DNL Experience Manager Assets].

![Cuadro de diálogo para obtener una licencia y guardar los recursos de Adobe Stock en Experience Manager Assets](assets/aem-stock_licenseandsave.jpg)

*Figura: Cuadro de diálogo para obtener una licencia y guardar  [!DNL Adobe Stock] recursos en  [!DNL Experience Manager Assets].*

### Acceso a metadatos y propiedades de recursos {#access-metadata-and-asset-properties}

Los usuarios pueden acceder a los metadatos y previsualizarlos, incluidas las propiedades de metadatos [!DNL Adobe Stock] de los recursos guardados en [!DNL Experience Manager], y agregar **[!UICONTROL Referencias de licencia]** para un recurso. Sin embargo, las actualizaciones de la referencia de licencia no se sincronizan entre los sitios web [!DNL Experience Manager] y [!DNL Adobe Stock].

Los usuarios pueden ver las propiedades de los recursos, con licencia y sin licencia.

![Ver y acceder a metadatos y referencias de licencia de recursos guardados](assets/metadata_properties.jpg)

*Figura: Vea y acceda a metadatos y referencias de licencia de recursos guardados.*

## Limitaciones conocidas {#known-limitations}

* **La advertencia de imagen editorial no se muestra**: Al conceder licencias para una imagen, los usuarios no pueden comprobar si una imagen es de uso editorial solamente. Para evitar un posible uso indebido, los administradores pueden desactivar el acceso del Admin Console a los recursos editoriales.

* **Se muestra** un tipo de licencia incorrecto: Es posible que se muestre un tipo de licencia incorrecto en  [!DNL Experience Manager] para un recurso. Los usuarios pueden iniciar sesión en el sitio web [!DNL Adobe Stock] para ver el tipo de licencia.

* **Los campos de referencia y los metadatos no se sincronizan**: Cuando un usuario actualiza un campo de referencia de licencia, la información de referencia de licencia se actualiza en  [!DNL Experience Manager] pero no en el  [!DNL Adobe Stock] sitio web. Del mismo modo, si el usuario actualiza los campos de referencia en el sitio web [!DNL Adobe Stock], las actualizaciones no se sincronizan en [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutorial de vídeo sobre el uso de Adobe Stock Assets con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html)
>* [Ayuda del plan empresarial de Adobe Stock](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)
>* [Preguntas frecuentes sobre Adobe Stock](https://helpx.adobe.com/stock/faq.html)

