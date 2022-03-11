---
title: Administrar experiencias de catálogo de productos por etapas
description: Obtenga información sobre cómo administrar experiencias de catálogo de productos organizadas.
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 2%

---

# Creación de experiencias de catálogo de productos por etapas {#building-experiences}

Obtenga información sobre cómo administrar experiencias de catálogo de productos organizadas.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de Contenido y Comercio AEM, [Administrar plantillas y páginas del catálogo de productos](catalog-templates.md), ha aprendido a administrar y crear experiencias de catálogo de productos basadas en plantillas.

Este artículo se basa en estos fundamentos.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo administrar la experiencia del catálogo de productos en función de los datos de productos clasificados y los lanzamientos AEM. Muchas veces, los autores tienen que preparar en paralelo un lanzamiento de producto próximo (como una nueva colección de ropa). Esto requiere acceso a los datos del producto clasificados (aún no activos) y la capacidad de preparar el contenido. Este nuevo contenido se activará con el lanzamiento del producto.

    >[!NOTE]
    >
    >Esta función solo está disponible con Adobe Commerce o Cloud Edition y conectores de terceros que admiten autenticación basada en token. Consulte [Introducción](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html) para obtener más información.

En primer lugar, veamos cómo los autores pueden acceder a los datos de producto clasificados con CIF.

## Uso de datos de producto por etapas {#staged-product-data}

Una forma de acceder a los datos de productos clasificados es usar la cabina de productos. Abra el catálogo de productos haciendo clic en el icono Comercio del menú AEM principal. Esto le proporcionará acceso a los datos de productos activos. Abra la pestaña de filtro de la izquierda y expanda **CATÁLOGO DE ENSAYOS**. Con los datos de vista previa, ahora puede acceder a los datos del producto por etapas en cualquier momento. Los datos por etapas incluyen categorías nuevas, productos o campos actualizados como el precio.

![cóctel de escenario](assets/staged-cockpit.png)

La vista deformación de tiempo permite previsualizar una tienda con datos clasificados. Abra el editor y cambie el modo a Deformación de tiempo. Seleccione cualquier fecha futura. Observe la información que aparece en la parte superior del editor de que está viendo la página durante una fecha determinada.

![deformación de tiempo de etapa](assets/staged-timewarp.png)

Ahora puede examinar el catálogo con los datos clasificados. Si abre una categoría o página de producto organizadas, el editor mostrará un indicador visual.

![plp de escenario](assets/staged-plp.png)

    >[!NOTE]
    >
    >Omnisearch no tiene contexto y, por lo tanto, solo devuelve datos del catálogo de productos activos

## AEM lanzamientos {#launches}

AEM Lanzamientos le permite crear contenido para datos de productos clasificados. Si no está familiarizado con los lanzamientos, siga el vínculo de documentación en la sección [Sección Recursos adicionales](#additional-resources). A continuación, la fecha de lanzamiento se utiliza para acceder a los datos del producto clasificados.

![inicio del escenario](assets/staged-launch.png)

Observe que los selectores respetan la fecha de lanzamiento con el indicador de ensayo a la derecha.

![selector de escenario](assets/staged-picker.png)

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido, debe:

* comprender los conceptos de catálogo de productos por etapas y contenido con lanzamientos
* poder acceder a los datos del catálogo de productos clasificados mediante la cabina y el editor de productos

Ya está listo para administrar [experiencias de producto](product-experience-management.md). Sin embargo, AEM Contenido y Comercio tienen muchas opciones adicionales disponibles. Consulte algunos de los recursos adicionales disponibles en la [Sección Recursos adicionales](#additional-resources) para obtener más información sobre las funciones que ha visto en este recorrido.

## Recursos adicionales {#additional-resources}

* [Product Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [Introducción](/help/commerce-cloud/getting-started.md)
* [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md)
