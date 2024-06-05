---
title: ContextHub
description: ContextHub es un marco para almacenar, manipular y presentar datos de contexto
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# ContextHub {#contexthub}

ContextHub es un marco de trabajo para almacenar, manipular y presentar datos de contexto. Su principal característica es la capacidad de [visualización de datos de contexto mientras se simulan y se cambia entre varias personalidades](/help/sites-cloud/authoring/personalization/contexthub.md).

ContextHub, que le permite:

* [Presentar, ver, cambiar de perfil y simular la experiencia del usuario](#presentation) al crear páginas con datos de contexto.
* [Conservar datos de contexto](#persistence) en el sitio web como una representación de la capa de datos.
* [Administración de segmentos](#segmentation) para el contexto seleccionado.

La API de JavaScript del lado del cliente le permite acceder a los datos para personalizar el contenido.

## Presentación {#presentation}

El [Barra de herramientas de ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) permite a los especialistas en marketing y a los autores ver y manipular los datos de almacén para simular la experiencia del usuario al crear páginas. La barra de herramientas consta de grupos de módulos de interfaz de usuario que proporcionan acceso a [tiendas de ContextHub,](#persistence) que conservan los datos de ContextHub en el cliente.

Cada módulo de IU de ContextHub es una instancia de un tipo de módulo predefinido:

* ContextHub proporciona varios [tipos de módulos de muestra](sample-modules.md).
* AEM Usar consolas de consola para [agregar módulos de IU](configuring-contexthub.md#adding-a-ui-module), y a [agruparlos en modos de IU](configuring-contexthub.md#adding-a-ui-mode).
* Los desarrolladores pueden [crear tipos de módulos personalizados](extending-contexthub.md#creating-contexthub-ui-module-types).

Los desarrolladores deben [añadir el componente ContextHub a la página](configuring-contexthub.md).

## Persistencia {#persistence}

ContextHub almacena datos de contexto persistentes en el cliente. La API de JavaScript de ContextHub le permite acceder a las tiendas para crear, actualizar y eliminar datos según sea necesario. De este modo, ContextHub representa una capa de datos en las páginas.

Cada tienda de ContextHub es una instancia de un tipo de tienda predefinido:

* ContextHub proporciona varios [tipos de almacén de muestra](sample-stores.md).
* AEM Usar consolas de consola para [crear tiendas](configuring-contexthub.md#creating-a-contexthub-store).
* Los desarrolladores pueden [crear tipos de tienda personalizados](extending-contexthub.md#creating-custom-store-candidates).
* Los desarrolladores pueden [datos de tienda de acceso](adding-contexthub.md#interacting-with-contexthub-stores) mediante JavaScript.

## Segmentación {#segmentation}

ContextHub incluye un motor de segmentación que administra segmentos y determina qué segmentos se resuelven para el contexto actual. Se definen varios segmentos. Puede utilizar la API de JavaScript para lo siguiente [determinar segmentos resueltos](adding-contexthub.md#determining-resolved-contexthub-segments).
