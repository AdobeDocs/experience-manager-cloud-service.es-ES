---
title: Fragmentos de experiencias
description: Utilice los fragmentos de experiencia Adobe Experience Manager as a Cloud Service para que sus experiencias puedan reutilizarse y adaptarse.
exl-id: 9dc33677-141f-47e5-a01e-6c7488686314
source-git-commit: ccf5cdf56867ca077d7ff71bfb2f1f4af1b32bd9
workflow-type: tm+mt
source-wordcount: '1971'
ht-degree: 79%

---

# Fragmentos de experiencias {#experience-fragments}

Dentro de Adobe Experience Manager as a Cloud Service, un fragmento de experiencia:

* es un grupo de uno o más componentes
* incluye contenido y diseño
* se le puede hacer referencia dentro de las páginas
* pueden contener cualquier componente

Un fragmento de experiencia:

* Forma parte de una experiencia (página).
* Se puede utilizar en varias páginas.
* Se basa en una plantilla (solo editable) para definir la estructura y los componentes.
* Esta plantilla se utiliza para crear la *página raíz* del Fragmento de experiencia.
* Se compone de uno o varios componentes, con diseño, en un sistema de párrafos.
* Puede contener otros fragmentos de experiencias.
* Se puede combinar con otros componentes (incluidos otros fragmentos de experiencias) para formar una página completa (experiencia).
* Se pueden crear una o más variaciones basadas en la página raíz.
* Estas pueden compartir contenido o componentes.
* Se puede desglosar en bloques de construcción que se pueden utilizar en varias variaciones del fragmento.

Puede utilizar los fragmentos de experiencias:

* Si un creador desea reutilizar partes (un fragmento de una experiencia) de una página.
Sin fragmentos de experiencias, el creador tendría que copiar y pegar ese fragmento. Crear y mantener estas experiencias de copia y pegado es un proceso laborioso y es posible que el usuario cometa errores.
Los fragmentos de experiencias eliminan la necesidad de copiar y pegar.
* Para admitir el caso práctico de CMS descentralizado.
Los autores quieren utilizar AEM solo para la creación, pero no para la entrega al cliente. Un punto de contacto o sistema de terceros consumiría esa experiencia y luego la entregaría al usuario final.

>[!NOTE]
>
>La escritura de acceso para fragmentos de experiencias requiere que la cuenta de usuario se registre en el grupo:
>
>* `experience-fragments-editors`
>
>Si tiene algún problema, póngase en contacto con el administrador del sistema.

## ¿Cuándo se deben utilizar los fragmentos de experiencias?   {#when-should-you-use-experience-fragments}

Los fragmentos de experiencias deben usarse en los siguientes casos:

* Cuando desee reutilizar experiencias.
   * Experiencias que se reutilizarán con un contenido igual o similar.
* Cuando se utiliza AEM como plataforma de distribución de contenido de terceros.
   * Cualquier solución que desee utilizar AEM como plataforma de distribución de contenido.
   * Incrustación de contenido en puntos de contacto de terceros.
* Si tiene una experiencia con diferentes variaciones o representaciones.
   * Variaciones de canal o específicas de contexto.
   * Experiencias que tiene sentido agrupar; por ejemplo, una campaña con distintas experiencias en diferentes canales.
* Al utilizar el comercio omnicanal.
   * Convertir los puntos de contacto en transaccionales.

## Organización de los fragmentos de experiencias {#organizing-your-experience-fragments}

Se recomienda:
* usar carpetas para organizar los fragmentos de experiencias,

