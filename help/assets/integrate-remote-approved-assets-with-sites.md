---
title: Integración de AEM Assets remoto con AEM Sites
description: AEM Obtenga información sobre cómo configurar y conectar sitios de con AEM Assets aprobados.
exl-id: 382e6166-3ad9-4d8f-be5c-55a7694508fa
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 15%

---

# Integración de AEM Assets remoto con AEM Sites  {#integrate-approved-assets}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>La guía de funciones de Dynamic Media con OpenAPI ya está disponible en formato de PDF. Descargue toda la guía y utilice Adobe Acrobat AI Assistant para responder a sus consultas.
>
>[!BADGE PDF de la Guía de Dynamic Media con funciones OpenAPI]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

La administración eficaz de los recursos digitales es crucial para ofrecer experiencias de marca atractivas y coherentes en varias plataformas en línea. Dynamic Media con funciones OpenAPI mejora la administración de recursos digitales al permitir una integración perfecta entre AEM Sites y los as a Cloud Service de los AEM Assets. AEM Esta innovadora función le permite compartir y administrar fácilmente diferentes tipos de recursos digitales aprobados en varios entornos de trabajo, lo que optimiza los flujos de trabajo para los autores de sitios y editores de contenido.

Dynamic Media AEM con funciones OpenAPI permite a los autores de sitios utilizar recursos de DAM remoto directamente dentro del Editor de páginas de la y [Fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments.html), lo que simplifica los procesos de creación y administración de contenido.

Los usuarios pueden conectar varias instancias de AEM Sites, sin restricciones en cuanto al número máximo, a una implementación de DAM remota, una ventaja notable con respecto a la característica [Assets conectado](use-assets-across-connected-assets-instances.md).

![imagen](/help/assets/assets/connected-assets-rdam.png)

Después de la configuración inicial, los usuarios pueden crear páginas en la instancia de AEM Sites y agregar recursos según sea necesario. Al agregar recursos, pueden seleccionar recursos almacenados en su DAM local o examinar y utilizar los recursos disponibles en el DAM remoto.

Dynamic Media con funciones de OpenAPI ofrece otras ventajas, como acceder y utilizar recursos remotos en fragmentos de contenido, recuperar metadatos de recursos remotos y mucho más. Obtenga más información sobre los otros [beneficios de Dynamic Media con capacidades OpenAPI sobre Assets conectado](/help/assets/dynamic-media-open-apis-faqs.md).

## Antes de empezar {#pre-requisites-sites-integration}

La compatibilidad con recursos remotos mediante Dynamic Media con funciones de OpenAPI requiere lo siguiente:

* AEM 6.5 SP 18+ o AEM as a Cloud Service

* Versión 2.23.2 o posterior de los componentes principales

