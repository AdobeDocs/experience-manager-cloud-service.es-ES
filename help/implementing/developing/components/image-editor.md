---
title: Editor de imágenes
description: AEM El editor de imágenes es una pieza central de la y los componentes pueden aprovecharla para facilitar la manipulación de imágenes por parte de los autores de contenido.
exl-id: c8ae4f59-75b1-49b4-8dd4-957d2e33000b
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 10%

---

# Editor de imágenes {#image-editor}

AEM El editor de imágenes es una pieza central de la y los componentes pueden aprovecharla para facilitar la manipulación de imágenes por parte de los autores de contenido.

## Unidades relativas para mapa de imagen {#relative-units-for-image-map}

El Editor de imágenes mantiene las áreas de mapa de imagen como unidades absolutas y relativas. Las unidades relativas son útiles cuando se proporcionan como atributos de datos para cambiar dinámicamente el tamaño de un mapa de imagen (en relación con el tamaño de la imagen) en el lado del cliente en un componente de imagen interactivo.

### Propiedad imageMap {#imagemap-property}

Las coordenadas de mapa de imagen se conservan en el JCR como un `imageMap` por el Editor de imágenes. Tiene el siguiente formato.

La propiedad almacena las áreas de mapas de la siguiente manera:

`[area1][area2][...]`

Formato de área:

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

Ejemplo:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## Compatibilidad con imágenes de SVG {#support-for-svg-images}

Los gráficos vectoriales escalables (SVG) son compatibles con el editor de imágenes.

* Se admiten las funciones de arrastrar y soltar un recurso SVG desde DAM y de cargar un archivo SVG cargado desde un sistema de archivos local.

## Habilitación de complementos por tipo MIME {#enabling-plugins-by-mime-type}

En determinadas situaciones, las acciones de creación deben restringirse para determinados tipos MIME, debido a la falta de compatibilidad en el procesamiento del lado del servidor. Por ejemplo, es posible que no se permita editar imágenes de SVG.

Los complementos del Editor de imágenes se pueden habilitar selectivamente por tipo MIME estableciendo un `supportedMimeTypes` en el nodo de configuración del complemento individual.

### Ejemplos {#example}

Por ejemplo, supongamos que la capacidad de recorte solo debe permitirse para imágenes de GIF, JPEG, PNG, WEBP y TIFF.

El `supportedMimeTypes` La propiedad debe establecerse como una cadena de los tipos MIME permitidos en el nodo de configuración del complemento en el `cq:editConfig` del componente de imagen.

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
