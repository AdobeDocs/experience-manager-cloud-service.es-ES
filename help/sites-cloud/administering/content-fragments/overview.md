---
title: Información general sobre el trabajo con fragmentos de contenido
description: Descubra cómo los fragmentos de contenido en Adobe Experience Manager AEM () as a Cloud Service le permiten crear y utilizar contenido estructurado; ideal para la entrega sin encabezado y la creación de páginas.
feature: Content Fragments
role: User, Developer, Architect
exl-id: ce9cb811-57d2-4a57-a360-f56e07df1b1a
solution: Experience Manager Sites
source-git-commit: 86a2c5f35d82010c84b74b6b5f0da09fd87c2b7a
workflow-type: tm+mt
source-wordcount: '1818'
ht-degree: 39%

---

# Información general sobre el trabajo con fragmentos de contenido {#overview-working-with-content-fragments}

Con Adobe Experience Manager AEM () as a Cloud Service, los fragmentos de contenido le permiten diseñar, crear, depurar y publicar contenido independiente de las páginas. Permiten preparar contenido listo para usar en varias ubicaciones y en varios canales, lo que resulta ideal para [entrega sin encabezado](/help/headless/what-is-headless.md) y [creación de páginas](/help/sites-cloud/authoring/fragments/content-fragments.md).

>[!IMPORTANT]
>
>Se puede acceder a los fragmentos de contenido desde dos consolas: **Fragmentos de contenido** y **Assets**.
>
>También hay dos editores para crear fragmentos de contenido; aunque la funcionalidad básica es la misma, hay algunas diferencias. Ambos editores son accesibles desde ambas consolas.
>
>Esta sección trata sobre la consola **Fragmentos de contenido** y el *nuevo* editor de fragmentos de contenido. Se han desarrollado para la entrega de contenido sin encabezado (aunque se pueden utilizar en todos los casos)
>
>Para obtener más información, consulte lo siguiente:
>
>* uso de la consola **Assets** para [administrar fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md)
>* uso del editor de fragmentos de contenido [*original*](/help/assets/content-fragments/content-fragments-variations.md),
>* uso de [fragmentos de contenido para la creación de páginas](/help/sites-cloud/authoring/fragments/content-fragments.md).


Los fragmentos de contenido incluyen contenido estructurado:

