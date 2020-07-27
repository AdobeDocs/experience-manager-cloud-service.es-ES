---
title: Fragmentos de contenido
description: Los fragmentos de contenido de Adobe Experience Manager as a Cloud Service le permiten diseñar, crear, depurar y utilizar contenido independiente de las páginas.
translation-type: tm+mt
source-git-commit: be65ba65fb6bbd7634da882ef8337565f1fce477
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 94%

---


# Fragmentos de contenido {#content-fragments}

Los fragmentos de contenido de Adobe Experience Manager (AEM) as a Cloud Service se [crean y administran como recursos independientes de las páginas](/help/assets/content-fragments/content-fragments.md).

Permiten crear contenido neutro con respecto al canal, así como variaciones (posiblemente específicas del canal). Después se pueden usar estos fragmentos, y sus variaciones, al crear páginas de contenido.

Junto con el exportador JSON actualizado, los fragmentos de contenido estructurados también se pueden utilizar para distribuir contenidos de AEM mediante servicios de contenido a canales en lugar de páginas de AEM.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencias](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)**son funciones distintas de AEM:
>
>* Los **fragmentos de contenido** son contenido editorial, principalmente texto e imágenes relacionadas. Se trata de contenido puro, sin diseño ni maquetación.
>* Los **fragmentos de experiencias** son contenido plenamente diseñado y partes de una página web.

>
>
Los fragmentos de experiencias pueden incluir contenido en forma de fragmentos de contenido, pero no lo contrario.

>[!CAUTION]
>
>Esta página se debe leer junto con [Trabajo con fragmentos de contenido](/help/assets/content-fragments/content-fragments.md) (y las páginas relacionadas), ya que introduce terminología y conceptos básicos, además de tratar la creación y gestión de fragmentos.

Los fragmentos de contenido permiten hacer lo siguiente:

* **Estrategia de campañas y mercadotecnia** 
   * Revisar contenido mediante fragmentos de contenido administrados centralmente.
* **Profesionales creativos** 
   * Hacer seguimientos de los recursos creativos a través de las colecciones asociadas con los fragmentos de contenido.
* **Redactores** 
   * Escriba en el editor de fragmentos de contenido de AEM.
   * Pueden crear variaciones de contenido.
   * Pueden asociar contenido relevante con el fragmento de contenido.
   * Pueden usar distintas versiones/flujos de trabajo.
   * Pueden compartir fragmentos de contenido.
   * Pueden administrar traducciones de forma centralizada.
* **Productores y gestores de trayectorias de clientes** 
   * Seleccionar fragmentos y variaciones predefinidos con la función de creación en AEM.
   * Pueden utilizar fragmentos y contenidos asociados y estar siempre al día a medida que creadores y redactores apliquen actualizaciones en recursos y fragmentos administrados centralmente.
   * Pueden utilizar contenido multimedia asociado seleccionado según relevancia.
   * Pueden crear variaciones de contenido ad hoc al instante garantizando al mismo tiempo que las variaciones siguen administradas de forma centralizada en el fragmento.

## Adición de un fragmento de contenido a la página      {#adding-a-content-fragment-to-your-page}

1. Abra la página para editarla. 
2. Añada el componente **Fragmento de contenido**, bien desde el navegador **Componentes** o con **Insertar nuevo componente**. 
3. Puede:
   * Abra el navegador **Recursos** y filtre por **Fragmentos de contenido** (el valor predeterminado es Imágenes). Arrastre el fragmento en cuestión a la instancia de componente.
   * Seleccione el componente de fragmento de contenido y, a continuación, **Configurar** en la barra de herramientas. En el cuadro de diálogo, puede abrir el cuadro de diálogo de selección para buscar y seleccionar el **fragmento de contenido** requerido.

   >[!NOTE]
   >
   >Otra posibilidad es arrastrar un fragmento de contenido específico directamente a la página. Esto creará automáticamente el componente asociado (fragmento de contenido). 

