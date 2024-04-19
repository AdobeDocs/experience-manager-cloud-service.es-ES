---
title: Integración de AEM Assets remoto con AEM Sites
description: AEM Obtenga información sobre cómo configurar y conectar sitios de con AEM Assets aprobado en Creative Cloud.
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---


# Integración de AEM Assets remoto con AEM Sites  {#integrate-approved-assets}

La administración eficaz de los recursos digitales es crucial para ofrecer experiencias de marca atractivas y coherentes en varias plataformas en línea. Dynamic Media con funciones OpenAPI mejora la administración de recursos digitales al permitir una integración perfecta entre AEM Sites y AEM Assets remoto. AEM Esta innovadora función le permite compartir y administrar fácilmente diferentes tipos de recursos digitales aprobados en varios entornos de trabajo, lo que optimiza los flujos de trabajo para los autores de sitios y editores de contenido.

Dynamic Media AEM con funciones de OpenAPI permite a los autores de sitios utilizar recursos de DAM remoto directamente dentro del Editor de páginas de la y [Fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html), simplificando los procesos de creación y gestión de contenido.

Los usuarios pueden conectar varias instancias de AEM Sites, sin restricciones en el número máximo, a una implementación remota de DAM, una notable ventaja sobre [Recursos conectados](use-assets-across-connected-assets-instances.md) función.

![imagen](/help/assets/assets/connected-assets-rdam.png)

Después de la configuración inicial, los usuarios pueden crear páginas en la instancia de AEM Sites y agregar recursos según sea necesario. Al agregar recursos, pueden seleccionar recursos almacenados en su DAM local o examinar y utilizar los recursos disponibles en el DAM remoto.

Dynamic Media con funciones de OpenAPI ofrece otras ventajas, como acceder y utilizar recursos remotos en fragmentos de contenido, recuperar metadatos de recursos remotos y mucho más. Más información sobre el otro [Ventajas de Dynamic Media con las capacidades de OpenAPI sobre los recursos conectados](/help/assets/new-dynamic-media-apis-faqs.md).

## Antes de empezar

* Configure lo siguiente [variables de entorno](/help/implementing/cloud-manager/environment-variables.md#add-variables) AEM para los as a Cloud Service:

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxx-eyyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` hace referencia al ID de programa <br>
     `eYYYY` hace referencia al ID de entorno

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]

  o configure el [Configuración de OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html) AEM para obtener la versión 6.5 de la instancia de AEM Sites, siga estos pasos:

   1. Inicie sesión en la consola y haga clic en **[!UICONTROL OSGi] >** o utilice la dirección URL directa; por ejemplo: `http://localhost:4502/system/console/configMgr`

   1. Añada el **[!UICONTROL repositoryID]**= &quot;delivery-pxxxxx-eyyyyyy.adobeaemcloud.com&quot; y **[!UICONTROL imsClient]**= [IMSClientId]
Más información sobre [Autenticación IMS](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html).

* AEM Acceso de IMS para iniciar sesión en una instancia remota de DAM as a Cloud Service.

* Active Dynamic Media con la opción de funcionalidades de OpenAPI en el DAM remoto.

* Configure el componente Image v3 en la instancia de AEM Sites. Si el componente no está presente, descargue e instale el [paquete de contenido](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## Acceder a recursos desde DAM remoto {#fetch-assets}

Dynamic Media con funciones de OpenAPI le permite acceder a los recursos disponibles en su instancia de DAM remoto en el editor de páginas de AEM Sites AEM local y en el fragmento de contenido de la.

![imagen](/help/assets/assets/open-APIs.png)

### AEM Acceso a recursos remotos en el editor de páginas de

AEM Siga los siguientes pasos para utilizar recursos remotos en el Editor de páginas de en la instancia de AEM Sites. AEM Puede llevar a cabo esta integración en las versiones as a Cloud Service AEM y 6.5 de.

1. Ir a **[!UICONTROL Sites]** > _su sitio web_ AEM donde el **[!UICONTROL Página]** está presente y en él debe agregar el recurso remoto.
1. AEM Vaya a la página de inicio de sesión de la **[!UICONTROL Página]** en el sitio web, en **[!UICONTROL Sites]** sección donde desea agregar el recurso remoto.
1. Seleccione la página y haga clic en **[!UICONTROL Editar (_e_)]**. AEM El **[!UICONTROL Editor de página]** abre.
1. Haga clic en el contenedor de diseño y añada una **[!UICONTROL Imagen]** componente.
1. Haga clic en **[!UICONTROL Imagen]** y haga clic en ![icono de configuración](/help/assets/assets/do-not-localize/settings-icon.svg) icono.
1. Desmarque la **[!UICONTROL Heredar imagen destacada de la página]** opción.
1. Clic **[!UICONTROL Seleccionar]** y seleccione **[!UICONTROL Remoto]**.
   ![imagen](/help/assets/assets/uncheck-inherit-option.jpg)

   Se le pedirá que inicie sesión.
1. Seleccione el recurso y haga clic en **[!UICONTROL Seleccionar]**.
1. Añada un texto alternativo y haga clic en **[!UICONTROL Listo]**.
   <br> El recurso remoto aparece en el componente de imagen. También puede verificar la dirección URL de envío del recurso cuando se carga en la página o mediante la pestaña Vista previa. La dirección URL de envío indica que se accede de forma remota al recurso.

#### AEM Vídeo: Acceder a recursos remotos en el editor de páginas de

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### AEM Acceder a recursos remotos en fragmentos de contenido de

AEM Siga los siguientes pasos para utilizar recursos remotos dentro de un fragmento de contenido en la instancia de AEM Sites en el que se haya creado el fragmento de contenido. AEM AEM Puede llevar a cabo esta integración en la versión 6.5 y no en la versión as a Cloud Service de la.

1. Ir a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Seleccione la carpeta de recursos donde esté presente el fragmento de contenido.
1. Seleccione el fragmento de contenido y haga clic en **[!UICONTROL Editar (_e_)]**.

   >[!NOTE]
   >
   >AEM Si no tiene el modelo de fragmento de contenido de la, es posible que tenga que hacer lo siguiente [crear uno](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en).

1. Haga clic en ![icono de marca de verificación](/help/assets/assets/do-not-localize/checkmark-icon.svg) junto al componente de texto.
1. Seleccionar **[!UICONTROL Remoto]** para recuperar el recurso del DAM remoto. <br>
Puede elegir una de estas opciones **[!UICONTROL Local]** o **[!UICONTROL Remoto]** Repositorio DAM basado en sus necesidades.

   ![imagen](/help/assets/assets/cf-pick.jpg)
Se le pedirá que inicie sesión.
1. Seleccione el recurso y haga clic en **[!UICONTROL Seleccionar]**.
   <br> La dirección URL del recurso remoto aparece en el componente de texto.

#### AEM Vídeo: Acceder a recursos remotos en fragmentos de contenido de

>[!VIDEO](https://video.tv.adobe.com/v/3427667)
