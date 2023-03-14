---
title: Gestionar experiencias de catálogo de productos clasificados
description: Obtenga información sobre cómo administrar las experiencias de catálogo de productos clasificados.
exl-id: 1db18818-b8e0-4127-8a65-dc3dea1f2927
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 10%

---

# Creación de experiencias de catálogo de productos por etapas {#building-experiences}

Obtenga información sobre cómo administrar las experiencias de catálogo de productos clasificados.

## La historia hasta ahora {#story-so-far}

AEM En el documento anterior del recorrido de Contenido y Comercio de la, [Administrar páginas y plantillas del catálogo de productos](catalog-templates.md), ha aprendido a administrar y crear experiencias de catálogo de productos basadas en plantillas.

Este artículo se basa en estos aspectos básicos.

## Objetivo {#objective}

AEM Este documento le ayuda a comprender cómo administrar la experiencia del catálogo de productos en función de los datos de los productos clasificados y los lanzamientos de la. Muchas veces, los autores tienen que preparar en paralelo un próximo lanzamiento de producto (como una nueva colección de ropa). Esto requiere acceso a los datos del producto clasificados (aún no están activos) y la capacidad de preparar el contenido. Este nuevo contenido se publicará con el lanzamiento del producto.

    >[!NOTA]
    >
    >Esta función solo está disponible con Adobe Commerce o Cloud Edition y conectores de terceros que admiten la autenticación basada en tokens. Consulte [Introducción](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content-and-commerce/storefront/getting-started.html) para obtener más información.

En primer lugar, veamos cómo los autores pueden acceder a los datos de productos clasificados con CIF.

## Uso de datos de productos clasificados {#staged-product-data}

Una forma de acceder a los datos de productos clasificados es utilizar la cabina de productos. AEM Abra el catálogo de productos haciendo clic en el icono Comercio en el menú principal de la. Esto le proporciona acceso a los datos del producto en directo. Abra la pestaña de filtro a la izquierda y expanda **CATÁLOGO CLASIFICADO**. Con los datos de vista previa, ahora puede acceder a los datos de productos clasificados en cualquier momento. Los datos clasificados incluyen nuevas categorías, productos o campos actualizados como el precio.

![cabina de pilotos](assets/staged-cockpit.png)

Es posible obtener una vista previa de una tienda con datos clasificados mediante la vista Deformación de tiempo. Abra el editor y cambie el modo a Deformación de tiempo. Seleccione cualquier fecha futura. Observe que, sobre el editor, la información indica que está viendo la página durante una fecha determinada.

![deformación de tiempo de ensayo](assets/staged-timewarp.png)

Ahora puede examinar el catálogo con los datos clasificados. Si abre una categoría o una página de producto clasificados, el editor mostrará un indicador visual.

![fase plp](assets/staged-plp.png)

    >[!NOTA]
    >
    >Omnisearch no tiene contexto y, por lo tanto, solo devuelve datos del catálogo de productos activo

## Lanzamientos de AEM {#launches}

AEM Los lanzamientos de le permiten crear contenido para los datos de productos clasificados. Si no está familiarizado con los lanzamientos, siga el vínculo de documentación debajo de [Sección Recursos adicionales](#additional-resources). A continuación, la fecha de lanzamiento se utiliza para acceder a los datos de productos clasificados.

![fase de lanzamiento](assets/staged-launch.png)

Observe que los selectores respetan la fecha de lanzamiento con el indicador de ensayo a la derecha.

![selector de escenarios](assets/staged-picker.png)

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido, debe:

* comprender los conceptos de catálogo de productos clasificados y contenido con lanzamientos
* poder acceder a los datos del catálogo de productos clasificados mediante la cabina de productos y el editor

Ya está listo para administrar [experiencias del producto](product-experience-management.md). AEM Sin embargo, Contenido y comercio de tienen muchas opciones adicionales disponibles. Consulte algunos de los recursos adicionales disponibles en la sección [Recursos adicionales](#additional-resources) para obtener más información acerca de las funciones que ha visto en este recorrido.

## Recursos adicionales {#additional-resources}

* [Product Cockpit](/help/commerce-cloud/authoring/product-cockpit.md)
* [Introducción](/help/commerce-cloud/getting-started.md)
* [Lanzamientos](/help/sites-cloud/authoring/launches/overview.md)
