---
title: Uso de recursos digitales de Adobe Stock en AEM Assets
description: Busque, busque, adquiera, adquiera licencias y administre recursos de Adobe Stock en Experience Manager. Trate los recursos con licencia como cualquier otro recurso Experience Manager.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b0436c74389ad0b3892d1258d993c00aa470c3ab
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 22%

---


# Use Adobe Stock assets in AEM Assets {#use-adobe-stock-assets-in-aem-assets}

Las organizaciones pueden integrar su plan empresarial de Adobe Stock con AEM Assets para garantizar que los recursos con licencia estén disponibles en general para sus proyectos creativos y de marketing, con las potentes funciones de gestión de recursos de AEM.

El servicio Adobe Stock proporciona a diseñadores y empresas acceso a millones de fotos, vectores, ilustraciones, vídeos, plantillas y recursos 3D de alta calidad, verificados y libres de derechos de autor para todos sus proyectos creativos. Los usuarios de AEM pueden buscar, previsualización y obtener licencias rápidamente de los recursos de Adobe Stock guardados en AEM, sin salir del espacio de trabajo de AEM.

## Integración de AEM y Adobe Stock {#integrate-aem-and-adobe-stock}

Para permitir la comunicación entre AEM y Adobe Stock, cree una configuración IMS y una configuración de Adobe Stock en AEM.

>[!NOTE]
>
>Solo los administradores de AEM y los administradores de Admin Console de una organización pueden realizar la integración ya que requiere privilegios de administrador.

### Create an IMS configuration {#create-an-ims-configuration}

1. Haga clic en el logotipo de AEM. Vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Seguridad]** > **[!UICONTROL Configuraciones de IMS de Adobe]**. Haga clic en **[!UICONTROL Crear]** y seleccione **[!UICONTROL Solución de nube]** > **[!UICONTROL Adobe Stock]**.
1. Vuelva a utilizar un certificado existente o seleccione **[!UICONTROL Crear nuevo certificado]**.
1. Haga clic en **[!UICONTROL Crear certificado]**. Una vez creada, descargue la clave pública. Haga clic en **[!UICONTROL Siguiente]**. 
1. Indique los valores adecuados en los campos **[!UICONTROL Título]**, **[!UICONTROL Servidor de autorizaciones]**, **[!UICONTROL Clave de API]**, **[!UICONTROL Secreto del cliente]** y **[!UICONTROL Carga]**. See [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md), for detailed information to fetch these values from Adobe Developer Console.
1. Añada la clave pública descargada en su cuenta de servicio de Adobe Developer Console.

<!--
TBD: Update this instance when AIO updates their documentation publish URL.
-->

### Creación de la configuración de Adobe Stock en AEM {#create-adobe-stock-configuration-in-aem}

1. En la interfaz de usuario de AEM, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Haga clic en **[!UICONTROL Crear]** para crear una configuración y asociarla con la configuración de IMS existente. Seleccione `PROD` como parámetro de entorno.
1. En el campo Ruta **[!UICONTROL de recursos con]** licencia, deje una ubicación tal cual. No cambie la ubicación en la que desea almacenar los recursos de Adobe Stock.
1. Complete la creación agregando todas las propiedades necesarias. Click **[!UICONTROL Save &amp; Close]**.
1. Añada usuarios o grupos de AEM que puedan obtener licencias para los recursos.

>[!NOTE]
>
>Si hay varias configuraciones de Adobe Stock, seleccione la configuración deseada en el panel Preferencias [!UICONTROL de] usuario haciendo clic en el logotipo de AEM en la interfaz de usuario de AEM.

## Uso y gestión de recursos de Adobe Stock en AEM {#usemanage}

Con esta función, las organizaciones pueden permitir que sus usuarios trabajen con los recursos de Adobe Stock en AEM Assets. Desde la interfaz de usuario de AEM, los usuarios pueden buscar recursos de Adobe Stock y obtener licencias para los recursos necesarios.

Una vez que un recurso de Adobe Stock tiene licencia en AEM, puede utilizarse y administrarse como un recurso típico. En AEM, los usuarios pueden buscar y previsualización de los recursos; copiar y publicar los recursos; compartir los recursos en Brand Portal; acceder a los recursos y utilizarlos mediante la aplicación de escritorio de AEM; y así sucesivamente.

<!--  ![Search for Adobe Stock assets and filter results from your AEM workspace](assets/adobe-stock-search-results-workspace.png)
*Figure: Search for Adobe Stock assets and filter results from your AEM workspace* -->

**A.** Busque recursos similares a los del ID de Adobe Stock proporcionado. **B.** Busque recursos que coincidan con la selección de forma u orientación. **C.** Busque uno de los tipos de recurso más admitidos **D.** Abra o contraiga el panel de filtros **E.** Obtenga la licencia y guarde el recurso seleccionado en AEM **F.** Guarde el recurso en AEM con la marca de agua **G.** Explore los recursos del sitio web de Adobe Stock que sean similares al recurso **H.** Vea los recursos seleccionados en el sitio web de Adobe Stock. **I.** Número de recursos seleccionados de los resultados de búsqueda **J.** Cambie entre la vista de tarjeta y la vista de lista