* [configurar las plantillas permitidas en estas carpetas](#configure-allowed-templates-folder).

La creación de carpetas permite:

* crear una estructura significativa para los fragmentos de experiencias; por ejemplo, según la clasificación.

   >[!NOTE]
   >
   >No es necesario alinear la estructura de los fragmentos de experiencias con la estructura de página del sitio.

* [asignar las plantillas permitidas en el nivel de carpeta](#configure-allowed-templates-folder)

   >[!NOTE]
   >
   >Puede utilizar el [editor de plantillas](/help/sites-cloud/authoring/features/templates.md) para crear su propia plantilla.

El proyecto WKND estructura algunos fragmentos de experiencias según `Contributors`. La estructura utilizada también ilustra cómo se pueden utilizar otras funciones, como la Administración de varios sitios (incluidas las copias de idiomas).

Consulte:

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![Carpetas para fragmentos de experiencias](/help/sites-cloud/authoring/assets/xf-folders.png)

## Creación y configuración de una carpeta para los fragmentos de experiencias {#creating-and-configuring-a-folder-for-your-experience-fragments}

Para crear y configurar una carpeta para los fragmentos de experiencias, se recomienda:

1. [Crear una carpeta](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-folder).

1. [Configurar las plantillas de fragmento de experiencia permitidas para esa carpeta](#configure-allowed-templates-folder).

>[!NOTE]
>
>También es posible configurar las plantillas [permitidas para su instancia](#configure-allowed-templates-instance), pero este método **no se recomienda**, ya que los valores se pueden sobrescribir tras la actualización.

### Configurar las plantillas permitidas para la carpeta {#configure-allowed-templates-folder}

>[!NOTE]
>
>Este es el método recomendado para especificar las **plantillas permitidas**, ya que los valores no se sobrescriben tras la actualización.

1. Vaya a la carpeta de **fragmentos de experiencias** necesaria.

1. Seleccione la carpeta y, a continuación, vaya a **Propiedades**.

1. Especifique la expresión regular para recuperar las plantillas necesarias en el campo **Plantillas permitidas**.

   Por ejemplo:
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   Consulte:
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![Propiedades de fragmentos de experiencias: plantillas permitidas](/help/sites-cloud/authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >Para obtener más información, consulte [Plantillas para fragmentos de experiencias](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments).

1. Seleccione **Guardar y cerrar**.

### Configure las plantillas permitidas para la instancia {#configure-allowed-templates-instance}

>[!CAUTION]
>
>No se recomienda cambiar las **plantillas permitidas** por este método, ya que las plantillas especificadas se pueden sobrescribir tras la actualización.
>
>Utilice este cuadro de diálogo únicamente con fines informativos.

1. Vaya a la consola de **fragmentos de experiencias** indicada.

1. Seleccione las **opciones de configuración**:

   ![Botón Configuración](/help/sites-cloud/authoring/assets/xf-18.png)

1. Especifique las plantillas necesarias en el cuadro de diálogo **Configurar fragmentos de experiencias**:

   ![Configurar Fragmentos de experiencias](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >Para obtener más información, consulte [Plantillas para fragmentos de experiencias](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments).

1. Seleccione **Guardar**.

## Creación de un fragmento de experiencia {#creating-an-experience-fragment}

Para crear un fragmento de experiencia:

1. Seleccione **fragmentos de experiencias** desde la navegación global.

   ![Fragmentos de experiencias en el panel de navegación](/help/sites-cloud/authoring/assets/xf-01.png)

1. Vaya a la carpeta indicada y seleccione **Crear**:

   ![Creación de una carpeta para fragmentos de experiencias](/help/sites-cloud/authoring/assets/xf-02.png)

1. Seleccione **Fragmento de experiencia** para abrir el asistente **Crear fragmento de experiencia**.

   Seleccione la **plantilla** adecuada y, a continuación, **Siguiente**:

   ![Selección de una plantilla de fragmento de experiencia](/help/sites-cloud/authoring/assets/xf-03.png)


1. Introduzca las **propiedades** del **fragmento de experiencia**.

   Es obligatorio escribir un **título**. Si el **nombre** se deja en blanco, se derivará del **título**.

   ![Propiedades del fragmento de experiencia](/help/sites-cloud/authoring/assets/xf-04.png)

   >[!NOTE]
   >
   >Las etiquetas de la plantilla de Fragmento de experiencia no se combinarán con etiquetas en esta página raíz del Fragmento de experiencia.
   >
   >Son totalmente independientes.

1. Haga clic en **Crear**.

   Se mostrará un mensaje. Seleccione:

   * **Listo** para volver a la consola
   * **Abrir** para abrir el editor de fragmentos

## Edición del fragmento de experiencia {#editing-your-experience-fragment}

El editor de fragmentos de experiencias ofrece funcionalidades similares a las del editor de páginas.

>[!NOTE]
>
>Consulte [Edición del contenido de una página](/help/sites-cloud/authoring/fundamentals/editing-content.md) para obtener más información acerca de cómo utilizar el editor de páginas.

El siguiente procedimiento de ejemplo ilustra cómo crear un teaser para un producto:

1. Arrastre y suelte el componente necesario desde el [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

1. Según el componente:
   * Añada contenido o recursos según sea necesario.
   * Configure las propiedades según sea necesario.

1. Agregue más componentes según sea necesario.

Por ejemplo: `http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![Fragmento de experiencia en la página](/help/sites-cloud/authoring/assets/xf-05.png)

## Creación de una variación de fragmento de experiencia {#creating-an-experience-fragment-variation}

Puede crear varias variaciones para este fragmento de experiencia en función de sus necesidades:

1. Abra la página para su [edición](#editing-your-experience-fragment).
1. Abra la pestaña **Variaciones**.

   ![Creación de una variación de fragmento de experiencia](/help/sites-cloud/authoring/assets/xf-06.png)

1. La opción **Crear** le permite crear:

   * **Variación**
   * **Variación como Live Copy**.

1. Defina las propiedades requeridas:

   * **Plantilla**
   * **Título**
   * **Nombre**: si se deja en blanco, se deriva del título
   * **Descripción**
   * **Etiquetas de variación**

   Por ejemplo:

   ![Propiedades de la variación](/help/sites-cloud/authoring/assets/xf-07.png)


1. Confirme con **Listo** para mostrar la nueva variación en el panel.

## Uso de los fragmentos de experiencias {#using-your-experience-fragment}

Ahora puede utilizar el fragmento de experiencia para crear páginas:

1. Abra cualquier página para su edición.

1. Cree una instancia del componente Fragmento de experiencia, dentro del sistema de párrafos de página:

1. Agregue el fragmento de experiencia real a la instancia de componente; o bien:

   * Arrastre el fragmento necesario desde el explorador de activos y colóquelo en el componente.
   * Seleccione **Configurar** en la barra de herramientas del componente y especifique el fragmento que quiere utilizar; confirme con **Listo**.

   >[!NOTE]
   >
   >La opción Editar, en la barra de herramientas del componente, funciona como un método abreviado para abrir el fragmento en el editor de fragmentos.

Por ejemplo: `http://<host>:<port>/editor.html/content/wknd/language-masters/en/about-us.html`

![Fragmento de experiencia en el editor de páginas](/help/sites-cloud/authoring/assets/xf-08.png)

## Componentes {#building-blocks}

Puede seleccionar uno o varios componentes para crear un bloque de creación y así reciclarlo en el fragmento:

### Crear un bloque de creación {#creating-a-building-block}

Para crear un nuevo bloque de creación:

1. En el editor de fragmentos de experiencias, seleccione los componentes que quiere reutilizar:

   ![Seleccionar componente para bloque de creación](/help/sites-cloud/authoring/assets/xf-09.png)

1. En la barra de herramientas de componentes, seleccione **Convertir en bloque de creación**:

   ![Botón Bloque de creación](/help/sites-cloud/authoring/assets/xf-10.png)

1. Escriba el nombre del **bloque de creación** y confirme con **Convertir**:

   ![Bloque de creación de nombres](/help/sites-cloud/authoring/assets/xf-11.png)

1. El **bloque de creación** aparece en la pestaña izquierda (**Local**) y se puede seleccionar para realizar más acciones:

   ![Bloque de creación en el carril](/help/sites-cloud/authoring/assets/xf-12.png)

#### Administración de un bloque de creación {#managing-a-building-block}

El bloque de creación se puede ver en la pestaña **Bloques de creación**. Para cada bloque, están disponibles las siguientes acciones:

* **Ir a la variación principal**: abrir la variación de la página raíz en una nueva pestaña
* **Cambiar nombre**
* **Eliminar**

![Administración de bloques de creación](/help/sites-cloud/authoring/assets/xf-13.png)

#### Uso de un bloque de creación {#using-a-building-block}

Puede arrastrar el bloque de creación al sistema de párrafos de cualquier fragmento, como con cualquier componente.

Al editar un fragmento de experiencia, los bloques de creación disponibles se muestran en la pestaña izquierda. Puede filtrarlos siguiendo los criterios siguientes:

* **Local**: bloques de creación a partir del fragmento de experiencia actual.
* **Todo**: bloques de creación a partir de todos los fragmentos.

![Seleccionar bloques de creación](/help/sites-cloud/authoring/assets/xf-14.png)

## Personalización en el fragmento de experiencia {#personalization-experience-fragment}

La personalización en el fragmento de experiencia le permite, como especialista en marketing, definir audiencias de destino para el fragmento de experiencia solo una vez y, a continuación, reutilizar el fragmento en cualquier página. Así pues:

* elimina la necesidad de especificar las variaciones necesarias para cada audiencia cada vez que se utiliza el fragmento
* mantiene el estilo en todas las ofertas

Puede crear un fragmento de experiencia con varios componentes agrupados dentro de este fragmento único. También puede crear variaciones del fragmento para cada segmento de audiencia específico y luego reutilizar estos fragmentos de experiencias en los canales requeridos.

La personalización se logra definiendo la variable **Personalización** propiedades en el fragmento de experiencia o la variación, o en la carpeta que contiene los fragmentos; esto significa que la herencia puede anular las propiedades de personalización.

La configuración de estas propiedades también habilita la variable **Segmentación** en el editor de fragmentos de experiencias.

### Definición de la personalización para el fragmento de experiencias {#defining-personalization-experience-fragment}

Para personalizar el fragmento:

1. Vaya a la ubicación requerida en la **Fragmentos de experiencias** consola.

1. Seleccione una carpeta o el fragmento y, a continuación, **Propiedades** en la barra de herramientas.

   >[!NOTE]
   >
   >Las propiedades de personalización definidas en una carpeta las heredarán todas las carpetas secundarias a través del subárbol y los fragmentos de experiencias (y variaciones) dentro de ese subárbol. Se pueden anular rompiendo la herencia.

1. Abra el **Personalización** para definir y guardar la configuración. Por ejemplo, en una carpeta:

   ![Fragmento de experiencia: propiedades de personalización](/help/sites-cloud/authoring/assets/xf-personalization-properties.png)

   >[!CAUTION]
   >
   >Cuando un fragmento está incrustado en una página Sitios, y **Personalización** se ha configurado, entonces solo se utilizará la versión de personalización de la página en el momento de procesar la página.
   >
   >Para que la segmentación realizada en los componentes de un fragmento funcione en la renderización de la página, se deben cumplir las siguientes condiciones:
   >
   >La variable **Ruta de ContextHub** seleccionados en el **Personalización** debe ser:
   >
   >* la misma ruta que la configurada para la página en la que se representará el fragmento
      >O bien:
   >* una ruta que contiene un subconjunto de los almacenes definidos en ContextHub configurados para la página

   >
   > 
La variable **Ruta de segmentos** seleccionados en el **Personalización** debe ser:
   * la misma ruta que la configurada para la página en la que se representará el fragmento o
   * una ruta que contiene un subconjunto de los segmentos configurados para la página


### Definición del objetivo para el fragmento de experiencia {#defining-targeting-experience-fragment}

Una vez configuradas las propiedades de personalización, el modo Segmentación estará disponible cuando se abra el fragmento para editarlo.

![Editor de fragmentos de experiencias: modo de Orientación](/help/sites-cloud/authoring/assets/xf-targeting-mode.png)

Este modo funciona del mismo modo que para la edición de páginas. Consulte [Modo de orientación del Editor de páginas](/help/sites-cloud/authoring/personalization/targeted-content.md) para obtener más información.

## Detalles del fragmento de experiencia {#details-of-your-experience-fragment}

Se pueden ver los detalles del fragmento:

1. Vaya a la ubicación de los fragmentos de experiencias (no vaya más allá hacia las variaciones dentro del fragmento).
Los detalles se muestran en todas las vistas de la consola de **fragmentos de experiencias**, con una **vista de lista**[ que incluye los detalles de una exportación a destino](/help/sites-cloud/integrating/integrating-adobe-target.md):

   ![Detalles del fragmento de experiencia](/help/sites-cloud/authoring/assets/xf-15.png)

1. Al abrir las **propiedades** del fragmento de experiencia:

   ![Botón Propiedades](/help/sites-cloud/authoring/assets/xf-16.png)

   Las propiedades están disponibles en varias pestañas:

   >[!CAUTION]
   Estas pestañas se muestran al abrir **Propiedades** desde la consola fragmentos de experiencias.
   Si se selecciona **Abrir propiedades** al editar un fragmento de experiencia, se muestran las [propiedades de página](/help/sites-cloud/authoring/fundamentals/page-properties.md) correspondientes.

   ![Propiedades del fragmento de experiencia](/help/sites-cloud/authoring/assets/xf-17.png)

   * **Básico**
      * **Título**: obligatorio
      * **Descripción**
      * **Etiquetas**
      * **Número total de variantes**: solo información
      * **Número de variantes web**: solo información
      * **Número de variantes que no son de web**:solo información
      * **Número de páginas que utilizan este fragmento**: solo información
   * **Cloud Services**
      * **Configuración de nube**
      * **Configuraciones de Cloud Service**
      * **ID de página de Facebook**
      * **Tablero de Pinterest**
   * **Referencias**
      * Una lista de referencias
   * **Personalización**
      * **Ruta de ContextHub**
      * **Ruta de segmentos**
      * **Marca**

## Representación HTML sin formato {#the-plain-html-rendition}

Uso del selector de `.plain.` en la URL; puede acceder a la representación HTML sin formato desde el explorador.

>[!NOTE]
Aunque esta opción está disponible directamente desde el explorador, [el objetivo principal es permitir a otras aplicaciones (por ejemplo, aplicaciones web de terceros o implementaciones móviles personalizadas) acceder al contenido del fragmento de experiencia directamente, únicamente mediante la URL](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## Publicación de fragmentos de experiencias {#publishing-experience-fragments}

La publicación del fragmento de experiencia es básicamente la misma que la [publicación de una página](/help/sites-cloud/authoring/fundamentals/publishing-pages.md) (desde la consola o el editor de fragmentos de experiencias).

También puede [publicar en previsualización](/help/sites-cloud/authoring/fundamentals/previewing-content.md) (desde la consola o el editor de fragmentos de experiencias).

## Exportación de fragmentos de experiencias   {#exporting-experience-fragments}

De forma predeterminada, los fragmentos de experiencias se envían en formato HTML. Los canales de AEM y los canales similares de terceros pueden usar esta opción.

Para la exportación a Adobe Target, también se puede utilizar JSON. Consulte:

* [Integración con Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Exportación de fragmentos de experiencias a Adobe Target](/help/sites-cloud/integrating/experience-fragments-target.md)
