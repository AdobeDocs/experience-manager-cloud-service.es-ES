---
title: Configuración de varias tiendas
description: Configuración de varias tiendas
translation-type: tm+mt
source-git-commit: 94c6abef36b6add300ba3b24855ebf3edf10e1ed
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---


# Configuración de varias tiendas {#multi-store}

Los componentes principales de AEM CIF se pueden utilizar en varias estructuras de sitios AEM y la implementación de cliente de GraphQL subyacente se puede conectar a diferentes almacenes de Magento o vistas de almacenamiento. Esto permite a los proyectos implementar configuraciones complejas de multitienda/multisitio.

Un tutorial en vídeo que detalla las opciones para integrar varias Vistas de la Tienda Magento con Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

AEM las funciones de administración multisitio de Live Copy y de copia de idioma se utilizan junto con el módulo de integración de comercio para administrar globalmente los sitios en las regiones y las configuraciones regionales.

La configuración recomendada es utilizar una relación 1:1 entre AEM sitio y la vista del almacén de Magento.

Para conectar un sitio de AEM y AEM componentes principales de CIF a una vista de almacenamiento dedicada, siga los pasos a continuación:

## Configuración {#configuration}

1. Configure varias tiendas y vistas de tiendas según el patrón descrito en Sitios web, tiendas y Vistas de [Magento](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)

2. Asegúrese de que la conexión entre AEM y Magento funciona.

3. Cree una configuración secundaria de la configuración del Cloud Service CIF siguiendo estos pasos:

   * En AEM vaya a Herramientas -> General -> Navegador de configuración
   * Seleccione la configuración base que ha creado
   * Cree una nueva configuración siguiendo los pasos descritos en el punto 2 anterior

   Esta nueva configuración se creará como una configuración secundaria de la base. Ahora puede ir a Herramientas -> General -> Navegador de configuración y crear los ajustes de configuración.

4. Asignar la configuración secundaria a un sitio AEM

   * Ir a la consola AEM Sites
   * Navegue hasta la región o la raíz de idioma de la estructura del sitio, por ejemplo: /content/venia/us _o_ /content/venia/us/es para la página de muestra de Venia
   * Seleccione la página y abra las propiedades de la página
   * Seleccione la ficha Opciones avanzadas
   * En la `Configuration` sección seleccione la configuración que creó en el paso

## Recursos adicionales

* [Sitios web, tiendas y Vistas Magento](https://docs.magento.com/m2/ce/user_guide/stores/websites-stores-views.html)
* [Componentes principales de CIF AEM: configuración de sitios y almacenes múltiples](https://github.com/adobe/aem-core-cif-components/wiki/configuration#multi-store--site-configuration)
* [Uso de Multi-Site Manager](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Reutilización del contenido: Multi Site Manager y Live Copy](https://helpx.adobe.com/experience-manager/6-5/sites/administering/using/msm.html)