### Buscar recursos {#find-assets}

Los usuarios de AEM pueden buscar recursos tanto en AEM como en Adobe Stock. Cuando la ubicación de búsqueda no está limitada a Adobe Stock, se muestran los resultados de búsqueda de AEM y Adobe Stock.

* Para buscar recursos de Adobe Stock, haga clic en **[!UICONTROL Navegación]** > **[!UICONTROL Recursos]** > **[!UICONTROL Buscar en Adobe Stock]**.

* Para buscar recursos en Adobe Stock y AEM Assets, haga clic en el icono de búsqueda ![search_icon](assets/do-not-localize/search_icon.png).

También puede escribir `Location: Adobe Stock` inicios en la barra de búsqueda para seleccionar recursos de Adobe Stock.  AEM oferta las funciones avanzadas de filtrado en los recursos buscados, lo que permite a los usuarios iniciar rápidamente los recursos necesarios con filtros como, por ejemplo, tipos de recursos admitidos, orientación de imagen y estado con licencia.

>[!NOTE]
>
>Los recursos que se buscan desde Adobe Stock solo se muestran en AEM. Los recursos de Adobe Stock se recuperan y almacenan en el repositorio de AEM solo después de que un usuario [guarde un recurso](/help/assets/aem-assets-adobe-stock.md#saveassets) o [conceda una licencia a un recurso](/help/assets/aem-assets-adobe-stock.md#licenseassets). Los recursos que ya están almacenados en AEM se muestran y resaltan para facilitar la referencia y el acceso. Además, estos recursos se guardan con algunos metadatos adicionales para indicar el origen como Adobe Stock.

![filtros de búsqueda en AEM y recursos de Adobe Stock resaltados en los resultados](assets/aem-search-filters2.jpg)de búsqueda *Figura: Buscar filtros en AEM y recursos de Adobe Stock resaltados en los resultados de búsqueda*

### Guardar y vista de los recursos necesarios {#saveassets}

Seleccione un recurso que desee guardar en AEM. Haga clic en Guardar en la barra de herramientas de la parte superior y proporcione el nombre y la ubicación del recurso. Los recursos sin licencia se guardan localmente con una marca de agua.

La próxima vez que busque recursos, los recursos guardados se resaltarán con un distintivo para indicar que dichos recursos están disponibles en AEM Assets.

>[!NOTE]
>
>Los recursos añadidos recientemente muestran un distintivo Nuevo en lugar de un distintivo Con licencia.

### Recursos de licencia {#licenseassets}

Los usuarios pueden obtener licencias de recursos de Adobe Stock mediante la cuota de su plan de Adobe Stock Enterprise. Al otorgar licencias a un recurso, éste se guarda sin marca de agua y está disponible para su búsqueda y uso en AEM Assets.

![Cuadro de diálogo para obtener licencias y guardar recursos de Adobe Stock en AEM Assets](assets/aem-stock_licenseandsave.jpg)*Figura: Cuadro de diálogo para obtener la licencia y guardar los recursos de Adobe Stock en AEM Assets*

### Acceso a metadatos y propiedades de recursos {#access-metadata-and-asset-properties}

Los usuarios pueden acceder a los metadatos y darles previsualización, incluidas las propiedades de metadatos de Adobe Stock para los recursos guardados en AEM, así como añadir referencias **[!UICONTROL de]** licencia para un recurso. Sin embargo, las actualizaciones de la referencia de licencia no se sincronizan entre el sitio web de AEM y Adobe Stock.

Los usuarios pueden ver las propiedades de los recursos con y sin licencia.

![Vista y acceso a metadatos y referencias de licencia de recursos](assets/metadata_properties.jpg)guardados *Figura: Vista y acceso a metadatos y referencias de licencia de recursos guardados*

## Limitaciones conocidas {#known-limitations}

### No se muestra la advertencia de imagen editorial

Al otorgar licencias a una imagen, los usuarios no pueden comprobar si una imagen es solo para uso editorial. Para evitar un posible uso indebido, los administradores pueden desactivar el acceso a los recursos editoriales del Admin Console.

### Se muestra un tipo de licencia incorrecto

Es posible que se muestre un tipo de licencia incorrecto en AEM para un recurso. Los usuarios pueden iniciar sesión en el sitio web de Adobe Stock para ver el tipo de licencia.

### Los campos de referencia y los metadatos no se sincronizan

Cuando un usuario actualiza un campo de referencia de licencia, la información de referencia de licencia se actualiza en AEM, pero no en el sitio web de Adobe Stock. Del mismo modo, si el usuario actualiza los campos de referencia en el sitio web de Adobe Stock, las actualizaciones no se sincronizan en AEM.

## Related resources {#related-resources}

[Tutorial de vídeo sobre el uso de recursos de Adobe Stock con AEM Assets](https://helpx.adobe.com/experience-manager/kt/assets/using/stock-assets-feature-video-use.html)

[Ayuda del plan empresarial de Adobe Stock](https://helpx.adobe.com/enterprise/using/adobe-stock-enterprise.html)

[Preguntas más frecuentes sobre Adobe Stock](https://helpx.adobe.com/stock/faq.html)