4. En un primer momento se muestra el contenido del elemento **Principal** y **Maestro** (variación). Puede [seleccionar otros elementos y variaciones](#selecting-the-element-or-variation) si lo desea.

   ![Fragmentos de contenido en el explorador de recursos](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >Para obtener más información sobre otras funciones de edición, consulte también:
   >
   >* [Diseño adaptable](/help/sites-cloud/authoring/features/responsive-layout.md)
   >* [Editar el contenido de una página](/help/sites-cloud/authoring/fundamentals/editing-content.md)


### Selección del elemento o la variación {#selecting-the-element-or-variation}

Abra el cuadro de diálogo **Configuración** del fragmento para configurar el fragmento que se va a utilizar en la página actual. El cuadro de diálogo puede depender del componente utilizado.

>[!NOTE]
>
>Consulte también Componentes [principales, el componente Fragmento de contenido](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/content-fragment-component.html)

En el cuadro de diálogo de configuración adecuado, puede seleccionar los parámetros disponibles, entre los que se incluyen:

* **Fragmento de contenido**
   * Especifique el fragmento que se va a utilizar.
* **Modo de visualización**:
   * **Elemento de texto único**
   * **Varios elementos**
* **Elemento**
   * Una selección estará disponible dependiendo del modelo utilizado.

   >[!NOTE]
   >
   >Los elementos disponibles dependen de la plantilla utilizada.

* **Variación**
   * **Principal** siempre aparecerá como la opción predeterminada.
   * Podrá realizar una selección si se crearon variaciones para el fragmento.

* **ID**

   * Atributo de **ID de HTML** que se aplicará al componente.

### Conexión rápida con el editor de fragmentos      {#quick-connection-to-fragment-editor}

Puede abrir el origen del fragmento para editarlo (el recurso) mediante el icono **Editar** de la barra de herramientas de componentes. Esto le permitirá [editar y gestionar el fragmento de contenido](/help/assets/content-fragments/content-fragments.md). 

>[!CAUTION]
>
>Como siempre, editar el origen del fragmento afectará a todas las páginas que hacen referencia a dicho fragmento de contenido.

### Añadir contenido intermedio      {#adding-in-between-content}

Cuando se añade a la página un fragmento de contenido específico, se dispone de un marcador de posición **Arrastre los componentes aquí** entre cada párrafo HTML (y en la parte superior/inferior) del fragmento.

De este modo puede añadir contenido adicional [entre](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) (es decir, entre el contenido) el contenido del fragmento (en cualquiera de los puntos disponibles) sin tener que cambiar el fragmento raíz.

Para el contenido intermedio puede:

* Agregar componentes desde el [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
* Agregar recursos desde el [navegador de recursos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
* Utilizar [contenido asociado](#using-associated-content) como fuente para el contenido intermedio.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

![Insertar componente](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>También puede [insertar recursos visuales (imágenes) en el propio fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Los recursos visuales insertados en el propio fragmento se adjuntan al párrafo anterior del fragmento. Esto significa que no puede colocar contenido intermedio entre un recurso visual y el párrafo precedente. Si necesita este nivel de conexión, puede agregar la imagen al fragmento (como un fragmento [de medios](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)mixtos).

>[!CAUTION]
>
>Una vez añadido contenido intermedio a un fragmento de contenido en la página, al cambiar la estructura del fragmento de contenido subyacente (es decir, en el editor de fragmentos de contenido) se pueden generar resultados erróneos o inesperados.
>
>Cuando esto sucede, el contenido intermedio se mantiene tal cual:
>
>* Los componentes intermedios tienen una posición absoluta dentro de la secuencia de componentes en el flujo del fragmento. Esta posición no cambia, aunque varíe el contenido de los párrafos del fragmento.
>
>  
Por este motivo, es posible que parezca que la posición relativa ha cambiado, ya que los párrafos intermedios no tienen relación contextual con los párrafos (del fragmento) junto a los que se sitúan.
>* Sin embargo, en caso de que exista conflicto entre las dos estructuras de párrafo, el contenido intermedio no se muestra (aunque siga presente internamente).


### Uso de contenido asociado      {#using-associated-content}

Si tiene [contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md) con el [fragmento de contenido](/help/assets/content-fragments/content-fragments.md), estos recursos estarán disponibles en el panel lateral (después de colocar el fragmento en la página de contenido). Associated content is effectively a special source of content for [in-between content](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments).

>[!NOTE]
>
>Hay varios métodos para agregar [recursos visuales (p. ej., imágenes)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al fragmento o página.

>[!NOTE]
>
>Si tiene varios fragmentos de contenido en la página, la pestaña **Contenido asociado** mostrará los recursos oportunos para todos los fragmentos.

Una vez que haya añadido un fragmento con contenido asociado a la página, se abrirá una nueva pestaña (**Contenido asociado**) en el panel lateral.

Desde aquí podrá arrastrar los recursos a la ubicación requerida (en un componente existente o a la posición que le interese donde se creará el componente correspondiente):

![Inserción de una imagen](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### Recursos insertados en el fragmento {#assets-inserted-into-the-fragment}

If assets (e.g. images) have been inserted into the fragment itself (as [mixed-media fragments](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)), then the options for editing these assets in the page editor is limited.

Por ejemplo, para una imagen puede

* Recortar, girar o voltear la imagen.
* Añadir un título o texto alternativo.
* Especificar un tamaño.
* También puede configurar el diseño.

Otros cambios, como mover, copiar o eliminar, deben realizarse en el editor de fragmentos.

### Publicación {#publishing}

Los fragmentos deben publicarse para poder usarse en las páginas web publicadas:

* Los fragmentos se pueden publicar después de [crear el fragmento en la consola Recursos](/help/assets/content-fragments/content-fragments-managing.md#publishing-and-referencing-a-fragment).
* Si se usa un *fragmento sin publicar* en una página que se está publicando, también se puede publicar en ese momento el fragmento.
