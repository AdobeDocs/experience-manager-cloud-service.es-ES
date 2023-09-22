---
title: Configuración de varias tiendas de Commerce
description: Obtenga información sobre cómo asignar varias vistas de tiendas de Adobe Commerce a Adobe Experience Manager. Esto permite que los proyectos admitan casos de uso de varios inquilinos y multilingües.
sub-product: Commerce
version: Cloud Service
doc-type: technical-video
activity: setup
audience: administrator
feature: Commerce Integration Framework
kt: 3046
thumbnail: 28952.jpg
exl-id: 4385c9e5-2b25-4f95-952f-72349431cf94
source-git-commit: 97a6a7865f696f4d61a1fb4e25619caac7b68b51
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 18%

---

# Configuración de varias tiendas de Commerce {#multi-store}

Los componentes principales de Adobe Experience Manager AEM CIF AEM () se pueden utilizar en varias estructuras de sitio de y la implementación de cliente de GraphQL subyacente se puede conectar a diferentes tiendas de Adobe Commerce o vistas de tiendas. Esto permite que los proyectos implementen configuraciones complejas de varias tiendas y sitios.

Un tutorial en vídeo que detalla las opciones para integrar varias vistas de la tienda Adobe Commerce con Adobe Experience Manager Sites.

>[!VIDEO](https://video.tv.adobe.com/v/28952/?quality=12)

AEM Las funciones de administración de varios sitios de Live Copy y de copia de idioma se utilizan con Commerce Integration Framework para administrar globalmente los sitios en las regiones y las configuraciones regionales.

AEM La configuración recomendada es utilizar una relación 1:1 entre el sitio de y la vista de la tienda de Adobe Commerce.

AEM AEM CIF Para conectar un sitio de y los componentes principales de la a una vista de tienda dedicada, haga lo siguiente:

## Configuración {#configuration}

1. Configure varias tiendas y vistas de las tiendas según el patrón descrito en [Sitios web, tiendas y vistas de Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)

2. AEM Asegúrese de que funcione la conexión entre y Adobe Commerce.

3. Cree una configuración secundaria de la configuración del CIF de Cloud Service siguiendo estos pasos:

   * AEM En el camino a Herramientas, vaya a Herramientas -> General -> [Explorador de configuración](/help/implementing/developing/introduction/configurations.md#using-configuration-browser)
   * Seleccione la configuración base que ha creado
   * Cree una configuración siguiendo los pasos descritos anteriormente en el punto 2

   Esta nueva configuración se crea como una configuración secundaria de la base. Ahora puede ir a Herramientas -> General -> Explorador de configuración y crear los ajustes de configuración.

   >[!TIP]
   >
   > Los catálogos de comercio se pueden abordar mediante el uso de ID o UID. Los UID se han introducido en Adobe Commerce 2.4.2. Habilite esta opción solo si el backend de Commerce admite un esquema GraphQL de la versión 2.4.2 o posterior.

4. Asigne la configuración secundaria a un sitio de AEM.

   * Vaya a la consola de AEM Sites
   * Vaya a la región o a la raíz de idioma de la estructura del sitio. Por ejemplo, `/content/venia/us _or_ /content/venia/us/en` para la página de muestra de Venia
   * Seleccione la página y abra las propiedades de página
   * Seleccione la pestaña Avanzadas.
   * En el `Configuration` , seleccione la configuración que creó en el paso 3

## Recursos adicionales

* [Sitios web, tiendas y vistas de Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html)
* [Componentes principales del CIF de AEM: configuración de varias tiendas y sitios](https://github.com/adobe/aem-core-cif-components#multi-store--site-configuration)
* [Uso del administrador de varios sitios](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/translation/multi-site-manager-feature-video-use.html)
* [Reutilización del contenido: administrador de varios sitios y Live Copy](/help/sites-cloud/administering/msm/overview.md)
