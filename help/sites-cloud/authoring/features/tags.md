---
title: Uso de etiquetas
description: Las etiquetas son un método rápido y fácil de clasificar contenido dentro del sitio web
exl-id: d2a9f578-fe0a-48ea-851c-2c84463661e0
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 96%

---

# Uso de etiquetas   {#using-tags}

Las etiquetas son un método rápido y sencillo de clasificar contenido dentro de un sitio web. Las etiquetas pueden considerarse como palabras clave o etiquetas que se pueden adjuntar a una página, un recurso o cualquier otro contenido para que con las búsquedas se encuentre ese contenido y el relacionado.

* Consulte Administración de etiquetas para obtener información sobre cómo crear y administrarlas y sobre las etiquetas de contenido que se han aplicado. <!-- See [Administering Tags](/help/sites-administering/tags.md) for information about creating and managing tags, and to which content tags have been applied.-->
* Consulte [Etiquetado para desarrolladores](/help/implementing/developing/introduction/tagging-framework.md) para obtener información sobre el marco de trabajo de etiquetado, así como la forma de incluir y ampliar las etiquetas en aplicaciones personalizadas.

## Diez motivos para utilizar etiquetas {#ten-reasons-to-use-tagging}

1. **Organización del contenido**: el etiquetado facilita las cosas a los creadores, ya que pueden organizar rápidamente el contenido con muy poco esfuerzo.
1. **Organización de etiquetas**: si bien las etiquetas organizan el contenido, las taxonomías jerárquicas o los espacios de nombres organizan las etiquetas.
1. **Etiquetas sumamente organizadas**: con la capacidad de crear etiquetas y subetiquetas, es posible expresar sistemas taxonómicos completos y cubrir términos, subtérminos y sus relaciones. Esto permite crear una segunda (o tercera) jerarquía de contenido en paralelo a la oficial.
1. **Etiquetado controlado**: el etiquetado puede controlarse aplicando permisos a las etiquetas o los espacios de nombres para controlar la creación y la aplicación de etiquetas.
1. **Etiquetado flexible**: las etiquetas tienen muchos nombres y rostros: etiquetas, términos de taxonomía, categorías, marcas y muchos más. Son flexibles en el modelo de contenido y en la manera de usarlas. Por ejemplo, al trazar información demográfica de destino, categorizar y calificar contenido o para crear una jerarquía de contenido secundario.
1. **Búsqueda mejorada**: el componente de búsqueda predeterminado en AEM incluye, en términos generales, las etiquetas creadas y las etiquetas aplicadas a los filtros que pueden emplearse para obtener únicamente los resultados relevantes.
1. **Habilitación de SEO**: las etiquetas aplicadas como propiedades de página se mostrarán automáticamente en las metaetiquetas de la página, por lo que serán visibles a los motores de búsqueda.
1. **Sofisticación simple**: las etiquetas se pueden crear simplemente a partir de una palabra y pulsar un botón. Después, se pueden añadir un título, una descripción y marcas ilimitadas para proporcionar más semántica a la etiqueta.
1. **Consistencia central**: el sistema de etiquetado es un componente central de AEM que todas las capacidades de AEM utilizan para categorizar contenido. Además, la API de etiquetado está disponible para los desarrolladores para que creen aplicaciones compatibles con el etiquetado con acceso a las mismas taxonomías.
1. **Combina estructura y flexibilidad**: AEM es ideal para trabajar con información estructurada, ya que anida páginas y rutas de acceso. También es extremadamente útil a la hora de trabajar con información sin estructurar, debido a la búsqueda incorporada de texto completo. El etiquetado combina las ventajas tanto de la estructura como de la flexibilidad.

A la hora de diseñar la estructura de contenido para un sitio y el esquema de metadatos para los recursos, considere la ligereza y la accesibilidad que proporciona el etiquetado.

## Aplicación de etiquetas   {#applying-tags}

En el entorno de creación, los creadores pueden aplicar etiquetas si acceden a las propiedades de página e introducen una o varias etiquetas en el campo **Etiquetas y palabras clave**.

Para aplicar las etiquetas predefinidas, vaya a la ventana **Propiedades de página** para usar el campo **Etiquetas** y la ventana **Seleccionar etiquetas**. La pestaña **Etiquetas estándar** es el espacio de nombres predeterminado, lo que indica que no hay un valor `namespace-string:` prefijado a la taxonomía. <!-- To apply [pre-defined tags](/help/sites-administering/tags.md), in the **Page Properties** window use the **Tags** field and the **Select Tags** window.-->

![Seleccionar varias etiquetas](/help/sites-cloud/authoring/assets/tags-select.png)

## Publicación de etiquetas {#publishing-tags}

De forma similar a como puede publicar y cancelar la publicación de páginas, puede realizar lo siguiente en etiquetas y espacios de nombres:

### Activar {#activate}

* Activar etiquetas individuales.

  Al igual que con las páginas, las etiquetas recién creadas deberán activarse antes de que estén disponibles en el entorno de publicación.

>[!NOTE]
>
>Cuando activa una página, se abre automáticamente un cuadro de diálogo que le permite activar las etiquetas desactivadas que pertenecen a la página.

### Desactivar {#deactivate}

* Desactivar las etiquetas seleccionadas.
