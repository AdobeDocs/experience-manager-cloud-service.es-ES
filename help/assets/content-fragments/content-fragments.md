---
title: Trabajar con fragmentos de contenido
description: Descubra cómo los fragmentos de contenido de Adobe Experience Manager (AEM) como Cloud Service le permiten diseñar, crear, depurar y utilizar contenido independiente de la página.
translation-type: tm+mt
source-git-commit: 6f8264ae53b30afac0cc523c312aea8918e5eafa
workflow-type: tm+mt
source-wordcount: '2027'
ht-degree: 6%

---


# Trabajar con fragmentos de contenido{#working-with-content-fragments}

Con Adobe Experience Manager (AEM) como Cloud Service, los fragmentos de contenido le permiten diseñar, crear, depurar y [publicar contenido independiente de la página](/help/sites-cloud/authoring/fundamentals/content-fragments.md). Permiten preparar contenido listo para su uso en varias ubicaciones o en varios canales.

Los fragmentos de contenido contienen contenido estructurado:

* Se basan en un [Modelo de fragmento de contenido](/help/assets/content-fragments/content-fragments-models.md), que predefine una estructura para el fragmento resultante.
* La estructura puede variar entre:
   * Básico
      * Por ejemplo, un solo campo de texto con varias líneas.
      * Se puede utilizar para preparar contenido directo para su uso en la creación de páginas.
   * Complejo
      * Combinación de muchos campos de distintos tipos de datos, como texto, número, booleano, datos y tiempo, entre otros.
      * Puede utilizarse para preparar contenido más estructurado para la creación de páginas o para el envío a la aplicación.
   * Anidado
      * Los tipos de datos de referencia disponibles le permiten anidar el contenido.
      * Tiende a utilizarse para el envío a la aplicación.

Los fragmentos de contenido también se pueden entregar en formato JSON, mediante las capacidades de exportación del Modelo Sling (JSON) de AEM componentes principales. Esta forma de envío:

* le permite utilizar el componente para administrar qué elementos de un fragmento entregar
* permite el envío masivo, agregando varios componentes principales de fragmento de contenido en la página que se está utilizando para el envío de API

Esta y las siguientes páginas cubren las tareas para crear, configurar, mantener y utilizar los fragmentos de contenido:

