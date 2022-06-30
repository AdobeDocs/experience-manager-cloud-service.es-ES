---
title: Activación de la exportación de JSON para un componente
description: Los componentes se pueden adaptar para generar la exportación JSON de su contenido en función de un marco de modelos.
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 11%

---

# Activación de la exportación de JSON para un componente {#enabling-json-export-for-a-component}

Los componentes se pueden adaptar para generar la exportación JSON de su contenido en función de un marco de modelos.

## Información general {#overview}

La exportación de JSON se basa en [Modelos de Sling](https://sling.apache.org/documentation/bundles/models.html), y en el [Exportador de modelo Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) marco (que en sí mismo se basa en [Anotaciones de Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Esto significa que el componente debe tener un modelo de Sling si necesita exportar JSON. Por lo tanto, debe seguir estos dos pasos para habilitar la exportación de JSON en cualquier componente.

* [Definir un modelo de Sling para el componente](#define-a-sling-model-for-the-component)
* [Anotar la interfaz del modelo Sling](#annotate-the-sling-model-interface)

## Definir un modelo de Sling para el componente {#define-a-sling-model-for-the-component}

Primero debe definirse un modelo de Sling para el componente.

>[!NOTE]
>
>Para ver un ejemplo del uso de modelos Sling, consulte el artículo [Desarrollo de exportadores de modelos de Sling en AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=es).

La clase de implementación del modelo de Sling debe estar anotada con lo siguiente:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Esto garantiza que el componente se pueda exportar por su cuenta, utilizando la variable `.model` y `.json` extensión.

Además, esto especifica que la clase del Modelo Sling se puede adaptar a la `ComponentExporter` interfaz.

>[!NOTE]
>
>Las anotaciones Jackson no suelen especificarse en el nivel de clase del Modelo Sling, sino en el nivel de interfaz del Modelo. Esto sirve para garantizar que la exportación de JSON se considere parte de la API de componente.

>[!NOTE]
>
>La variable `ExporterConstants` y `ComponentExporter` las clases provienen de `com.adobe.cq.export.json` paquete.

### Uso de varios selectores {#multiple-selectors}

Aunque no es un caso de uso estándar, es posible configurar varios selectores además del `model` selector.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Sin embargo, en tal caso, el `model` debe ser el primer selector y la extensión debe ser `.json`.

## Anotar la interfaz del modelo Sling {#annotate-the-sling-model-interface}

Para que el marco del exportador JSON lo tenga en cuenta, la interfaz del modelo debe implementar la variable `ComponentExporter` interfaz (o `ContainerExporter`, en el caso de un componente contenedor).

La interfaz del modelo de Sling correspondiente (`MyComponent`) se anotaría usando [Anotaciones de Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir cómo se debe exportar (serializado).

La interfaz del modelo debe estar debidamente anotada para definir qué métodos deben serializarse. De forma predeterminada, todos los métodos que respetan la convención de nombres habitual para los captadores se serializarán y derivarán sus nombres de propiedades JSON de forma natural de los nombres de los captadores. Esto se puede evitar o anular utilizando `@JsonIgnore` o `@JsonProperty` para cambiar el nombre de la propiedad JSON.

## Ejemplo {#example}

[Los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) admiten la exportación de JSON y pueden utilizarse como referencia.

Para ver un ejemplo, consulte la implementación del modelo Sling del componente principal de imagen y su interfaz anotada.

## Documentación relacionada {#related-documentation}

Para obtener más información, consulte:

* [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md)
* [Modelos de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) y [Componente Fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es)
