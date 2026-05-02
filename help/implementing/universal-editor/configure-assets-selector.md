---
title: Configuración del selector de Assets para el editor universal
description: Descubra cómo puede configurar el selector de recursos para utilizarlo con el editor universal.
feature: Developing
role: Admin, Developer
exl-id: 0bf7b418-5ecd-454f-ac46-03792268c59c
source-git-commit: a03eb72ee1b46756f003a60709019aa3122d26f2
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Configuración del selector de Assets para el editor universal {#configure-assets-selector}

Descubra cómo puede configurar el selector de recursos para utilizarlo con el editor universal.

## Información general {#overview}

El editor universal utiliza el selector de recursos para permitir que los autores busquen y seleccionen los recursos que desean insertar en el contenido.

El selector de recursos se puede configurar en el editor universal mediante [filtros de componentes.](/help/implementing/universal-editor/filtering.md) Este documento describe qué opciones de configuración están disponibles.

>[!NOTE]
>
>Al iniciar un proyecto de editor universal, no hay filtros para el selector de recursos. Los creadores tendrán acceso a todos los recursos que normalmente permiten sus permisos de usuario.

## Definición de filtro {#filter-definition}

La definición del filtro para el selector de recursos tiene una estructura simple.

```json
[
  {
    "id": "assets-filter",
    "assets": {...}
   }
]
```

## Opciones de filtro {#filter-options}

El filtro `assets` puede tener las siguientes opciones.

* `deliveryTier?`: - Define cuál de los siguientes niveles de entrega utilizar:
   * `dm`: Dynamic Media (preferido) con reserva a `publish` si es necesario
   * `publish`: instancia de publicación de AEM
* `repoNames?`: cadena: lista de repositorios de AEM que se pueden usar para seleccionar imágenes.
   * Predeterminado: todos los repositorios de envío
* `selectionTier?`: cadena: niveles de AEM para seleccionar recursos
   * Predeterminado: `["author", "delivery"]`
* `disableRemote?`: booleano: deshabilitar la compatibilidad con repositorios remotos
* `preselectedTypes?`: cadena: los tipos de archivo preseleccionados que se aplicarán como filtro predeterminado en el Selector de recursos
* `minMaxDimensions?`: objeto: proporciona dimensiones mínimas o máximas (en píxeles) que se aplicarán como filtro predeterminado en el selector de recursos
   * `widthMin?`: número - anchura mínima
   * `widthMax?`: número - anchura máxima
   * `heightMin?`: número - altura mínima
   * `heightMax?`: número - altura máxima
* `minMaxFileSize?`: objeto: proporcione el tamaño de archivo mínimo o máximo (en bytes) que se aplicará como filtro predeterminado en el selector de recursos
   * `min?`: número: tamaño mínimo de archivo
   * `max?`: número: tamaño máximo de archivo
* `customFileTypeFilters?`: objeto: proporciona filtros de tipo de archivo personalizados para mostrarlos en el selector de recursos
   * `label`: cadena: etiqueta que se mostrará en la IU de selección de recursos
   * `value`: cadena: valor del tipo de archivo que se va a filtrar
* `displayFilters?`: booleano: se utiliza para deshabilitar la interfaz de usuario de filtros en el selector de recursos; true de forma predeterminada

## Ejemplo {#example}

El siguiente ejemplo contiene la mayoría de las opciones con fines ilustrativos.

```json
[
  {
    "id": "assets-filter",
    "assets": {
      "deliveryTier": "dm",
      "repoNames": ["thisRepo", "thatRepo"],
      "selectionTier": ["author", "delivery"],
      "disableRemote": true,
      "preselectedTypes": ["png", "svg", "jpg", "gif"],
      "minMaxDimensions": {
        "widthMin": 640,
        "widthMax": 640,
        "heightMin": 480,
        "heightMax": 480
      },
      "minMaxFileSize": {
        "min": 1024,
        "max": 1024
      }
    }
   }
]
```

<!--

## Additional Resources {#additional-resources}

For details on the assets selector, please see the document [Micro-Frontend Asset Selector](/help/assets/overview-asset-selector.md#using-asset-selector) in the assets documentation.

-->
