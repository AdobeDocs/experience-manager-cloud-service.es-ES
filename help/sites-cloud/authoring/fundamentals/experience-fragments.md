---
title: Fragmentos de experiencias
description: Utilice Adobe Experience Manager como fragmentos de experiencia de servicios en la nube para que sus experiencias sean reutilizables y flexibles.
translation-type: tm+mt
source-git-commit: b7a2e86de27dbfcdecaf3a2bc1984678b7b69375

---


# Fragmentos de experiencias {#experience-fragments}

Dentro de Adobe Experience Manager como servicio de nube, un fragmento de experiencia:
* es un grupo de uno o más componentes
* incluye contenido y diseño
* se puede hacer referencia dentro de las páginas
* puede contener cualquier componente

Un fragmento de experiencias:

* Forma parte de una experiencia (página).
* Se puede utilizar en varias páginas.
* Se basa en una plantilla (solo editable) para definir la estructura y los componentes.
* Se compone de uno o varios componentes, con diseño, en un sistema de párrafos.
* Puede contener otros fragmentos de experiencias.
* Se puede combinar con otros componentes (incluidos otros fragmentos de experiencias) para formar una página completa (experiencia).
* Puede tener diferentes variaciones y compartir el contenido o los componentes.
* Se puede desglosar en bloques de construcción que se pueden utilizar en varias variaciones del fragmento.

Puede utilizar los fragmentos de experiencia:

* Si un autor desea reutilizar partes (un fragmento de una experiencia) de una página.
Sin fragmentos de experiencia, el autor tendría que copiar y pegar ese fragmento. Crear y mantener estas experiencias de copia y pegado es un proceso laborioso y es posible que el usuario cometa errores.
Los fragmentos de experiencias eliminan la necesidad de copiar y pegar.
* Para admitir el caso de uso CMS sin cabezal.
Los autores solo desean utilizar AEM para la creación, pero no para la entrega al cliente. Un punto de contacto o sistema de terceros consumiría esa experiencia y luego la entregaría al usuario final.

>[!NOTE]
>
>La escritura de acceso para fragmentos de experiencias requiere que la cuenta de usuario se registre en el grupo:
>
>* `experience-fragments-editors`
>
>
Si tiene algún problema, póngase en contacto con el administrador del sistema.

## ¿Cuándo se deben utilizar los fragmentos de experiencias? {#when-should-you-use-experience-fragments}

Los fragmentos de experiencias deben usarse en los siguientes casos:

* Cuando desee reutilizar experiencias.
   * Experiencias que se reutilizarán con un contenido igual o similar.
* Cuando se utiliza AEM como plataforma de distribución de contenido de terceros.
   * Cualquier solución que desee utilizar AEM como plataforma de distribución de contenido.
   * Incrustación de contenido en puntos de contacto de terceros.
* Si tiene una experiencia con diferentes variaciones o representaciones.
   * Variaciones de canal o específicas de contexto.
   * Experiencias que tienen sentido agrupar; por ejemplo, una campaña con diferentes experiencias en los distintos canales.
