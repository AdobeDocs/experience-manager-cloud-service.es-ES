---
title: Creación de lanzamientos
description: Puede crear un lanzamiento para poder actualizar las páginas web existentes a una versión nueva que se activará en el futuro.
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 87%

---


# Creación de lanzamientos {#creating-launches}

Cree un lanzamiento para poder actualizar las páginas web existentes a una versión nueva que se activará en el futuro. Al crear un lanzamiento, especificará un título y la página de origen:

* The title appears in the [References](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) rail, from where authors can access them to work on them.
* Las páginas secundarias de la página de origen se incluyen en el lanzamiento de forma predeterminada. Si lo desea, puede utilizar solo una página de origen.
* De forma predeterminada, Live Copy actualiza automáticamente las páginas de lanzamiento a medida que cambian las páginas de origen. Puede especificar que se cree una copia estática para evitar cambios automáticos. <!--By default, [Live Copy](/help/sites-administering/msm.md) automatically updates the launch pages as the source pages change. You can specify that a static copy is created to prevent automatic changes.-->

De forma opcional, puede especificar la **fecha de lanzamiento** (y hora) para establecer cuándo se promocionarán y activarán las páginas. Sin embargo, la **fecha de lanzamiento** solo funciona en combinación con el indicador **Producción lista** (consulte [Edición de la configuración de un lanzamiento](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration)); para que las acciones se produzcan de forma automática, se deben configurar ambas.

## Creación de un lanzamiento {#creating-a-launch}

Puede crear un lanzamiento desde las consolas Sitios o Lanzamientos:

1. Abra cualquiera de las consolas **Sitios** o **Lanzamientos**.

   >[!NOTE]
   >
   >Al utilizar la consola **Sitios**, es usual navegar a la ubicación de la página de origen, pero no es obligatorio ya que puede desplazarse al seleccionar **Origen de lanzamiento** en el asistente.

1. En función de la consola que esté utilizando:
   * **Lanzamientos**:
      1. Seleccione **Crear lanzamiento** en la barra de herramientas para abrir el asistente.
   * **Sites**:
      1. Seleccione **Crear** en la barra de herramientas para abrir el cuadro de selección.
      1. Aquí, seleccione **Crear lanzamiento** para abrir el asistente.

   >[!NOTE]
   >
   >En la consola de **Sites** también puede utilizar el [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) para seleccionar una página antes de hace clic en **Crear**.
   >
   >La página seleccionada se utilizará como página de origen inicial.

