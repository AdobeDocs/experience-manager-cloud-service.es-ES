---
title: La consola Componentes
description: La consola Componentes permite examinar todos los componentes definidos para una instancia.
exl-id: f4949331-5302-46d3-a004-b813bb95ec2f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: ht
source-wordcount: '275'
ht-degree: 100%

---

# Consola Componentes {#components-console}

La consola Componentes permite examinar todos los componentes definidos para la instancia y ver información clave de cada componente.

Se puede acceder a ella desde **Herramientas ->** **General ->** **Componentes**. Como no hay una estructura de árbol para componentes, solo está disponible la vista en lista.

![La consola Componentes](/help/sites-cloud/authoring/assets/components-console.png)

>[!NOTE]
>
>La consola Componentes muestra todos los componentes en el sistema. El [navegador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser) muestra los componentes disponibles para los autores y oculta cualquier grupo de componentes que comience con un punto ( `.`).

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
   >Debido a que `/apps` no se puede editar en el tiempo de ejecución, la consola Componentes es de solo lectura.

* **Políticas**

   ![Políticas de la consola Componentes](/help/sites-cloud/authoring/assets/components-console-policies.png)

* **Uso de Live**

   ![Uso activo de los componentes](/help/sites-cloud/authoring/assets/components-console-live-usage.png)

   >[!CAUTION]
   >
   >Dada la naturaleza de la información recopilada para esta vista, puede tardar un rato en recopilarse o mostrarse. 

* **Documentación**

   Si el desarrollador ha proporcionado documentación del componente, esta aparecerá en la pestaña **Documentación**. Si no hay documentación disponible, no se mostrará la pestaña **Documentación**. <!-- If the developer has provided [documentation for the component](/help/sites-developing/developing-components.md#documenting-your-component), it will appear on the **Documentation** tab. If there is no documentation available, the **Documentation** tab will not be shown.-->

   ![Documentación de los componentes](/help/sites-cloud/authoring/assets/components-console-documentation.png)