* Al utilizar el comercio omnicanal.
   * Uso compartido de contenido relacionado con el comercio en canales de [redes sociales](/help/implementing/developing/extending/experience-fragments.md#social-variations) a escala.
   * Convertir los puntos de contacto en transaccionales.

## Organización de los fragmentos de experiencias {#organizing-your-experience-fragments}

Se recomienda:
* utilice carpetas para organizar los fragmentos de experiencias,

* [configure las plantillas permitidas en estas carpetas](#configure-allowed-templates-folder).

La creación de carpetas permite:

* cree una estructura significativa para los fragmentos de experiencia; por ejemplo, según la clasificación

   >[!NOTE]
   >
   >No es necesario alinear la estructura de los fragmentos de experiencia con la estructura de página del sitio.

* [asignar las plantillas permitidas en el nivel de carpeta](#configure-allowed-templates-folder)

   >[!NOTE]
   >
   >Puede utilizar el [editor de plantillas](/help/sites-cloud/authoring/features/templates.md) para crear su propia plantilla.

El proyecto WKND estructura algunos fragmentos de experiencias según `Contributors`. La estructura utilizada también ilustra cómo se pueden utilizar otras funciones, como la Administración de múltiples sitios (incluidas las copias de idiomas).

Consulte:

`http://localhost:4502/aem/experience-fragments.html/content/experience-fragments/wknd/language-masters/en/contributors/kumar-selveraj/master`

![Carpetas para fragmentos de experiencias](/help/sites-cloud/authoring/assets/xf-folders.png)

## Creación y configuración de una carpeta para los fragmentos de experiencia {#creating-and-configuring-a-folder-for-your-experience-fragments}

Para crear y configurar una carpeta para sus fragmentos de experiencias, se recomienda:

1. [Cree una carpeta](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-folder).

1. [Configure las plantillas de fragmento de experiencia permitidas para esa carpeta](#configure-allowed-templates-folder).

>[!NOTE]
>
>También es posible configurar las plantillas [permitidas para su instancia](#configure-allowed-templates-instance), pero este método **no se recomienda** , ya que los valores se pueden sobrescribir tras la actualización.

### Configurar las plantillas permitidas para la carpeta {#configure-allowed-templates-folder}

>[!NOTE]
>
>Este es el método recomendado para especificar las plantillas **** permitidas, ya que los valores no se sobrescribirán tras la actualización.

1. Vaya a la carpeta de **fragmentos de experiencias** necesaria.

1. Seleccione la carpeta y, a continuación, **Propiedades**.

1. Especifique la expresión regular para recuperar las plantillas necesarias en el campo Plantillas **** permitidas.

   Por ejemplo:
   `/conf/(.*)/settings/wcm/templates/experience-fragment(.*)?`

   Consulte:
   `http://localhost:4502/mnt/overlay/cq/experience-fragments/content/experience-fragments/folderproperties.html/content/experience-fragments/wknd`

   ![Propiedades del fragmento de experiencias: plantillas permitidas](/help/sites-cloud/authoring/assets/xf-folders-templates.png)

   >[!NOTE]
   >
   >Para obtener más información, consulte [Plantillas para fragmentos de experiencias](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments).

1. Seleccione **Guardar y cerrar**.

### Configurar las plantillas permitidas para la instancia {#configure-allowed-templates-instance}

>[!CAUTION]
>
>No se recomienda cambiar las plantillas **** permitidas por este método, ya que las plantillas especificadas se pueden sobrescribir tras la actualización.
>
>Utilice este cuadro de diálogo únicamente con fines informativos.

1. Navigate to the required **Experience Fragments** console.

1. Seleccione las **opciones de configuración**:

   ![Botón Configuración](/help/sites-cloud/authoring/assets/xf-18.png)

1. Especifique las plantillas necesarias en el cuadro de diálogo **Configurar fragmentos de experiencias**:

   ![Configurar Fragmentos de experiencias](/help/sites-cloud/authoring/assets/xf-19.png)

   >[!NOTE]
   >
   >Para obtener más información, consulte [Plantillas para fragmentos de experiencias](/help/implementing/developing/extending/experience-fragments.md#templates-for-experience-fragments).

1. Seleccione **Guardar**.


## Creación de un fragmento de experiencias {#creating-an-experience-fragment}

Para crear un fragmento de experiencias:

1. Select **Experience Fragments** from the Global Navigation.

   ![Fragmentos de experiencia en el panel Navegación](/help/sites-cloud/authoring/assets/xf-01.png)

1. Vaya a la carpeta requerida y seleccione **Crear**:

   ![Creación de una carpeta para fragmentos de experiencias](/help/sites-cloud/authoring/assets/xf-02.png)

1. Seleccione **Fragmento** de experiencias para abrir el asistente **Crear fragmento** de experiencias.

   Seleccione la **plantilla** adecuada y, a continuación, **Siguiente**:

   ![Selección de una plantilla de fragmento de experiencia](/help/sites-cloud/authoring/assets/xf-03.png)


1. Introduzca las **propiedades** del **fragmento de experiencias**.

   Es obligatorio escribir un **título**. Si el **nombre** se deja en blanco, se derivará del **título**.

   ![Propiedades del fragmento de experiencias](/help/sites-cloud/authoring/assets/xf-04.png)

1. Haga clic en **Crear**.

   Se mostrará un mensaje. Seleccione:

   * **Listo** para volver a la consola
   * **Abrir** para abrir el editor de fragmentos

## Edición del fragmento de experiencias {#editing-your-experience-fragment}

El editor de fragmentos de experiencias ofrece funcionalidades similares a las del editor de páginas.

>[!NOTE]
>
>Consulte [Edición del contenido de una página](/help/sites-cloud/authoring/fundamentals/editing-content.md) para obtener más información acerca de cómo utilizar el editor de páginas.

El siguiente procedimiento de ejemplo ilustra cómo crear un teaser para un producto:

1. Arrastre y suelte el componente requerido desde el [navegador](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser)de componentes.

1. Según el componente:
   * Agregue contenido o recursos según sea necesario.
   * Configure las propiedades según sea necesario.

1. Agregue más componentes según sea necesario.

Por ejemplo: `http://<host>:<port>/editor.html/content/experience-fragments/wknd/language-masters/en/contributors/stacey-roswells/master.html`

![Fragmento de experiencias en la página](/help/sites-cloud/authoring/assets/xf-05.png)

## Creación de una variación de fragmento de experiencias {#creating-an-experience-fragment-variation}

Puede crear varias variaciones para este fragmento de experiencias en función de sus necesidades:

1. Abra la página para su [edición](#editing-your-experience-fragment).
1. Abra la ficha **Variaciones**.

   ![Creación de una variación de fragmento de experiencia](/help/sites-cloud/authoring/assets/xf-06.png)

1. La opción **Crear** le permite crear:

   * **Variación**
   * **Variación como Live Copy**.

1. Defina las propiedades requeridas:

   * **Plantilla**
   * **Título**
   * **Nombre** : si se deja en blanco, se derivará del título
   * **Descripción**
   * **Etiquetas de variación**
   Por ejemplo:

   ![Propiedades de la variación](/help/sites-cloud/authoring/assets/xf-07.png)

1. Confirm with **Done**, the new variation will be shown in the panel.

## Uso de los fragmentos de experiencias {#using-your-experience-fragment}

Ahora puede utilizar el fragmento de experiencias para crear páginas:

1. Abra cualquier página para su edición.

1. Cree una instancia del componente Fragmento de experiencia, dentro del sistema de párrafos de página:

1. Agregue el fragmento de experiencia real a la instancia de componente; o bien:

   * Arrastre el fragmento necesario desde el explorador de activos y colóquelo en el componente.
   * Select **Configure** from the component toolbar and specify the fragment to use, confirm with **Done**.
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

1. El **bloque** de creación se mostrará en la ficha izquierda (**Local**) y se puede seleccionar para realizar más acciones:

   ![Bloque de creación en el carril](/help/sites-cloud/authoring/assets/xf-12.png)

#### Administración de un bloque de creación {#managing-a-building-block}

El bloque de creación se puede ver en la ficha **Bloques de creación**. Para cada bloque, están disponibles las siguientes acciones:

* **** Ir a la variación principal: abrir la variación principal en una nueva ficha
* **Cambiar nombre**
* **Eliminar**

![Administración de bloques de creación](/help/sites-cloud/authoring/assets/xf-13.png)

#### Uso de un bloque de creación {#using-a-building-block}

Puede arrastrar el bloque de creación al sistema de párrafos de cualquier fragmento, como con cualquier componente.

Al editar un fragmento de experiencia, los bloques de creación disponibles se muestran en la ficha izquierda. Puede filtrar según:

* **Local** : Generación de bloques a partir del fragmento de experiencias actual
* **Todo** : Generación de bloques a partir de todos los fragmentos

![Seleccionar bloques de creación](/help/sites-cloud/authoring/assets/xf-14.png)

## Detalles del fragmento de experiencias {#details-of-your-experience-fragment}

Se pueden ver los detalles del fragmento:

1. Vaya a la ubicación de los fragmentos de experiencia (no vaya más allá hacia las variaciones dentro del fragmento).
Los detalles se muestran en todas las vistas de la consola de **fragmentos de experiencias**, con una **vista de lista** que incluye los detalles de una exportación a destino: <!--Details are shown in all views of the **Experience Fragments** console, with the **List View** including details of an [export to Target](/help/sites-administering/experience-fragments-target.md):-->

   ![Detalles del fragmento de experiencias](/help/sites-cloud/authoring/assets/xf-15.png)

1. Al abrir las **propiedades** del fragmento de experiencias:

   ![Botón Propiedades](/help/sites-cloud/authoring/assets/xf-16.png)

   Las propiedades están disponibles en varias fichas:

   >[!CAUTION]
   >
   >Estas fichas se muestran al abrir **Propiedades** desde la consola Fragmentos de experiencia.
   >
   >Si **abre Propiedades** al editar un fragmento de experiencia, se muestran las propiedades [de](/help/sites-cloud/authoring/fundamentals/page-properties.md) página correspondientes.

   ![Propiedades del fragmento de experiencias](/help/sites-cloud/authoring/assets/xf-17.png)

   * **Básico**
      * **Título**: obligatorio
      * **Descripción**
      * **Etiquetas**
      * **Número total de variantes**: solo información
      * **Número de variantes web**: solo información
      * **Número de variantes** que no son web: solo información
      * **Número de páginas que utilizan este fragmento**: solo información
   * **Servicios de nube**
      * **Configuración de nube**
      * **Configuraciones de Cloud Service**
      * **ID de página de Facebook**
      * **Tablero de Pinterest**
   * **Referencias**
      * Una lista de referencias
   * **Estado de medios sociales**
      * Detalles de las variaciones de las redes sociales

## Representación HTML sin formato {#the-plain-html-rendition}

Using the `.plain.` selector in the URL, you can access the plain HTML rendition from the browser.

>[!NOTE]
>
>Aunque esta opción está disponible directamente desde el explorador, [el objetivo principal es permitir a otras aplicaciones (por ejemplo, aplicaciones web de terceros o implementaciones móviles personalizadas) acceder al contenido del fragmento de experiencias directamente, únicamente mediante la URL](/help/implementing/developing/extending/experience-fragments.md#the-plain-html-rendition).

## Exportación de fragmentos de experiencia {#exporting-experience-fragments}

De forma predeterminada, los fragmentos de experiencias se envían en formato HTML. Los canales de AEM y los canales similares de terceros pueden usar esta opción.

Para la exportación a Adobe Target, también se puede utilizar JSON. Consulte Target Integration with Experience Fragments (Integración de objetivos con fragmentos de experiencias) para obtener información completa. <!--For export to Adobe Target, JSON can also be used. See [Target Integration with Experience Fragments](/help/sites-administering/experience-fragments-target.md) for full information.-->
