---
title: Trabajar con fragmentos de contenido
description: Descubra cómo los fragmentos de contenido en Adobe Experience Manager (AEM) as a Cloud Service le permiten diseñar, crear, depurar y utilizar contenido independiente de las páginas, lo que resulta ideal para envíos sin periféricos.
feature: Content Fragments
role: User
exl-id: db17eff1-4252-48d5-bb67-5e476e93ef7e
source-git-commit: e592dd7a3a717259493f23943933fe3d0e71b7ab
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 6%

---

# Trabajar con fragmentos de contenido {#working-with-content-fragments}

Con Adobe Experience Manager (AEM) as a Cloud Service, los fragmentos de contenido le permiten diseñar, crear, depurar y [publicar contenido independiente de la página](/help/sites-cloud/authoring/fundamentals/content-fragments.md) Permiten preparar contenido listo para usar en varias ubicaciones o en varios canales, lo que resulta ideal para una entrega sin periféricos.

Los fragmentos de contenido contienen contenido estructurado:

* Se basan en un [Modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md), que predefine una estructura para el fragmento resultante.
* La estructura puede variar entre:
   * Básico
      * Por ejemplo, un campo de texto de varias líneas.
      * Se puede utilizar para preparar contenido directo para su uso en la creación de páginas.
   * Complejo
      * Una combinación de muchos campos de diferentes tipos de datos, incluyendo texto, número, booleano, datos y tiempo, entre otros.
      * Se puede utilizar para preparar contenido más estructurado para la creación de páginas o para su envío a la aplicación.
   * Anidado
      * Los tipos de datos de referencia disponibles le permiten anidar el contenido.
      * Tiende a utilizarse para su envío a la aplicación.

Los fragmentos de contenido también se pueden entregar en formato JSON, utilizando las capacidades de exportación del Modelo Sling (JSON) de AEM componentes principales. Esta forma de envío:

* permite utilizar el componente para administrar qué elementos de un fragmento enviar
* permite la entrega masiva, añadiendo varios componentes principales de fragmento de contenido en la página que se utiliza para la entrega de API

Esta y las siguientes páginas tratan sobre las tareas para crear, configurar, mantener y utilizar sus fragmentos de contenido:

* [Habilitar la funcionalidad de fragmento de contenido para su instancia](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modelos de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md) - activar, crear y definir sus modelos
* [Administración de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) - cree sus fragmentos de contenido; a continuación, edite, publique y haga referencia a
* [Variaciones: creación de contenido de fragmentos](/help/assets/content-fragments/content-fragments-variations.md) - cree el contenido del fragmento y cree variaciones del patrón
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) - uso de la sintaxis de markdown para el fragmento
* [Uso de contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md) - añadir contenido asociado
* [Metadatos: Propiedades del fragmento](/help/assets/content-fragments/content-fragments-metadata.md) : visualización y edición de las propiedades del fragmento
* Uso [Fragmentos de contenido, junto con GraphQL, para entregar contenido](/help/assets/content-fragments/content-fragments-graphql.md) para usar en sus aplicaciones. Para ayudarle con esto, puede obtener una vista previa [Salida JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>Estas páginas pueden leerse junto con:
>
>* [Creación de páginas con fragmentos de contenido](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* [Personalizar y ampliar fragmentos de contenido](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Fragmentos de contenido Configurar componentes para procesamiento](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [AEM API de GraphQL para su uso con fragmentos de contenido](/help/headless/graphql-api/content-fragments.md)


El número de canales de comunicación aumenta anualmente. Normalmente, los canales hacen referencia al mecanismo de envío, ya sea como:

* Canal físico; p. ej., escritorio o móvil.
* Forma de entrega en un canal físico; Por ejemplo, la &quot;página de detalles del producto&quot;, la &quot;página de categoría del producto&quot; para escritorio o la &quot;web móvil&quot;, la &quot;aplicación móvil&quot; para móvil.

Sin embargo, usted (probablemente) no desea utilizar exactamente el mismo contenido para todos los canales, necesita optimizar su contenido según el canal específico.

Los fragmentos de contenido le permiten:

* Piense en cómo llegar a las audiencias de destino de forma eficaz en todos los canales.
* Cree y administre contenido editorial neutro para el canal.
* Cree grupos de contenido para una amplia gama de canales.
* Diseñe variaciones de contenido para canales específicos.
* Añada imágenes al texto insertando recursos (fragmentos de medios mixtos).
* Cree contenido anidado para reflejar la complejidad de sus datos.

Estos fragmentos de contenido se pueden ensamblar para ofrecer experiencias en una variedad de canales.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencias](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** son funciones distintas de AEM:
>* **Fragmentos de contenido** son contenido editorial, que puede utilizarse para acceder a datos estructurados, incluidos textos, números y fechas, entre otros. Son contenido puro, con definición y estructura, pero sin diseño visual y/o diseño adicional.
>* Los **fragmentos de experiencia** son contenido plenamente diseñado; un fragmento de una página web. 
>
>Los fragmentos de experiencias pueden incluir contenido en forma de fragmentos de contenido, pero no lo contrario.
>
>Para obtener más información, consulte también [Explicación de los fragmentos de contenido y los fragmentos de experiencia en AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html#content-fragments).

## Fragmentos de contenido y servicios de contenido {#content-fragments-and-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y el envío de contenido desde o hacia AEM más allá del enfoque en las páginas web.

Proporcionan la entrega de contenido a canales que no son páginas web AEM tradicionales, utilizando métodos estandarizados que cualquier cliente puede consumir. Estos canales pueden incluir:

* Aplicaciones de una sola página
* Aplicaciones móviles nativas
* otros canales y puntos de contacto externos a AEM

La entrega se realiza en formato JSON utilizando el exportador JSON.

AEM fragmentos de contenido se pueden usar para describir y administrar el contenido estructurado. El contenido estructurado se define en modelos que pueden contener una variedad de tipos de contenido; incluido texto, datos numéricos, booleano, fecha y hora, etc.

Junto con las capacidades de exportación de JSON de AEM componentes principales, este contenido estructurado se puede utilizar para entregar contenido AEM a canales que no sean páginas de AEM.

>[!NOTE]
>
>Consulte [Sin encabezado y AEM](/help/headless/introduction.md) para obtener una introducción al desarrollo sin encabezado para AEM Sites as a Cloud Service.

>[!NOTE]
>
>AEM también admite la traducción del contenido del fragmento.

>[!NOTE]
>
>AEM también admite la traducción del contenido del fragmento. Consulte [Traducción de recursos](/help/assets/translate-assets.md) para obtener más información.

## Tipo de contenido {#content-type}

Los fragmentos de contenido son:

* Almacenado como **Recursos**:

   * Los fragmentos de contenido (y sus variaciones) se pueden crear y mantener a partir del **Recursos** consola.
   * Se ha creado y editado en el Editor de fragmentos de contenido.

* Se usa en la variable [editor de páginas mediante el componente Fragmento de contenido](/help/sites-cloud/authoring/fundamentals/content-fragments.md) (componente de referencia):

   * La variable **Fragmento de contenido** está disponible para los autores de páginas. Les permite hacer referencia y enviar el fragmento de contenido requerido en formato HTML o JSON.

* Accesible mediante la variable [API de AEM GraphQL](/help/headless/graphql-api/content-fragments.md).

Los fragmentos de contenido son una estructura de contenido que:

* No tienen diseño o diseño (es posible aplicar formato de texto en el modo Texto enriquecido).
* Incluir uno o más, [partes constitutivas](#constituent-parts-of-a-content-fragment).
* Can [contener imágenes o conectarse a ellas](#fragments-with-visual-assets).
* Puede usar [contenido intermedio](#in-between-content-when-page-authoring-with-content-fragments) cuando se haga referencia a en una página.

* Son independientes del mecanismo de envío (es decir, página, canal).

### Fragmentos con recursos visuales {#fragments-with-visual-assets}

Para que los autores tengan un mayor control sobre su contenido, las imágenes se pueden añadir o integrar con un fragmento de contenido.

Los recursos se pueden utilizar con un fragmento de contenido de varias formas; cada uno con sus propias ventajas:

* **Insertar recurso** en un fragmento (fragmentos de medios mixtos)

   * Son una parte integral del fragmento (consulte [Partes constitutivas de un fragmento de contenido](#constituent-parts-of-a-content-fragment)).
   * Defina la posición del recurso.
   * Consulte [Inserción de recursos en el fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) en el Editor de fragmentos para obtener más información.

   >[!NOTE]
   >
   >Los recursos visuales insertados en el propio fragmento de contenido se adjuntan al párrafo anterior. Cuando se añade el fragmento a una página, estos recursos se mueven en relación con ese párrafo cuando se añade contenido intermedio.

* **Contenido asociado**

   * están conectadas a un fragmento; pero no una parte fija del fragmento (consulte [Partes constitutivas de un fragmento de contenido](#constituent-parts-of-a-content-fragment)).
   * Permite cierta flexibilidad de posicionamiento.
   * Están fácilmente disponibles para su uso (como contenido intermedio) al utilizar el fragmento en una página.
   * Consulte [Contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md) para obtener más información.

* Recursos disponibles desde el **explorador de Assets** del editor de páginas

   * Permitir flexibilidad total para la selección de un recurso.
   * Permite cierta flexibilidad de posicionamiento.
   * No proporciona el concepto de ser aprobado para un fragmento específico.
   * Consulte [Navegador de recursos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) para obtener más información.

### Partes constitutivas de un fragmento de contenido {#constituent-parts-of-a-content-fragment}

Los recursos de fragmento de contenido están formados por las siguientes partes (directa o indirectamente):

* **Elementos de fragmento**

   * Los elementos se correlacionan con los campos de datos que contienen contenido.
   * Utilice un modelo de contenido para crear el fragmento de contenido. Los elementos (campos) especificados en el modelo definen la estructura del fragmento. Estos elementos (campos) pueden ser de varios tipos de datos.

* **Párrafos de fragmento**

   * Bloques de texto, a menudo multilínea, que se delimitan como entidades individuales.

   * En los modos [Texto enriquecido](/help/assets/content-fragments/content-fragments-variations.md#rich-text) y [Marcado](/help/assets/content-fragments/content-fragments-variations.md#markdown), un párrafo se puede formatear como un encabezado, en cuyo caso, ese párrafo y el siguiente se unirán como una sola unidad.

   * Habilite el control de contenido durante la creación de páginas.

* **Recursos insertados en un fragmento (fragmentos de medios mixtos)**

   * Recursos (imágenes) insertados en el fragmento real y utilizados como contenido interno de un fragmento.
   * Están incrustadas en el sistema de párrafos del fragmento.
   * Se le puede dar formato cuando [se utiliza/se hace referencia al fragmento en una página](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Solo se puede agregar, eliminar o mover dentro de un fragmento con el editor de fragmentos. Estas acciones no se pueden realizar en el editor de páginas.
   * Solo se puede agregar, eliminar o mover dentro de un fragmento mediante [Formato de texto enriquecido en el editor de fragmentos](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Solo se puede añadir a elementos de texto multilínea (cualquier tipo de fragmento).
   * Se adjuntan al texto anterior (párrafo).

      >[!CAUTION]
      >
      >Los recursos se pueden eliminar (de forma involuntaria) de un fragmento cambiando al formato de texto sin formato.

      >[!NOTE]
      >
      >Los recursos también se pueden añadir como [contenido adicional (intermedio)](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) al utilizar un fragmento en una página; usar contenido asociado o recursos del navegador Recursos.

* **Contenido asociado**

   * Es contenido externo a un fragmento, pero con relevancia editorial para él. Normalmente, imágenes, vídeos u otros fragmentos.
   * Los recursos individuales de la colección están disponibles para su uso con el fragmento en el editor de páginas, cuando se añada a una página. Esto significa que son opcionales, según los requisitos del canal específico.
   * Los recursos son [asociados a fragmentos mediante colecciones](/help/assets/content-fragments/content-fragments-assoc-content.md); las colecciones asociadas permiten al autor decidir qué recursos utilizar cuando esté creando la página.

      * Las colecciones se pueden asociar a fragmentos como contenido predeterminado, o por parte de los autores durante la creación de fragmentos.
      * [Colecciones de recursos (DAM)](/help/assets/manage-collections.md) son la base del contenido asociado de los fragmentos.
   * De forma opcional, también puede agregar el fragmento a una colección para ayudar en el seguimiento.

* **Metadatos de fragmento**

   * Utilice la variable [Esquemas de metadatos de recursos](/help/assets/metadata-schemas.md).
   * Las etiquetas se pueden crear cuando:

      * Creación y creación del fragmento
      * O posterior:

         * Visualización/edición del fragmento **Propiedades** desde la consola
         * Al editar la variable **Metadatos** en el editor de fragmentos

   >[!CAUTION]
   >
   >Los perfiles de procesamiento de metadatos no se aplican a los fragmentos de contenido.

* **Principal**

   * Una parte integral del fragmento

      * Cada fragmento de contenido tiene una instancia de Maestro.
      * El patrón no se puede eliminar.
   * Se puede acceder al formato principal en el editor de fragmentos, en **[Variaciones](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Master no es una variación como tal, sino la base de todas las variaciones.


* **Variaciones**

   * Representaciones de texto de fragmento específicas para fines editoriales; puede estar relacionado con el canal, pero no es obligatorio, también puede ser para modificaciones locales específicas.
   * Se crean como copias de **Maestro**, pero se pueden editar según sea necesario; normalmente, el contenido se superpone entre las propias variaciones.
   * Se puede definir durante la creación de fragmentos.
   * Almacenadas en el fragmento para evitar la dispersión de copias de contenido.
   * Las variaciones se pueden [sincronizar](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) con Principal si se ha actualizado el contenido principal.
   * Puede [Resumida](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) para truncar rápidamente el texto a una longitud predefinida.
   * Disponible en la sección [Variaciones](/help/assets/content-fragments/content-fragments-variations.md) del editor de fragmentos.

### Contenido intermedio al crear páginas con fragmentos de contenido {#in-between-content-when-page-authoring-with-content-fragments}

Contenido intermedio:

* Está disponible para su uso en el Editor de páginas al trabajar con fragmentos de contenido.
* Is [contenido adicional añadido dentro del flujo de un fragmento](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) una vez que se ha utilizado o se ha hecho referencia a él en una página.
* Está disponible para su uso en la variable [Editor de páginas al trabajar con fragmentos de contenido](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
* El contenido intermedio se puede añadir a cualquier fragmento, donde solo hay un elemento visible.
* Se puede utilizar contenido asociado, así como recursos o componentes del navegador adecuado.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

### Requerido por fragmentos {#required-by-fragments}

Para crear fragmentos de contenido necesita:

* **Modelo de contenido**

   * Son [habilitado mediante el Explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * Son [creado mediante Herramientas](/help/assets/content-fragments/content-fragments-models.md).
   * Requerido para [crear un fragmento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Define la estructura de un fragmento (título, elementos de contenido, definiciones de etiquetas).
   * Las definiciones de modelos de contenido requieren un título y un elemento de datos; todo lo demás es opcional.
   * El modelo puede definir el contenido predeterminado, si corresponde.
   * Los autores no pueden cambiar la estructura definida al crear contenido de fragmento.
   * Los cambios realizados en un modelo después de crear fragmentos de contenido dependientes pueden afectar a esos fragmentos de contenido.

Para utilizar los fragmentos de contenido para la creación de páginas, también necesita:

* **Componente Fragmento de contenido**

   * Instrumental para entregar el fragmento en formato HTML o JSON.
   * Requerido para [hacer referencia al fragmento en una página](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Responsable de la presentación y entrega de un fragmento; es decir, canales.
   * Los fragmentos necesitan uno o más componentes dedicados para definir el diseño y proporcionar algunos o todos los elementos/variaciones y el contenido asociado.
   * Al arrastrar un fragmento a una página en la creación, se asociará automáticamente el componente requerido.

## Uso de ejemplo {#example-usage}

Un fragmento, con sus elementos y variaciones, se puede utilizar para crear contenido coherente para varios canales. Al diseñar el fragmento, debe tener en cuenta qué se utilizará donde.

### Ejemplo de WKND {#wknd-sample}

La variable [Sitio WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) se proporcionan ejemplos para ayudarle a obtener más información sobre AEM as a Cloud Service.

El proyecto WKND incluye:

* Modelos de fragmento de contenido disponibles en:
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Fragmentos de contenido (y otro contenido) disponibles en:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
