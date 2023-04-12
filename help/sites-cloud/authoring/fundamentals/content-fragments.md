---
title: Fragmentos de contenido
description: Los fragmentos de contenido de Adobe Experience Manager as a Cloud Service le permiten diseñar, crear, depurar y utilizar contenido independiente de las páginas.
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
source-git-commit: 7ce05d282d553c5552cd828d08aaf6b7b5fb4e05
workflow-type: tm+mt
source-wordcount: '1227'
ht-degree: 63%

---

# Fragmentos de contenido {#content-fragments}

Los fragmentos de contenido de Adobe Experience Manager (AEM) as a Cloud Service se [crean y administran como recursos independientes de las páginas](/help/sites-cloud/administering/content-fragments/content-fragments.md).

Permiten crear contenido neutro con respecto al canal, así como variaciones (posiblemente específicas del canal). Después se pueden usar estos fragmentos, y sus variaciones, al crear páginas de contenido.

Junto con el exportador JSON actualizado, los fragmentos de contenido estructurados también se pueden utilizar para distribuir contenidos de AEM mediante servicios de contenido a canales en lugar de páginas de AEM.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencias](/help/sites-cloud/authoring/fundamentals/experience-fragments.md)** son funciones distintas de AEM:
>* Los **fragmentos de contenido** son contenidos editoriales, con definición y estructura, pero sin diseño y/o maquetación visuales adicionales. Pueden utilizarse para acceder a datos estructurados, incluidos textos, números y fechas, entre otros.
>* Los **fragmentos de experiencias** son contenidos plenamente diseñados; un fragmento de una página web. 
>
>Los fragmentos de experiencias pueden incluir contenido en forma de fragmentos, pero no lo contrario.
>
>Para obtener más información, consulte también [Explicación de los fragmentos de contenido y de experiencias en AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=es#content-fragments).

>[!CAUTION]
>
>Esta página se debe leer junto con [Trabajo con fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md) (y las páginas relacionadas), ya que introduce terminología y conceptos básicos, además de tratar la creación y gestión de fragmentos.

Los fragmentos de contenido permiten:

* **Estrategia de campañas y marketing**
   * Revise el contenido a través de fragmentos de contenido administrados centralmente.
* **Creative Pro**
   * Seguimiento de recursos creativos mediante colecciones asociadas con fragmentos de contenido.
* **Copiar escritores**
   * Escriba en el editor de fragmentos de contenido de AEM.
   * Pueden crear variaciones de contenido.
   * Puede asociar contenido relevante con el fragmento de contenido.
   * Puede utilizar el control de versiones/flujo de trabajo.
   * Pueden compartir fragmentos de contenido.
   * Puede administrar traducciones de forma centralizada.
* **Productores y gestores de Recorridos**
   * Seleccione fragmentos y variaciones predefinidos con la creación en AEM.
   * Pueden confiar en fragmentos y contenido asociado siempre estando actualizado a medida que creadores y redactores realizan sus actualizaciones en recursos y fragmentos administrados centralmente.
   * Pueden depender del contenido multimedia asociado seleccionado para su relevancia.
   * Puede crear variaciones de contenido ad-hoc sobre la marcha, asegurándose de que dichas variaciones permanezcan administradas de forma centralizada en el fragmento.

## Adición de un fragmento de contenido a la página       {#adding-a-content-fragment-to-your-page}

1. Abra la página para editarla. 
2. Añada el componente **Fragmento de contenido**, bien desde el navegador **Componentes** o con **Insertar nuevo componente**. 
3. Puede:
   * Abra el navegador **Recursos** y filtre por **Fragmentos de contenido** (el valor predeterminado es Imágenes). A continuación, arrastre el fragmento requerido a la instancia del componente.
   * Seleccione el componente de fragmento de contenido y, a continuación, **Configurar** en la barra de herramientas. En el cuadro de diálogo, puede abrir el cuadro de diálogo de selección para buscar y seleccionar el **fragmento de contenido** requerido.

   >[!NOTE]
   >
   >Otra posibilidad es arrastrar un fragmento de contenido específico directamente a la página. Esto creará automáticamente el componente asociado (fragmento de contenido). 

4. En un primer momento se muestra el contenido del elemento **Principal** y **Maestro** (variación). Puede [seleccionar otros elementos y variaciones](#selecting-the-element-or-variation) si lo desea.

   ![Fragmentos de contenido en el explorador de recursos](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >Para obtener más información sobre las funciones de edición adicionales, consulte también:
   >
   >* [Diseño adaptable](/help/sites-cloud/authoring/features/responsive-layout.md)
   >* [Edición del contenido de una página](/help/sites-cloud/authoring/fundamentals/editing-content.md)


### Selección del elemento o la variación {#selecting-the-element-or-variation}

Abra el **Configuración** para configurar el fragmento que se utilizará en la página actual. El cuadro de diálogo puede depender del componente utilizado.

>[!NOTE]
>
>Consulte también [los componentes principales y el componente de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es)

En el cuadro de diálogo de configuración adecuado, puede seleccionar los parámetros disponibles, incluidos:

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
   * Habrá una selección disponible si se crearon variaciones para el fragmento.

* **ID**

   * Atributo de **ID de HTML** que se aplicará al componente.

### Conexión rápida con el editor de fragmentos       {#quick-connection-to-fragment-editor}

Puede abrir el origen del fragmento para editarlo (el recurso) mediante el icono **Editar** de la barra de herramientas de componentes. Esto le permitirá [editar y gestionar el fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md). 

>[!CAUTION]
>
>Como siempre, editar el origen del fragmento afectará a todas las páginas que hacen referencia a dicho fragmento de contenido.

### Añadir contenido intermedio       {#adding-in-between-content}

Cuando se agrega un fragmento de contenido específico a la página, aparece una variable **Arrastre los componentes aquí** marcador de posición entre cada párrafo de HTML (y en la parte superior/inferior) del fragmento.

Esto le permite añadir contenido adicional [intermedio (es decir, entre contenido)](/help/sites-cloud/administering/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) el contenido del fragmento (en cualquiera de los puntos disponibles), sin tener que cambiar el fragmento raíz.

Para el contenido intermedio puede:

* Añadir componentes desde el [Navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).
* Agregue recursos desde [Navegador de recursos](/help/sites-cloud/authoring/fundamentals/environment-tools.md#assets-browser).
* Utilizar [contenido asociado](#using-associated-content) como fuente para el contenido intermedio.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

![Insertar componente](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>También puede [insertar recursos visuales (imágenes) en el propio fragmento](/help/sites-cloud/administering/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Los recursos visuales insertados en el propio fragmento se adjuntan al párrafo anterior del fragmento. Esto significa que no puede colocar contenido intermedio entre un recurso visual y el párrafo precedente. Si necesita este nivel de conexión, puede agregar la imagen al fragmento (como un [fragmento de medios mixtos](/help/sites-cloud/administering/content-fragments/content-fragments.md#fragments-with-visual-assets)).

>[!CAUTION]
>
>Una vez añadido contenido intermedio a un fragmento de contenido en la página, al cambiar la estructura del fragmento de contenido subyacente (es decir, en el editor de fragmentos de contenido) se pueden generar resultados erróneos o inesperados.
>
>Cuando esto sucede, el contenido intermedio se mantiene tal cual:
>
>* Los componentes intermedios tienen una posición absoluta dentro de la secuencia de componentes en el flujo del fragmento. Esta posición no cambia, incluso cuando cambia el contenido de los párrafos del fragmento.
>
>  Por este motivo, es posible que parezca que la posición relativa ha cambiado, ya que los párrafos intermedios no tienen relación contextual con los párrafos (del fragmento) junto a los que se sitúan.
>* Sin embargo, en caso de que exista conflicto entre las dos estructuras de párrafo, el contenido intermedio no se muestra (aunque siga presente internamente).


### Uso de contenido asociado       {#using-associated-content}

Si tiene [contenido asociado](/help/sites-cloud/administering/content-fragments/content-fragments-assoc-content.md) con el [fragmento de contenido](/help/sites-cloud/administering/content-fragments/content-fragments.md), estos recursos estarán disponibles en el panel lateral (después de colocar el fragmento en la página de contenido). El contenido asociado es en realidad una fuente especial de contenido para [contenido intermedio](/help/sites-cloud/administering/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments).

>[!NOTE]
>
>Existen varios métodos para añadir [recursos visuales (por ejemplo, imágenes)](/help/sites-cloud/administering/content-fragments/content-fragments.md#fragments-with-visual-assets) al fragmento o la página.

>[!NOTE]
>
>Si tiene varios fragmentos de contenido en la página, la variable **Contenido asociado** muestra los recursos adecuados para todos los fragmentos.

Una vez que haya añadido un fragmento con contenido asociado a la página, agregue una nueva pestaña (**Contenido asociado**) se abre en el panel lateral.

Desde aquí podrá arrastrar los recursos a la ubicación requerida (en un componente existente o a la posición que le interese donde se creará el componente correspondiente):

![Inserción de una imagen](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### Recursos insertados en el fragmento {#assets-inserted-into-the-fragment}

Si se insertan recursos (por ejemplo, imágenes) en el fragmento en sí (como [fragmentos de medios mixtos](/help/sites-cloud/administering/content-fragments/content-fragments.md#fragments-with-visual-assets)), las opciones para modificarlos en el editor de páginas son limitadas.

Por ejemplo, para una imagen puede

* Recortar, rotar o voltear la imagen.
* Añada un título o texto alternativo.
* Especifique un tamaño.
* También puede configurar el diseño.

Otros cambios, como mover, copiar o eliminar, deben realizarse en el editor de fragmentos.

### Publicación {#publishing}

Los fragmentos deben publicarse para poder usarse en las páginas web publicadas:

* Los fragmentos se pueden publicar después de [crear el fragmento en la consola Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/content-fragments-managing.md#publishing-and-referencing-a-fragment).
* Si se usa un *fragmento sin publicar* en una página que se está publicando, también se puede publicar en ese momento el fragmento.

## Exportación de fragmentos de contenido {#exporting-content-fragments}

Para exportar a Adobe Target, JSON se puede utilizar para enviar el fragmento. Consulte:

* [Integración con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Exportación de fragmentos de contenido a Adobe Target](/help/sites-cloud/integrating/content-fragments-target.md)
