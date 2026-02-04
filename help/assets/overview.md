---
title: Introducción a Assets as a Cloud Service para la administración de recursos digitales en AEM
description: Introducción a Assets as a Cloud Service para la administración de recursos digitales en AEM
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: 5606d66dfa9c7d11063eea495088e1263a2cc5fb
workflow-type: tm+mt
source-wordcount: '5642'
ht-degree: 87%

---

# Introducción a Assets as a Cloud Service para la administración de recursos digitales en AEM {#assets-as-cloud-service-digital-asset-management-aem}

AEM Assets as a Cloud Service ofrece una solución PaaS nativa de la nube para que las empresas no solo realicen sus operaciones de administración de recursos digitales y medios dinámicos, sino que también utilicen funciones inteligentes de próxima generación, como la IA y el aprendizaje automático. Todo ello desde un sistema que siempre está actualizado, siempre disponible y siempre aprendiendo.

Adobe ofrece una solución sólida de soluciones de administración de recursos digitales (DAM) para que pueda sacar el máximo partido de sus recursos digitales. Adobe Experience Manager Assets cuenta con dos experiencias independientes que utilizan el mismo repositorio de Cloud Services para cumplir los requisitos. Para obtener información sobre experiencias basadas en perfiles para AEM Assets, consulte [Experiencias disponibles basadas en perfiles para la administración de recursos digitales](#persona-based-experiences).

Para obtener información sobre las ofertas de AEM Assets y AEM Assets Prime, consulte [Assets as a Cloud Service Ultimate](/help/assets/assets-ultimate-overview.md) y [Assets as a Cloud Service Prime](/help/assets/assets-prime.md).

Algunas de las funciones clave de la administración de recursos digitales de Adobe son:

![add-tags](assets/aem-assets-features-landing-page.png)


>[!BEGINTABS]

>[!TAB Ingesta]

## Ingesta de recursos {#asset-ingestion}

Utilice la función de importación masiva para importar un gran número de recursos directamente desde una fuente de datos, como Azure, AWS, Google Cloud, Dropbox y OneDrive, a Assets as a Cloud Service.

Puede realizar la operación de importación masiva mediante la vista del administrador o la vista de recursos. La vista de recursos proporciona más opciones de fuentes de datos que la vista del administrador.

Además de la interfaz de usuario del explorador web, Experience Manager admite otros clientes en el escritorio. También proporcionan una experiencia de carga sin necesidad de ir al explorador web.

* Adobe Asset Link proporciona acceso a recursos de Experience Manager en aplicaciones de escritorio de Adobe Photoshop, Adobe Illustrator y Adobe InDesign. Puede cargar el documento abierto en Experience Manager. Puede hacerlo directamente a través de la interfaz de Adobe Asset Link que se encuentra en las aplicaciones de escritorio.

* La aplicación de escritorio de Experience Manager simplifica el trabajo con recursos en el escritorio, independientemente del tipo de archivo o de la aplicación nativa que los gestiona. Es útil cargar archivos en jerarquías de carpetas anidadas desde el sistema de archivos local, ya que la carga desde el explorador solo permite cargar listas de archivos sin formato.

Utilice estos vínculos para acceder a la documentación detallada sobre estas herramientas de ingesta de recursos:

<table>
<td>
   <a href="/help/assets/bulk-import-assets-view.md">
   <img alt="Herramienta de importación masiva" src="./assets/bulk-images.jpeg" />
   </a>
   <div>
      <a href="/help/assets/bulk-import-assets-view.md">
      <strong>Uso de la herramienta de importación masiva</strong>
      </a>
   </div>
   <p>
      <em>Obtenga información sobre cómo importar un gran número de recursos directamente desde una fuente de datos</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/es/docs/experience-manager-desktop-app/using/get-started">
   <img alt="Uso de la aplicación de escritorio de AEM" src="./assets/desktop-app-upload.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/es/docs/experience-manager-desktop-app/using/get-started">
      <strong>Uso de la aplicación de escritorio de AEM</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a utilizar la aplicación de escritorio de AEM para cargar archivos en jerarquías de carpetas anidadas desde el sistema de archivos local.</em>
   </p>
</td>
<td>
   <a href="https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html?lang=es">
   <img alt="Uso de Adobe Asset Link" src="./assets/adobe-asset-link.jpeg" />
   </a>
   <div>
      <a href="https://helpx.adobe.com/es/enterprise/using/adobe-asset-link.html?lang=es">
      <strong>Uso de Adobe Asset Link</strong>
      </a>
   </div>
   <p>
      <em>Obtenga información sobre cómo cargar recursos en Experience Manager mediante aplicaciones de Creative Cloud.</em>
   </p>
</td>
</table>

>[!TAB Funciones con tecnología de IA]

**Etiquetas inteligentes**: Las etiquetas inteligentes utilizan el marco de trabajo artificialmente inteligente de Adobe AI para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial. A continuación, esta inteligencia de contenido se utiliza para aplicar las etiquetas relevantes a un conjunto diferente de recursos. De forma predeterminada, AEM aplica etiquetas inteligentes a los recursos cargados.

**Etiquetado y búsqueda inteligentes basados en color**: Los AEM Assets utilizan las capacidades de Adobe AI para distinguir entre colores en una imagen y aplicar esos rasgos como etiquetas automáticamente al ingerirlos. Estas etiquetas permiten una experiencia de búsqueda mejorada, basada en la composición de color de la imagen.

**Metadatos generados por IA**: AEM Assets usa la IA para generar metadatos automáticamente, incluidos títulos, descripciones y palabras clave. Estos campos generados por IA mejoran la precisión de los metadatos, lo que facilita la búsqueda, la categorización y la recomendación de recursos. Este enfoque no solo mejora la eficacia al eliminar el etiquetado manual, sino que también garantiza la coherencia y la escalabilidad en grandes volúmenes de contenido digital.

**Cambio masivo de nombre de los recursos con tecnología de IA**: [la vista Recursos permite cambiar el nombre de varios recursos a la vez mediante la inteligencia artificial](/help/assets/bulk-rename-assets-view.md). Puede seleccionar varios archivos a la vez y cambiarles el nombre. Algunas de las solicitudes de cambio de nombre conversacional de ejemplo incluyen *Cambiar todos los archivos a &#39;my-file&#39; y anexar un número incremental* y *Añadir los prefijos 001, 002, etc., a los archivos y traducir al inglés*.

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="Etiquetas inteligentes en AEM Assets" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>Añadir etiquetas inteligentes de IA a los recursos</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a aplicar etiquetas inteligentes automáticamente a los recursos cargados.</em>
   </p>
</td>

<td>
   <a href="/help/assets/color-tag-images.md">
   <img alt="Añadir etiquetas inteligentes basadas en el color" src="./assets/color-tags.jpg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong>Añadir etiquetas inteligentes basadas en el color</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a aplicar etiquetas basadas en el color automáticamente durante la ingesta.</em>
   </p>
</td>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="Metadatos generados por IA" src="./assets/ai-generated-metadata-landing.jpg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>Metadatos generados por IA</strong>
      </a>
   </div>
   <p>
      <em>Use la IA para generar metadatos de recursos, como el título y la descripción. </em>
   </p>
</td>
</table>

**Búsqueda contextual**: AEM Assets le permite buscar los recursos disponibles en el repositorio definiendo indicaciones de texto. Experience Manager Assets transforma automáticamente esas indicaciones de texto en filtros de búsqueda y muestra los resultados de la búsqueda. Puede ver y modificar los filtros automáticos mediante el panel Filtros para delimitar aún más los resultados de la búsqueda. Algunos de los ejemplos de indicaciones de texto conversacionales son los siguientes:

* *Imágenes de al menos 200 píxeles de altura y 100 píxeles de anchura con playa y cielo despejado* y
* *Necesito imágenes de cielo azul de 1500 y 2500 píxeles de altura y creadas en el último mes que no hayan caducado y estén aprobadas*.

**Generar recursos mediante Adobe Firefly en AEM**: AEM Assets le permite generar un recurso si la consulta de búsqueda no devuelve ningún resultado utilizando Adobe Firefly en tiempo real. A continuación, AEM Assets también permite cargar la imagen generada en el repositorio de AEM Assets desde la propia interfaz de usuario de AEM Assets.

**Integración con Adobe Express**: AEM Assets se integra de forma nativa con Adobe Express, lo que le permite acceder directamente a los recursos almacenados en AEM Assets desde la interfaz de usuario de Adobe Express. También puede utilizar la inteligencia artificial de Adobe Firefly en Express para generar imágenes mediante simples indicaciones de texto y colocarlas en el lienzo de Express. A continuación, puede guardar contenido nuevo o editado en un repositorio de AEM Assets.

<table>
<td>
   <a href="/help/assets/search-assets-view.md#contextual-search">
   <img alt="Búsqueda contextual" src="./assets/ai-based-search.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#contextual-search">
      <strong>Búsqueda contextual</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a buscar recursos con simples mensajes de texto.</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md#search-firefly">
   <img alt="Generar recursos mediante Adobe Firefly" src="./assets/adobe-firefly.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#search-firefly">
      <strong>Generar recursos mediante Adobe Firefly</strong>
      </a>
   </div>
   <p>
      <em>Generar recursos en tiempo real mediante Adobe Firefly.</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="Integración con Adobe Express" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>Integración con Adobe Express</strong>
      </a>
   </div>
   <p>
      <em>Use las funciones de IA de Adobe Express en la interfaz de usuario de AEM Assets.</em>
   </p>
</td>
</table>

**Imágenes inteligentes**: las imágenes inteligentes ofrecen un rendimiento aun mejor en el envío de recursos de la imagen ya que optimizan automáticamente el formato y el tamaño de archivo de una imagen en función de la capacidad del explorador del cliente. Funciona con los ajustes preestablecidos de imagen existentes y utiliza inteligencia en el envío. Esta inteligencia reduce aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red y del explorador.

**Recorte inteligente**: una funcionalidad de Adobe AI que permite detectar automáticamente el punto focal en cualquier imagen o vídeo y recortar para mantenerlo. Captura el punto de interés deseado independientemente del tamaño de la pantalla y, por lo tanto, elimina las tareas manuales tediosas, y ofrece imágenes y vídeo de alta calidad y carga rápida que se ven bien en cualquier dispositivo o pantalla.

**Subtítulos de vídeo generados por IA**: los subtítulos de vídeo generados por IA en Adobe Dynamic Media utilizan la inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. Esta función se ha diseñado para mejorar la accesibilidad y la experiencia del usuario gracias a la provisión de subtítulos precisos. Los subtítulos se generan a partir del audio original, de cualquier pista de audio adicional o de subtítulos adicionales proporcionados en la pestaña `Captions and Audio` de la página de propiedades del vídeo. Con compatibilidad con más de 60 idiomas, los subtítulos se pueden revisar y previsualizar antes de publicar el vídeo.
<table>
<td>
   <a href="/help/assets/dynamic-media/imaging-faq.md">
   <img alt="Imágenes inteligentes" src="./assets/smart-imaging.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/imaging-faq.md">
      <strong>imágenes inteligentes</strong>
      </a>
   </div>
   <p>
      <em>Optimice el formato y el tamaño de archivo de una imagen en función de la capacidad del explorador y la velocidad de red del usuario.</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video">
   <img alt="Recorte inteligente" src="./assets/smart-cropping.jpg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video">
      <strong>Recorte inteligente</strong>
      </a>
   </div>
   <p>
      <em>Use la IA para detectar automáticamente el punto focal en cualquier imagen o vídeo y aplicar el recorte para mantenerlo</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/video.md">
   <img alt="Subtítulos de vídeo generados por IA" src="./assets/videos-with-captions.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/video.md">
      <strong>Subtítulos de vídeo generados por IA</strong>
      </a>
   </div>
   <p>
      <em>Use la inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. </em>
   </p>
</td>
</table>

>[!TAB Descubrimiento]

## Detección de recursos {#asset-discovery}

Después de importar los recursos a AEM Assets, el reto consiste en encontrar rápidamente los recursos adecuados entre una colección tan grande.

AEM Assets proporciona funciones que le ayudan a encontrar rápidamente el recurso adecuado. Estas funciones incluyen etiquetado generado por IA (etiquetas inteligentes), metadatos personalizados y funciones de búsqueda mejoradas.

**Administración de metadatos**: los metadatos son el aspecto más crítico a la hora de iniciar el recorrido de administración de recursos. La administración de metadatos queda completamente fuera del control de los administradores una vez que los recursos se distribuyen a los usuarios. Los metadatos de recursos efectivos garantizan una mejor búsqueda, que es el destino final de cualquier herramienta DAM.


**Formularios de metadatos**: Assets as a Cloud Service proporciona muchos campos de metadatos estándar de forma predeterminada. Si tiene necesidades de metadatos adicionales y necesita más campos de metadatos para añadir metadatos específicos de la empresa. Los formularios de metadatos permiten a las empresas añadir campos de metadatos personalizados a la página Detalles de un recurso. Los metadatos específicos de la empresa mejoran el control y el descubrimiento de sus recursos. Puede crear formularios desde cero o reutilizar uno existente.

<table>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="Administración de metadatos en la vista Recursos" src="./assets/manage-metadata-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>Administración de metadatos en la vista Recursos</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a administrar metadatos y formularios de metadatos mediante la vista Recursos.</em>
   </p>
</td>


<td>
   <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298?profile.language=es">
   <img alt="Prácticas recomendadas de administración de metadatos" src="./assets/metadata-best-practices.jpeg" />
   </a>
   <div>
      <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298?profile.language=es">
      <strong>Prácticas recomendadas de administración de metadatos</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a administrar metadatos antes y después de migrar los recursos a AEM.</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-metadata.md">
   <img alt="Uso de Adobe Asset Link" src="./assets/metadata-management-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-metadata.md">
      <strong>Administración de metadatos en la vista Administración</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a administrar los metadatos y los formularios de metadatos mediante la vista Administración.</em>
   </p>
</td>
</table>

**Etiquetas inteligentes**: Las etiquetas inteligentes utilizan el marco de trabajo artificialmente inteligente de Adobe AI para entrenar su algoritmo de reconocimiento de imágenes en la estructura de etiquetas y la taxonomía empresarial. A continuación, esta inteligencia de contenido se utiliza para aplicar las etiquetas relevantes a un conjunto diferente de recursos. De forma predeterminada, AEM aplica etiquetas inteligentes a los recursos cargados.

**Buscar recursos**: una vez que disponga de los metadatos adecuados, AEM Assets permitirá realizar búsquedas mediante varios operadores, caracteres comodín, consultas avanzadas y filtros personalizados.

**Búsqueda contextual**: AEM Assets también proporciona la funcionalidad Búsqueda contextual, que permite buscar recursos disponibles en el repositorio mediante la definición de mensajes de texto. Experience Manager Assets transforma automáticamente esas indicaciones de texto en filtros de búsqueda y muestra los resultados de la búsqueda. Puede ver y modificar los filtros automáticos mediante el panel Filtros para delimitar aún más los resultados de la búsqueda.

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="Etiquetas inteligentes en AEM Assets" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong>Incorporación de etiquetas inteligentes a recursos</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a aplicar etiquetas inteligentes automáticamente a los recursos cargados.</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md">
   <img alt="Vista Buscar recursos" src="./assets/search-assets-view-landing.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md">
      <strong>Búsqueda de recursos en la vista Recursos</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a utilizar de forma eficaz la función Búsqueda contextual y otras funciones de búsqueda en la vista Recursos.</em>
   </p>
</td>
<td>
   <a href="/help/assets/search-best-practices.md">
   <img alt="Prácticas recomendadas de búsqueda" src="./assets/search-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-best-practices.md">
      <strong>Prácticas recomendadas de búsqueda</strong>
      </a>
   </div>
   <p>
      <em>Obtenga información acerca de diversos escenarios para ayudar a los usuarios de AEM a realizar búsquedas de nivel básico a avanzado.</em>
   </p>
</td>
</table>

>[!TAB Gobernanza]

## Administración y control de recursos {#asset-management-governance}

Una vez que haya cargado los recursos a AEM Assets y haya establecido sus metadatos para mejorar la capacidad de detección, puede realizar varias tareas de administración de recursos digitales mediante la sencilla interfaz de usuario de la vista Recursos.

**Tareas de administración de recursos**: algunas de las tareas básicas incluyen operaciones de búsqueda, descarga, movimiento, copia, cambio de nombre, eliminación, actualización y edición.

También puede mantener versiones del recurso, establecer el estado del recurso y establecer la caducidad del recurso.

**Mi espacio de trabajo**: la vista Recursos también incluye un espacio de trabajo personalizable que proporciona widgets. Estos widgets ofrecen un práctico acceso a las áreas clave de la interfaz de usuario de Assets y a la información que le es más relevante. Esta página sirve como solución integral para proporcionar información general sobre los elementos de trabajo y un acceso rápido a los flujos de trabajo clave.

**Credenciales de contenido**: otra versátil característica que AEM Assets admite es Credenciales de contenido. Las marcas están más preocupadas que nunca por la transparencia del contenido, la divulgación de la inteligencia artificial y la prevención de la manipulación de activos. Content Authenticity Initiative (CAI) de Adobe crea herramientas compatibles con el estándar técnico Content Provenance and Authenticity (C2PA) (C2PA). Credenciales de contenido, un nuevo tipo de metadatos cifrados y a prueba de manipulaciones, puede ayudar a los visores a comprender el linaje del contenido y garantizar la integridad de los activos de la marca. Pueden incluir una amplia gama de datos de procedencia que ofrecen información del historial de un recurso digital.

<table>
<td>
   <a href="/help/assets/manage-organize-assets-view.md">
   <img alt="Tareas de administración de recursos" src="./assets/asset-management.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-organize-assets-view.md">
      <strong>Tareas de administración de recursos</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a realizar algunas tareas básicas y avanzadas de administración de recursos.</em>
   </p>
</td>

<td>
   <a href="/help/assets/my-workspace-assets-view.md">
   <img alt="Mi espacio de trabajo" src="./assets/my-workspace.jpeg" />
   </a>
   <div>
      <a href="/help/assets/my-workspace-assets-view.md">
      <strong>Mi espacio de trabajo</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a trabajar con Mi espacio de trabajo para acceder rápidamente a áreas clave de la interfaz de usuario de Assets.</em>
   </p>
</td>
<td>
   <a href="/help/assets/content-credentials.md">
   <img alt="Content Credentials" src="./assets/content-credentials.jpeg" />
   </a>
   <div>
      <a href="/help/assets/content-credentials.md">
      <strong>Credenciales de contenido</strong>
      </a>
   </div>
   <p>
      <em>Obtenga información sobre el historial de un recurso digital mediante las credenciales de contenido.</em>
   </p>
</td>
</table>

**Colecciones**: AEM Assets también le permite organizar sus recursos en colecciones. Una colección es un conjunto de recursos, carpetas u otras colecciones dentro de la vista Recursos de Adobe Experience Manager. Utilice las colecciones para compartir recursos entre los usuarios. A diferencia de las carpetas, una colección puede incluir recursos de distintas ubicaciones. Puede compartir varias colecciones con un usuario. Cada colección contiene referencias a recursos. La integridad referencial de los recursos se mantiene entre colecciones.

**Notificaciones**: la vista Recursos le permite monitorizar las operaciones realizadas en los recursos, carpetas o colecciones disponibles en el repositorio. Debe seleccionar y suscribirse al contenido para el que se le envían las notificaciones. También puede configurar las categorías a las que se envían las notificaciones.

**Detectar recursos duplicados**: AEM Assets también permite detectar recursos duplicados. Si un usuario de DAM carga uno o más recursos que ya existen en el repositorio, Experience Manager detecta la duplicación y se lo comunica al usuario.



<table>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="Administrar colecciones" src="./assets/manage-collections.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong>Administrar colecciones</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a organizar sus recursos en colecciones para compartir recursos de forma eficaz.</em>
   </p>
</td>


<td>
   <a href="/help/assets/manage-notifications-assets-view.md">
   <img alt="Establecer notificaciones" src="./assets/manage-notifications.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong>Establecer notificaciones</strong>
      </a>
   </div>
   <p>
      <em>Obtenga información sobre cómo establecer notificaciones para monitorizar las operaciones realizadas en recursos, carpetas o colecciones.</em>
   </p>
</td>
<td>
   <a href="/help/assets/detect-duplicate-assets.md">
   <img alt="Detección de recursos duplicados" src="./assets/duplicate-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/detect-duplicate-assets.md">
      <strong>Detección de recursos duplicados</strong>
      </a>
   </div>
   <p>
      <em>Detecte los recursos duplicados cargados en AEM Assets y notifíqueselo a los usuarios.</em>
   </p>
</td>
</table>

>[!TAB Integraciones]

## Integración con aplicaciones de Adobe y que no son de Adobe {#integration-adobe-non-adode-apps}

AEM Assets se puede integrar sin problemas con varias aplicaciones de Adobe y que no sean de Adobe. A continuación se ofrece una vista resumida de las integraciones disponibles:

+++**Integración con aplicaciones de Adobe y que no son de Adobe**

* **Dynamic Media con funciones de OpenAPI**: [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) ofrece un conjunto completo de API de [búsqueda](/help/assets/search-assets-api.md) y [envío](/help/assets/deliver-assets-apis.md). Permite a los desarrolladores integrar fácilmente el envío de recursos con sus aplicaciones. Las aplicaciones incluyen aplicaciones de Adobe y también de terceros. Proporciona una interfaz de usuario del selector de recursos Micro-Frontend para buscar y seleccionar los recursos aprobados. El selector se puede integrar fácilmente con cualquier aplicación basada en marcos de trabajo de JavaScript como React JS, Angular JS y Vanilla JS.

* **Selector de recursos de Micro-Frontend**: el selector de recursos de Micro-Frontend proporciona una interfaz de usuario que se integra con el repositorio de Experience Manager Assets para que pueda examinar o buscar los recursos digitales disponibles en el repositorio. A continuación, puede utilizarlos en la experiencia de creación de la aplicación.
Puede integrar el selector de recursos con una aplicación de Adobe o que no sea de Adobe.

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="Información general sobre Dynamic Media con funciones de OpenAPI" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>Información general sobre Dynamic Media con funciones de OpenAPI</strong>
      </a>
   </div>
   <p>
      <em>Conozca las ventajas clave y cómo habilitarlo. </em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Restringir el acceso a los recursos en Experience Manager" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Restringir el acceso a los recursos de Experience Manager</strong>
      </a>
   </div>
   <p>
      <em> Configurar funciones para restringir el acceso a los recursos aprobados.</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="Selector de recursos" src="./assets/integration-asset-selector.jpeg" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong>Selector de recursos Micro-Frontend</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a integrar el Selector de recursos Micro-Frontend con una aplicación de Adobe o que no sea de Adobe.</em>
   </p>
</td>
</table>

+++

+++**Integración nativa con aplicaciones de Adobe**

* **Integración con Adobe Workfront**: [!DNL Adobe Workfront]es una aplicación de administración de trabajo que le ayuda a administrar todo el ciclo de vida del trabajo en un solo lugar. La integración nativa entre [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] permite a las organizaciones mejorar la velocidad del contenido y el tiempo de salida al mercado conectando intrínsecamente el trabajo con la administración de recursos. En el contexto de la administración de su trabajo en Workfront, los usuarios tienen acceso a los documentos e imágenes necesarios. 

  Adobe ofrece [integrar [!DNL Workfront] y [!DNL Adobe Experience Manager Assets] de forma nativa](https://experienceleague.adobe.com/es/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations).

* **Integración con Figma**:AEM Assets se integra de forma nativa con Figma, lo que permite a los diseñadores acceder directamente a los recursos almacenados en AEM Assets desde la propia interfaz de usuario de Figma. Puede colocar contenido administrado en AEM Assets en el lienzo Figma y, a continuación, guardar contenido nuevo o editado en un repositorio de AEM Assets. Para acceder al conector de AEM Assets disponible en la página de la comunidad Figma, haga clic [aquí](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector).

* **Integración nativa con Adobe Express**: AEM Assets se integra de forma nativa con Adobe Express, lo que le permite acceder directamente a los recursos almacenados en AEM Assets desde la interfaz de usuario de Adobe Express. Puede colocar contenido administrado en AEM Assets en el lienzo Express y, a continuación, guardar contenido nuevo o editado en un repositorio de AEM Assets.

* **Conectar AEM Assets a Creative Cloud**: Experience Manager Assets puede conectarse a una asignación de derechos de Creative Cloud aprovisionada en una organización IMS diferente. Esta capacidad le permite utilizar las integraciones de Creative Cloud más recientes en AEM Assets, incluidos Express y Creative Cloud Libraries. Si los productos de Creative Cloud y AEM Assets se suministran a organizaciones IMS independientes, puede conectarse a una organización de Creative Cloud diferente para poder ejecutar flujos de trabajo integrados entre las dos soluciones.

<table>
<td>
   <a href="/help/assets/workfront-integrations.md">
   <img alt="Integración con Adobe Workfront" src="./assets/integration-adobe-workfront.jpeg" />
   </a>
   <div>
      <a href="/help/assets/workfront-integrations.md">
      <strong>Integración con Adobe Workfront</strong>
      </a>
   </div>
   <p>
      <em>Intégrese con Adobe Workfront para administrar todo el ciclo de vida del trabajo en un solo lugar.</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="Integración con Figma" src="./assets/integration-commerce.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong>Integración con Figma</strong>
      </a>
   </div>
   <p>
      <em>Acceda a los recursos almacenados en AEM Assets desde la interfaz de usuario de Figma</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="Integración nativa con Adobe Express" src="./assets/integration-adobe-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>Integración nativa con Adobe Express</strong>
      </a>
   </div>
   <p>
      <em>Coloque los recursos disponibles en AEM Assets en el lienzo de Express y guarde los recursos actualizados en AEM. </em>
   </p>
</td>


</table>


* **Integración con Adobe Journey Optimizer**: combine los flujos de trabajo creativos y de marketing mediante Adobe Experience Manager Assets. Integrado de forma nativa con Adobe Journey Optimizer, acceda a Assets as a Cloud Service para almacenar, administrar, descubrir y distribuir recursos digitales. Proporciona un único repositorio centralizado de recursos que puede utilizar para rellenar los mensajes.

* **Integración con Commerce**: la integración de Adobe Experience Manager (AEM) Assets para Commerce combina las sólidas capacidades de AEM como un sistema de administración de recursos digitales (DAM) con Adobe Commerce para mejorar las experiencias de comercio electrónico. Estas funciones se ofrecen conectando los proyectos de Commerce al potente entorno de administración de recursos de AEM para proporcionar una forma sencilla, escalable y eficaz de administrar y distribuir recursos en las tiendas de comercio.
* **Integración de AEM Assets con flujos de creación basados en documentos para Edge Delivery Services**: cuando [!DNL AEM Assets] se integra con sus herramientas de creación basada en documentos, como [!DNL Microsoft Word] o [!DNL Google Docs], proporciona un selector de recursos en su herramienta de creación. Use este selector de recursos para acceder a [!DNL AEM Assets] e insertar recursos aprobados en el contenido.
Si ya tiene un sitio web de [!DNL Edge Delivery Services], consulte la documentación de [[!DNL AEM Assets] plugin](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md) para obtener información sobre cómo integrar [!DNL AEM Assets] con su proyecto de [!DNL AEM] existente.

* **Integración de [!DNL AEM Assets] con flujos de creación basados en el [!DNL Universal Editor] para[!DNL Edge Delivery Services]**: configure el [!DNL Universal Editor] para integrarlo con [!DNL AEM Assets]. Esta integración le permite usar [!DNL Dynamic Media with OpenAPI capabilities] para envíar recursos.

   * Consulte [Configuración en el  [!DNL Edge Delivery] sitio](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site) para obtener información sobre cómo añadir una función del selector de recursos personalizada en el [!DNL Universal Editor]. El selector de recursos personalizado le permite insertar recursos directamente en el contenido de [!DNL Universal Editor].
   * Consulte [Información general sobre la extensión](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) para obtener información sobre cómo acceder a [!DNL AEM Assets] e insertar los recursos durante la creación en [!DNL Universal Editor].

<table>
<td>
   <a href="https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/combine/assets">
   <img alt="Integración con Adobe Journey Optimizer" src="./assets/integration-figma.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/es/docs/journey-optimizer/using/content-management/combine/assets">
      <strong>Integración con Adobe Journey Optimizer</strong>
      </a>
   </div>
   <p>
      <em>Combinación de los flujos de trabajo creativos y de marketing mediante la integración con AJO</em>
   </p>
</td>
<td>
   <a href="https://experienceleague.adobe.com/es/docs/commerce/aem-assets-integration/overview">
   <img alt="Integración con Commerce" src="./assets/integration-ajo.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/es/docs/commerce/aem-assets-integration/overview">
      <strong>Integración con Commerce</strong>
      </a>
   </div>
   <p>
      <em>Integre AEM Assets con Commerce para mejorar las experiencias de comercio electrónico.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
   <img alt="Integración de AEM Assets con EDS" src="./assets/integrate-ue-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
      <strong>Integración de AEM Assets con EDS</strong>
      </a>

   </div>
   <p>
      <em>Integre AEM Assets con los flujos de creación basados en documentos y en el Editor universal.</em>
   </p>
</td>
</table>

+++

>[!TAB Agentes de IA]

## Agentes de IA {#ai-agents}

AEM as a Cloud Service proporciona **agentes** inteligentes para mejorar la administración, optimización y control del contenido. Estos agentes permiten a los usuarios descubrir contenido rápidamente, optimizar campañas y garantizar el cumplimiento de las normas en los recursos digitales.

**Agente de detección**

Discovery Agent ofrece contenido de AEM bajo demanda a través de mensajes naturales y conversacionales para una experiencia de detección optimizada y sin clics. Busca de forma inteligente en **Assets, fragmentos de contenido y Forms adaptable** para ofrecer contenido relevante, como imágenes, vídeos, PDF, artículos y plantillas de formulario. Con el lenguaje natural, puede buscar sin crear consultas complejas ni aplicar filtros en la interfaz de AEM Assets. En función de la solicitud, el agente devuelve resultados depurados junto con metadatos de recursos y direcciones URL de entrega, listos para incrustarse en otras aplicaciones.

Algunas de las ventajas clave de Discovery Agent son:

* **Detección de contenido unificado:** Acceda a todo tipo de contenido de AEM, como imágenes, vídeos, documentos de PDF, artículos y formularios, desde una sola interfaz de conversación.
* **Planificación de campañas más rápida:** recopile rápidamente imágenes y formularios para las campañas de marketing en los canales de correo electrónico, web y social.
* **Productividad mejorada:** Reduzca el tiempo empleado en explorar repositorios o filtrar metadatos mediante búsquedas automatizadas basadas en la intención.
* **Utilización coherente del contenido:** Garantiza la reutilización de los recursos y fragmentos aprobados, manteniendo la coherencia de la marca en todos los canales.

**Habilidades:** descubrimiento de contenido en lenguaje natural, descubrimiento de recursos basados en etiquetas, descubrimiento de contenido basado en carpetas, descubrimiento de recursos basados en formato y orientación\
**Personas:** Administradores de campañas, Especialistas en marketing de canal, Bibliotecarios de DAM, Agencias y socios\
**Acceso:** mediante el Asistente de IA en AEM

**Casos de uso comunes/Indicadores de ejemplo:**

* Mostrar imágenes etiquetadas como &quot;office&quot; en la carpeta WKND.
* Enumerar todos los fragmentos de contenido publicados para bebidas WKND.
* Busque formularios para solicitar un trabajo.
* Mostrar recursos con la persona en orientación horizontal.

**Agente de optimización de contenido**

El **Agente de optimización de contenido** ayuda a refinar y adaptar los recursos mediante mensajes en lenguaje natural. Puede generar nuevas representaciones, ajustar imágenes, cambiar fondos y crear variaciones listas para el canal automáticamente. Funciona con Discovery Agent y **Dynamic Media con OpenAPI** para una optimización perfecta.

**Ventajas principales:**

* **Transformación de recursos sin esfuerzo:** Cambiar el tamaño, enfocar, cambiar el color o reflejar imágenes.
* **Salidas optimizadas para canales:** Generar representaciones para Instagram, banners web y otros canales de marketing.
* **Mejoras de Creative a escala:** aplique cambios de fondo o superposiciones para flujos de trabajo de gran volumen.

**Acceso:** mediante el Asistente de IA en AEM.

**Indicadores de ejemplo:**

* Cree una representación de JPEG de 2000 px.
* Enfocar la imagen.
* Cambie el color de fondo a #ff8932.
* Crear una representación para una historia de Instagram.

**Limitaciones:** Algunas optimizaciones no son compatibles con los recursos PNG.

**Agente de control**

El agente de gobernanza ayuda a garantizar el cumplimiento, la coherencia de la marca y la aplicación de las políticas en todo el contenido de AEM. Identifica contenido que no cumple con los metadatos, la accesibilidad o las directrices corporativas.

Algunas de las ventajas clave de Governance Agent son:

* **Supervisión del cumplimiento:** Detecta infracciones de directivas en el contenido.
* **Aplicación de metadatos:** Garantiza que los recursos tengan los metadatos requeridos para el control.
* **Coherencia de la marca:** Indica contenido que no cumple con los estándares corporativos.

**Habilidades:** comprobaciones de cumplimiento de directivas, validación de metadatos, auditoría de accesibilidad, alertas automatizadas para infracciones\
**Personas:** administradores de DAM, funcionarios de cumplimiento, administradores de marcas\
**Acceso:** mediante el Asistente de IA de AEM

**Casos de uso comunes/Indicadores de ejemplo:**

* Valide los metadatos de todos los recursos de la carpeta WKND.
* Identificar los recursos que carecen de directrices de marca.
* Auditar el contenido publicado para comprobar el cumplimiento de la accesibilidad.

<table>
<td>
   <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/ai-in-aem/agents/discovery/overview">
   <img alt="Información general de Discovery Agent" src="./assets/discovery-agent.jpg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/ai-in-aem/agents/discovery/overview">
      <strong>Información general del agente de detección</strong>
      </a>
   </div>
   <p>
      <em>Información general sobre Discovery Agent y sus capacidades de detección de contenido conversacional.</em>
   </p>
</td>

<td>
   <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/ai-in-aem/agents/content-optimization/overview">
   <img alt="Resumen de optimización de contenido" src="./assets/content-optimization-agent.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/ai-in-aem/agents/content-optimization/overview">
      <strong>Información general del agente de optimización de contenido</strong>
      </a>
   </div>
   <p>
      <em>Información general sobre el agente de optimización de contenido y flujos de trabajo de optimización admitidos.</em>
   </p>
</td>

<td>
   <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/ai-in-aem/agents/governance/overview">
   <img alt="Introducción al agente de gobernanza" src="./assets/governance-agent-overview.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/ai-in-aem/agents/governance/overview">
      <strong>Información general del agente de administración</strong>
      </a>
   </div>
   <p>
      <em>Información general del agente de gobernanza para el cumplimiento y la aplicación de políticas.</em>
   </p>
</td>
</table>

### **Cómo acceder a agentes en AEM**

Se puede acceder a los agentes a través de **AI Assistant** en AEM Cloud Service. Inicie sesión en [experience.adobe.com](https://experience.adobe.com/) e interactúe con el asistente de IA utilizando indicaciones en lenguaje natural.

>[!TAB Activación]

## Activación de recursos {#asset-activation}

Aproveche todo el potencial de sus recursos digitales con AEM Assets utilizando el centro de contenido para usar medios dinámicos, incluidas las potentes funciones de OpenAPI. AEM Assets ofrece un conjunto completo de soluciones diseñadas para optimizar la transformación de recursos y el envío a través de diversos canales.

+++**Centro de contenido**

Centro de contenido está disponible como parte de Experience Manager Assets as a Cloud Service para democratizar el acceso al contenido sobre la marca por parte de las organizaciones y sus socios comerciales. Se centra en la distribución de recursos para su activación a escala y la creación de variantes de contenido de la marca para mejorar la agilidad comercial.

Content Hub ofrece las siguientes ventajas clave:

* **Busque y comparta todos los recursos aprobados por la marca disponibles en un portal intuitivo**: AEM Assets constituye una única fuente de confianza y todos los recursos aprobados están disponibles automáticamente en Content Hub en una jerarquía plana para mejorar la experiencia de búsqueda.

* **Interfaz de usuario configurable**: se pueden configurar las propiedades más comunes de Content Hub, como los filtros para la búsqueda, los campos disponibles al añadir o importar recursos, las propiedades de recursos, el contenido del titular para la promoción de la marca y un administrador puede configurar fácilmente la interfaz de usuario de Content Hub según sus necesidades.

* **Habilite a los no creativos para editar y versionar contenido sin desviarse de la marca**: Content Hub le permite crear contenido nuevo con Adobe Express (si tiene derechos para Adobe Express). Puede editar el contenido existente con herramientas fáciles de usar, producir variaciones alineadas con la marca con plantillas y elementos de marca, y crear contenido nuevo con las últimas funciones de IA generativa de Adobe Firefly.

* **Obtenga información valiosa sobre cómo se utiliza el contenido en los distintos equipos**: [!DNL Content Hub] proporciona información valiosa sobre los recursos, abordando un reto común al que se enfrentan a menudo los responsables de marketing: las estadísticas de uso de los recursos que se utilizan en campañas de marketing, canales y diferentes regiones. Al obtener una comprensión clara del rendimiento y la popularidad de los recursos, proporciona información útil esencial para mejorar la experiencia del usuario.

<table>
<td>
   <a href="/help/assets/product-overview.md">
   <img alt="Información general sobre Content Hub" src="./assets/content-hub-overview.jpeg" />
   </a>
   <div>
      <a href="/help/assets/product-overview.md">
      <strong>Información general sobre Content Hub</strong>
      </a>      
   </div>
   <p>
      <em>Obtenga más información sobre Content Hub, sus ventajas clave y cómo acceder a él. </em>
   </p>
</td>


<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="Configuración de la interfaz de usuario de Content Hub" src="./assets/content-hub-configuration.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
     <strong>Configuración de la interfaz de usuario de Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Obtenga información sobre cómo configurar las opciones disponibles en la interfaz de usuario de Content Hub.</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="Edición mediante Adobe Express" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>Edición mediante Adobe Express</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a editar imágenes en Content Hub mediante Adobe Express.</em>
   </p>
</td>
</table>

+++

+++**Dynamic Media**

Dynamic Media le ayuda a ofrecer recursos de marketing y comercialización visuales enriquecidos bajo demanda. También le ayuda a crear y ofrecer experiencias de visualización interactivas, como zoom, giro de 360 grados y vídeo. Los recursos se escalan dinámicamente para su consumo en sitios web, móviles y redes sociales. Mediante un conjunto principal de recursos de origen, como imágenes, vídeo y 3D, Dynamic Media genera y ofrece varias variaciones de este contenido enriquecido, en tiempo real a través de su CDN (red de distribución de contenido) global, escalable y optimizada para el rendimiento.

Dynamic Media ofrece las siguientes funciones clave:

* **Imágenes inteligentes**: las imágenes inteligentes ofrecen un rendimiento del envío de recursos de la imagen aún mejor ya que optimizan automáticamente el formato y el tamaño de archivo de una imagen en función de la capacidad del explorador del cliente. Funciona con los ajustes preestablecidos de imagen existentes y utiliza inteligencia en el envío. Esta inteligencia reduce aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red y del explorador.

* **Conjuntos de vídeos adaptables**: un conjunto de vídeos adaptables agrupa versiones del mismo vídeo que se codifican con diferentes formatos y velocidades de bits. Empiece con el vídeo original principal, que cargue en el sistema. Dynamic Media cambia automáticamente el tamaño de ese vídeo o lo transcodifica en varios vídeos. A continuación, en el momento del envío, determina de forma inteligente qué pantalla de vídeo, qué calidad y qué formato utilizar, y la envía al teléfono, a la tableta o al equipo del escritorio.

* **Recorte inteligente**: una función de Adobe AI que detecta automáticamente el punto focal de cualquier imagen o vídeo, y recorta para mantenerlo. Captura el punto de interés deseado independientemente del tamaño de la pantalla y, por lo tanto, elimina las tareas manuales tediosas, y ofrece imágenes y vídeo de alta calidad y carga rápida que se ven bien en cualquier dispositivo o pantalla.

* **Plantillas de Dynamic Media**: cree plantillas personalizables en tiempo real para sus titulares y prospectos con plantillas de Dynamic Media, un editor de plantillas de WYSIWYG. Publique la plantilla de Dynamic Media y utilícela en aplicaciones posteriores. Una plantilla de Dynamic Media incluye capas de imagen y texto. Añada parámetros a las capas de imagen y texto de la plantilla y utilice URL de Dynamic Media para cambiar la posición y el tamaño de la capa y actualizar su contenido en tiempo real.

* **Subtítulos y audio múltiples**: añada varios subtítulos y pistas de audio a un vídeo principal. Esta capacidad significa que los vídeos son accesibles para un público global. Puede personalizar un solo vídeo principal publicado para un público global en varios idiomas y seguir las directrices de accesibilidad para diferentes regiones geográficas. Los autores también pueden administrar los subtítulos y las pistas de audio desde una sola pestaña en la interfaz de usuario.

* **Compatibilidad con el protocolo DASH (Dynamic Adaptive Streaming over HTTP)**: Dynamic Media admite el streaming adaptable en el envío de vídeos de Dynamic Media (con CMAF habilitado), lo que garantiza una mejor experiencia de visualización de vídeos para el usuario. DASH es el protocolo estándar internacional para el streaming de vídeo adaptable y es ampliamente adoptado en el sector.

* **Subtítulos de vídeo generados por IA**: los subtítulos de vídeo generados por IA en Adobe Dynamic Media utilizan la inteligencia artificial para generar subtítulos automáticamente para el contenido de vídeo. Con compatibilidad con más de 60 idiomas, los subtítulos se pueden revisar y previsualizar antes de publicar el vídeo.

Para obtener información sobre las ofertas de Dynamic Media disponibles, consulte [Dynamic Media Prime y Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).



<table>
<td>
   <a href="/help/assets/dynamic-media/dynamic-media.md">
   <img alt="Trabajar con Dynamic Media" src="./assets/work-with-dynamic-media.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dynamic-media.md">
      <strong>Trabajo con Dynamic Media</strong>
      </a>
   </div>
   <p>
      <em>Aprenda a entregar recursos para su consumo en sitios web, móviles y sociales. </em>
   </p>
</td>


<td>
   <a href="/help/assets/dynamic-media/dm-journey-part1.md">
   <img alt="Recorrido por Dynamic Media" src="./assets/dm-journey.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-journey-part1.md">
      <strong>Recorrido por Dynamic Media</strong>
      </a>
   </div>
   <p>
      <em>Aprenda cómo Dynamic Media aporta valor al trabajo.</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/dm-best-practices.md">
   <img alt="Conectar AEM Assets a Creative Cloud" src="./assets/dm-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-best-practices.md">
      <strong>Prácticas recomendadas de Dynamic Media</strong>
      </a>
   </div>
   <p>
      <em>Prácticas recomendadas al trabajar con imágenes, vídeos y visores.</em>
   </p>
</td>
</table>

+++

+++**Dynamic Media con funciones de OpenAPI**

En el vertiginoso mundo digital actual, aprovechar todo el potencial de los recursos digitales de su marca es crucial para ir un paso por delante de la competencia. Una solución integral de administración de recursos digitales (DAM) facilita la gobernanza de los recursos, promueve la uniformidad de la marca y acelera la entrega de contenido, al tiempo que garantiza la integridad de la marca y una experiencia excepcional para el cliente.

Dynamic Media con funciones de OpenAPI coloca a DAM en el centro de un ecosistema de cadena de suministro de contenido ágil y eficiente para garantizar la gobernanza y la entrega de los recursos.

Dynamic Media con funciones de OpenAPI ofrece las siguientes ventajas clave:

* **Integraciones perfectas**: Dynamic Media con funciones de OpenAPI ofrece un conjunto completo de API de búsqueda y entrega. Permite a los desarrolladores [integrar fácilmente la entrega de recursos con sus aplicaciones](/help/assets/integrate-dynamic-media-open-apis.md). Las aplicaciones incluyen aplicaciones de Adobe y también de terceros. Proporciona una [interfaz de usuario del Selector de recursos de Micro-Frontend](/help/assets/overview-asset-selector.md) para buscar y seleccionar recursos aprobados. El selector se puede integrar fácilmente con cualquier aplicación basada en marcos de trabajo de JavaScript como React JS, Angular JS y Vanilla JS.

* **Administración centralizada de recursos digitales**: DAM es la única fuente de confianza para todos los recursos digitales. Los recursos digitales se administran de forma centralizada en AEM Assets y se entregan a las aplicaciones consumidoras por referencia mediante direcciones URL de entrega, sin copiar los binarios de recursos.

* **Actualizaciones en tiempo real**: cualquier cambio realizado en los recursos aprobados en DAM, incluidas las actualizaciones de la versión y las modificaciones de metadatos, se refleja automáticamente en las direcciones URL de entrega. Con un valor corto de tiempo de vida (TTL) de 10 minutos configurado para Dynamic Media con funciones de OpenAPI a través de CDN, las actualizaciones se pueden ver en todas las interfaces de creación y publicación en menos de 10 minutos.

* **Uniformidad de la marca**: solo [los recursos de marca aprobados](/help/assets/approve-assets.md) están expuestos a aplicaciones descendentes. [Los directores de marcas y los especialistas en marketing mantienen un control estricto sobre los recursos de la marca](/help/assets/restrict-assets-delivery.md). La versión más reciente aprobada del recurso es la única disponible para su uso, lo que garantiza la coherencia de marca en todos los canales y aplicaciones.

* **Entrega optimizada para la web**: los recursos digitales se entregan en formatos optimizados para la web a fin de mejorar los elementos vitales principales de las experiencias digitales. Esta optimización incluye la compatibilidad con representaciones WebP para imágenes, streaming adaptable a través de protocolos HLS o DASH para vídeos, y representaciones originales para documentos.

* **Transformación dinámica de recursos**: el sistema permite la transformación de imágenes sobre la marcha mediante parámetros de URL conocidos como modificadores de imagen. [Por ejemplo, anchura, altura, girar, voltear, calidad, recorte, formato y recorte inteligente](/help/assets/deliver-assets-apis.md). Las representaciones transformadas se generan dinámicamente y se entregan sin problemas a través de la CDN.

* **Entrega segura de recursos**: Dynamic Media con funciones de OpenAPI proporciona un mecanismo para controlar el acceso a sus recursos digitales. Puede especificar roles de usuario o grupos como metadatos para los recursos que se van a proteger y establecer un intervalo de tiempo predefinido durante el cual [solo los usuarios autorizados puedan acceder a estos recursos](/help/assets/restrict-assets-delivery.md). Las URL de entrega de los recursos protegidos no se resuelven para los usuarios no autorizados durante el período restringido.

Para obtener información sobre las ofertas de Dynamic Media disponibles, consulte [Dynamic Media Prime y Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="Información general sobre Dynamic Media con funciones de OpenAPI" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong>Información general sobre Dynamic Media con funciones de OpenAPI</strong>
      </a>
   </div>
   <p>
      <em>Conozca las ventajas clave y cómo habilitarlo. </em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Restringir el acceso a los recursos en Experience Manager" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Restringir el acceso a los recursos de Experience Manager</strong>
      </a>
   </div>
   <p>
      <em> Configure funciones para restringir el acceso a los recursos aprobados.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="Integración de AEM Assets remoto con AEM Sites" src="./assets/integration-aem-sites.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong>Integración de AEM Assets remoto con AEM Sites</strong>
      </a>
   </div>
   <p>
      <em>Integración de AEM Assets remoto con el entorno de AEM Sites. </em>
   </p>
</td>
</table>

+++

>[!TAB Perspectivas]

## Perspectivas de recursos {#asset-insights}

La creación de informes de recursos proporciona a los administradores visibilidad de la actividad del entorno de la vista Recursos de Adobe Experience Manager. Estos datos proporcionan información útil sobre cómo los usuarios interactúan con el contenido y el producto. Cualquier persona usuaria puede acceder al panel de control de Insights. Además, las personas asignadas al perfil de producto del administrador pueden crear informes definidos por el usuario.

Puede generar varios tipos de informes, como Cargar, Descargar y Entrega de Dynamic Media.

* **Información en la vista Recursos**: la vista Recursos le permite ver datos en tiempo real de su entorno de la vista Recursos con el panel de control de información. Puede ver las métricas de eventos en tiempo real durante los últimos 30 días o 12 meses. Los eventos incluyen Descargas, Cargas, Uso del almacenamiento, Búsquedas principales, Número de recursos por tamaño y Número de recursos por tipo de recurso.

* **Integración de Adobe Analytics en la vista de administrador**: la funcionalidad de la información sobre los recursos le permite realizar un seguimiento de las valoraciones de los usuarios y las estadísticas de uso de las imágenes que se utilizan en sitios web de terceros, campañas de marketing y soluciones creativas de Adobe. Ayuda a obtener información sobre el rendimiento y la popularidad de las imágenes. La información sobre los recursos captura los detalles de la actividad del usuario, como el número de veces que se clasifica una imagen, se hace clic en ella y las impresiones (el número de veces que se carga una imagen en el sitio web). Asigna puntuaciones a las imágenes en función de estas estadísticas. Puede utilizar las puntuaciones y las estadísticas de rendimiento para seleccionar imágenes populares para incluirlas en catálogos, campañas de marketing, etc. Incluso puede formular políticas de archivado y renovación de licencias basadas en estas estadísticas. Para permitir que la información de los recursos muestre las estadísticas de uso de los recursos, configure primero la función para recuperar los datos de informes de Adobe Analytics.

* **Información de Content Hub** Content Hub proporciona información valiosa sobre los recursos, abordando un reto común con el que se encuentran a menudo los profesionales del marketing: las estadísticas de uso de los recursos utilizados en las campañas de marketing, los canales y las distintas regiones. Al obtener una comprensión clara del rendimiento y la popularidad de los recursos, proporciona información útil esencial para mejorar la experiencia del usuario.

<table>
<td>
   <a href="/help/assets/manage-reports-assets-view.md">
   <img alt="Administración de informes en la vista Recursos" src="./assets/assets-insights-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-reports-assets-view.md">
      <strong>Administración de informes en la vista Recursos</strong>
      </a>
   </div>
   <p>
      <em>Obtenga información sobre las métricas de éxito clave usando la vista Recursos. </em>
   </p>
</td>


<td>
   <a href="/help/assets/asset-reports.md">
   <img alt="Administración de informes en la vista del administrador" src="./assets/assets-insights-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/asset-reports.md">
      <strong>Administración de informes en la vista del administrador</strong>
      </a>
   </div>
   <p>
      <em>Obtenga información sobre cómo administrar los informes integrados de Adobe Analytics en la vista del administrador.</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="Información sobre los recursos en Content Hub" src="./assets/asset-insights-content-hub.jpeg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong>Información sobre los recursos en Content Hub</strong>
      </a>
   </div>
   <p>
      <em>Obtenga información sobre cómo ver la información de los recursos en Content Hub.</em>
   </p>
</td>
</table>

>[!ENDTABS]

## Experiencias basadas en los grupos de usuarios disponibles para la administración de activos digitales {#persona-based-experiences}

Adobe ofrece una solución sólida de soluciones de administración de recursos digitales (DAM) para que pueda sacar el máximo partido de sus recursos digitales. Adobe Experience Manager Assets tiene dos experiencias independientes que utilizan el mismo repositorio de Cloud Services:

* **Vista de administrador**: la interfaz de usuario as a Cloud Service de Assets existente. Utilice la Vista del administrador para todas las funciones avanzadas de administración de recursos digitales, entre ellas las integraciones, los flujos de trabajo, la automatización de contenido, la publicación y mucho más.

* **Vista de recursos**: la experiencia de administración de recursos ligera de Adobe para almacenar, administrar, descubrir y utilizar recursos digitales. Interfaz de usuario optimizada que contiene funciones esenciales de administración de activos digitales. Diseñada para los usuarios de DAM ligeros con un enfoque en la carga, administración de metadatos, búsqueda, descarga y uso compartido.

![add-tags](assets/newui-overview.svg)

Los usuarios con acceso a la vista del administrador también pueden acceder a la vista Recursos. La vista de recursos proporciona una interfaz de usuario simplificada que facilita la administración, la detección y la distribución de sus recursos digitales. Un amplio conjunto de usuarios de diferentes funciones, incluidos los equipos creativos, de marketing y de línea de negocios, pueden colaborar en los recursos y acceder a los recursos adecuados y aprobados cuando y donde los necesiten. Muchos usuarios ocasionales de DAM prefieren la vista Recursos porque solo contiene un subconjunto de funciones. La experiencia está dirigida a creativos, consumidores de recursos de solo lectura y usuarios de DAM de menor peso.

Los bibliotecarios, desarrolladores y superusuarios de DAM pueden seguir utilizando la vista de administrador o cambiar entre las interfaces de usuario, según sea necesario. Puede seleccionar la experiencia que mejor se adapte a su función.

Para obtener información sobre cómo acceder a la vista Recursos y algunas de las simplificaciones que ofrece a través de la vista del administrador, consulte [Introducción a la vista de recursos](/help/assets/assets-view-introduction.md).

## Asistente de IA en AEM

Para los clientes que han [completado los criterios de requisitos previos](/help/implementing/cloud-manager/ai-assistant-in-aem.md#get-access), el Asistente de IA en AEM está disponible para los usuarios de su organización. Consulte [Asistente de IA en AEM](/help/implementing/cloud-manager/ai-assistant-in-aem.md).
