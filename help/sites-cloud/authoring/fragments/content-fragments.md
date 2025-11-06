---
title: Fragmentos de contenido
description: Los fragmentos de contenido de Adobe Experience Manager as a Cloud Service le permiten diseñar, crear, depurar y utilizar contenido independiente del canal que también se puede utilizar al crear páginas.
exl-id: 7a44fc4e-3793-4aa3-8c21-db0567c93244
solution: Experience Manager Sites
feature: Authoring, Content Fragments
role: User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 82%

---

# Fragmentos de contenido {#content-fragments}

Los fragmentos de contenido de Adobe Experience Manager (AEM) as a Cloud Service se [crean y administran como recursos independientes de la página](/help/sites-cloud/administering/content-fragments/overview.md), lo que le permite crear contenido neutro con respecto al canal, además de variaciones (posiblemente específicas del canal). Puede utilizar estos fragmentos, y sus variaciones, al crear páginas de contenido.

>[!CAUTION]
>
>Esta página se debe leer junto con [Trabajo con fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md) (y las páginas relacionadas), ya que presenta terminología y conceptos básicos, junto con información sobre la creación y administración de fragmentos y la entrega de fragmentos de contenido estructurados a canales que no sean páginas de AEM.

>[!NOTE]
>
>Los fragmentos de contenido son una característica de **Sites**, pero se almacenan como **Assets**.
>
>Se administran principalmente con la consola **[Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console)**, aunque aún se pueden administrar desde la consola **[Assets](/help/assets/content-fragments/content-fragments-managing.md)**.
>
>El editor predeterminado para [Fragmentos de contenido: creación](/help/sites-cloud/administering/content-fragments/authoring.md) es el nuevo editor; se accede a él desde la consola **Fragmentos de contenido** y la consola **Assets**.
>
>Para usar el [editor original](/help/assets/content-fragments/content-fragments-variations.md), primero abre el nuevo editor y luego desactiva el conmutador **Nuevo editor**.