* Cada fragmento se basa en un [Modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * El modelo de fragmento de contenido define la estructura del fragmento resultante.
* Cada fragmento consta de:
   * **[Principal](#main-and-variations)**: una parte integral del fragmento que contiene el contenido principal; siempre existe y no se puede eliminar
   * **[Variaciones](#main-and-variations)**: una o más permutaciones del contenido, creadas por el autor
* La estructura puede variar entre lo siguiente:
   * Básico
      * Por ejemplo, un campo de texto de varias líneas.
      * Se puede utilizar para preparar contenido directo para su uso en la creación de páginas.
      * También se puede utilizar para la entrega sin encabezado a la aplicación.
   * Complejo
      * Una combinación de muchos campos de diferentes tipos de datos, incluidos texto, número, booleano, fecha y hora, entre otros.
      * Se puede utilizar para preparar contenido más estructurado para la creación de páginas o para la entrega sin encabezado a la aplicación.
   * Anidado
      * Los tipos de datos de referencia disponibles le permiten anidar el contenido.
      * Tiende a utilizarse para la entrega sin encabezado a la aplicación.

AEM Los fragmentos de contenido también se pueden entregar en formato JSON, utilizando las capacidades de exportación del Modelo Sling (JSON) de los componentes principales de la. Esta forma de entrega:

* permite utilizar el componente para administrar qué elementos enviar de un fragmento.
* permite la entrega por lotes; agregando varios [componentes principales de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=es) en la página que se está usando para la entrega de API

El número de canales de comunicación aumenta de forma anual. Normalmente, los canales hacen referencia al mecanismo de entrega, ya sea como los siguientes:

* Canal físico; por ejemplo, escritorio o móvil.
* Forma de entrega en un canal físico; por ejemplo, la “página de detalles del producto”, la “página de categoría del producto” para escritorio o la “web móvil” o la “aplicación móvil” para móvil.

Sin embargo, probablemente no quiera usar el mismo contenido de *exacto* para todos los canales y necesita optimizar su contenido según el canal específico.

Los fragmentos de contenido le permiten lo siguiente:

* Pensar en cómo llegar a las audiencias de destino de forma eficaz en todos los canales.
* Crear y administrar contenido editorial neutro para el canal.
* Creargrupos de contenido para una amplia gama de canales.
* Diseñar variaciones de contenido para canales específicos.
* Agregue imágenes al texto insertando recursos.
* Crear contenido anidado para reflejar la complejidad de sus datos.

Estos fragmentos de contenido se pueden ensamblar para ofrecer experiencias en una variedad de canales.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencias](/help/sites-cloud/authoring/fragments/content-fragments.md)** son funciones distintas de AEM:
>* Los **fragmentos de contenido** son contenidos editoriales, con definición y estructura, pero sin diseño y/o maquetación visuales adicionales. Pueden utilizarse para acceder a datos estructurados, incluidos textos, números y fechas, entre otros.
>* Los **fragmentos de experiencias** son contenidos plenamente diseñados; un fragmento de una página web.
>
>Los fragmentos de experiencias pueden incluir contenido en forma de fragmentos, pero no lo contrario.
>
>AEM Para obtener más información, consulte [Explicación de los fragmentos de contenido y de experiencias en la sección de fragmentos de experiencias en la sección de fragmentos de experiencias en la sección de fragmentos de experiencias en la sección de experiencias de la página de datos ](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=es#content-fragments).

Esta y las siguientes páginas tratan sobre las tareas para crear, configurar, mantener y utilizar los fragmentos de contenido:

* [Habilitación de la funcionalidad de fragmento de contenidos para la instancia](/help/sites-cloud/administering/content-fragments/setup.md)
* [Modelos de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragment-models.md): habilitando, creando y definiendo sus modelos
* [Cree sus fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md#creating-a-content-fragment) (mediante la consola de fragmentos de contenido)

Una vez creados los fragmentos, puede:

* [Use la consola Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md) para acceder, publicar (para vista previa o producción) y hacer referencia a sus fragmentos
* [Use el editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md) para editar, publicar (para vista previa o producción) y hacer referencia a sus fragmentos
* [Analice](/help/sites-cloud/administering/content-fragments/analysis.md) la estructura del fragmento de contenido mediante el editor
* [Acceda a sus fragmentos con GraphQL para enviarlos sin encabezado a sus aplicaciones](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md).
* [O use sus fragmentos para la creación de páginas](/help/sites-cloud/authoring/fragments/content-fragments.md)

>[!NOTE]
>
>Estas páginas pueden leerse junto con las siguientes:
>
>* [Personalizar y ampliar fragmentos de contenido](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Fragmentos de contenido Configurar componentes para procesamiento](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [API de GraphQL de AEM para su uso con fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)
>* [Creación de páginas con fragmentos de contenido](/help/sites-cloud/authoring/fragments/content-fragments.md).
>* Las [OpenAPI de fragmento de contenido y modelo de fragmento de contenidos](/help/headless/content-fragment-openapis.md) también están disponibles.


## Principal y variaciones {#main-and-variations}

AEM Las variaciones son una característica importante de los fragmentos de contenido que se van a. Permiten crear y editar copias del contenido de **Main** para usarlas en canales y escenarios específicos, lo que hace que la entrega de contenido sin encabezado y la creación de páginas sean aún más flexibles.

* **Principal**

   * **Principal** no es una variación como tal, pero es la base de todas las variaciones.
   * Una parte integral del fragmento

      * Cada fragmento de contenido tiene una instancia de **Main**.
      * **Principal** no se puede eliminar.

   * **Principal** es accesible en el editor de fragmentos en **[Variaciones](/help/sites-cloud/administering/content-fragments/authoring.md#variations)**.

  >[!NOTE]
  >
  >En el editor disponible en la consola **Assets**, **Principal** está etiquetado como **Principal**.

* **Variaciones**

   * Representaciones de texto de fragmento específicas para fines editoriales; pueden estar relacionadas con el canal, pero no es obligatorio, y también pueden ser para modificaciones locales específicas.
   * Se crean como copias de **Main**, pero se pueden editar según sea necesario; a menudo, el contenido se superpone entre las propias variaciones.
   * Se puede definir durante la creación de fragmentos; desde el panel izquierdo.
   * Almacenadas en el fragmento para evitar la dispersión de copias de contenido.
   * Las variaciones se pueden [comparar y sincronizar](/help/sites-cloud/administering/content-fragments/authoring.md#compare-and-synchronize-rich-text) con **Principal**.
  <!--
  * Can be [Summarized](/help/sites-cloud/administering/content-fragments/authoring.md#summarizing-text) to quickly truncate the text to a predefined length.
  -->

## Fragmentos de contenido y servicios de contenido {#content-fragments-and-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y la entrega de contenido desde o hacia AEM, más allá del enfoque en las páginas web.

Proporcionan la entrega de contenido a canales que no son páginas web de AEM tradicionales, mediante métodos estandarizados que cualquier cliente puede consumir. Estos canales pueden incluir lo siguiente:

* Aplicaciones de una sola página
* Aplicaciones móviles nativas
* Otros canales y puntos de contacto externos a AEM

La entrega se ejecuta en formato JSON utilizando el exportador de JSON.

Los fragmentos de contenido de AEM se pueden usar para describir y administrar el contenido estructurado. El contenido estructurado se define en modelos que pueden contener una variedad de tipos de contenido; incluido texto, datos numéricos, booleanos, fecha y hora, etc.

Junto con las capacidades de exportación de JSON de los componentes principales de AEM, este contenido estructurado se puede utilizar para entregar contenido de AEM a canales que no sean páginas de AEM.

>[!NOTE]
>
>Consulte [Sin encabezado y AEM](/help/headless/introduction.md) para ver una introducción al desarrollo sin encabezado para AEM Sites as a Cloud Service.

>[!NOTE]
>
>AEM también admite la traducción del contenido del fragmento. Consulte [Traducción de recursos](/help/assets/translate-assets.md) para obtener más información.

## Tipo de contenido {#content-type}

Los fragmentos de contenido son lo siguiente:

* Una función de **Sites**.

* Se almacenan como **Recursos**:

   * Los fragmentos de contenido (y sus variaciones) se pueden crear y mantener desde la [consola Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md#content-fragments-console).
   * Se crearon y editaron en [Editor de fragmentos de contenido](/help/sites-cloud/administering/content-fragments/authoring.md).

* AEM Se puede acceder a él para enviar contenido mediante la [API de GraphQL ](/help/headless/graphql-api/content-fragments.md) de.

* Disponible en el editor de páginas [mediante el componente Fragmento de contenido](/help/sites-cloud/authoring/fragments/content-fragments.md) (componente de referencia):

   * El [componente principal de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=es) está disponible para los autores de páginas. Les permite hacer referencia y enviar el fragmento de contenido requerido en formato HTML o JSON.

Los fragmentos de contenido son una estructura de contenido que:

* No tienen diseño (el formato de texto es posible para los campos de texto).
* Son independientes del mecanismo de envío (como la página o el canal).
* Incluye una o más [partes constitutivas](#constituent-parts-of-a-content-fragment).
* Puede [contener imágenes o estar conectada a ellas](#fragments-with-visual-assets).

### Fragmentos con recursos visuales {#fragments-with-visual-assets}

Para que los autores tengan un mayor control sobre su contenido, las imágenes se pueden añadir o integrar con un fragmento de contenido.

Assets se puede utilizar con un fragmento de contenido de varias formas, cada una con sus propias ventajas:

* como **referencia de contenido**
* dentro de un campo **Texto multilínea**

### Partes constitutivas de un fragmento de contenido {#constituent-parts-of-a-content-fragment}

Los recursos de fragmento de contenido están formados por las siguientes partes (directa o indirectamente):

* **Elementos de fragmento**

   * Los elementos se correlacionan con los campos de datos que tienen contenido.
   * Utiliza un [Modelo de fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) para crear el fragmento de contenido. Los elementos (campos) especificados en el modelo definen la estructura del fragmento. Estos elementos (campos) pueden ser de varios tipos de datos.

* **Párrafos de fragmento**

   * Bloques de texto, a menudo de varias líneas, que se delimitan como entidades individuales.

   * Habilite el control de contenido durante la creación de páginas.

* **Metadatos de fragmento**

   * Utilice los [Esquemas de metadatos de recursos](/help/assets/metadata-schemas.md).
   * Las etiquetas se pueden crear cuando hace lo siguiente:

      * Crea el fragmento
      * O más tarde, cuando [vea o edite las propiedades](/help/sites-cloud/administering/content-fragments/authoring.md#view-properties-tags) en el editor de fragmentos

  >[!CAUTION]
  >
  >Los perfiles de procesamiento de metadatos no se aplican a los fragmentos de contenido.

  >[!CAUTION]
  >
  >Un modelo de fragmento de contenido puede definir con frecuencia campos de datos llamados **Title** y **Description**. Si existen estos dos campos, son campos definidos por el usuario y se pueden actualizar en el área de contenido del editor.
  >
  >El fragmento de contenido y sus variaciones también tienen campos de metadatos (propiedad) llamados **Title** y **Description**. Estos dos campos de metadatos son parte integral de cualquier fragmento de contenido, y variación, y se definen inicialmente cuando se crea el fragmento. Se pueden actualizar en el área de propiedades/metadatos del editor.

* **[Principal](#main-and-variations)**
* **[Variaciones](#main-and-variations)**

### Requerido por fragmentos {#required-by-fragments}

Para crear fragmentos de contenido necesita lo siguiente:

* **Modelo de contenido**

   * Están [habilitados mediante el Explorador de configuración](/help/sites-cloud/administering/content-fragments/setup.md).
   * Son [creados mediante Herramientas](/help/sites-cloud/administering/content-fragments/content-fragment-models.md).
   * Requerido para [crear un fragmento](/help/sites-cloud/administering/content-fragments/managing.md#creating-content-fragments).
   * Define la estructura de un fragmento (título, elementos de contenido, definiciones de etiquetas).
   * Las definiciones del modelo de fragmento de contenido requieren un título y un elemento de datos; todo lo demás es opcional.
   * El modelo puede definir el contenido predeterminado, si corresponde.
   * Los autores no pueden cambiar la estructura definida al crear contenido de fragmento; aunque pueden abrir el editor de modelos desde el editor de fragmentos.
   * Los cambios realizados en un modelo después de crear fragmentos de contenido dependientes pueden afectar a esos fragmentos de contenido.

Para utilizar los fragmentos de contenido para la entrega de contenido sin encabezado, también necesita lo siguiente:

* una [consulta de GraphQL](/help/headless/graphql-api/content-fragments.md) para solicitar el contenido requerido
* SPA AEM este contenido se puede utilizar para desarrollar su propio contenido para el desarrollo de su propio de trabajo; para obtener más información, consulte los siguientes documentos:

   * [Tutorial WKND de SPA](/help/implementing/developing/hybrid/wknd-tutorial.md)
   * [Introducción a React](/help/implementing/developing/hybrid/getting-started-react.md)
   * [Introducción a Angular](/help/implementing/developing/hybrid/getting-started-angular.md)

Para utilizar los fragmentos de contenido para la creación de páginas, también necesita lo siguiente:

* Un **componente de fragmento de contenido**

   * Instrumental para entregar el fragmento en formato HTML o JSON.
   * Requerido para [hacer referencia al fragmento en una página](/help/sites-cloud/authoring/fragments/content-fragments.md).
   * Responsable del diseño y la entrega de un fragmento; por ejemplo, de los canales.
   * Los fragmentos necesitan uno o más componentes dedicados para definir el diseño y proporcionar algunos o todos los elementos/variaciones y el contenido asociado.
   * Al arrastrar un fragmento a una página en la creación, se asocia automáticamente el componente requerido.
   * Ver [Componente principal de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=es).

## Uso de ejemplo {#example-usage}

Un fragmento, con sus elementos y variaciones, se puede utilizar para crear contenido coherente para varios canales. Al diseñar el fragmento, debe tener en cuenta qué se utilizará y dónde.

### Ejemplo de WKND {#wknd-sample}

Las muestras [WKND Site y WKND Shared](/help/implementing/developing/introduction/develop-wknd-tutorial.md) se proporcionan para ayudarle a obtener más información acerca de AEM as a Cloud Service.

<!-- CHECK: which links can/should be used these days? -->

El proyecto WKND incluye lo siguiente:

* Modelos de fragmentos de contenido disponibles en:

   * `.../libs/dam/cfm/models/console/content/models.html/conf/wknd`

   * `.../ui#/aem/libs/dam/cfm/models/console/content/models.html/conf/wknd-shared`

* Fragmentos de contenido (y otro contenido) disponibles en:

   * `.../assets.html/content/dam/wknd/en`
