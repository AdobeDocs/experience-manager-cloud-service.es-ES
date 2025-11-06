---
title: Habilitación de la exportación de JSON para un componente
description: Los componentes se pueden adaptar para generar la exportación JSON de su contenido en función de un marco de trabajo del modelador.
exl-id: e9be5c0c-618e-4b56-a365-fcdd185ae808
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 7%

---

# Habilitación de la exportación de JSON para un componente {#enabling-json-export-for-a-component}

Los componentes se pueden adaptar para generar la exportación JSON de su contenido en función de un marco de trabajo del modelador.

## Información general {#overview}

La exportación de JSON se basa en [Modelos Sling](https://sling.apache.org/documentation/bundles/models.html?lang=es) y en el marco de [Exportador de modelos Sling](https://sling.apache.org/documentation/bundles/models.html#exporter-framework-since-130) (que a su vez se basa en [anotaciones Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations)).

Esto significa que el componente debe tener un modelo Sling si debe exportar JSON. Por lo tanto, siga estos dos pasos para habilitar la exportación de JSON en cualquier componente.

* [Defina un modelo Sling para el componente](#define-a-sling-model-for-the-component)
* [Anotar la interfaz del modelo Sling](#annotate-the-sling-model-interface)

## Definir un modelo Sling para el componente {#define-a-sling-model-for-the-component}

En primer lugar, se debe definir un modelo Sling para el componente.

>[!NOTE]
>
>Para ver un ejemplo del uso de modelos Sling, consulte el artículo [Desarrollo de exportadores de modelos Sling en AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/development/develop-sling-model-exporter.html?lang=es).

La clase de implementación del modelo Sling debe estar anotada con lo siguiente:

```java
@Model(... adapters = {..., ComponentExporter.class})
@Exporter(name = ExporterConstants.SLING_MODEL_EXPORTER_NAME, extensions = ExporterConstants.SLING_MODEL_EXTENSION)
@JsonSerialize(as = MyComponent.class)
```

Esto garantiza que el componente se pueda exportar solo, utilizando el selector `.model` y la extensión `.json`.

Además, esto especifica que la clase de modelo Sling se puede adaptar a la interfaz `ComponentExporter`.

>[!NOTE]
>
>Las anotaciones de Jackson no suelen especificarse en el nivel de clase del Modelo Sling, sino en el nivel de interfaz del Modelo. Esto sirve para garantizar que la exportación de JSON se considere como parte de la API del componente.

>[!NOTE]
>
>Las clases `ExporterConstants` y `ComponentExporter` provienen del paquete `com.adobe.cq.export.json`.

### Uso de varios selectores {#multiple-selectors}

Aunque no es un caso de uso estándar, es posible configurar varios selectores además del selector `model`.

```
https://<server>:<port>/content/page.model.selector1.selector2.json
```

Sin embargo, en tal caso, el selector `model` debe ser el primer selector y la extensión debe ser `.json`.

## Anotar la interfaz del modelo Sling {#annotate-the-sling-model-interface}

Para que el marco del exportador JSON lo tenga en cuenta, la interfaz del modelo debe implementar la interfaz `ComponentExporter` (o `ContainerExporter`, en el caso de un componente contenedor).

La interfaz del modelo Sling correspondiente (`MyComponent`) se anotaría usando [anotaciones Jackson](https://github.com/FasterXML/jackson-annotations/wiki/Jackson-Annotations) para definir cómo se debe exportar (serializar).

La interfaz del modelo debe estar anotada correctamente para definir qué métodos se deben serializar. De forma predeterminada, todos los métodos que respetan la convención de nombres habitual de los captadores se serializan y derivan sus nombres de propiedades JSON de forma natural de los nombres de captadores. Esto se puede evitar o sobrescribir usando `@JsonIgnore` o `@JsonProperty` para cambiar el nombre de la propiedad JSON.

## Ejemplo {#example}

[Los componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) admiten la exportación de JSON y se pueden usar como referencia.

Para ver un ejemplo, consulte la implementación del modelo Sling del componente principal de imagen y su interfaz anotada.

## Documentación relacionada {#related-documentation}

* [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md)
* [Modelos de fragmento de contenido](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)
* [Creación con fragmentos de contenido](/help/sites-cloud/authoring/fragments/content-fragments.md)
* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y el [componente de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es)
