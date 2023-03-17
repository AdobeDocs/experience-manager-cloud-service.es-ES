---
title: Edición de las propiedades de página
description: Permite definir las propiedades de una página
exl-id: 27521a6d-c6e9-4f43-9ddf-9165b0316084
source-git-commit: ba1f2b7f1f61f7ba094047171e42e3cc8811a1b6
workflow-type: tm+mt
source-wordcount: '2387'
ht-degree: 81%

---

# Edición de las propiedades de página   {#editing-page-properties}

Puede definir las propiedades para una página. Estas pueden variar en función de la naturaleza de la página. Por ejemplo, algunas páginas pueden estar conectadas a una Live Copy. Otras no lo están y la información de la Live Copy está disponible según corresponda.

## Propiedades de página {#page-properties}

Las propiedades se distribuyen entre varias pestañas.

### Básico {#basic}

* **Título y etiquetas**

   * **Título**: el título de la página se muestra en varias ubicaciones. Por ejemplo, la vista de la pestaña **Sitios web** y las vistas de lista o tarjeta **Sitios**.
      * Es un campo obligatorio.
   * **Etiquetas** - Aquí puede agregar o quitar etiquetas de la página al actualizar la lista en el cuadro de diálogo de selección.
      * Tras seleccionar una etiqueta, esta se muestra bajo el cuadro de selección. Para eliminar una etiqueta de esta lista, utilice la x.
      * Se puede especificar una etiqueta completamente nueva si se escribe el nombre en un cuadro de selección vacío.
         * La nueva etiqueta se creará cuando pulse Intro.
         * A continuación, la nueva etiqueta se mostrará con una pequeña estrella a la derecha que indicará que es una etiqueta nueva.
      * Con la función de lista desplegable, puede seleccionar etiquetas existentes.
      * Aparece una x cuando pasa el puntero sobre una entrada de etiqueta en el cuadro de selección; esto puede usarse para quitar esa etiqueta para esta página.
      * Para obtener más información sobre las etiquetas, consulte [Utilizar etiquetas](/help/sites-cloud/authoring/features/tags.md).
   * **Ocultar en navegación** - Indica si se muestra o se oculta la página en la navegación por páginas del sitio resultante.

* **Marca**

   Aplique una identidad de marca uniforme en todas las páginas adjuntando un slug de marca al título de cada página. Esta funcionalidad requiere el uso del componente de página de la versión 2.14.0 o posterior de los [Componentes principales.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es)

   * **Marcas**

      * **Sobrescribir**: marque para definir el slug de marca en esta página.
         * El valor lo heredará cualquier página secundaria a menos que también tenga valores establecidos de **Sobrescribir**.
      * **Sobrescribir valor**: el texto del slug de marca que se añadirá al título de la página.
         * El valor se anexa al título de la página después de un carácter de barra vertical como “Ciclismo en Toscana | Siempre listo para WKND”

* **ID de HTML**

   * **ID**: ID de HTML que se aplicará al componente.

* **Títulos y descripción de Más**

   * **Título de página**: un título que se usará en la página. Normalmente, lo utilizan los componentes del título. Si la opción se deja vacía, se utilizará el **Título**.
   * **Título de navegación**: puede especificar un título diferente para utilizarlo en la navegación (por ejemplo, si requiere algo más conciso). Si la opción se deja vacía, se usará el **Título**.
   * **Subtítulo**: un subtítulo que se usará en la página.
   * **Descripción**: la descripción de la página, su propósito o cualquier otro detalle que quiera añadir.

