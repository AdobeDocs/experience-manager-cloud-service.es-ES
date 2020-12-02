---
title: ContextHub
description: ContextHub es un marco para almacenar, manipular y presentar datos de contexto
translation-type: tm+mt
source-git-commit: b8bc27b51eefcfcfa1c23407a4ac0e7ff068081e
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---


# ContextHub {#contexthub}

ContextHub es un marco para almacenar, manipular y presentar datos de contexto. Su función principal es ofrecer la capacidad de [datos de contexto de vista mientras simula y cambia entre varias personas.](/help/sites-cloud/authoring/personalization/contexthub.md)

ContextHub permite:

* [Presente, vista, cambie de persona y simule la ](#presentation) experiencia del usuario mientras crea páginas con datos de contexto.
* [Persista ](#persistence) los datos de contexto en el sitio web como una representación de capa de datos.
* [Administrar ](#segmentation) segmentos para el contexto seleccionado.

La API de JavaScript del lado del cliente le permite acceder a los datos para personalizar el contenido.

## Presentación {#presentation}

La [barra de herramientas de ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md) permite a los especialistas en marketing y a los autores ver y manipular los datos del almacén para simular la experiencia del usuario al crear páginas. La barra de herramientas consiste en grupos de módulos de interfaz de usuario que proporcionan acceso a [almacenes de ContextHub,](#persistence) que mantienen los datos de ContextHub en el cliente.

Cada módulo de interfaz de usuario de ContextHub es una instancia de un tipo de módulo predefinido:

* ContextHub proporciona varios [tipos de módulos de muestra](sample-modules.md).
* Utilice consolas de AEM para [agregar módulos de interfaz de usuario](configuring-contexthub.md#adding-a-ui-module) y para [agruparlos en modos de interfaz de usuario](configuring-contexthub.md#adding-a-ui-mode).
* Los desarrolladores pueden [crear tipos de módulos personalizados](extending-contexthub.md#creating-contexthub-ui-module-types).

Los desarrolladores deben [agregar el componente ContextHub a la página](configuring-contexthub.md).

## Persistencia {#persistence}

ContextHub almacena datos de contexto persistentes en el cliente. La API de JavaScript de ContextHub le permite acceder a las tiendas para crear, actualizar y eliminar datos según sea necesario. Como tal, ContextHub representa una capa de datos en las páginas.

Cada tienda de ContextHub es una instancia de un tipo de tienda predefinido:

* ContextHub proporciona varios [tipos de almacén de muestra](sample-stores.md).
* Use consolas AEM para [crear almacenes](configuring-contexthub.md#creating-a-contexthub-store).
* Los desarrolladores pueden [crear tipos de tienda personalizados](extending-contexthub.md#creating-custom-store-candidates).
* Los desarrolladores pueden [acceder a los datos del almacén](adding-contexthub.md#interacting-with-contexthub-stores) mediante Javascript.

## Segmentación {#segmentation}

ContextHub incluye un motor de segmentación que administra segmentos y determina qué segmentos se resuelven para el contexto actual. Se definen varios segmentos. Puede utilizar la API de JavaScript para [determinar los segmentos resueltos](adding-contexthub.md#determining-resolved-contexthub-segments).