* Configure las [variables de entorno](/help/implementing/cloud-manager/environment-variables.md#add-variables) siguientes para AEM as a Cloud Service:

   * ASSET_DELIVERY_REPOSITORY_ID= &quot;delivery-pxxxx-eyyyyyy.adobeaemcloud.com&quot; <br>
     `pXXXX` hace referencia al ID de programa <br>
     `eYYYY` hace referencia al ID de entorno

  Estas variables se configuran mediante la interfaz de usuario de Cloud Manager del entorno de AEM as a Cloud Service, que actúa como la instancia local de Sites.

   * ASSET_DELIVERY_IMS_CLIENT= [IMSClientId]: debe enviar un ticket de asistencia de Adobe para obtener el ID de cliente de IMS.

     AEM o configure la [configuración de OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/content/implementing/deploying/configuring/configuring-osgi.html) para la versión 6.5 de en la instancia de AEM Sites siguiendo estos pasos:

   1. Inicie sesión en la consola y haga clic en **[!UICONTROL OSGi] >** o
usar la dirección URL directa; por ejemplo: `https://localhost:4502/system/console/configMgr`

   1. Configure la configuración OSGi de **próxima generación** (`NextGenDynamicMediaConfigImpl`) de Dynamic Media de la siguiente manera, reemplazando los valores por los del entorno de recursos remotos.

      ```text
        imsClient="<ims-client-ID>"
        enabled=B"true"
        imsOrg="<ims-org>@AdobeOrg"
        repositoryId="<repo-id>.adobeaemcloud.com"
      ```

      `imsOrg` no es una entrada obligatoria.
      `repositoryId` = &quot;delivery-pxxxx-eyyyyyy.adobeaemcloud.com&quot;
donde `pXXXX` hace referencia al ID de programa
      `eYYYY` hace referencia al ID de entorno

      ![Ventana de configuración OSGi de la configuración de Dynamic Media de próxima generación](/help/assets/assets/remote-assets-osgi.png)

  Más información sobre la [autenticación IMS](https://experienceleague.adobe.com/docs/experience-manager-65/content/security/ims-config-and-admin-console.html).

  Para obtener más información sobre cómo configurar OSGi, consulte los siguientes documentos:

   * [Configurar OSGi para Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/configuring-osgi.html?lang=es) para AEM as a Cloud Service
   * [Configurar OSGi](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-osgi.html?lang=es) para AEM 6.5

* Acceso de IMS para iniciar sesión en una instancia remota de AEM as a Cloud Service DAM. Hace referencia al autor de Sites que tiene acceso IMS al entorno DAM remoto.

* Configure el componente Image v3 en la instancia de AEM Sites. Si el componente no está presente, descargue e instale el [paquete de contenido](https://github.com/adobe/aem-core-wcm-components/releases/tag/core.wcm.components.reactor-2.23.0).

## Configurar HTTPS {#https}

Por lo general, se recomienda ejecutar todas las instancias de AEM de producción mediante HTTP. Sin embargo, es posible que sus entornos de desarrollo local no estén configurados como tales. No obstante, los recursos remotos de Dynamic Media con OpenAPI requieren HTTPS para funcionar.

[Utilice esta guía](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/use-the-ssl-wizard.html?lang=es) para configurar HTTPS donde desee utilizar recursos remotos, incluidos entornos de desarrollo.

## Acceder a recursos desde DAM remoto {#fetch-assets}

Dynamic Media con funciones de OpenAPI le permite acceder a los recursos disponibles en su instancia de DAM remoto en el editor de páginas de AEM Sites AEM local y en el fragmento de contenido de la.

![imagen](/help/assets/assets/open-APIs.png)

### AEM Acceso a recursos remotos en el editor de páginas de {#access-assets-page-editor}

AEM Siga los siguientes pasos para utilizar recursos remotos en el Editor de páginas de en la instancia de AEM Sites. Puede llevar a cabo esta integración en AEM as a Cloud Service AEM y en 6.5.

1. AEM Vaya a **[!UICONTROL Sitios]** > _su sitio web_, donde está presente la **[!UICONTROL Página]** en la que necesita agregar el recurso remoto.
1. Seleccione la página y haga clic en **[!UICONTROL Editar (_e_)]**. AEM Se abre el **[!UICONTROL Editor de páginas]** de la.
1. Haga clic en el contenedor de diseño y agregue un componente **[!UICONTROL Image]**.
1. Haga clic en el componente **[!UICONTROL Image]** y luego en el icono ![settings](/help/assets/assets/do-not-localize/settings-icon.svg).
1. Desmarque la opción **[!UICONTROL Heredar imagen destacada de la página]**.
1. Haga clic en **[!UICONTROL Seleccionar]** y seleccione **[!UICONTROL Remoto]**.
   ![imagen](/help/assets/assets/uncheck-inherit-option.jpg)

   Se le pedirá que inicie sesión.
1. Seleccione el recurso y haga clic en **[!UICONTROL Seleccionar]**.
1. Agregue un texto alternativo y haga clic en **[!UICONTROL Listo]**.
   <br>: el recurso remoto aparece en el componente de imagen. También puede verificar la dirección URL de envío del recurso cuando se carga en la página o mediante la pestaña Vista previa. La dirección URL de envío indica que se accede de forma remota al recurso.

AEM Puede acceder a recursos remotos en el editor de páginas de forma predeterminada solo para el componente principal de imagen v3 y el componente principal de teaser v2. Para otros componentes, incluidos los personalizados, es necesario realizar personalizaciones para integrar el Selector de recursos con esos componentes.

#### AEM Vídeo: Acceder a recursos remotos en el editor de páginas de

>[!VIDEO](https://video.tv.adobe.com/v/3427666)

### AEM Acceder a recursos remotos en fragmentos de contenido de {#access-assets-content-fragment}

AEM Siga los siguientes pasos para utilizar recursos remotos dentro de un fragmento de contenido en la instancia de AEM Sites en el que se haya creado el fragmento de contenido. AEM Puede llevar a cabo esta integración en la versión 6.5 de y no en AEM as a Cloud Service.

1. Vaya a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Seleccione la carpeta de recursos donde esté presente el fragmento de contenido.
1. Seleccione el fragmento de contenido y haga clic en **[!UICONTROL Editar (_e_)]**.

   >[!NOTE]
   >
   AEM Si no cuenta con el modelo de fragmento de contenido de, es posible que tenga que [crear uno](https://experienceleague.adobe.com/docs/experience-manager-65/content/assets/content-fragments/content-fragments-models.html?lang=en).

1. Haga clic en el icono de ![marca de verificación](/help/assets/assets/do-not-localize/checkmark-icon.svg) junto al componente de texto.
1. Seleccione **[!UICONTROL Remoto]** para recuperar el recurso del DAM remoto. <br>
Puede elegir el repositorio DAM **[!UICONTROL Local]** o **[!UICONTROL Remoto]** según sus necesidades.

   ![imagen](/help/assets/assets/cf-pick.jpg)
Se le pedirá que inicie sesión.
1. Elija el recurso y haga clic en **[!UICONTROL Seleccionar]**.
   <br>: la dirección URL del recurso remoto aparece en el componente de texto.

#### AEM Vídeo: Acceder a recursos remotos en fragmentos de contenido de

>[!VIDEO](https://video.tv.adobe.com/v/3427667)

### Acceso a recursos remotos en Edge Delivery Services {#access-assets-eds}

También puede acceder a recursos remotos en Edge Delivery Services. Para obtener más información, consulte [Uso de recursos de Assets as a Cloud Service mediante Dynamic Media con funciones OpenAPI](https://www.aem.live/docs/aem-assets-sidekick-plugin#utilizing-assets-from-assets-cloud-services-delivered-via-dynamic-media-with-openapi).
