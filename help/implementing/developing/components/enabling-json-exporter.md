---
title: Activación de la exportación de JSON para un componente
description: Los componentes se pueden adaptar para generar la exportación JSON de su contenido en base a un modelo de modelo.
translation-type: tm+mt
source-git-commit: 83c27daae4e8ae2ae6a8f115c9da9527971c6ecb
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 7%

---


# Activación de la exportación de JSON para un componente {#enabling-json-export-for-a-component}

Los componentes se pueden adaptar para generar la exportación JSON de su contenido en base a un modelo de modelo.

## Información general {#overview}

La exportación de JSON se basa en [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html) y en el marco [Exportador de modelo Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (que se basa en [anotaciones Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Esto significa que el componente debe tener un modelo Sling si necesita exportar JSON. Por lo tanto, deberá seguir estos dos pasos para habilitar la exportación de JSON en cualquier componente.

* [Definición de un modelo Sling para el componente](#define-a-sling-model-for-the-component)
* [Anotar la interfaz del modelo de Sling](#annotate-the-sling-model-interface)

## Definir un modelo Sling para el componente {#define-a-sling-model-for-the-component}

Primero se debe definir un modelo de Sling para el componente.

>[!NOTE]
>
>Para ver un ejemplo del uso de modelos Sling, consulte el artículo [Desarrollo de exportadores de modelos Sling en AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/foundation/development/develop-sling-model-exporter.html).

La clase de implementación del modelo Sling debe anotarse con lo siguiente:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Esto garantiza que el componente se pueda exportar por su cuenta, mediante el selector `.model` y la extensión `.json`.

Además, esto especifica que la clase Sling Model se puede adaptar a la interfaz `ComponentExporter`.

>[!NOTE]
>
>Las anotaciones Jackson no suelen especificarse en el nivel de clase del Modelo Sling, sino en el nivel de interfaz del Modelo. Esto sirve para garantizar que la exportación JSON se considere como parte de la API de componente.

>[!NOTE]
>
>Las clases `ExporterConstants` y `ComponentExporter` provienen del paquete `com.adobe.cq.export.json`.

### Uso de varios selectores {#multiple-selectors}

Aunque no es un caso de uso estándar, es posible configurar varios selectores además del selector `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Sin embargo, en este caso el selector `model` debe ser el primer selector y la extensión debe ser `.json`.

## Anotar la interfaz del modelo Sling {#annotate-the-sling-model-interface}

Para que el marco de trabajo del exportador JSON lo tenga en cuenta, la interfaz del modelo debe implementar la interfaz `ComponentExporter` (o `ContainerExporter`, en el caso de un componente de contenedor).

La interfaz del modelo de Sling correspondiente (`MyComponent`) se anotaría utilizando [anotaciones Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir cómo se debe exportar (serializar).

La interfaz del modelo debe anotarse correctamente para definir qué métodos deben serializarse. De forma predeterminada, todos los métodos que respetan la convención de nombre habitual para captadores se serializarán y derivarán los nombres de propiedades JSON de forma natural de los nombres de captador. Esto se puede evitar o anular con `@JsonIgnore` o `@JsonProperty` para cambiar el nombre de la propiedad JSON.

## Ejemplo {#example}

[Los ](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) componentes principales admiten la exportación JSON y pueden utilizarse como referencia.

Para ver un ejemplo, consulte la implementación del modelo Sling del componente principal de imagen y su interfaz anotada.

## Documentación relacionada {#related-documentation}

Para obtener más información, consulte:

* [Fragmentos de contenido en la guía del usuario Recursos](/help/assets/content-fragments/content-fragments.md)
* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componentes principales ](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) y el componente Fragmento  [de contenido](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)
