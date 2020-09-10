---
title: ContextHub
description: ContextHub es un marco para almacenar, manipular y presentar datos de contexto
translation-type: tm+mt
source-git-commit: 75d6b51c0148a21ca401d98a5eaf644fc6b0e8cc
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---


# ContextHub {#contexthub}

ContextHub es un marco para almacenar, manipular y presentar datos de contexto. Su característica principal es ofrecer la capacidad de [vista de datos de contexto mientras simula y cambia entre varias personas.](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub permite:

* [Presente, vista, cambie de persona y simule la experiencia](#presentation) del usuario mientras crea páginas con datos de contexto.
* [Persista los datos](#persistence) de contexto en el sitio web como una representación de capa de datos.
* [Administrar segmentos](#segmentation) para el contexto seleccionado.

La API de JavaScript del lado del cliente le permite acceder a los datos para personalizar el contenido.

## Presentación {#presentation}

La barra de herramientas [de](/help/sites-cloud/authoring/personalization/contexthub.md) ContextHub permite a los especialistas en marketing y a los autores ver y manipular los datos del almacén para simular la experiencia del usuario al crear páginas. La barra de herramientas está formada por grupos de módulos de interfaz de usuario que proporcionan acceso a los almacenes de [ContextHub,](#persistence) que conservan los datos de ContextHub en el cliente.

Cada módulo de interfaz de usuario de ContextHub es una instancia de un tipo de módulo predefinido:

* ContextHub proporciona varios tipos [de módulos de](sample-modules.md)muestra.
* Utilice consolas AEM para [agregar módulos](configuring-contexthub.md#adding-a-ui-module)de interfaz de usuario y [agruparlos en modos](configuring-contexthub.md#adding-a-ui-mode)de interfaz de usuario.
* Los desarrolladores pueden [crear tipos](extending-contexthub.md#creating-contexthub-ui-module-types)de módulos personalizados.

Los desarrolladores deben [agregar el componente ContextHub a la página](configuring-contexthub.md).

## Persistencia {#persistence}

ContextHub almacena datos de contexto persistentes en el cliente. La API de JavaScript de ContextHub le permite acceder a las tiendas para crear, actualizar y eliminar datos según sea necesario. Como tal, ContextHub representa una capa de datos en las páginas.

Cada tienda de ContextHub es una instancia de un tipo de tienda predefinido:

* ContextHub proporciona varios tipos [de almacén de](sample-stores.md)muestra.
* Utilice AEM consolas para [crear tiendas](configuring-contexthub.md#creating-a-contexthub-store).
* Los desarrolladores pueden [crear tipos](extending-contexthub.md#creating-custom-store-candidates)de tienda personalizados.
* Los desarrolladores pueden [acceder a los datos](configuring-contexthub.md#interacting-with-contexthub-stores) del almacén a través de Javascript.

## Segmentación {#segmentation}

ContextHub incluye un motor de segmentación que administra segmentos y determina qué segmentos se resuelven para el contexto actual. Se definen varios segmentos. Puede utilizar la API de JavaScript para [determinar los segmentos](configuring-contexthub.md#determining-resolved-contexthub-segments)resueltos.