* **Tiempo de activación/desactivación**

   >[!NOTE]
   >
   > Consulte [Horas de activación y desactivación: configuración de activador](/help/operations/replication.md#on-and-off-times-trigger-configuration) para obtener detalles sobre cómo configurar la replicación automática relacionada.

   >[!NOTE]
   >Si el **Tiempo de activación** o el **Tiempo de desactivación** se sitúan en el pasado y se configura la replicación automática, la acción relevante se activará de inmediato.

   * **Tiempo de activación**: la fecha y hora a las que se hará visible (procesada) la página publicada en el entorno de publicación. La página debe publicarse, ya sea de forma manual o mediante replicación automática preconfigurada.

      * Si ya se ha [publicado (manualmente)](/help/sites-cloud/authoring/fundamentals/publishing-pages.md), esta página se mantendrá inactiva (oculta) hasta que se procese a la hora especificada.
      * Si no se publica y se configura para la replicación automática, la página se publicará automáticamente y, a continuación, se procesará a la hora especificada.
      * Si no se publica y no está configurada para la replicación automática, la página no se publicará automáticamente, por lo que se verá un error 404 cuando se intente acceder a ella.
   * **Tiempo de desactivación**: similar a **Tiempo de activación** y usado a menudo en combinación, define el momento en el que la página publicada se ocultará en el entorno de publicación.

   * Deje estos campos (**Tiempo de activación** y **Tiempo de desactivación**) vacíos para las páginas que desea publicar de inmediato y disponibles en el entorno de publicación hasta que se desactiven (el escenario normal).


* **URL de vanidad**

   * Permite introducir una URL de vanidad para esta página, que le permitirá disponer de una URL más corta y/o descriptiva.
   * Por ejemplo, si la URL de vanidad se establece como `welcome` en la página identificada por la ruta `/v1.0/startpage` del sitio web `http://example.com`, entonces `http://example.com/welcome` es la URL de vanidad de `http://example.com/content/v1.0/startpage`.

   >[!CAUTION]
   >
   >URL de vanidad:
   >
   >* Deben ser únicas, por lo que tiene que asegurarse de que ninguna otra página utilice este valor.
   >* No admiten patrones regex.
   >* No debe configurarse en una página existente.


   * **Añadir**: pulse o haga clic para mostrar un campo con el que definir una URL de vanidad para la página.
      * Pulse o haga clic de nuevo para añadir varias.
      * Pulse o haga clic en el botón **Eliminar** para eliminar la URL de vanidad.
   * **Redirigir URL de vanidad**: indica si desea que la página use la URL de vanidad.


### Avanzado  {#advanced}

* **Configuración**

   * **Idioma**: el idioma de la página
   * **Raíz del idioma**: si la página es la raíz de una copia en un idioma, es necesario marcar esta opción
   * **Redirigir**: indica la página a la cual esta deberá redirigirse automáticamente con un estado HTML `302 Found`.
      * **Redirección permanente**: cuando se selecciona, la página redirige a la ruta de destino proporcionada junto con un estado HTML `301 Moved Permanently`.
   * **Diseño**: indica si se muestra o se oculta la página en la navegación de páginas del sitio resultante
   * **Alias**: especifica un alias que se usará con esta página
      * Por ejemplo, si define un alias de `private` para la página `/content/wknd/us/en/magazine/members-only`, se puede acceder a esta página también mediante `/content/wknd/us/en/magazine/private`
      * La creación de un alias establece la propiedad `sling:alias` en el nodo de página, lo que solo afecta al recurso, no a la ruta del repositorio.
      * Las páginas a las que se accede mediante alias en el editor no se pueden publicar. Las [Opciones de publicación](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) del editor solo están disponibles para las páginas a las que se accede a través de sus rutas reales.
      * Para obtener más información, consulte [Nombres de páginas localizados en Recomendaciones para la administración de direcciones URL y SEO](/help/overview/seo-and-url-management.md#localized-page-names).

* **Configuración**

   * **Heredado de &lt;path>** - habilitar/deshabilitar la herencia; alterna la disponibilidad de **Configuración de nube** para la selección

   * **Configuración de nube** - La ruta a la configuración seleccionada

* **Configuración de plantilla**

   * **Plantillas permitidas**: [define la lista de plantillas disponibles](/help/sites-cloud/authoring/features/templates.md#enabling-and-allowing-a-template-template-author) dentro de esta rama secundaria

* **Requisito de autenticación**

   * **Habilitar**: habilite el uso de la autenticación para acceder a la página

      >[!NOTE]
      >
      >Los grupos de usuarios cerrados para la página se definen en la pestaña **[Permisos](#permissions)**.

   * **Página de inicio de sesión**: la página que se usará para iniciar sesión

* **Exportar**

   * **Configuración de exportación**: especifica una configuración de exportación

* **SEO**

   * **Url Canónica** - se puede usar para sobrescribir la dirección URL canónica de la página; si se deja en blanco, la dirección URL de la página será su dirección URL canónica

   * **Etiquetas de robots** - seleccione las etiquetas robots para controlar el comportamiento de los rastreadores de motores de búsqueda.

      >[!NOTE]
      >
      >Algunas de las opciones entran en conflicto entre sí. En caso de conflicto, la opción más permisiva tiene prioridad.

   * **Generar mapa del sitio** : cuando se selecciona, se genera un archivo sitemap.xml para esta página y sus descendientes

### Imágenes {#images}

* **Imagen destacada**

   Seleccione y configure la imagen que desea mostrar. Se utiliza en los componentes que hacen referencia a la página; por ejemplo, teasers, listas de páginas, etc.

   * **Imagen**

      Puede **Seleccionar** un recurso o busque un archivo para cargarlo y **Editar** o **Borrar**.

   * **Texto alternativo** - un texto utilizado para representar el significado o la función de la imagen; por ejemplo, para uso de los lectores de pantalla.

   * **Heredar : valor tomado del recurso DAM** : cuando se selecciona, se rellena el texto alternativo con el valor de la variable `dc:description`metadatos en DAM

* **Miniatura**

   Configuración de la miniatura de la página

   * **Generar previsualización**: genere una previsualización de la página para utilizarla como miniatura
   * **Cargar imagen**: cargue una imagen para utilizarla como miniatura
   * **Seleccionar imagen**: seleccione un recurso existente para utilizarlo como miniatura
   * **Revertir**: esta opción está disponible después de hacer un cambio en la miniatura Si no desea mantener el cambio, puede revertirlo antes de guardar.

### Cloud Services {#cloud-services}

* **Configuraciones de Cloud Service**: defina propiedades para servicios en la nube

### Personalización {#personalization}

* **Configuración de ContextHub**

   * **Heredado de &lt;path>** - habilitar/deshabilitar la herencia; alterna la disponibilidad de **Ruta de ContextHub** y **Ruta de segmentos** para la selección

   * **Ruta de ContextHub**: defina la [Configuración de ContextHub](/help/sites-cloud/authoring/personalization/contexthub.md)
   * **Ruta de segmentos**: defina la [Ruta de segmentos](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)

* **Configuración de ámbito**

   * **Marca**: defina una [marca para especificar un ámbito de segmentación](/help/sites-cloud/authoring/personalization/targeted-content.md).
   >[!NOTE]
   >Esta opción requiere una cuenta de usuario en el grupo `Target Administrators`.

### Permisos    {#permissions}

* **Permisos**

   * **Agregar permisos**
   * **Editar grupo de usuarios cerrado**
   * Ver los **permisos efectivos**

### Modelo {#blueprint}

Esta pestaña solo está visible para páginas que sirven como modelos. Los modelos sirven de base para Live Copies y forman parte de [Administración de varios sitios.](/help/sites-cloud/administering/msm/overview.md)

* **Live Copies actuales**: enumera las páginas que se basan en (es decir, que son Live Copies de) esta página de modelo

* **Configuraciones de despliegue**: controla las circunstancias dentro de las que se propagarán las modificaciones a la Live Copy

### Live Copy    {#live-copy}

Esta ficha solo está visible para páginas configuradas como Live Copies. Al igual que con los modelos, las Live Copies forman parte de [Administración de varios sitios.](/help/sites-cloud/administering/msm/overview.md).

* **Sincronizar**: sincronice la Live Copy con el modelo, conservando las modificaciones locales
* **Restablecer**: restablezca la Live Copy al estado del modelo y elimine las modificaciones locales
* **Suspender**: suspenda la Live Copy de nuevas modificaciones en el despliegue
* **Desasociar**: separe la Live Copy del modelo

* **Origen**

   * Muestra la ruta del modelo para esta Live Copy

* **Estado**

   * Enumera el estado actual de Live Copy de la página

* **Configuración**

   * **Herencia de Live Copy**: si está marcada, la configuración de Live Copy es eficaz en todas las tareas secundarias.
   * **Heredar configuraciones de despliegue de la página principal**: si está marcada, la configuración de despliegue se hereda de la página principal de la página
   * **Elija la configuración de despliegue**: define las circunstancias en las que se propagarán las modificaciones desde el modelo y solo está disponible cuando **Hereda configuraciones de despliegue de la página principal** no está seleccionado

### Vista previa {#preview}

Cuando un entorno de previsualización esté habilitado, verá lo siguiente:

* URL de previsualización: la URL utilizada para acceder al contenido en el entorno de previsualización.

### Aplicación web progresiva {#progressive-web-app}

A través de una configuración sencilla, un autor de contenido ahora puede habilitar las funciones de aplicación web progresiva (PWA) para las experiencias creadas en AEM Sites.

>[!NOTE]
>
>Para obtener más información, consulte [Activación de las funciones progresivas de la aplicación web](/help/sites-cloud/authoring/features/enable-pwa.md).

* **Configurar la experiencia instalable**

   * **Habilitar PWA** - habilitar/deshabilitar la función; permite a los usuarios instalar el sitio como PWA
   * **URL de inicio** - la URL de inicio preferida
   * **Modo de visualización** : cómo se debe ocultar o presentar el navegador al usuario desde el dispositivo local
   * **Orientación de la pantalla** - cómo gestionará el PWA las orientaciones del dispositivo
   * **Color del tema** : el color de la aplicación que afecta a cómo el sistema operativo del usuario local muestra la barra de herramientas de la IU nativa y los controles de navegación
   * **Color de fondo** : el color de fondo de la aplicación, que se muestra a medida que se carga la aplicación.
   * **Icono** : el icono que representa la aplicación en el dispositivo del usuario.

* **Administración de caché (avanzada)**

   * **Estrategia de almacenamiento en caché y frecuencia de actualización del contenido** - define el modelo de almacenamiento en caché para su PWA
   * **Archivos para almacenar en caché para su uso sin conexión**
      * **Almacenamiento en caché previo de archivos (vista previa técnica)** : los archivos alojados en AEM se guardarán en la caché del navegador local cuando el trabajador de servicios esté instalando y antes de que se utilicen
      * **Bibliotecas del lado del cliente** - bibliotecas del lado del cliente para almacenar en caché para la experiencia sin conexión
      * **Inclusiones de rutas** - las solicitudes de red para las rutas definidas se interceptan y el contenido almacenado en caché se devuelve de acuerdo con la estrategia de almacenamiento en caché configurada y la frecuencia de actualización del contenido
      * **Exclusiones de ruta** : estos archivos nunca se almacenarán en caché, independientemente de la configuración en Almacenamiento en caché de archivos previo al almacenamiento en caché e inclusiones de rutas

## Edición de las propiedades de página   {#editing-page-properties-1}

* Desde la consola **Sitios:**
   * [Creando una página nueva](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) (un subconjunto de las propiedades)
   * Pulsando o haciendo clic en **Propiedades**
      * Para una sola página
      * Para varias páginas (solo se pueden editar en masa un subconjunto de las propiedades)
* Desde el editor de páginas:
   * Utilizando **Información de página** (a continuación, **Abrir propiedades**)

### Desde la consola Sitios: página individual {#from-the-sites-console-single-page}

Tocando o haciendo clic en **Propiedades** para definir las propiedades de la página:

1. Mediante la consola **Sitios**, desplácese hasta la ubicación de la página para la que desee ver y editar las propiedades.
1. Seleccione la opción **Propiedades** de la página requerida mediante:
   * [Acciones rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [Modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources)
   * Las propiedades de página se mostrarán mediante las pestañas adecuadas.
1. Visualice o edite las propiedades según sea oportuno. 
1. A continuación, utilice **Guardar** para guardar las actualizaciones, seguido de **Cerrar** para volver a la consola.

### Al editar una página {#when-editing-a-page}

Al editar una página puede, utilizar **Información de página** para definir las propiedades de la página:

1. Abra la página para la que desee editar las propiedades.
1. Seleccione el icono **Información de página** para abrir el menú de selección:
1. Seleccione **Abrir propiedades** para abrir un cuadro de diálogo que le permite editar las propiedades, ordenadas por la pestaña adecuada. Los siguientes botones también están disponibles en la parte derecha de la barra de herramientas:
   * **Cancelar**
   * **Guardar y cerrar**
1. Utilice el botón **Guardar y cerrar** para guardar los cambios. 

### Desde la consola Sitios: varias páginas {#from-the-sites-console-multiple-pages}

Desde la consola **Sites** puede seleccionar varias páginas y luego utilizar **Ver propiedades** para ver o editar las propiedades de la página. Esto se conoce como edición masiva de propiedades de página.

>[!NOTE]
>
>La edición de propiedades por lotes también está disponible para los recursos. Se parece mucho, pero presenta algunos aspectos diferentes. Consulte Edición de propiedades de varios recursos para obtener más información.
>
>También dispone del Editor por lotes, que le permite buscar contenido de varias páginas con GQL (Google Query Language) y, a continuación, editar el contenido directamente en el editor por lotes para luego guardar los cambios (en las páginas originales).

<!--
>Bulk editing of properties is also available for Assets. It is very similar, but differs in a few points. See [Editing Properties of Multiple Assets](/help/assets/managing-multiple-assets.md) for details.
>
>There is also the [Bulk Editor](/help/sites-administering/bulk-editor.md), which allows you to search for content from multiple pages using GQL (Google Query Language) and then edit the content directly in the bulk editor before saving your changes to the originating pages.
-->

Puede seleccionar varias páginas para editarlas por lotes utilizando distintos métodos, como los siguientes:

* Mientras se desplaza por la consola **Sitios**
* Después de utilizar la opción **Buscar** para localizar un conjunto de páginas

Después de seleccionar las páginas y hacer clic o pulsar en la opción **Propiedades**, se muestran las propiedades por lotes:

![Propiedades de la página de edición masivas](/help/sites-cloud/authoring/assets/page-properties-bulk-edit.png)

Solo se pueden editar por lotes las páginas que:

* Comparten el mismo tipo de recurso.
* No forman parte de una Live Copy
   * Si alguna de las páginas está en una Live Copy, se mostrará un mensaje cuando se abran las propiedades. 

Cuando esté en la edición por lotes, podrá efectuar las siguientes acciones:

* **Ver**

   * Una lista de las páginas afectadas
      * Si lo desea, puede seleccionarlas o deseleccionarlas.
      * Pestañas
         * Las propiedades se ordenan en pestañas, al igual que cuando se visualizan las propiedades de una página.
   * Un subconjunto de propiedades
      * Se pueden ver las propiedades que están disponibles en todas las páginas seleccionadas (deben haberse marcado específicamente como disponibles para la edición por lotes).
      * Si reduce la selección de páginas a una sola página, se verán todas las propiedades.
   * Propiedades comunes con un valor común
      * En el modo Ver solo se muestran las propiedades con un valor común.
      * Cuando el campo admite varios valores (por ejemplo, etiquetas), los valores solo se mostrarán si *todos* son comunes. Si solo son comunes algunos de ellos, solo se mostrarán en el momento de editar.
      * Cuando no existen propiedades con un valor común, se muestra un mensaje. 

* **Editar**

   * Puede actualizar los valores en los campos disponibles.
      * Los nuevos valores se aplicarán a todas las páginas seleccionadas al activar **Listo**.
      * Si el campo admite varios valores (por ejemplo, Etiquetas), puede agregar un valor nuevo o eliminar un valor común.
   * Los campos que son comunes en las páginas, pero que tienen diferentes valores, se señalizarán con un valor especial; por ejemplo, el texto `<Mixed Entries>`.

>[!NOTE]
>
>El componente de página se puede configurar para especificar los campos disponibles para la edición por lotes. Consulte Configuración de la página para editar las propiedades de página por lotes.

<!--
>The page component can be configured to specify the fields available for bulk editing. See [Configuring your page for bulk editing of page properties](/help/sites-developing/bulk-editing.md).
-->
