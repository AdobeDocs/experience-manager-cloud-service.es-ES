---
title: Creación de lanzamientos
description: Puede crear un lanzamiento para habilitar la actualización de una nueva versión de las páginas web existentes para una activación futura.
exl-id: 216ccb7a-1409-4f55-8be2-2b088f91a430
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 60%

---

# Creación de lanzamientos {#creating-launches}

Cree un lanzamiento para permitir la actualización de una nueva versión de las páginas web existentes para una activación futura. Al crear un lanzamiento, especificará un título y la página de origen:

* El título aparece en el carril [Referencias](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references); desde allí, los autores pueden acceder al título y trabajar con él.
* Las páginas secundarias de la página de origen se incluyen en el lanzamiento de forma predeterminada. Si lo desea, puede utilizar únicamente la página de origen.
* De forma predeterminada, [Live Copy](/help/sites-cloud/administering/msm/overview.md) actualiza automáticamente las páginas de lanzamiento a medida que cambian las páginas de origen. Puede especificar que se cree una copia estática para evitar cambios automáticos.

De forma opcional, puede especificar la **fecha de lanzamiento** (y hora) para establecer cuándo se promocionarán y activarán las páginas. Sin embargo, la **fecha de lanzamiento** solo funciona en combinación con el indicador **Producción lista** (consulte [Edición de la configuración de un lanzamiento](/help/sites-cloud/authoring/launches/editing.md#editing-a-launch-configuration)); para que las acciones se produzcan de forma automática, se deben configurar ambas.

>[!NOTE]
>
>Cuando crea un lanzamiento, las páginas superiores en la jerarquía no son copias de las páginas de origen. Son marcadores de posición creados con la plantilla:
>
>* `/libs/launches/templates/outofscope`
>
>Estas páginas no se pueden editar. Verá el siguiente mensaje:
>
>* **Esta página no forma parte del lanzamiento. Vaya a la página de producción**


## Creación de un lanzamiento {#creating-a-launch}

Puede crear un lanzamiento desde la consola Sitios o Lanzamientos:

1. Abra cualquiera de las consolas **Sites** o **Lanzamientos**.

   >[!NOTE]
   >
   >Al usar el **Sites** consola es habitual desplazarse a la ubicación de la página de origen, pero esto no es obligatorio, ya que puede navegar al seleccionar la **Origen de lanzamiento** en el asistente.

1. Según la consola que utilice:
   * **Lanzamientos**:
      1. Seleccionar **Crear lanzamiento** en la barra de herramientas para abrir el asistente.
   * **Sites**:
      1. Seleccione **Crear** en la barra de herramientas para abrir el cuadro de selección.
      1. De esta selección **Crear lanzamiento** para abrir el asistente.

   >[!NOTE]
   >
   >En la consola de **Sites** también puede utilizar el [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) para seleccionar una página antes de hace clic en **Crear**.
   >
   >La página seleccionada se utilizará como página de origen inicial.

1. En el paso **Seleccionar origen**, debe **Añadir páginas**. Puede seleccionar varias páginas, pero debe especificar la ruta de acceso de cada una de ellas:
   * Vaya a la ubicación requerida.
   * Seleccione la(s) página(s) de origen y confírmela(s) (marca de verificación).

   Repita el proceso tantas veces como sea necesario.

   ![Seleccionar origen de lanzamiento](/help/sites-cloud/authoring/assets/launches-select-source.png)

   >[!NOTE]
   >
   >Para agregar páginas o ramas a un lanzamiento, deben estar dentro de un sitio, es decir, debajo de una raíz de nivel superior común.
   >
   >Si un sitio contiene raíces de idioma por debajo del nivel superior, las páginas y ramas de un lanzamiento deben estar por debajo de una raíz de idioma común.

1. Para cada entrada puede especificar si desea:

   * **Incluir páginas secundarias**:

      * Especifique si desea crear un lanzamiento con o sin las páginas secundarias.  De forma predeterminada, se incluyen estas subpáginas.

   Continúe con **Siguiente**.

   ![Seleccionar origen de lanzamiento](/help/sites-cloud/authoring/assets/launches-select-source-2.png)

1. En el paso **Propiedades** del asistente, puede especificar lo siguiente:

   * **Título del lanzamiento**: Nombre del lanzamiento. El nombre debe tener significado para los autores.
   * **con contenido existente**: el contenido original se utilizará para crear el lanzamiento.
   * **utilice una plantilla nueva para sustituir la página**: consulte [Creación de un lanzamiento con una plantilla nueva](#create-launch-with-new-template) para obtener más información.
   * **Heredar los datos publicados de la página de origen**: seleccione esta opción para actualizar automáticamente el contenido de las páginas de lanzamiento cuando cambien las páginas de origen. Para conseguirlo, esta opción convierte el lanzamiento en una [Live Copy](/help/sites-cloud/administering/msm/overview.md). Está opción está seleccionada de forma predeterminada.-->
   * **Fecha del lanzamiento**: la fecha y hora en que la copia de lanzamiento se debe activar (depende del indicador **Producción lista**; consulte [Lanzamientos: orden de los eventos](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events)).

   ![Propiedades del lanzamiento](/help/sites-cloud/authoring/assets/launches-properties.png)

1. Uso **Crear** para completar el proceso y crear el nuevo lanzamiento. El cuadro de diálogo de confirmación le preguntará si desea abrir el lanzamiento inmediatamente.

   Si devuelve la consola (con **Listo**) puede ver (y acceder) al lanzamiento desde las ubicaciones siguientes:

   * La [**consola de** lanzamientos](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
   * Las [**referencias** en la **consola** Sites](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console)

### Creación de un lanzamiento con una plantilla nueva {#create-launch-with-new-template}

Al crear un lanzamiento, puede seleccionar si desea utilizar una plantilla nueva:

>[!NOTE]
>
>Esta opción solo está disponible al crear un lanzamiento desde la consola **Sitios**. No está disponible al crear un lanzamiento desde la consola **Lanzamientos**.

![Creación de un lanzamiento con una plantilla nueva](/help/sites-cloud/authoring/assets/launches-create-new-template.png)

Al seleccionar esto, ocurrirá lo siguiente:

* se actualizarán las otras opciones disponibles,
* se incluirá un paso nuevo en el que puede seleccionar la plantilla requerida.

![Selección de una nueva plantilla](/help/sites-cloud/authoring/assets/launches-select-template.png)

>[!CAUTION]
>
>Como se utiliza una plantilla diferente, la nueva página estará vacía. Debido a la diferente estructura de la página, no se copia ningún contenido.
>
>Este mecanismo se puede utilizar para cambiar la plantilla de un [página existente](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#creating-a-new-page) - aunque debe considerarse la pérdida de contenido.

### Creación de un lanzamiento anidado {#creating-a-nested-launch}

Crear un lanzamiento anidado (dentro de un lanzamiento) le ofrece la capacidad de crear un lanzamiento a partir de un lanzamiento existente para que los autores puedan aprovechar los cambios ya realizados, en lugar de tener que realizar los mismos cambios varias veces para cada lanzamiento.

>[!NOTE]
>
>Consulte también [Promoción de un lanzamiento anidado](/help/sites-cloud/authoring/launches/promoting.md#promoting-a-nested-launch).

#### Creación de un lanzamiento anidado: consola Lanzamientos {#creating-a-nested-launch-launches-console}

Crear un lanzamiento anidado desde la consola **Lanzamientos** es básicamente lo mismo que crear cualquier otra forma de lanzamiento, con la excepción de que debe desplazarse a la rama de lanzamientos `/content/launches`:

1. En la consola **Lanzamientos**, seleccione **Crear**.
1. Seleccione **Agregar páginas** y, a continuación, vaya a la rama de lanzamientos especificando `/content/launches` en el carril **Filtros**. Seleccione el lanzamiento necesario y confirme con la opción **Seleccionar**:

   ![Creación de un lanzamiento anidado](/help/sites-cloud/authoring/assets/launches-create-nested.png)

1. Continúe con **Siguiente**.

1. Complete las **Propiedades** como con cualquier otro lanzamiento.

1. Complete con **Crear**.

#### Creación de un lanzamiento anidado: consola Sites {#creating-a-nested-launch-sites-console}

Para crear un lanzamiento anidado desde la consola **Sites** basado en un lanzamiento existente:

1. Acceda a [Lanzamiento desde las referencias (consola Sites)](/help/sites-cloud/authoring/launches/overview.md#launches-in-references-sites-console) para mostrar las acciones disponibles.
1. Seleccione **Crear lanzamiento** para abrir el asistente (como el origen ya se ha seleccionado, se omitirá el paso **Seleccionar origen**).
1. Introduzca el **título del lanzamiento** y cualquier otra información necesaria (como con un lanzamiento normal).
1. Uso **Crear** para completar el proceso y crear el nuevo lanzamiento. El cuadro de diálogo de confirmación le preguntará si desea abrir el lanzamiento inmediatamente.

Si selecciona **Listo**, volverá al carril **Referencias** de la **consola de Sites**, si selecciona la página adecuada en la que se muestra el nuevo lanzamiento.

### Eliminación de un lanzamiento {#deleting-a-launch}

Puede eliminar un lanzamiento desde el [consola lanzamientos](/help/sites-cloud/authoring/launches/overview.md#the-launches-console):

* Seleccione el lanzamiento tocando o haciendo clic en la miniatura.
* Aparecerá la barra de herramientas. Seleccione Eliminar.
* Confirme la acción.

>[!CAUTION]
>
>Al eliminar un lanzamiento, se quitarán el lanzamiento en sí y todos los lanzamientos anidados descendentes.
