---
title: ContextHub
description: ContextHub es un marco para almacenar, manipular y presentar datos de contexto
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
feature: Developing, Personalization
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---

# ContextHub {#contexthub}

ContextHub es un marco de trabajo para almacenar, manipular y presentar datos de contexto. Su característica principal es la posibilidad de [ver datos de contexto mientras se simulan y se cambia entre distintas personalidades](/help/sites-cloud/authoring/personalization/contexthub.md).

ContextHub, que le permite:

* [Presente, vea, cambie de persona y simule la experiencia del usuario](#presentation) durante la creación de páginas con datos de contexto.
* [Conservar datos de contexto](#persistence) en el sitio web como representación de la capa de datos.
* [Administrar segmentos](#segmentation) para el contexto seleccionado.

La API de JavaScript del lado del cliente le permite acceder a los datos para personalizar el contenido.

## Presentación {#presentation}

La [barra de herramientas de ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) permite a los especialistas en marketing y a los autores ver y manipular los datos del almacén para simular la experiencia del usuario al crear páginas. La barra de herramientas consta de grupos de módulos de interfaz de usuario que proporcionan acceso a [almacenes de ContextHub](#persistence), que conservan los datos de ContextHub en el cliente.

Cada módulo de IU de ContextHub es una instancia de un tipo de módulo predefinido:

* ContextHub proporciona [tipos de módulos de ejemplo](sample-modules.md).
* Use las consolas de AEM para [agregar módulos de interfaz de usuario](configuring-contexthub.md#adding-a-ui-module) y [agruparlos en modos de interfaz de usuario](configuring-contexthub.md#adding-a-ui-mode).
* Los desarrolladores pueden [crear tipos de módulos personalizados](extending-contexthub.md#creating-contexthub-ui-module-types).

Los desarrolladores deben [agregar el componente ContextHub a la página](configuring-contexthub.md).

## Persistencia {#persistence}

ContextHub almacena datos de contexto persistentes en el cliente. La API de JavaScript de ContextHub le permite acceder a las tiendas para crear, actualizar y eliminar datos según sea necesario. De este modo, ContextHub representa una capa de datos en las páginas.

Cada tienda de ContextHub es una instancia de un tipo de tienda predefinido:

* ContextHub proporciona [tipos de almacén de muestra](sample-stores.md).
* Use las consolas de AEM para [crear tiendas](configuring-contexthub.md#creating-a-contexthub-store).
* Los desarrolladores pueden [crear tipos de almacén personalizados](extending-contexthub.md#creating-custom-store-candidates).
* Los desarrolladores pueden [acceder a los datos del almacén](adding-contexthub.md#interacting-with-contexthub-stores) a través de JavaScript.

## Segmentación {#segmentation}

ContextHub incluye un motor de segmentación que administra segmentos y determina qué segmentos se resuelven para el contexto actual. Se definen varios segmentos. Puede usar la API de JavaScript para [determinar los segmentos resueltos](adding-contexthub.md#determining-resolved-contexthub-segments).
