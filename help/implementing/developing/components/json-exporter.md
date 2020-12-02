---
title: JSON Exporter for Content Services
description: Los servicios de contenido de AEM están diseñados para generalizar la descripción y el envío del contenido desde/hacia AEM más allá del enfoque en las páginas web. Proporcionan el envío de contenido a canales que no son páginas web AEM tradicionales, utilizando métodos estandarizados que pueden ser consumidos por cualquier cliente.
translation-type: tm+mt
source-git-commit: 0799a817095558edd49b53ddc915c9474181fef7
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 7%

---


# Exportador JSON para Content Services {#json-exporter-for-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y el envío del contenido desde/hacia AEM fuera del enfoque de las páginas web.

Proporcionan el envío de contenido a canales que no son páginas web AEM tradicionales, utilizando métodos estandarizados que pueden ser consumidos por cualquier cliente. Estos canales pueden incluir:

* Aplicaciones de una sola página
* Aplicaciones móviles nativas
* Otros canales y puntos de contacto externos a AEM

Con los fragmentos de contenido que utilizan contenido estructurado, puede proporcionar servicios de contenido mediante el exportador JSON para entregar el contenido de una página AEM en formato de modelo de datos JSON. Esto puede ser consumido por sus propias aplicaciones.

## Exportador JSON con componentes principales de fragmento de contenido {#json-exporter-with-content-fragment-core-components}

Con el exportador JSON de AEM puede entregar el contenido de una(y) página AEM en formato de modelo de datos JSON. Esto puede ser consumido por sus propias aplicaciones.

Dentro de AEM el envío se logra mediante la extensión `model` y `.json` del selector.

`.model.json`

1. Por ejemplo, una dirección URL como:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. Entregará contenido como:

   ![Modelo JSON del contenido WKND](assets/json-model-wknd.png)

También puede ofrecer el contenido de un fragmento de contenido estructurado segmentándolo específicamente.

Esto se realiza mediante la ruta completa del fragmento (mediante `jcr:content`); por ejemplo, con un sufijo como.

`.../jcr:content/root/container/container/contentfragment.model.json`

La página puede contener un solo fragmento de contenido o varios componentes de distintos tipos. También puede utilizar mecanismos como componentes de lista para buscar automáticamente contenido relevante.

* Por ejemplo, una dirección URL como:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
   ```

* Entregará contenido como:

   ![Modelo JSON del fragmento de contenido WKND](assets/json-model-wknd-content-fragment.png)

   >[!NOTE]
   >
   >Puede [adaptar sus propios componentes](enabling-json-exporter.md) para acceder y utilizar estos datos.

   >[!NOTE]
   >
   >Aunque no es una implementación estándar, [se admiten varios selectores,](enabling-json-exporter.md#multiple-selectors) pero `model` debe ser el primero.

### Información adicional {#further-information}

Consulte también:

* API de HTTP de Assets
   * [API de HTTP de Assets](/help/assets/developer-reference-material-apis.md)
* Modelos Sling:
   * [Modelos Sling: Asociación de una clase model con un tipo de recurso desde 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM con JSON:
   * [Activación de la exportación de JSON para un componente](enabling-json-exporter.md)

## Documentación relacionada {#related-documentation}

Para obtener más información, consulte:

* [Fragmentos de contenido en la guía del usuario Recursos](/help/assets/content-fragments/content-fragments.md)
* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componentes principales ](https://docs.adobe.com/content/help/es-ES/experience-manager-core-components/using/introduction.html) y el componente Fragmento  [de contenido](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)