1. En el paso **Seleccionar origen**, debe **Añadir páginas**. Puede seleccionar varias páginas, pero debe especificar la ruta de acceso de cada una de ellas:
   * Vaya a la ubicación requerida.
   * Seleccione las páginas de origen y confirme (marca de verificación).

   Repita el proceso tantas veces como sea necesario.

   ![Seleccionar origen de inicio](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >Las páginas o ramas que se deseen añadir a un lanzamiento deben estar dentro de un sitio; es decir, por debajo de una raíz de nivel superior común.
   >
   >Si un sitio contiene raíces de idioma por debajo del nivel superior, las páginas y las ramas para un lanzamiento deben estar por debajo de una raíz de idioma común.

1. Para cada entrada, puede especificar si:

   * **Incluir páginas secundarias**:

      * Especifique si desea crear un lanzamiento con o sin las páginas secundarias.  De forma predeterminada, se incluyen estas subpáginas.

   Continúe con **Siguiente**.

   ![Seleccionar origen de inicio](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. En el paso **Propiedades** del asistente, puede especificar:

   * **Título del lanzamiento**: el nombre del lanzamiento. El nombre debería tener sentido para los autores.
   * **con contenido existente**: el contenido original se utilizará para crear el lanzamiento.
   * **utilice una plantilla nueva para sustituir la página**: consulte [Creación de un lanzamiento con una plantilla nueva](#create-launch-with-new-template) para obtener más información.
   * **Heredar los datos publicados de la página de origen**: seleccione esta opción para actualizar automáticamente el contenido de las páginas de lanzamiento cuando cambien las páginas de origen. Esta opción logra esto haciendo que el lanzamiento sea una Live Copy. De forma predeterminada, está opción está seleccionada.<!--Select this option to automatically update the content of launch pages when the source pages change. This option achieves this by making the launch a [live copy](/help/sites-administering/msm.md). By default, this option is selected.-->
   * **Fecha del lanzamiento**: la fecha y hora en que la copia de lanzamiento se debe activar (depende del indicador **Producción lista**; consulte [Lanzamientos: orden de los eventos](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)).

   ![Propiedades de lanzamiento](/help/sites-cloud/authoring/assets/launches-properties.png)

1. Utilice **Crear** para completar el proceso y crear el lanzamiento nuevo. El cuadro de diálogo de confirmación le preguntará si desea abrir el lanzamiento inmediatamente.

   Si vuelve a la consola (con **Hecho**), puede ver el lanzamiento (y acceder a él) desde:

   * The [**Launches** console](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * The [**References** in the **Sites** console](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)

### Creación de un lanzamiento con una plantilla nueva {#create-launch-with-new-template}

Al crear un lanzamiento, puede seleccionar si desea utilizar una plantilla nueva:

>[!NOTE]
>
>Esta opción solo está disponible al crear un lanzamiento desde la consola **Sitios**. No está disponible al crear un lanzamiento desde la consola **Lanzamientos**.

![Creación de un lanzamiento con una nueva plantilla](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

Al seleccionar esto, ocurrirá lo siguiente:

* Actualice las demás opciones disponibles,
* Incluya un nuevo paso en el que puede seleccionar la plantilla requerida.

![Selección de una nueva plantilla](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>Al utilizar una plantilla diferente, la página nueva estará vacía. Debido a la estructura de página diferente, no se volverá a copiar ningún contenido.
>
>Este mecanismo se puede utilizar para cambiar la plantilla de una [página existente](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page): sin embargo, debe tenerse en cuenta la pérdida de contenido.

### Creación de un lanzamiento anidado {#creating-a-nested-launch}

Crear un lanzamiento anidado (un lanzamiento dentro de otro lanzamiento) le ofrece la posibilidad de crear un lanzamiento a partir de un lanzamiento existente de modo que los autores pueden aprovechar los cambios que ya se hayan realizado, en lugar de tener que realizar los mismos cambios varias veces en cada lanzamiento.

>[!NOTE]
>
>Consulte también [Promoción de un lanzamiento anidado](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch).

#### Creación de un lanzamiento anidado: consola Lanzamientos {#creating-a-nested-launch-launches-console}

Creating a nested launch from the **Launches** console is basically the same as creating any other form of launch, with the exception that you need to navigate to the launches branch `/content/launches`:

1. En la consola **Lanzamientos**, seleccione **Crear**.
1. Seleccione **Agregar páginas** y, a continuación, vaya a la rama de lanzamientos especificando `/content/launches` en el filtro. Seleccione el lanzamiento necesario y confirme con la opción **Seleccionar**:

   ![Creación de un lanzamiento anidado](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. Continúe con **Siguiente** y complete las **Propiedades** como con cualquier otro lanzamiento.

   ![Seleccionar origen para inicio anidado](/help/sites-cloud/authoring/assets/launches-create-nested-select.png)

#### Creación de un lanzamiento anidado: consola Sitios {#creating-a-nested-launch-sites-console}

Para crear un lanzamiento anidado desde la consola **Sitios** basado en un lanzamiento existente:

1. Acceda a [Lanzamiento desde las referencias (consola de sitios)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar las acciones disponibles.
1. Seleccione **Crear lanzamiento** para abrir el asistente (como el origen ya se ha seleccionado, se omitirá el paso **Seleccionar origen**).
1. Introduzca el **título del lanzamiento** y cualquier otra información necesaria (como con un lanzamiento normal).
1. Utilice **Crear** para completar el proceso y crear el lanzamiento nuevo. El cuadro de diálogo de confirmación le preguntará si desea abrir el lanzamiento inmediatamente.

Si selecciona **Listo**, volverá al carril **Referencias** de la **consola de Sites**, si selecciona la página adecuada en la que se muestra el nuevo lanzamiento.

### Eliminación de un lanzamiento {#deleting-a-launch}

Puede eliminar un lanzamiento desde la [consola de lanzamientos](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):

* Para seleccionar el lanzamiento, toque o haga clic en la miniatura.
* Se mostrará la barra de herramientas: seleccione Eliminar.
* Confirme la acción.

>[!CAUTION]
>
>Al eliminar un lanzamiento, se quitarán el lanzamiento en sí y todos los lanzamientos anidados descendentes.