>[!NOTE]
>
>Los **fragmentos de contenido** y los **[fragmentos de experiencias](/help/sites-cloud/authoring/fragments/content-fragments.md)** son funciones distintas de AEM:
>
>* Los **fragmentos de contenido** son contenidos editoriales, con definición y estructura, pero sin diseño y/o maquetación visuales adicionales. Pueden utilizarse para acceder a datos estructurados, incluidos textos, números y fechas, entre otros.
>* Los **fragmentos de experiencias** son contenidos plenamente diseñados; un fragmento de una página web.
>
>Los fragmentos de experiencias pueden incluir contenido en forma de fragmentos, pero no lo contrario.
>
>Para obtener más información, consulte [Explicación de los fragmentos de contenido y de experiencias en AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=es#content-fragments).

Los fragmentos de contenido permiten lo siguiente:

* **Estrategia de campañas y marketing**
   * Revise el contenido a través de fragmentos de contenido administrados de forma centralizada.
* **Creative Pro**
   * Seguimiento de recursos creativos mediante colecciones asociadas con fragmentos de contenido.
* **Redactores**
   * Escriba en el editor de fragmentos de contenido de AEM.
   * Puede crear variaciones de contenido.
   * Puede asociar contenido relevante con el fragmento de contenido.
   * Puede utilizar el control de versiones/flujo de trabajo.
   * Puede compartir fragmentos de contenido.
   * Puede administrar traducciones de forma centralizada.
* **Productores y gestores de recorridos**
   * Seleccione fragmentos y variaciones predefinidos con la creación en AEM.
   * Puede confiar en que el fragmento y el contenido asociado estarán siempre actualizados, ya que los redactores y creativos realizan sus actualizaciones en fragmentos y activos administrados de forma centralizada.
   * Puede confiar en que el contenido multimedia asociado se seleccione en función de la relevancia.
   * Pueden crear variaciones de contenido ad hoc al instante garantizando al mismo tiempo que las variaciones siguen administradas de forma centralizada en el fragmento.

## Adición de un fragmento de contenido a la página       {#adding-a-content-fragment-to-your-page}

1. Abra la página para editarla.
2. Añada el componente **Fragmento de contenido**, bien desde el navegador **Componentes** o con **Insertar nuevo componente**.
3. Puede:
   * Abra el navegador **Recursos** y filtre por **Fragmentos de contenido** (el valor predeterminado es Imágenes). A continuación, arrastre el fragmento requerido a la instancia del componente.
   * Seleccione el componente de fragmento de contenido y, a continuación, **Configurar** en la barra de herramientas. En el cuadro de diálogo, puede abrir el cuadro de diálogo de selección para buscar y seleccionar el **fragmento de contenido** requerido.

   >[!NOTE]
   >
   >Otra posibilidad es arrastrar un fragmento de contenido específico directamente a la página. Esto creará automáticamente el componente asociado (fragmento de contenido).

4. En un primer momento, se muestra el contenido del elemento **General** y **Principal** (variación). Puede [seleccionar otros elementos y variaciones](#selecting-the-element-or-variation) si lo desea.

   ![Fragmentos de contenido en el explorador de recursos](/help/sites-cloud/authoring/assets/content-fragments.png)

   >[!NOTE]
   >
   >Para obtener más información acerca de otras funcionalidades de edición, consulte también lo siguiente:
   >
   >* [Diseño adaptable](/help/sites-cloud/authoring/page-editor/responsive-layout.md)
   >* [Edición del contenido de una página](/help/sites-cloud/authoring/page-editor/edit-content.md)

### Selección del elemento o la variación {#selecting-the-element-or-variation}

Abra el cuadro de diálogo **Configuración** para ajustar el fragmento que se utilizará en la página actual. El cuadro de diálogo puede depender del componente utilizado.

>[!NOTE]
>
>Consulte también [los componentes principales y el componente de fragmento de contenido](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=es)

En el cuadro de diálogo de configuración adecuado, puede seleccionar los parámetros disponibles, incluidos los siguientes:

* **Fragmento de contenido**
   * Especifique el fragmento que se va a utilizar.
* **Modo de visualización**:
   * **Elemento de texto único**
   * **Varios elementos**
* **Elemento**
   * Una selección está disponible dependiendo del modelo utilizado.

  >[!NOTE]
  >
  >Los elementos disponibles dependen de la plantilla utilizada.

* **Variación**
   * La opción predeterminada **Principal** siempre está disponible.
   * Hay disponible una selección si se crearon variaciones para el fragmento.

* **ID**

   * Atributo de **ID de HTML** que se aplicará al componente.

### Conexión rápida con el editor de fragmentos       {#quick-connection-to-fragment-editor}

Puede abrir el origen del fragmento para editarlo (el recurso) mediante el icono **Editar** de la barra de herramientas de componentes. Esto le permitirá [editar y gestionar el fragmento de contenido](/help/sites-cloud/administering/content-fragments/overview.md).

>[!CAUTION]
>
>Como siempre, editar el origen del fragmento afectará a todas las páginas que hacen referencia a dicho fragmento de contenido.

### Añadir contenido intermedio       {#adding-in-between-content}

Cuando se agrega un fragmento de contenido específico a la página, aparece un marcador de posición **Arrastre los componentes aquí** entre cada párrafo HTML (y en la parte superior/inferior) del fragmento.

Esto le permite agregar contenido adicional [intermedio (es decir, contenido intermedio)](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments) al contenido del fragmento (en cualquiera de los puntos disponibles), sin tener que cambiar el fragmento raíz.

Para el contenido intermedio puede hacer lo siguiente:

* Agregar componentes desde el [Explorador de componentes](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#components-browser)
* Agregar recursos desde el [explorador Assets](/help/sites-cloud/authoring/page-editor/editor-side-panel.md#assets-browser)
* Utilizar [contenido asociado](#using-associated-content) como fuente para el contenido intermedio.

>[!CAUTION]
>
>El contenido intermedio es contenido de página. No se almacena en el fragmento de contenido.

![Insertar componente](/help/sites-cloud/authoring/assets/content-fragments-insert.png)

>[!NOTE]
>
>También puede [insertar recursos visuales (imágenes) en el propio fragmento](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
>
>Los recursos visuales insertados en el propio fragmento se adjuntan al párrafo anterior del fragmento. Esto significa que no puede colocar contenido intermedio entre un recurso visual y el párrafo precedente. Si necesita este nivel de conexión, puede agregar la imagen al fragmento (como un [fragmento de medios mixtos](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)).

>[!CAUTION]
>
>Una vez añadido contenido intermedio a un fragmento de contenido en la página, al cambiar la estructura del fragmento de contenido subyacente (es decir, en el editor de fragmentos de contenido) se pueden generar resultados erróneos o inesperados.
>
>Cuando esto sucede, el contenido intermedio se mantiene tal cual:
>
>* Los componentes intermedios tienen una posición absoluta dentro de la secuencia de componentes en el flujo del fragmento. Esta posición no cambia, aunque varíe el contenido de los párrafos del fragmento.
>
>  Por este motivo, es posible que parezca que la posición relativa ha cambiado, ya que los párrafos intermedios no tienen relación contextual con los párrafos (del fragmento) junto a los que se sitúan.
>
>* Sin embargo, en caso de que exista conflicto entre las dos estructuras de párrafo, el contenido intermedio no se muestra (aunque siga presente internamente).

### Uso de contenido asociado       {#using-associated-content}

Si tiene [contenido asociado](/help/assets/content-fragments/content-fragments-assoc-content.md) con el [fragmento de contenido](/help/assets/content-fragments/content-fragments.md), estos recursos estarán disponibles en el panel lateral (después de colocar el fragmento en la página de contenido). El contenido asociado es en realidad una fuente especial de contenido para [contenido intermedio](/help/assets/content-fragments/content-fragments.md#in-between-content-when-page-authoring-with-content-fragments).

>[!NOTE]
>
>Existen varios métodos para añadir [recursos visuales (por ejemplo, imágenes)](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets) al fragmento o la página.

>[!NOTE]
>
>Si tiene varios fragmentos de contenido en la página, la pestaña **Contenido asociado** mostrará los recursos oportunos para todos los fragmentos.

Una vez que haya añadido un fragmento con contenido asociado a la página, se abrirá una nueva pestaña (**Contenido asociado**) en el panel lateral.

Desde aquí podrá arrastrar los recursos a la ubicación requerida (a un componente existente o a la posición que le interese donde se creará el componente correspondiente):

![Inserción de una imagen](/help/sites-cloud/authoring/assets/content-fragments-image.png)

### Recursos insertados en el fragmento {#assets-inserted-into-the-fragment}

Si se insertan recursos (por ejemplo, imágenes) en el fragmento en sí (como [fragmentos de medios mixtos](/help/assets/content-fragments/content-fragments.md#fragments-with-visual-assets)), las opciones para modificarlos en el editor de páginas son limitadas.

Por ejemplo, para una imagen puede

* Recortar, rotar o voltear la imagen.
* Añadir un título o texto alternativo.
* Especificar un tamaño.
* También puede configurar el diseño.

Otros cambios, como mover, copiar o eliminar, deben efectuarse en el editor de fragmentos.

### Publicación {#publishing}

Los fragmentos deben publicarse para poder usarse en las páginas web publicadas:

* Los fragmentos se pueden publicar después de [crear el fragmento en la consola Fragmentos de contenido](/help/sites-cloud/administering/content-fragments/managing.md#publishing-and-previewing-a-fragment).
* Si se usa un *fragmento sin publicar* en una página que se está publicando, también se puede publicar en ese momento el fragmento.

## Exportación de fragmentos de contenido {#exporting-content-fragments}

Para exportar a Adobe Target, se puede utilizar JSON para enviar el fragmento. Consulte:

* [Integración con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Exportación de fragmentos de contenido a Adobe Target](/help/sites-cloud/integrating/content-fragments-target.md)
