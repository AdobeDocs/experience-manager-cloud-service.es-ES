---
title: Propiedades de página
description: Obtenga información acerca de las diferentes propiedades que puede tener una página y cómo controlan su comportamiento y cómo se administra.
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
solution: Experience Manager Sites
feature: Authoring
role: User
mini-toc-levels: 2
source-git-commit: b9328a22ff544f2c663868d33d7b06e02819f1d7
workflow-type: tm+mt
source-wordcount: '2138'
ht-degree: 33%

---


# Propiedades de página {#page-properties}

Obtenga información acerca de las diferentes propiedades que puede tener una página y cómo controlan su comportamiento y cómo se administra.

>[!TIP]
>
>Para obtener más información sobre cómo editar y cambiar las propiedades de una página, consulte el documento [Edición de propiedades de página.](/help/sites-cloud/authoring/sites-console/edit-page-properties.md)

## Información general y disponibilidad de propiedades {#overview}

Las propiedades de página pueden controlar muchos aspectos de una página, desde el título y la marca de la página hasta sus permisos. Las propiedades se distribuyen entre varias pestañas, algunas de las cuales pueden estar ocultas según el tipo de página. Al igual que la mayoría de las propiedades de AEM, [las propiedades de página se pueden heredar.](/help/sites-cloud/authoring/sites-console/edit-page-properties.md#inheritance)

>[!NOTE]
>
>Este documento describe todas las propiedades de página posibles. Según el tipo de página, no todas las propiedades estarán disponibles.

## Pestaña Básicos {#basic}

### Título y etiquetas {#title-tags}

* **Título**: define el metatítulo de la página para fines de SEO, así como el título mostrado en el contenido de la página (a menos que se anule)
   * El título de la página se muestra en varias ubicaciones de la interfaz de usuario de AEM, incluidas las vistas de lista o tarjeta **Sitios** de la consola [Sitios](/help/sites-cloud/authoring/sites-console/introduction.md).
   * Este es un campo obligatorio.
* **Etiquetas**: define las metaetiquetas de la página para fines de SEO
   * Puede agregar o quitar etiquetas de la página al actualizar la lista en el cuadro de diálogo de selección.
   * Utilice la lista desplegable para seleccionar entre las etiquetas existentes.
   * Después de seleccionar una etiqueta, aparece debajo del cuadro de selección. Puede quitar una etiqueta de esta lista utilizando la x.
   * Se puede especificar una etiqueta completamente nueva si se escribe el nombre en un cuadro de selección vacío.
      * La etiqueta nueva se crea al pulsar Intro.
      * La nueva etiqueta se mostrará con una pequeña estrella a la derecha que indicará que es una etiqueta nueva.
   * Aparece una x cuando pasa el ratón sobre una entrada de etiqueta en el cuadro de selección, que se puede utilizar para quitar esa etiqueta para esa página.
   * Para obtener más información sobre las etiquetas, vea [Usar la etiqueta.](/help/sites-cloud/authoring/sites-console/tags.md)
* **Ocultar en navegación**: indica si se muestra o se oculta la página en la navegación por páginas del sitio resultante

### Personalización de marca {#branding}

Aplique una identidad de marca uniforme en todas las páginas adjuntando un slug de marca al título de cada página. Esta funcionalidad requiere el uso del componente de página de la versión 2.14.0 o posterior de los [Componentes principales.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)

* **Anotaciones de marca**
   * **Sobrescribir**: marque para definir el slug de marca en esta página.
      * El valor lo hereda cualquier página secundaria a menos que también tenga valores establecidos de **Sobrescribir**.
   * **Sobrescribir valor**: el texto del slug de marca que se añadirá al título de la página.
      * El valor se anexa al título de la página después de un carácter de barra vertical como `Cycling Tuscany | Always ready for the WKND`

### ID HTML {#html-id}

* **ID**: ID de HTML que se aplicará al componente.

### Más títulos y descripciones {#more-titles}

* **Título de página**: un título que se usará en la página
   * Normalmente, lo utilizan los componentes de título.
   * Si está vacío, se utiliza **Título**.
* **Título de navegación**: puede especificar un título independiente para utilizarlo en la navegación (por ejemplo, si desea algo más conciso).
   * Si está vacío, se usa **Page Title**.
* **Subtítulo**: un subtítulo para usar en la página
* **Descripción**: la descripción de la página, su propósito o cualquier otro detalle que desee agregar

### Tiempo de activación/desactivación {#on-off-time}

El tiempo de activación/desactivación de una página es una forma cómoda de ocultar temporalmente contenido que ya se ha publicado. El contenido permanece en la instancia de publicación cuando está desactivado. Desactivar una página no cancela la publicación del contenido.

* **Tiempo de activación**: la fecha y hora a las que se hace visible (procesada) la página publicada en el entorno de publicación. La página debe publicarse, ya sea de forma manual o mediante replicación automática preconfigurada.

   * Si ya se ha [publicado,](/help/sites-cloud/authoring/sites-console/publishing-pages.md) esta página está disponible en la instancia de publicación, pero se mantiene inactiva (oculta) hasta que se procese a la hora especificada.
   * Si no se publica y se configura [para la replicación automática](/help/operations/replication.md#on-and-off-times-trigger-configuratio), la página se publicará automáticamente y, a continuación, se procesará a la hora especificada.
   * Si no se publica y no se configura para la replicación automática, la página no se publica automáticamente, por lo que se ve un error 404 al intentar acceder a la página.

* **Tiempo de desactivación**: similar a **Tiempo de activación** y usado a menudo en combinación, define el momento en el que la página publicada se oculta en el entorno de publicación.

Deje estos campos (**Tiempo de activación** y **Tiempo de inactividad**) vacíos para las páginas que desee publicar y disponibles de inmediato y disponibles en el entorno de publicación hasta que se desactiven (el escenario normal).

>[!NOTE]
>Si el **Tiempo de activación** o el **Tiempo de desactivación** se sitúan en el pasado y se configura la replicación automática, la acción relevante se activa de inmediato.

>[!TIP]
>
>Los tiempos de activación/desactivación tratan estrictamente el contenido que ya se ha publicado (ya sea de forma manual o mediante replicación automática). Por este motivo, los flujos de trabajo de publicación, como los de aprobación de contenido, no se activan por los tiempos de activación/desactivación y los tiempos de activación/desactivación no afectan al estado de publicación de la página. Por este motivo, los momentos de activación y desactivación son los más adecuados para mostrar u ocultar temporalmente contenido que ya se ha aprobado y publicado.
>
>Si desea publicar contenido nuevo con todos los flujos de trabajo asociados o eliminar por completo (cancelar la publicación) del sitio, considere [administrar la publicación.](/help/sites-cloud/authoring/sites-console/publishing-pages.md#manage-publication)

### URL mnemónica {#vanity-url}

Esta propiedad permite introducir una URL de vanidad para esta página, lo que permite tener una URL más corta o más expresiva. Por ejemplo, si la URL de vanidad se establece como `welcome` en la página identificada por la ruta `/v1.0/startpage` del sitio web `http://example.com`, entonces `http://example.com/welcome` es la URL de vanidad de `http://example.com/content/v1.0/startpage`.

>[!CAUTION]
>
>URL de vanidad:
>
>* Debe ser único.
>* No admiten patrones regex.
>* No debe configurarse en una página existente.

* **Agregar**: seleccione esta opción para mostrar un campo con el que definir una URL de vanidad para la página.
   * Seleccione de nuevo para añadir varias.
   * Seleccione el icono **Quitar** para eliminar la URL de vanidad.
* **Redirigir URL de vanidad**: indica si desea que la página use la URL de vanidad o redirija a la URL real de la página

## Avanzado  {#advanced}

### Configuración {#settings}

* **Idioma**: el idioma de la página
* **Raíz del idioma**: si la página es la raíz de una copia en un idioma, es necesario marcar esta opción
* **Redireccionar**: indica la página a la que esta página debe redireccionarse automáticamente con un estado de HTML `302 Found`
   * **Redirección permanente**: cuando se selecciona, la página redirige a la ruta de destino proporcionada junto con un estado HTML `301 Moved Permanently`.
* **Design**
* **Alias**: especifica un alias que se usará con esta página
   * Por ejemplo, si define un alias de `private` para la página `/content/wknd/us/en/magazine/members-only`, se puede acceder a esta página también mediante `/content/wknd/us/en/magazine/private`
   * La creación de un alias establece la propiedad `sling:alias` en el nodo de página, lo que solo afecta al recurso, no a la ruta del repositorio.
   * No se pueden publicar páginas a las que se accede mediante alias en el editor. Las [Opciones de publicación](/help/sites-cloud/authoring/sites-console/publishing-pages.md) del editor solo están disponibles para las páginas a las que se accede a través de sus rutas reales.
   * Consulte [Nombres de páginas localizados en Procedimientos recomendados para la administración de direcciones URL y SEO](/help/overview/seo-and-url-management.md#localized-page-names) para obtener más información.

### Configuración {#configuration}

* **Heredado de &lt;path>**: habilita o deshabilita la herencia de **Configuración de nube** para la página
   * Alterna la disponibilidad de **Configuración de nube** para la edición

* **Configuración de nube**: la ruta de la configuración seleccionada

### Configuración de plantilla {#template-settings}

* **Plantillas permitidas**: [define la lista de plantillas que están disponibles](/help/sites-cloud/authoring/page-editor/templates.md#enabling-and-allowing-a-template-template-author) dentro de esta rama secundaria
   * Cada valor debe ser una ruta absoluta a una plantilla.
   * Use `/.*` para permitir todas las plantillas por debajo de esta ruta.
* **Usar página como plantilla** - [Cree una nueva plantilla basada en la página actual.](/help/sites-cloud/authoring/universal-editor/templates.md)
   * Solo se aplica a las páginas creadas para utilizarlas con el editor universal que aprovecha Edge Delivery Services.

### Requisito de autenticación {#authentication}

* **Habilitar**: habilita el uso de la autenticación para acceder a la página

>[!NOTE]
>
>Los grupos de usuarios cerrados para la página se definen en la pestaña **[Permisos](#permissions)**.

* **Página de inicio de sesión**: la página que se usará para iniciar sesión

### Exportar {#export}

* **Configuración de exportación**: especifica una configuración de exportación

## SEO {#seo}

* **URL canónica**: se usa para sobrescribir la URL canónica de la página
   * Si se deja en blanco, la dirección URL de la página es su dirección URL canónica.

* **Etiquetas de robots**: utilice el menú desplegable para seleccionar las etiquetas de robots y controlar el comportamiento de los rastreadores de los motores de búsqueda
   * Algunas opciones entran en conflicto entre sí, en cuyo caso la opción más permisiva tiene prioridad.

* **Generar mapa de sitio**: cuando se selecciona, se genera un `sitemap.xml` para esta página y sus descendientes.

## Imágenes {#images}

### Imagen destacada {#featured-image}

Esta sección se utiliza para seleccionar y configurar la imagen que desea mostrar. Se utiliza en los componentes que hacen referencia a la página; por ejemplo, teasers, listas de páginas, etc.

* **Imagen** - Puedes **elegir** un recurso o buscar un archivo para cargar, después **editar** o **borrar** la imagen seleccionada.
* **Texto alternativo**: texto utilizado para representar el significado o la función de la imagen, que suelen utilizar los lectores de pantalla
* **Heredar: valor tomado del recurso DAM**: cuando se selecciona, el texto alternativo se rellena con el valor de los `dc:description`metadatos de DAM.

### Miniaturas {#thumbnail}

Esta sección se utiliza para seleccionar y configurar la miniatura de la imagen para la página. Se utiliza en los componentes que hacen referencia a la página; por ejemplo, teasers, listas de páginas, etc.

* **Generar previsualización**: genere una previsualización de la página para utilizarla como miniatura
* **Cargar imagen**: cargue una imagen para utilizarla como miniatura
* **Seleccionar imagen**: seleccione un recurso existente para utilizarlo como miniatura
* **Revertir**: esta opción está disponible después de hacer un cambio en la miniatura Si no desea mantener el cambio, puede revertirlo antes de guardarlo.

## Cloud Services {#cloud-services}

* **Configuraciones de Cloud Service**: define qué configuración se usa para los servicios en la nube de la página
* **Heredado de**: para Live Copies y copias de idioma, las configuraciones en la nube se heredan del modelo de forma predeterminada.
   * Anular selección para anular herencia

## Personalización {#personalization}

### Configuración de ContextHub {#contexthub-config}

* **Ruta de ContextHub**: defina la [Configuración de ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)
* **Ruta de segmentos**: defina la [Ruta de segmentos](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

### Configuración de segmentación {#targeting-config}

* **Marca** - Define una [marca para especificar un ámbito de segmentación](/help/sites-cloud/authoring/personalization/targeted-content.md)
   * Esta opción requiere que la cuenta de usuario esté en el grupo `Target Administrators`.

## Permisos {#permissions}

Utilice la ficha **Permisos** para definir qué usuarios, grupos o [grupos de usuarios cerrados (CUG)](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/advanced/closed-user-groups.html?lang=es) pueden acceder o modificar la página.

* **Agregar permisos**
* **Editar grupo de usuarios cerrado**
* Ver los **Permisos efectivos**

## Modelo {#blueprint}

Esta pestaña solo está visible para páginas que sirven como modelos. Los modelos sirven de base para Live Copies y forman parte de la [Administración de varios sitios](/help/sites-cloud/administering/msm/overview.md)

* **Despliegue**: inicie un despliegue del contenido del modelo en Live Copies
* **Información general de Live Copy**: abre una ventana para examinar la estructura de la página de Live Copy
* **Live Copies actuales**: una lista de páginas basadas en (es decir, que son Live Copies de) la página de modelo seleccionada

## Live Copy {#live-copy}

Esta pestaña solo está visible para páginas configuradas como Live Copies. Al igual que con los [modelos,](#blueprint) Live Copies son parte de [Administración de varios sitios.](/help/sites-cloud/administering/msm/overview.md)

* **Sincronizar** - Sincronizar Live Copy con el modelo, conservando las modificaciones locales
* **Restablecer**: restablezca la Live Copy al estado del modelo y elimine las modificaciones locales
* **Suspender**: suspenda la Live Copy de nuevas modificaciones en el despliegue
* **Desasociar** - Desasociar Live Copy del modelo

### Origen {#source}

* Muestra la ruta del modelo para esta Live Copy

### Estado {#status}

* Enumera el estado actual de Live Copy de la página

### Configuración {#live-copy-config}

* **Herencia de Live Copy**: si está marcada, la configuración de Live Copy es efectiva en todas las tareas secundarias.
* **Heredar configuraciones de despliegue de la página principal**: si está marcada, la configuración de despliegue se hereda de la página principal de la página.
* **Elija la configuración de despliegue**: define las circunstancias en las que se propagan las modificaciones desde el modelo y solo está disponible cuando **Heredar configuraciones de despliegue de la página principal** no está seleccionado
* **Lista de rutas excluidas**

## Vista previa {#preview}

Cuando un [entorno de vista previa](/help/sites-cloud/authoring/sites-console/previewing-content.md) está habilitado, están disponibles los siguientes detalles:

* **URL de vista previa**: URL utilizada para acceder al contenido en el entorno de vista previa

## Aplicación web progresiva {#progressive-web-app}

A través de una configuración sencilla, un autor de contenido puede habilitar las funciones de aplicación web progresiva (PWA) para las experiencias creadas en AEM Sites. El sitio se puede comportar como una aplicación nativa volviéndolo instalable en la pantalla de inicio del dispositivo de los visitantes y disponible sin conexión.

{{pwa-deprecation}}

### Configurar la experiencia instalable {#config-pwa}

* **Habilitar PWA**: cuando esté habilitado, los visitantes de la página podrán instalar el sitio como PWA.
* **URL de inicio**: URL que se debe cargar cuando el usuario inicie la aplicación web
   * Si la dirección URL es relativa, la dirección URL de manifiesto se utiliza como dirección URL base para resolver
   * Cuando está vacía, se utiliza la dirección URL de la página desde la que se instaló la aplicación.
   * Se recomienda configurar un valor.
* **Modo de visualización**: cómo se debe ocultar o presentar el explorador al usuario en el dispositivo local
* **Orientación de la pantalla**: cómo gestionará PWA las orientaciones del dispositivo
* **Color del tema**: el color de la aplicación que afecta a la forma en que el sistema operativo del usuario local muestra la barra de herramientas de la IU nativa y los controles de navegación
* **Color de fondo**: El color de fondo de la aplicación, que se muestra a medida que se carga la aplicación.
* **Icono**: el icono que representa la aplicación en el dispositivo del usuario cuando PWA está instalado

### Administración de caché (avanzada) {#cache-management}

* **Estrategia de almacenamiento en caché y frecuencia de actualización del contenido**: define el modelo de almacenamiento en caché para su PWA.
* **Archivos para almacenar en caché para su uso sin conexión**
   * **Almacenamiento en caché previo de archivos (vista previa técnica)**: los archivos alojados en AEM se guardan en la memoria caché del explorador local cuando el trabajador de servicio se está instalando y antes de que se utilice.
   * **Bibliotecas del lado cliente**: Bibliotecas del lado cliente para almacenar en caché para la experiencia sin conexión
   * **Inclusiones de rutas**: las solicitudes de red para las rutas definidas se interceptan y el contenido almacenado en caché se devuelve de acuerdo con la estrategia de almacenamiento en caché y frecuencia de actualización del contenido configuradas
   * **Exclusiones de rutas**: estos archivos nunca se almacenarán en caché, independientemente de la configuración de Almacenamiento en caché previo de archivos e Inclusiones de rutas.

>[!NOTE]
>
>Consulte [Habilitación de funciones de aplicación web progresiva](/help/sites-cloud/authoring/sites-console/enable-pwa.md) para obtener más información.

