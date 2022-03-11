---
title: ContextHub
description: ContextHub es un marco para almacenar, manipular y presentar datos de contexto
exl-id: 604477c6-d96a-441f-b5fc-5def93832478
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# ContextHub {#contexthub}

ContextHub es un marco para almacenar, manipular y presentar datos de contexto. Su característica principal es ofrecer la capacidad de [ver datos de contexto al simular y cambiar entre varias personas.](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub permite:

* [Presentar, ver, cambiar personalidades y simular la experiencia del usuario](#presentation) durante la creación de páginas con datos de contexto.
* [Conservar datos de contexto](#persistence) en el sitio web como una representación de capa de datos.
* [Administrar segmentos](#segmentation) para el contexto seleccionado.

La API de JavaScript del lado del cliente le permite acceder a los datos para personalizar el contenido.

## Presentación {#presentation}

La variable [Barra de herramientas de ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) permite a los especialistas en marketing y a los autores ver y manipular los datos de almacenamiento para simular la experiencia del usuario al crear páginas. La barra de herramientas consta de grupos de módulos de IU que proporcionan acceso a [Almacenes de ContextHub,](#persistence) que conservan los datos de ContextHub en el cliente.

Cada módulo de interfaz de usuario de ContextHub es una instancia de un tipo de módulo predefinido:

* ContextHub proporciona varios [tipos de módulo de muestra](sample-modules.md).
* Usar AEM consolas para [añadir módulos de IU](configuring-contexthub.md#adding-a-ui-module)y [agruparlos en modos de IU](configuring-contexthub.md#adding-a-ui-mode).
* Los desarrolladores pueden [crear tipos de módulos personalizados](extending-contexthub.md#creating-contexthub-ui-module-types).

Los desarrolladores deben [añadir el componente ContextHub a la página](configuring-contexthub.md).

## Persistencia {#persistence}

ContextHub almacena datos de contexto persistentes en el cliente. La API de JavaScript de ContextHub le permite acceder a las tiendas para crear, actualizar y eliminar datos según sea necesario. Como tal, ContextHub representa una capa de datos en las páginas.

Cada almacén de ContextHub es una instancia de un tipo de almacén predefinido:

* ContextHub proporciona varios [tipos de almacén de muestras](sample-stores.md).
* Usar AEM consolas para [crear tiendas](configuring-contexthub.md#creating-a-contexthub-store).
* Los desarrolladores pueden [crear tipos de almacén personalizados](extending-contexthub.md#creating-custom-store-candidates).
* Los desarrolladores pueden [datos de almacenamiento de acceso](adding-contexthub.md#interacting-with-contexthub-stores) a través de Javascript.

## Segmentación {#segmentation}

ContextHub incluye un motor de segmentación que administra segmentos y determina qué segmentos se resuelven para el contexto actual. Se definen varios segmentos. Puede utilizar la API de Javascript para [determinar segmentos resueltos](adding-contexthub.md#determining-resolved-contexthub-segments).
