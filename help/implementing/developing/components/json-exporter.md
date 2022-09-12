---
title: Exportador JSON para servicios de contenido
description: Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido desde o hacia AEM, más allá del enfoque en las páginas web. Proporcionan la entrega de contenido a canales que no son páginas web de AEM tradicionales, mediante métodos estandarizados que cualquier cliente puede consumir.
exl-id: d3ddffb7-cef9-4c86-aa31-175f13f9b4a5
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 31%

---

# Exportador JSON para servicios de contenido {#json-exporter-for-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y el envío de contenido desde o hacia AEM fuera del foco de las páginas web.

Proporcionan la entrega de contenido a canales que no son páginas web de AEM tradicionales, mediante métodos estandarizados que cualquier cliente puede consumir. Estos canales pueden incluir lo siguiente:

* Aplicaciones de una sola página
* Aplicaciones móviles nativas
* Otros canales y puntos de contacto externos a AEM

Con los fragmentos de contenido que utilizan contenido estructurado, puede proporcionar servicios de contenido utilizando el exportador JSON para ofrecer el contenido de una (y) página AEM en formato de modelo de datos JSON. Esto se puede consumir en sus propias aplicaciones.

## Exportador JSON con componentes principales de fragmentos de contenido {#json-exporter-with-content-fragment-core-components}

Con el exportador JSON de AEM, puede enviar el contenido de una (y) página AEM en formato de modelo de datos JSON. Esto se puede consumir en sus propias aplicaciones.

Dentro de AEM la entrega se logra mediante el selector `model` y `.json` extensión.

`.model.json`

1. Por ejemplo, una dirección URL como:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks.model.json
   ```

1. Ofrecerá contenido como:

   ![Modelo JSON del contenido WKND](assets/json-model-wknd.png)

Alternativamente, puede enviar el contenido de un fragmento de contenido estructurado segmentándolo específicamente.

Esto se realiza mediante la ruta completa al fragmento (a través de la variable `jcr:content`); por ejemplo, con un sufijo como .

`.../jcr:content/root/container/container/contentfragment.model.json`

La página puede contener un solo fragmento de contenido o varios componentes de varios tipos. También puede utilizar mecanismos como componentes de lista para buscar automáticamente contenido relevante.

* Por ejemplo, una dirección URL como:

   ```shell
   http://localhost:4502/content/wknd/language-masters/en/magazine/guide-la-skateparks/jcr:content/root/container/container/contentfragment.model.json
   ```

* Ofrecerá contenido como:

   ![Modelo JSON del fragmento de contenido WKND](assets/json-model-wknd-content-fragment.png)

   >[!NOTE]
   >
   >Puede [adaptar sus propios componentes](enabling-json-exporter.md) para acceder a estos datos y utilizarlos.

   >[!NOTE]
   >
   >Aunque no es una implementación estándar, [se admiten varios selectores,](enabling-json-exporter.md#multiple-selectors) but `model` debe ser el primero.

### Información adicional {#further-information}

Consulte también lo siguiente:

* API de HTTP de Assets
   * [API de HTTP de Assets](/help/assets/developer-reference-material-apis.md)
* Modelos Sling:
   * [Modelos de Sling: Asociación de una clase de modelo con un tipo de recurso desde 130](https://sling.apache.org/documentation/bundles/models.html#associating-a-model-class-with-a-resource-type-since-130)
* AEM con JSON:
   * [Activación de la exportación de JSON para un componente](enabling-json-exporter.md)

## Documentación relacionada {#related-documentation}

Para obtener más información, consulte:

* [Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md)
* [Modelos de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-models.md)
* [Creación con fragmentos de contenido](/help/sites-cloud/authoring/fundamentals/content-fragments.md)
* [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) y [Componente Fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es)
