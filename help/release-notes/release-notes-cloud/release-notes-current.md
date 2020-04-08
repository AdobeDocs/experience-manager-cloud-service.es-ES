---
title: Notas de la versión 2020.4.0
description: Notas de la versión 2020.4.0
translation-type: tm+mt
source-git-commit: 77163877bea36f854ac8ea6fbc78cbcf4d58ccc0

---


# Notas de la versión de AEM as a Cloud Service 2020.4.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.4.0.

## Assets {#assets}

Siga esta sección para conocer las novedades y las actualizaciones de Experience Manager Assets y Dynamic Media en AEM como una versión 2020.4.0 de Cloud Service.

### Novedades {#assets-what-is-new}

* [Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) está disponible para AEM como Cloud Service Assets y admite casos de uso de distribución de recursos. Brand Portal ayuda a las organizaciones a satisfacer sus necesidades de marketing mediante la distribución segura de recursos de productos y marcas aprobados a agencias externas, socios, equipos internos y distribuidores para su descarga.
   * La configuración de Brand Portal se realiza a través de la consola de Adobe I/O
   * El abastecimiento de recursos en Brand Portal aún no es compatible con AEM como servicio de nube
* La nueva versión de [Adobe Asset Link](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html) 2.0 es compatible con AEM como servicio de nube. Adobe Asset Link facilita la colaboración entre creativos y especialistas en marketing en el proceso de creación de contenido al conectar Recursos AEM con aplicaciones de escritorio de Creative Cloud, Photoshop, Illustrator e InDesign mediante el panel Vínculo de recursos en la aplicación.
   * AEM como servicio de nube está preconfigurado para Adobe Asset Link, lo que resulta en una configuración [](https://helpx.adobe.com/enterprise/using/configure-aem-assets-for-asset-link.html)simplificada.
   * Asset Link ahora es compatible con un conmutador [de entorno](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html#UseAdobeAssetLink)AEM, lo que permite a los usuarios creativos conectarse a distintos entornos AEM con mayor facilidad (por ejemplo, en el caso de diseñadores de agencias que trabajen con varios clientes con Recursos AEM)
* El inicio automático para flujos de trabajo [posteriores al procesamiento](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) se puede configurar en la interfaz de usuario de Propiedades de carpeta para jerarquías de carpetas específicas.
   * Se ha simplificado la interfaz de usuario de Propiedades de la carpeta. La nueva ficha Procesamiento de recursos contiene Perfil de metadatos, Perfil de procesamiento y la nueva configuración de Flujo de trabajo de Inicio automático
* El cuadro de diálogo de reprocesamiento de recursos permite seleccionar un perfil de procesamiento específico y decidir volver a procesarlo en subcarpetas
* Medios dinámicos: Configuración Añadida de publicación selectiva, lo que significa que los recursos se publican automáticamente solo para previsualización segura y se pueden publicar explícitamente en AEM sin necesidad de publicarlos en DMS7 para envío de dominio público.

### Corrección de errores {#assets-bug-fixes}

* Correcciones en el procesamiento de recursos
* Correcciones en la configuración de Dynamic Media y publicación de recursos en el servicio envío de Dynamic Media