* [Habilitar la funcionalidad de fragmento de contenido para su instancia](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modelos](/help/assets/content-fragments/content-fragments-models.md)  de fragmentos de contenido: activar, crear y definir sus modelos
* [Administración de fragmentos](/help/assets/content-fragments/content-fragments-managing.md)  de contenido: cree sus fragmentos de contenido; a continuación, edite, publique y haga referencia a
* [Variaciones - Creación de contenido](/help/assets/content-fragments/content-fragments-variations.md)  de fragmento- cree el contenido de fragmento y las variaciones del patrón
* [Markdown](/help/assets/content-fragments/content-fragments-markdown.md) : uso de la sintaxis de marca para el fragmento
* [Uso de contenido](/help/assets/content-fragments/content-fragments-assoc-content.md)  asociado: adición de contenido asociado
* [Metadatos - Propiedades](/help/assets/content-fragments/content-fragments-metadata.md)  del fragmento: visualización y edición de las propiedades del fragmento
* Utilice [Fragmentos de contenido, junto con GraphQL, para entregar contenido](/help/assets/content-fragments/content-fragments-graphql.md) para su uso en las aplicaciones. Para ayudarle con esto, puede realizar la previsualización [salida de JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>Estas páginas se pueden leer junto con:
>
>* [Creación de páginas con fragmentos de contenido](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
>* [Personalizar y ampliar fragmentos de contenido](/help/implementing/developing/extending/content-fragments-customizing.md)
>* [Fragmentos de contenido Configurar componentes para procesamiento](/help/implementing/developing/extending/content-fragments-configuring-components-rendering.md)
>* [Compatibilidad con fragmentos de contenido en la API HTTP de AEM Assets](/help/assets/content-fragments/assets-api-content-fragments.md)
>* [API de AEM GraphQL para usar con fragmentos de contenido](/help/assets/content-fragments/graphql-api-content-fragments.md)


El número de canales de comunicación aumenta cada año. Normalmente, los canales hacen referencia al mecanismo de envío, ya sea como:

* Canal físico; Por ejemplo, escritorio, móvil.
* Forma de envío en un canal físico; Por ejemplo: &quot;página de detalles del producto&quot;, &quot;página de categoría del producto&quot; para escritorio o &quot;web móvil&quot;, &quot;aplicación móvil&quot; para dispositivos móviles.

Sin embargo, usted (probablemente) no desea utilizar exactamente el mismo contenido para todos los canales; necesita optimizar su contenido según el canal específico.

Los fragmentos de contenido le permiten:

* Considere cómo alcanzar audiencias de destinatario de manera eficiente en todos los canales.
* Cree y gestione contenido editorial neutro para el canal.
* Cree grupos de contenido para una amplia gama de canales.
* Diseñar variaciones de contenido para canales específicos.
* Añada imágenes al texto insertando recursos (fragmentos de medios mixtos).
* Cree contenido anidado para reflejar la complejidad de los datos.

Estos fragmentos de contenido se pueden ensamblar para proporcionar experiencias en diversos canales.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencias](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** son funciones distintas de AEM:
>* **Los** fragmentos de contenido son contenido editorial que se puede utilizar para acceder a datos estructurados, incluidos textos, números y fechas, entre otros. Son contenidos puros, con definición y estructura, pero sin diseño visual y/o diseño adicional.
>* Los **fragmentos de experiencia** son contenido plenamente diseñado; un fragmento de una página web. 

>
>
Los fragmentos de experiencias pueden incluir contenido en forma de fragmentos de contenido, pero no lo contrario.
>
>Para obtener más información, consulte también [Explicación de los fragmentos de contenido y los fragmentos de experiencia en AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=en#content-fragments).

## Fragmentos de contenido y servicios de contenido {#content-fragments-and-content-services}

Los servicios de contenido de AEM están diseñados para generalizar la descripción y el envío del contenido desde/hacia AEM más allá del enfoque en las páginas web.

Proporcionan el envío de contenido a canales que no son páginas web AEM tradicionales, utilizando métodos estandarizados que pueden ser consumidos por cualquier cliente. Estos canales pueden incluir:

* Aplicaciones de una sola página
* Aplicaciones móviles nativas
* otros canales y puntos de contacto externos a AEM

El envío se realiza en formato JSON mediante el exportador JSON.

AEM fragmentos de contenido se pueden utilizar para describir y administrar el contenido estructurado. El contenido estructurado se define en modelos que pueden contener diversos tipos de contenido; incluyendo texto, datos numéricos, booleano, fecha y hora, etc.

Junto con las capacidades de exportación JSON de AEM componentes principales, este contenido estructurado se puede utilizar para entregar contenido AEM a canales que no sean páginas AEM.

>[!NOTE]
>
>Consulte [Sin cabeza y AEM](/help/implementing/developing/headless/introduction.md) para obtener una introducción al desarrollo sin cabeza para AEM Sites como Cloud Service.

>[!NOTE]
>
>AEM también admite la traducción del contenido del fragmento.

>[!NOTE]
>
>AEM también admite la traducción del contenido del fragmento. Consulte [Traducción de recursos](/help/assets/translate-assets.md) para obtener más información.

## Tipo de contenido {#content-type}

Los fragmentos de contenido son:

* Almacenados como **Recursos**:

   * Los fragmentos de contenido (y sus variaciones) se pueden crear y mantener desde la consola **Assets**.
   * Se ha creado y editado en el Editor de fragmentos de contenido.

* Se utiliza en el editor de páginas [mediante el componente Fragmento de contenido](/help/sites-cloud/authoring/fundamentals/content-fragments.md) (componente de referencia):

   * El componente **Fragmento de contenido** está disponible para los autores de páginas. Les permite hacer referencia y entregar el fragmento de contenido requerido en formato HTML o JSON.

* Accesible mediante la [API de GraphQL de AEM](/help/assets/content-fragments/graphql-api-content-fragments.md).

Los fragmentos de contenido son una estructura de contenido que:

* Están sin diseño o diseño (se puede aplicar algún formato de texto en el modo Texto enriquecido).
* Contener una o más partes constituyentes [](#constituent-parts-of-a-content-fragment).
* Puede [contener o estar conectado a imágenes](#fragments-with-visual-assets).
* Puede utilizar [contenido intermedio](#in-between-content-when-page-authoring-with-content-fragments) cuando se hace referencia a él en una página.

* Son independientes del mecanismo de envío (p. ej. página, canal).

### Fragmentos con recursos visuales {#fragments-with-visual-assets}

Para otorgar a los autores un mayor control sobre su contenido, las imágenes se pueden añadir o integrar con un fragmento de contenido.

Los recursos se pueden utilizar con un fragmento de contenido de varias formas; cada uno con sus propias ventajas:

* **Insertar** recurso en un fragmento (fragmentos de medios mixtos)

   * Son una parte integral del fragmento (consulte [Partes constituyentes de un fragmento de contenido](#constituent-parts-of-a-content-fragment)).
   * Defina la posición del recurso.
   * Consulte [Inserción de recursos en el fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) en el Editor de fragmentos para obtener más información.

   >[!NOTE]
   >
   >Los recursos visuales insertados en el propio fragmento de contenido se adjuntan al párrafo anterior. Cuando se agrega el fragmento a una página, estos recursos se mueven en relación con ese párrafo cuando se agrega contenido intermedio.

* **Contenido asociado**

   * Están conectados a un fragmento; pero no una parte fija del fragmento (consulte [Partes constituyentes de un fragmento de contenido](#constituent-parts-of-a-content-fragment)).
   * Permite cierta flexibilidad en la colocación.
   * Están fácilmente disponibles para su uso (como contenido intermedio) al utilizar el fragmento en una página.
   * Consulte [Contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md) para obtener más información.

* Recursos disponibles desde el **explorador de Assets** del editor de páginas

   * Permite una flexibilidad total para seleccionar un recurso.
   * Permite cierta flexibilidad en la colocación.
   * No proporciona el concepto de aprobación para un fragmento específico.
   * Consulte [Navegador de recursos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser) para obtener más información.

### Partes constituyentes de un fragmento de contenido {#constituent-parts-of-a-content-fragment}

Los recursos de fragmento de contenido están formados por las siguientes partes (directa o indirectamente):

* **Elementos de fragmento**

   * Los elementos se correlacionan con los campos de datos que contienen contenido.
   * Utilice un modelo de contenido para crear el fragmento de contenido. Los elementos (campos) especificados en el modelo definen la estructura del fragmento. Estos elementos (campos) pueden ser de diversos tipos de datos.

* **Párrafos de fragmento**

   * Bloques de texto, a menudo multilínea, que se delimitan como entidades individuales.

   * En los modos [Texto enriquecido](/help/assets/content-fragments/content-fragments-variations.md#rich-text) y [Marcado](/help/assets/content-fragments/content-fragments-variations.md#markdown), un párrafo se puede formatear como un encabezado, en cuyo caso, ese párrafo y el siguiente se unirán como una sola unidad.

   * Habilite el control de contenido durante la creación de páginas.

* **Recursos insertados en un fragmento (fragmentos de medios mixtos)**

   * Recursos (imágenes) insertados en el fragmento real y utilizados como contenido interno de un fragmento.
   * Están incrustadas en el sistema de párrafos del fragmento.
   * Se puede dar formato cuando se utiliza o hace referencia al fragmento [en una página](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Solo se puede agregar, eliminar o mover dentro de un fragmento mediante el editor de fragmentos. Estas acciones no se pueden realizar en el editor de páginas.
   * Solo se puede agregar, eliminar o mover dentro de un fragmento con formato [Texto enriquecido en el editor de fragmentos](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Solo se puede agregar a elementos de texto de varias líneas (cualquier tipo de fragmento).
   * Se adjuntan al texto anterior (párrafo).

      >[!CAUTION]
      >
      >Los recursos pueden eliminarse (inadvertidamente) de un fragmento cambiando al formato de texto sin formato.

      >[!NOTE]
      >
      >Los recursos también se pueden agregar como [contenido adicional (intermedio)](/help/sites-cloud/authoring/fundamentals/content-fragments.md#using-associated-content) al utilizar un fragmento en una página; mediante Contenido asociado o recursos del navegador de recursos.

* **Contenido asociado**

   * Se trata de contenido externo a un fragmento, pero con relevancia editorial. Normalmente, imágenes, vídeos u otros fragmentos.
   * Los recursos individuales de la colección están disponibles para utilizarse con el fragmento en el editor de páginas, cuando se añada a una página. Esto significa que son opcionales, según los requisitos del canal específico.
   * Los recursos están [asociados a fragmentos mediante colecciones](/help/assets/content-fragments/content-fragments-assoc-content.md); las colecciones asociadas permiten al autor decidir qué recursos utilizar al crear la página.

      * Las colecciones pueden asociarse a fragmentos como contenido predeterminado o por autores durante la creación de fragmentos.
      * [Las ](/help/assets/manage-collections.md) colecciones de recursos (DAM) son la base del contenido asociado de los fragmentos.
   * Opcionalmente, también puede agregar el propio fragmento a una colección para facilitar el seguimiento.

* **Metadatos de fragmento**

   * Utilice los [esquemas de metadatos de recursos](/help/assets/metadata-schemas.md).
   * Las etiquetas se pueden crear cuando:

      * Creación y creación del fragmento
      * O posterior:

         * Al ver/editar el fragmento **Propiedades** desde la consola
         * Al editar los **metadatos** en el editor de fragmentos

   >[!CAUTION]
   >
   >Los perfiles de procesamiento de metadatos no se aplican a los fragmentos de contenido.

* **Principal**

   * Parte integrante del fragmento

      * Cada fragmento de contenido tiene una instancia de Master.
      * No se puede eliminar el patrón principal.
   * Se puede acceder a Master en el editor de fragmentos en **[Variaciones](/help/assets/content-fragments/content-fragments-variations.md)**.
   * Master no es una variación como tal, sino la base de todas las variaciones.


* **Variaciones**

   * Representaciones de texto de fragmento específicas para fines editoriales; puede estar relacionado con el canal pero no es obligatorio, también puede ser para modificaciones locales ad hoc.
   * Se crean como copias de **Master**, pero se pueden editar según sea necesario; normalmente hay superposición de contenido entre las variaciones mismas.
   * Se puede definir durante la creación de fragmentos.
   * Almacenada en el fragmento, para evitar la dispersión de copias de contenido.
   * Las variaciones se pueden [sincronizar](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) con Master si se ha actualizado el contenido principal.
   * Puede [Resumirse](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) para truncar rápidamente el texto a una longitud predefinida.
   * Disponible en la ficha [Variaciones](/help/assets/content-fragments/content-fragments-variations.md) del editor de fragmentos.

### Contenido intermedio al crear páginas con fragmentos de contenido {#in-between-content-when-page-authoring-with-content-fragments}

Contenido intermedio:

* Está disponible para su uso en el Editor de páginas al trabajar con fragmentos de contenido.
* Se agrega [contenido adicional dentro del flujo de un fragmento](/help/sites-cloud/authoring/fundamentals/content-fragments.md#adding-in-between-content) una vez que se ha utilizado o se ha hecho referencia a él en una página.
* Está disponible para su uso en el [Editor de páginas al trabajar con fragmentos de contenido](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
* El contenido intermedio se puede agregar a cualquier fragmento, donde solo hay un elemento visible.
* Se puede utilizar el contenido asociado, al igual que los recursos o componentes del navegador correspondiente.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

### Requerido por fragmentos {#required-by-fragments}

Para crear fragmentos de contenido necesita:

* **Modelo de contenido**

   * Se [habilitan mediante el Explorador de configuración](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * Se [crean mediante Herramientas](/help/assets/content-fragments/content-fragments-models.md).
   * Necesario para [crear un fragmento](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Define la estructura de un fragmento (título, elementos de contenido, definiciones de etiquetas).
   * Las definiciones del modelo de contenido requieren un título y un elemento de datos; todo lo demás es opcional.
   * El modelo puede definir el contenido predeterminado, si corresponde.
   * Los autores no pueden cambiar la estructura definida al crear contenido de fragmento.
   * Los cambios realizados en un modelo después de crear fragmentos de contenido dependientes pueden afectar a dichos fragmentos de contenido.

Para utilizar los fragmentos de contenido para la creación de páginas, también necesita:

* **Componente de fragmento de contenido**

   * Instrumental para entregar el fragmento en formato HTML o JSON.
   * Necesario para [hacer referencia al fragmento en una página](/help/sites-cloud/authoring/fundamentals/content-fragments.md).
   * Responsable de la presentación y el envío de un fragmento; es decir, canales.
   * Los fragmentos necesitan uno o más componentes dedicados para definir el diseño y entregar algunos o todos los elementos/variaciones y el contenido asociado.
   * Al arrastrar un fragmento a una página en la creación, se asociará automáticamente el componente requerido.

## Ejemplo de uso {#example-usage}

Un fragmento, con sus elementos y variaciones, puede utilizarse para crear contenido coherente para varios canales. Al diseñar el fragmento, debe tener en cuenta qué se utilizará en cada lugar.

### Muestra WKND {#wknd-sample}

Los ejemplos del [sitio de WKND](/help/implementing/developing/introduction/develop-wknd-tutorial.md) se proporcionan para ayudarle a obtener información sobre AEM como Cloud Service.

El proyecto WKND incluye:

* Modelos de fragmento de contenido disponibles en:
   `http://<hostname>:<port>/libs/dam/cfm/models/console/content/models.html/conf/wknd`

* Fragmentos de contenido (y otro contenido) disponibles en:
   `http://<hostname>:<port>/assets.html/content/dam/wknd/en`
