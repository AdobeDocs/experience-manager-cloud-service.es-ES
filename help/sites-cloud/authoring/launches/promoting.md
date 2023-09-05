---
title: Promoción de lanzamientos
description: Debe promocionar las páginas de lanzamiento para devolver el contenido al origen (producción) antes de publicarlo.
exl-id: 5f5ed17c-43db-4ef6-ab79-c491326fa01c
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: ht
source-wordcount: '814'
ht-degree: 100%

---

# Promoción de lanzamientos {#promoting-launches}

Debe promocionar las páginas de lanzamiento para devolver el contenido al origen (producción) antes de publicarlo. Cuando se promociona una página de lanzamiento, la página correspondiente de las páginas de origen se reemplaza con el contenido de la página promocionada. Las siguientes opciones están disponibles al promocionar una página de lanzamiento:

* Promocionar solo la página actual o todo el lanzamiento.
* Promocionar las páginas secundarias de la página actual.
* Promocionar el lanzamiento completo o solo las páginas que han cambiado.
* Eliminar el lanzamiento después de la promoción.

>[!NOTE]
>
>Tras promocionar las páginas de lanzamiento al destino (**producción**), puede activar las páginas de **producción** como entidad (para que el proceso sea más rápido). Añada las páginas a un paquete de flujo de trabajo y utilícelo como carga útil para un flujo de trabajo que active un paquete de páginas. Debe crear el paquete de flujo de trabajo antes de promocionar el lanzamiento. Consulte [Procesamiento de páginas promocionadas mediante el flujo de trabajo de AEM](#processing-promoted-pages-using-aem-workflow).

>[!CAUTION]
>
>Un solo lanzamiento no se puede promocionar de forma simultánea. Esto significa que dos acciones promocionales en el mismo lanzamiento al mismo tiempo pueden dar lugar a un error: `Launch could not be promoted` (así como errores de conflictos en el registro).

>[!CAUTION]
>
>Al promocionar lanzamientos para páginas *modificadas*, se tienen en cuenta las modificaciones tanto en la rama de origen como en la de lanzamiento.

## Promoción de páginas de lanzamiento {#promoting-launch-pages}

>[!NOTE]
>
>Esta sección trata sobre la operación manual de promocionar las páginas de lanzamiento cuando solo hay un nivel de lanzamiento. Consulte:
>
>* [Promover un lanzamiento anidado](#promoting-a-nested-launch) cuando hay más de un lanzamiento en la estructura.
>* [Lanzamientos: el orden de los eventos](/help/sites-cloud/authoring/launches/overview.md#launches-the-order-of-events) para obtener más información sobre la promoción y publicación automáticas.
>

Puede promocionar lanzamientos desde la consola **Sites** o la consola **Lanzamientos**:

1. Abra:
   * La consola **Sites** al navegar por las páginas de origen:
      1. Abra el [carril de referencias](/help/sites-cloud/authoring/fundamentals/environment-tools.md#references) y seleccione la página de origen necesaria con el [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md) (o seleccione y abra el carril de referencias, el orden no importa). Se muestran todas las referencias.
      1. Seleccione **Lanzamientos** (por ejemplo, Lanzamientos (1)) para mostrar una lista de los lanzamientos específicos.
      1. Seleccione el lanzamiento específico para mostrar las acciones disponibles.
      1. Seleccione **Promocionar lanzamiento** para abrir el asistente.
   * La consola **Sites** al navegar por las páginas de lanzamiento:
      1. Seleccione la página de lanzamiento necesaria mediante el [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md).
      1. La acción **Promocionar** está disponible en la barra de herramientas.
   * La consola **Lanzamientos**:
      1. Seleccione el lanzamiento (toque o haga clic en la miniatura).
      1. Seleccione **Promocionar**.
1. En el primer paso puede especificar:
   * **Destino**
      * **Eliminar lanzamiento después de la promoción**
   * **Ámbito**
      * **Promocionar lanzamiento completo**
      * **Promocionar las páginas modificadas**
      * **Promocionar páginas aprobadas**: depende del flujo de trabajo de aprobación del lanzamiento
      * **Promocionar página actual**
      * **Promocionar la página actual y sus páginas secundarias**

     Por ejemplo, al seleccionar para promocionar solo las páginas modificadas:

     ![Promoción del lanzamiento](/help/sites-cloud/authoring/assets/launches-promote.png)

     >[!NOTE]
     >
     >Esto cubre un solo lanzamiento. Si tiene lanzamientos anidados, consulte [Promocionar un lanzamiento anidado](#promoting-a-nested-launch).
1. Seleccione **Siguiente** para continuar.
1. Puede revisar las páginas que se promocionarán, que dependerán del intervalo de páginas que haya elegido:

   ![Revisar promoción](/help/sites-cloud/authoring/assets/launches-promote-review.png)

1. Seleccione **Promocionar**.

## Promoción de páginas de lanzamiento al editar {#promoting-launch-pages-when-editing}

Cuando está editando una página de lanzamiento, la acción **Promocionar lanzamiento** también está disponible en **Información de la página**. Esta acción abrirá el asistente para recopilar la información necesaria.

![Promocionar lanzamiento desde la información del sitio](/help/sites-cloud/authoring/assets/launches-promote-page-info.png)

>[!NOTE]
>
>Esta opción está disponible para los [lanzamientos anidados](#promoting-a-nested-launch) y únicos.

## Promoción de un lanzamiento anidado {#promoting-a-nested-launch}

Después de crear un lanzamiento anidado, puede promocionarlo de nuevo a cualquiera de los orígenes, incluido el origen raíz (producción).

![Un lanzamiento anidado](/help/sites-cloud/authoring/assets/launches-promoting-nested.png)

1. Al igual que con Crear un lanzamiento anidado, localice y seleccione el lanzamiento requerido en la consola **Lanzamientos** o en el raíl de **referencias**.
1. Seleccione **Promocionar lanzamiento** para abrir el asistente.
1. Introduzca la información necesaria:
   * **Destino**
      * **Destino promocional**: puede promocionar a cualquiera de los orígenes.
      * **Eliminar el lanzamiento después de la promoción**: después de la promoción, se elimina el lanzamiento seleccionado y los lanzamientos anidados en él.
   * **Ámbito**: aquí puede seleccionar si debe promocionar el lanzamiento completo o solo las páginas que se han editado. En este último caso, puede seleccionar incluir/excluir páginas secundarias. La configuración predeterminada es promocionar solo los cambios de página para la página actual:
      * **Promocionar lanzamiento completo**
      * **Promocionar las páginas modificadas**
      * **Promocionar páginas aprobadas**: depende del flujo de trabajo de aprobación del lanzamiento
      * **Promocionar página actual**
      * **Promocionar la página actual y sus páginas secundarias**

   ![Promocionar configuración de lanzamiento](/help/sites-cloud/authoring/assets/launches-promote-settings.png)

1. Seleccione **Siguiente**.
1. Revise los detalles de la promoción antes de seleccionar **Promocionar**:

   ![Revisar configuración de promoción](/help/sites-cloud/authoring/assets/launches-promote-review-2.png)

   >[!NOTE]
   >
   >Las páginas que se muestran dependerán del **ámbito** que haya definido y, posiblemente, de las páginas que realmente se han editado.

1. Los cambios se promocionan y reflejan en la consola **Lanzamientos**:

   ![En la consola Lanzamientos](/help/sites-cloud/authoring/assets/launches-console.png)

## Procesamiento de páginas promocionadas mediante el flujo de trabajo de AEM {#processing-promoted-pages-using-aem-workflow}

Utilice modelos de flujo de trabajo para realizar procesamientos masivos de páginas de lanzamiento promocionadas:

1. Cree un paquete de flujo de trabajo.
1. Cuando los autores promocionan páginas de lanzamiento, las guardan en el paquete de flujo de trabajo.
1. Inicie un modelo de flujo de trabajo con el paquete como carga útil.

Para iniciar un flujo de trabajo automáticamente cuando se promocionen páginas, configure un lanzador de flujos de trabajo para el nodo del paquete. <!--To start a workflow automatically when pages are promoted, [configure a workflow launcher](/help/sites-administering/workflows-starting.md#workflows-launchers) for the package node.-->

Por ejemplo, puede generar automáticamente solicitudes de activación de página cuando los autores promocionen páginas de lanzamiento. Configure un lanzador de flujo de trabajo para iniciar el flujo de trabajo de activación de solicitud cuando se modifique el nodo del paquete.

![Flujo de trabajo de promoción](/help/sites-cloud/authoring/assets/launches-create-workflow.png)
