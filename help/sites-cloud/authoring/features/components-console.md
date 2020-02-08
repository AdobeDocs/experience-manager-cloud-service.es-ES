---
title: La consola Componentes
description: La consola Componentes permite examinar todos los componentes definidos para la instancia
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8

---


# La consola Componentes {#components-console}

La consola Componentes permite examinar todos los componentes definidos para la instancia y ver la información clave de cada componente.

It can be accessed from **Tools ->** **General ->** **Components**. Como no hay una estructura de árbol para los componentes, solo está disponible la vista de lista.

![Consola Componentes](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>La consola Componentes muestra todos los componentes del sistema. El [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) muestra los componentes disponibles para los autores y oculta cualquier grupo de componentes que comience con un punto ( `.`).

## Búsqueda {#search-field}

Con el icono **Solo contenido** (parte superior izquierda) podrá abrir el panel **Buscar** para buscar o para filtrar los componentes: 

![Búsqueda en la consola Componentes](/help/sites-cloud/authoring/assets/components-console-search.png)

### Detalles de los componentes {#component-details}

Para ver los detalles de un componente específico, toque o haga clic en el recurso necesario. Encontrará lo siguiente en tres fichas:

* **Propiedades**

   ![Propiedades de la consola Componentes](/help/sites-cloud/authoring/assets/components-console-properties.png)

   En la pestaña Propiedades puede:

   * Consulte las propiedades generales del componente.
      * Ver cómo se ha definido el icono o la abreviatura para el componente. <!-- View how the [icon or abbreviation has been defined](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) for the component.-->
      * Si hace clic en el origen del icono, se le dirigirá a dicho componente.
   * Ver el **tipo de recurso** y el **supertipo de recurso** (si está definido) para el componente.
      * Si hace clic en el supertipo de recurso, se le dirigirá a dicho componente.
   >[!NOTE]
   >
   >Because `/apps` is not editable at runtime, the Components Console is read-only.

* **Políticas**

   ![Directivas de la consola de componentes](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **Uso de Live**

   ![Uso activo de los componentes](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

   >[!CAUTION]
   >
   >Dada la naturaleza de la información recopilada para esta vista, puede tardar un rato en recopilarse o mostrarse. 

* **Documentación**

   Si el desarrollador ha proporcionado documentación del componente, esta aparecerá en la pestaña **Documentación**. Si no hay documentación disponible, no se mostrará la pestaña **Documentación.**<!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

   ![Documentación de componentes](/help/sites-cloud/authoring/assets/components-console-documentation.png)
