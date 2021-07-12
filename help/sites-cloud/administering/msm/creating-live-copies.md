---
title: Creación y sincronización de Live Copies
description: Aprenda a crear y sincronizar Live Copies para reutilizar el contenido en el sitio.
feature: Administrador de varios sitios
role: Admin
exl-id: 53ed574d-e20d-4e73-aaa2-27168b9d05fe
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '4277'
ht-degree: 1%

---

# Creación y sincronización de Live Copies {#creating-and-synchronizing-live-copies}

Puede crear una Live Copy a partir de una página o configuración de modelo para reutilizar ese contenido en el sitio. Administre la herencia y la sincronización, puede controlar cómo se propagan los cambios al contenido.

## Administración de configuraciones de modelo {#managing-blueprint-configurations}

Una configuración de modelo identifica un sitio web existente que desea usar como fuente para una o varias páginas de Live Copy.

>[!TIP]
>
>Las configuraciones del modelo permiten insertar cambios en el contenido en Live Copies. Consulte [Live Copies: configuración de origen, modelos y modelo](overview.md#source-blueprints-and-blueprint-configurations).

Al crear una configuración de modelo, se selecciona una plantilla que define la estructura interna del modelo. La plantilla de modelo predeterminada supone que el sitio web de origen tiene las siguientes características:

* El sitio web tiene una página raíz.
* Las páginas secundarias inmediatas de la raíz son ramas de idioma del sitio web. Al crear una Live Copy, los idiomas se presentan como contenido opcional para incluirlos en la copia.
* La raíz de cada rama de idioma tiene una o más páginas secundarias. Al crear una Live Copy, se presentan las páginas secundarias para que pueda incluirlas en la Live Copy.

>[!NOTE]
>
>Una estructura diferente requiere una plantilla de modelo diferente.

Después de crear la configuración de modelo, configure las siguientes propiedades:

* **Nombre**: Nombre de la configuración del modelo
* **Ruta de origen**: Ruta de la página raíz del sitio que está utilizando como origen (modelo)
* **Descripción**. (Opcional) Descripción de la configuración del modelo, que aparece en la lista de configuraciones de modelo para elegir al crear un sitio

Cuando se utiliza la configuración del modelo, puede asociarla con una configuración de lanzamiento que determina cómo se sincronizan las Live Copies del origen/modelo. Consulte [Especificación de las opciones de configuración de lanzamiento para utilizar](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use).

### Creación y edición de configuraciones de modelo {#creating-editing-blueprint-configurations}

Las configuraciones del modelo se consideran datos inmutables y, como tales, no se pueden editar durante la ejecución. Por este motivo, cualquier cambio en la configuración debe implementarse mediante Git utilizando la canalización CI/CD.

Encontrará más información en el artículo [Cambios importantes en Adobe Experience Manager (AEM) como Cloud Service.](/help/release-notes/aem-cloud-changes.md)

Los siguientes pasos están disponibles para un administrador en una instancia de desarrollo local solo para fines de prueba y desarrollo. Estas opciones no están disponibles en ninguna instancia de nube AEMaaCS.

#### Creación de una configuración de modelo localmente {#creating-a-blueprint-configuration}

Para crear una configuración de modelo:

1. [](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) Vaya al menú  **** Herramientas y, a continuación, seleccione el menú  **** Sitios .
1. Seleccione **Blueprints** para abrir la consola **Configuración de modelo**:

   ![Configuraciones del modelo](../assets/blueprint-configurations.png)

1. Seleccione **Crear**.
1. Seleccione la plantilla de modelo y, a continuación, **Next** para continuar.
1. Seleccione la página de origen que se utilizará como modelo; a continuación **Siguiente** para continuar.
1. Definir:

   * **Título**: título obligatorio para el modelo
   * **Descripción**: una descripción opcional para proporcionar más detalles.

1. **** Cree la configuración del modelo en función de su especificación.

### Edición o eliminación de una configuración de modelo localmente{#editing-or-deleting-a-blueprint-configuration}

Puede editar o eliminar una configuración de modelo existente:

1. [](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) Vaya al menú  **** Herramientas y, a continuación, seleccione el menú  **** Sitios .
1. Seleccione **Blueprints** para abrir la consola **Configuración de modelo**:

   ![Configuraciones del modelo](../assets/blueprint-configurations.png)

1. Seleccione la configuración del modelo necesaria: las acciones adecuadas estarán disponibles en la barra de herramientas:

   * **Propiedades**; puede utilizarlo para ver y luego editar las propiedades de la configuración.
   * **Eliminar**

## Creación de una copia activa {#creating-a-live-copy}

Existen varias formas de crear una Live Copy.

### Creación de una Live Copy de una página {#creating-a-live-copy-of-a-page}

Puede crear una Live Copy de cualquier página o rama. Al crear Live Copy, puede especificar las opciones de configuración de lanzamiento que se utilizarán para sincronizar el contenido:

* Las configuraciones de lanzamiento seleccionadas se aplican a la página Live Copy y a sus páginas secundarias.
* Si no especifica ninguna configuración de lanzamiento, MSM determina qué configuraciones de lanzamiento usar. Consulte [Especificación de la configuración de lanzamiento para utilizar](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use).

Puede crear una Live Copy de cualquier página:

* Páginas a las que se hace referencia mediante una [configuración de modelo](#creating-a-blueprint-configuration)
* Y páginas que no tienen conexión con una configuración
* Live Copy dentro de las páginas de otra Live Copy ([Live Copies anidadas](overview.md#nested-live-copies))

La única diferencia es que la disponibilidad del comando **Rollout** en las páginas de origen/modelo depende de si la fuente está referenciada por una configuración de modelo:

* Si crea Live Copy desde una página de origen a la que **se hace referencia** en una configuración de modelo, el comando Desplegar estará disponible en las páginas de origen/modelo.
* Si crea Live Copy desde una página de origen a la que **no se hace referencia** en una configuración de modelo, el comando Despliegue no estará disponible en las páginas de origen/modelo.

Para crear una Live Copy:

1. En la consola **Sites**, seleccione **Crear** y, a continuación, **Live Copy**.

   ![Crear Live Copy](../assets/create-live-copy.png)

1. Seleccione la página de origen y, a continuación, toque o haga clic en **Siguiente**. Por ejemplo:

   ![Seleccionar origen de Live Copy](../assets/live-copy-from.png)

1. Especifique la ruta de destino de Live Copy (abra la carpeta o página principal de Live Copy) y, a continuación, haga clic o pulse **Siguiente**.

   ![Seleccionar destino de Live Copy](../assets/live-copy-to.png)

   >[!NOTE]
   >
   >La ruta de destino no puede estar dentro de la ruta de origen.

1. Escriba:

   * un **Título** para la página.
   * a **Name**, que se utiliza en la dirección URL.

   ![Propiedades de Live Copy](../assets/live-copy-properties.png)

1. Utilice la casilla de verificación **Excluir páginas secundarias**:

   * Seleccionado: crear una Live Copy solo de la página seleccionada (Live Copy superficial)
   * No seleccionado: crear una Live Copy que incluya todos los descendientes de la página seleccionada (Live Copy profundo)

1. (Opcional) Para especificar una o más opciones de configuración de lanzamiento que se utilizarán para Live Copy, utilice la lista desplegable **Rollout Configs** para seleccionarlas. Las configuraciones seleccionadas se mostrarán debajo del selector desplegable.
1. Haga clic o pulse **Crear**. Se mostrará un mensaje de confirmación, desde el cual puede seleccionar **Open** o **Done**.

### Creación de una Live Copy de un sitio a partir de una configuración de modelo {#creating-a-live-copy-of-a-site-from-a-blueprint-configuration}

Cree una Live Copy con una configuración de modelo para crear un sitio basado en el contenido del modelo (origen). Cuando crea una Live Copy a partir de una configuración de modelo, selecciona una o varias ramas de idioma del origen del modelo que desea copiar y, a continuación, selecciona los capítulos que desea copiar de las ramas de idioma. Consulte [Creación de una configuración de modelo](#creating-a-blueprint-configuration).

Si omite algunas ramas de idioma de Live Copy, puede agregarlas más adelante. Consulte [Creación de una Live Copy dentro de una Live Copy (configuración de modelo)](#creating-a-live-copy-inside-a-live-copy-blueprint-configuration) para obtener más información.

>[!CAUTION]
>
>Cuando el origen del modelo contiene vínculos y referencias que dirigen un párrafo a una rama diferente, los destinatarios no se actualizan en las páginas de Live Copy, sino que siguen apuntando al destino original.

Cuando cree el sitio, proporcione valores para las siguientes propiedades:

* **Idiomas** iniciales: Las ramas de idioma del origen del modelo que se incluirán en Live Copy
* **Capítulos** iniciales: Las páginas secundarias de las ramas de idioma del modelo que se incluirán en Live Copy
* **Ruta** de destino: La ubicación de la página raíz del sitio de Live Copy
* **Título**: Título de la página raíz del sitio de Live Copy
* **Nombre**: (Opcional) El nombre del nodo JCR que almacena la página raíz de Live Copy (el valor predeterminado se basa en el título)
* **Propietario** del sitio: (Opcional) Información sobre la parte responsable de Live Copy
* **Live Copy**: Seleccione esta opción para establecer una relación activa con el sitio de origen. Si no selecciona esta opción, se crea una copia del modelo, pero no se sincroniza posteriormente con el origen.
* **Configuración de lanzamiento**: (Opcional) Seleccione una o varias opciones de configuración de lanzamiento para sincronizar Live Copy. De forma predeterminada, las configuraciones de lanzamiento se heredan del modelo. Consulte [Especificación de las opciones de configuración de lanzamiento para utilizar](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use) para obtener más información.

Para crear una Live Copy de un sitio a partir de una configuración de modelo:

1. En la consola **Sitios**, seleccione **Crear** y, a continuación, **Sitio** en el selector desplegable.
1. Seleccione la configuración de modelo que se utilizará como origen de Live Copy y continúe con **Next**:

   ![Crear sitio a partir de modelo](../assets/create-site-from-blueprint.png)

1. Utilice el selector **Initial Languages** para especificar el idioma o los idiomas del sitio del modelo que se utilizarán para Live Copy.

   Todos los idiomas disponibles están seleccionados de forma predeterminada. Para eliminar un idioma, toque o haga clic en el **X** que aparece junto al idioma.

   Por ejemplo:

   ![Especificar propiedades al crear el sitio](../assets/create-site-properties.png)

1. Utilice la lista desplegable **Initial Chapters** para seleccionar las secciones del modelo que desea incluir en Live Copy. Todos los capítulos disponibles se incluyen de forma predeterminada, pero se pueden eliminar.
1. Proporcione valores para las propiedades restantes y, a continuación, seleccione **Crear**. En el cuadro de diálogo de confirmación, seleccione **Listo** para volver a la consola **Sitios** o **Abrir sitio** para abrir la página raíz del sitio.

### Creación de una Live Copy dentro de una Live Copy (configuración de modelo) {#creating-a-live-copy-inside-a-live-copy-blueprint-configuration}

Cuando crea una Live Copy dentro de la Live Copy existente (creada con una configuración de modelo), puede insertar cualquier copia de idioma o capítulos que no se incluyeron cuando se creó originalmente la Live Copy.

## Supervisión de Live Copy {#monitoring-your-live-copy}

### Ver el estado de una Live Copy {#seeing-the-status-of-a-live-copy}

Las propiedades de una página Live Copy muestran la siguiente información sobre Live Copy:

* **Fuente**: La página de origen de la página Live Copy
* **Estado**: El estado de sincronización de Live Copy, que incluye si Live Copy está actualizado con el origen, cuándo se produjo la última sincronización y quién realizó la sincronización
* **Configuración**:

   * Si la página sigue estando sujeta a la herencia de Live Copy
   * Si la configuración se hereda de la página principal
   * Cualquier configuración de lanzamiento que utilice Live Copy

Para ver las propiedades:

1. En la consola **Sitios**, seleccione la página Live Copy y abra las propiedades.
1. Seleccione la pestaña **Live Copy**.

   Por ejemplo:

   ![Ficha Live Copy en las propiedades de página](../assets/live-copy-inherit.png)

   Consulte la sección [Uso de la información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview) en el artículo Consola de información general de Live Copy para obtener más información.

### Ver las Live Copies de una página de modelo {#seeing-the-live-copies-of-a-blueprint-page}

Las páginas de modelo (a las que se hace referencia en una configuración de modelo) proporcionan una lista de las páginas de Live Copy que utilizan la página actual (modelo) como origen. Utilice esta lista para realizar un seguimiento de las Live Copies. La lista aparece en la pestaña **Blueprint** de las [propiedades de página](/help/sites-cloud/authoring/fundamentals/page-properties.md).

![Pestaña Modelo de las propiedades de página](../assets/live-copy-blueprint-tab.png)

## Sincronización de Live Copy {#synchronizing-your-live-copy}

Hay varias formas de sincronizar tu Live Copy.

### Despliegue de un modelo {#rolling-out-a-blueprint}

Despliegue una página de modelo para insertar los cambios de contenido en Live Copies. Una acción **Rollout** ejecuta las configuraciones de lanzamiento que utilizan el déclencheur [On Rollout](live-copy-sync-config.md#rollout-triggers).

>[!NOTE]
>
>Pueden producirse conflictos si se crean nuevas páginas con el mismo nombre de página en la rama del modelo y en una rama de Live Copy dependiente.
>
>Estos [conflictos deben manejarse y resolverse en el momento del despliegue](rollout-conflicts.md).

#### Despliegue de un modelo desde las propiedades de página {#rolling-out-a-blueprint-from-page-properties}

1. En la consola **Sites**, seleccione la página en el modelo y abra las propiedades.
1. Abra la pestaña **Modelo**.
1. Seleccione **Despliegue**.

   ![Botón Desplegar](../assets/rollout.png)

1. Especifique las páginas y las páginas secundarias y, a continuación, confirme con la marca de verificación:

   ![Seleccionar páginas para desplegar](../assets/select-rollout-pages.png)

1. Especifique si el trabajo de despliegue debe ejecutarse inmediatamente (**Now**) o en otra fecha u hora (**Later**).

   ![Definir el tiempo de lanzamiento](../assets/rollout-now-later.png)

Los lanzamientos se procesan como trabajos asincrónicos y se pueden comprobar en la página [***Estado de trabajos asincrónicos**.](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)

#### Despliegue un modelo desde el carril de referencia {#roll-out-a-blueprint-from-the-reference-rail}

1. En la consola **Sitios**, seleccione la página en la Live Copy y abra el panel **[Referencias](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** (en la barra de herramientas).
1. Seleccione la opción **Blueprint** de la lista para mostrar los modelos asociados con esta página.
1. Seleccione el modelo requerido de la lista.
1. Toque o haga clic en **Despliegue**.

   ![Implementar modelo a partir del carril de referencias](../assets/rollout-blueprint-from-references.png)

1. Se le pedirá que confirme los detalles del despliegue:

   * **Ámbito de despliegue**:

      Especifique si el ámbito es solo para la página seleccionada o si debe incluir las subpáginas.

   * **Programa**:

      Especifique si el trabajo de despliegue debe ejecutarse inmediatamente (**Now**) o en una fecha u hora posterior (**Later**).

      ![Definir el alcance y la programación del despliegue](../assets/rollout-scope-schedule.png)

1. Después de confirmar estos detalles, seleccione **Rollout** para realizar la acción.

Los lanzamientos se procesan como trabajos asincrónicos y se pueden comprobar en la página [**Estado de trabajos asincrónicos**.](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)

#### Implementar un modelo desde la información general de Live Copy {#roll-out-a-blueprint-from-the-live-copy-overview}

La acción [**Despliegue** también está disponible en la Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de modelo.

1. Abra [Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview) y seleccione una Página de modelo.
1. Seleccione **Despliegue** en la barra de herramientas.

   ![Información general de Live Copy](../assets/live-copy-overview-actions-blueprint.png)

1. Especifique las páginas y las páginas secundarias y, a continuación, confirme con la marca de verificación:

   ![Seleccionar páginas para el despliegue](../assets/select-rollout-pages.png)

1. Especifique si el trabajo de despliegue debe ejecutarse inmediatamente (**Now**) o en otra fecha u hora (**Later**).

   ![Definir programación de lanzamiento](../assets/rollout-now-later.png)

Los lanzamientos se procesan como trabajos asincrónicos y se pueden comprobar en la página [**Estado de trabajos asincrónicos**.](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)

### Sincronización de una Live Copy {#synchronizing-a-live-copy}

Sincronice una página de Live Copy para extraer los cambios de contenido del origen a Live Copy.

#### Sincronizar una Live Copy desde las propiedades de página {#synchronize-a-live-copy-from-page-properties}

Sincronice una Live Copy para extraer cambios del origen a la Live Copy.

>[!NOTE]
>
>La sincronización ejecuta las configuraciones de lanzamiento que utilizan el déclencheur [On Rollout](live-copy-sync-config.md#rollout-triggers).

1. En la consola **Sitios**, seleccione la página Live Copy y abra las propiedades.
1. Abra la pestaña **Live Copy**.
1. Toque o haga clic en **Sincronizar**.

   ![Botón Sincronizar](../assets/synchronize.png)

   Se solicitará confirmación, use **Sync** para continuar.

#### Sincronizar una Live Copy desde la información general de Live Copy {#synchronize-a-live-copy-from-the-live-copy-overview}

La acción [Sincronizar también está disponible en la Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de Live Copy.

1. Abra [Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview) y seleccione una página de Live Copy.
1. Seleccione **Sincronizar** en la barra de herramientas.
1. Confirme la acción **Despliegue** en el cuadro de diálogo después de especificar si desea incluir:

   * **Página y páginas secundarias**
   * **Página solamente**

   ![Desplegar páginas con o sin subpáginas](../assets/rollout-page-and-subpages.png)

## Cambio del contenido de Live Copy {#changing-live-copy-content}

Para cambiar el contenido de Live Copy, puede:

* Agregue párrafos a la página.
* Actualice el contenido existente rompiendo la herencia de Live Copy para cualquier página o componente.

>[!TIP]
>
>Si crea manualmente una nueva página en Live Copy, la nueva página será local para Live Copy, lo que significa que no tiene una página de origen correspondiente a la que esté adjunta.
>
>Como práctica recomendada para crear una página local que forme parte de la relación, es crear la página local en el origen y realizar un despliegue profundo. Esto creará la página localmente como Live Copies.

>[!NOTE]
>
>Pueden producirse conflictos si se crean nuevas páginas con el mismo nombre de página en la rama del modelo y en una rama de Live Copy dependiente.
>
>Estos [conflictos deben manejarse y resolverse en el momento del despliegue](rollout-conflicts.md).

### Adición de componentes a una página de Live Copy {#adding-components-to-a-live-copy-page}

Puede añadir componentes a una página de Live Copy en cualquier momento. El estado de herencia de Live Copy y su sistema de párrafos no controla la capacidad de añadir componentes.

Cuando la página Live Copy se sincroniza con la página de origen, los componentes añadidos permanecen inalterados. Consulte también [Cambio del orden de los componentes en una página de Live Copy.](#changing-the-order-of-components-on-a-live-copy-page)

>[!TIP]
>
>Los cambios realizados localmente en un componente marcado como contenedor no se sobrescribirán con el contenido del modelo en un lanzamiento. Consulte [Prácticas recomendadas de MSM](best-practices.md#components-and-container-synchronization) para obtener más información.

### Suspender la herencia de una página {#suspending-inheritance-for-a-page}

Cuando crea una Live Copy, la configuración de Live Copy se guarda en la página raíz de las páginas copiadas. Todas las páginas secundarias de la página raíz heredan las configuraciones de Live Copy. Los componentes de las páginas de Live Copy también heredan la configuración de Live Copy.

Puede suspender la herencia de Live Copy de una página de Live Copy para poder cambiar las propiedades y los componentes de la página. Al suspender la herencia, las propiedades y los componentes de la página ya no se sincronizan con el origen.

>[!TIP]
>
>También puede [separar una Live Copy](#detaching-a-live-copy) de su modelo para eliminar todas las conexiones. A diferencia de la suspensión de la herencia, la acción de desprendimiento es permanente e irreversible.

#### Suspender la herencia de las propiedades de página {#suspending-inheritance-from-page-properties}

Para suspender la herencia en una página:

1. Abra las propiedades de la página Live Copy mediante el comando **Ver propiedades** de la consola **Sitios** o utilizando **Información de página** en la barra de herramientas de la página.
1. Toque o haga clic en la pestaña **Live Copy**.
1. Seleccione **Suspender** en la barra de herramientas. A continuación, puede seleccionar:

   * **Suspender**: para suspender solo la página actual.
   * **Suspender con elementos secundarios**: para suspender la página actual junto con las páginas secundarias.

1. Seleccione **Suspender** en el cuadro de diálogo de confirmación.

#### Suspender herencia de la información general de Live Copy {#suspending-inheritance-from-the-live-copy-overview}

La acción [Suspender también está disponible en la Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de Live Copy.

1. Abra [Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview) y seleccione una página de Live Copy.
1. Seleccione **Suspender** en la barra de herramientas.
1. Seleccione la opción adecuada desde:

   * **Suspender**
   * **suspender con elto.sup.**

   ![suspender con elto.sup.](../assets/suspend-with-children.png)

1. Confirme la acción **Suspender** en el cuadro de diálogo **Suspender Live Copy**:

   ![Confirmar suspensión](../assets/confirm-suspend.png)

### Reanudar la herencia de una página {#resuming-inheritance-for-a-page}

Suspender la herencia de Live Copy de una página es una acción temporal. Una vez suspendida, la acción **Resume** está disponible, lo que le permite restablecer la relación activa.

![Reanudar herencia](../assets/resume-inheritance.png)

Al volver a habilitar la herencia, la página no se sincroniza automáticamente con el origen. Puede solicitar una sincronización, si es necesario:

* En el cuadro de diálogo **Reanudar**/**Revertir**; por ejemplo:

   ![Reanudar y sincronizar](../assets/resume-and-synch.png)

* En una etapa posterior, seleccionando manualmente la acción de sincronización.

>[!NOTE]
>
>Al volver a habilitar la herencia, la página no se sincroniza automáticamente con el origen. Si es necesario, puede solicitar manualmente una sincronización en el momento de reanudarla o más tarde.

#### Reanudar la herencia de las propiedades de página {#resuming-inheritance-from-page-properties}

Una vez [suspendida](#suspending-inheritance-from-page-properties) la acción **Reanudar** se convierte en la barra de herramientas de las propiedades de la página:

![Botón Reanudar](../assets/resume.png)

Cuando se selecciona, se muestra el cuadro de diálogo. Puede seleccionar una sincronización, si es necesario, y confirmar la acción.

#### Reanudar una página de Live Copy desde la información general de Live Copy {#resume-a-live-copy-page-from-the-live-copy-overview}

La acción [Reanudar también está disponible en la Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de Live Copy.

1. Abra [Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview) y seleccione una página de Live Copy que se haya suspendido. La página se mostrará como **HERENCIA CANCELADA**.
1. Seleccione **Reanudar** en la barra de herramientas.
1. Indique si desea sincronizar la página después de revertir la herencia y, a continuación, confirme la acción **Reanudar** en el cuadro de diálogo **Reanudar Live Copy**.

### Cambio de la profundidad de herencia (superficial/profunda) {#changing-inheritance-depth-shallow-deep}

En una Live Copy existente, puede cambiar la profundidad de una página, es decir, si se incluyen páginas secundarias.

* Cambio a una Live Copy superficial:

   * Tendrá un efecto inmediato y no es reversible.

   * Desasocia explícitamente las páginas secundarias de Live Copy. No se pueden conservar más modificaciones en niños si se deshacen.

   * Eliminará cualquier descendiente `LiveRelationships` aunque haya anidado `LiveCopies`.

* Cambio a una Live Copy profunda:

   * Deja las páginas secundarias intactas.
   * Para ver el efecto del conmutador, puede realizar un despliegue, las modificaciones de contenido se aplican según la configuración de lanzamiento.

* Cambie a una Live Copy superficial y, a continuación, vuelva a una copia profunda:

   * Trata a todos los elementos secundarios de la Live Copy (anteriormente) superficial como si se hubieran creado manualmente y, por lo tanto, se mueven utilizando `[oldname]_msm_moved name`.

Para especificar o cambiar la profundidad:

1. Abra las propiedades de la página Live Copy mediante el comando **Ver propiedades** de la consola **Sitios** o utilizando **Información de página** en la barra de herramientas de la página.
1. Toque o haga clic en la pestaña **Live Copy**.
1. En la sección **Configuration**, defina o borre la opción **Live Copy Inheritance** en función de si se incluyen las páginas secundarias:

   * Comprobado: una Live Copy profunda (se incluyen las páginas secundarias)
   * Sin marcar: Live Copy superficial (se excluyen las páginas secundarias)

   >[!CAUTION]
   >
   >Cambiar a una Live Copy superficial tendrá un efecto inmediato y no es reversible.
   >
   >Consulte [Live Copies - Composición](overview.md#live-copies-composition) para obtener más información.

1. Toque o haga clic en **Guardar** para mantener las actualizaciones.

### Cancelación de la herencia de un componente {#cancelling-inheritance-for-a-component}

Cancele la herencia de Live Copy de un componente para que el componente ya no se sincronice con el componente de origen. Si es necesario, puede habilitar la herencia en un momento posterior.

>[!NOTE]
>
>Al volver a habilitar la herencia, el componente no se sincroniza automáticamente con el origen. Puede solicitar manualmente una sincronización si es necesario.

Cancele la herencia para cambiar el contenido del componente o eliminar el componente:

1. Toque o haga clic en el componente cuya herencia desea cancelar.

   ![Herencia en la barra de herramientas de componentes](../assets/inheritance-toolbar.png)

1. En la barra de herramientas de componentes, toque o haga clic en el icono **Cancelar herencia**.

   ![Cancelar icono de herencia](../assets/cancel-inheritance-icon.png)

1. En el cuadro de diálogo Cancelar herencia, confirme la acción con **Yes**.

   La barra de herramientas de componentes se actualiza para incluir todos los comandos de edición (adecuados).

### Volver a habilitar la herencia para un componente {#re-enabling-inheritance-for-a-component}

Para habilitar la herencia para un componente, toque o haga clic en el icono **Volver a habilitar la herencia** de la barra de herramientas de componentes.

![Icono Volver a activar herencia](../assets/re-enable-inheritance-icon.png)

### Cambio del orden de los componentes en una página de Live Copy {#changing-the-order-of-components-on-a-live-copy-page}

Si una Live Copy contiene componentes que forman parte de un sistema de párrafos, la herencia de ese sistema de párrafos observa las siguientes reglas:

* Se puede modificar el orden de los componentes de un sistema de párrafos heredado, incluso con la herencia establecida.
* Al desplegar, el orden de los componentes se restaurará a partir del modelo. Si se agregaron nuevos componentes a Live Copy antes del lanzamiento, estos se reordenarán junto con los componentes por encima de los cuales se añadieron.
* Si se cancela la herencia del sistema de párrafos, el orden de los componentes no se restaurará durante el despliegue y permanecerá tal cual en Live Copy.

>[!NOTE]
>
>Al revertir una herencia cancelada en un sistema de párrafos, el orden de los componentes **no se restaurará automáticamente** del modelo. Puede solicitar manualmente una sincronización si es necesario.

Utilice el siguiente procedimiento para cancelar la herencia del sistema de párrafos.

1. Abra la página Live Copy .
1. Arrastre un componente existente a una nueva ubicación de la página.
1. En el cuadro de diálogo **Cancelar herencia**, confirme la acción con **Yes**.

### Omisión de las propiedades de una página de Live Copy {#overriding-properties-of-a-live-copy-page}

Las propiedades de página de una página Live Copy se heredan de la página de origen de forma predeterminada y no se pueden editar.

Puede cancelar la herencia de una propiedad cuando necesite cambiar el valor de la propiedad de Live Copy. Un icono de vínculo indica que la herencia está habilitada para la propiedad.

![Propiedades de página heredadas](../assets/properties-inherited.png)

Al cancelar la herencia, puede cambiar el valor de la propiedad. Un icono de vínculo roto indica que se ha cancelado la herencia.

![Propiedades no heredadas](../assets/properties-not-inherited.png)

Posteriormente, puede volver a habilitar la herencia para una propiedad si es necesario.

>[!NOTE]
>
>Al volver a habilitar la herencia, la propiedad de página Live Copy no se sincroniza automáticamente con la propiedad de origen. Puede solicitar manualmente una sincronización si es necesario.

1. Abra las propiedades de la página Live Copy mediante la opción **Ver propiedades** de la consola **Sitios** o el icono **Información de página** de la barra de herramientas de la página.
1. Para cancelar la herencia de una propiedad, toque o haga clic en el icono de vínculo que aparece a la derecha de la propiedad.

   ![Botón Cancelar herencia](../assets/cancel-inheritance-button.png)

1. En el cuadro de diálogo de confirmación **Cancelar herencia**, pulse o haga clic en **Sí**.

### Revertir propiedades de una página de Live Copy {#revert-properties-of-a-live-copy-page}

Para habilitar la herencia para una propiedad, toque o haga clic en el icono **Revertir herencia** que aparece junto a la propiedad.

![Botón Revertir herencia](../assets/revert-inheritance-button.png)

### Restablecer una página de Live Copy {#resetting-a-live-copy-page}

Puede restablecer una página de Live Copy para:

* Elimine todas las cancelaciones de herencia y
* Devuelva la página al mismo estado que la página de origen.

El restablecimiento afecta a los cambios realizados en las propiedades de la página, el sistema de párrafos y los componentes.

#### Restaurar una página de Live Copy desde las propiedades de página {#reset-a-live-copy-page-from-the-page-properties}

1. En la consola **Sites**, seleccione la página Live Copy y seleccione **Ver propiedades**.
1. Abra la pestaña **Live Copy**.
1. Seleccione **Reset** en la barra de herramientas.

   ![Botón Restablecer](../assets/reset.png)

1. En el cuadro de diálogo **Restaurar Live Copy**, confirme con **Restaurar**.

#### Restaurar una página de Live Copy desde la información general de Live Copy {#reset-a-live-copy-page-from-the-live-copy-overview}

La acción [**Reset** también está disponible en la Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de Live Copy.

1. Abra [Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview) y seleccione una página de Live Copy.
1. Seleccione **Reset** en la barra de herramientas.
1. Confirme la acción **Reset** en el cuadro de diálogo **Restaurar Live Copy**:

   ![Confirmar restablecimiento de Live Copy](../assets/reset-live-copy.png)

## Comparación de una página de Live Copy con una página de modelo {#comparing-a-live-copy-page-with-a-blueprint-page}

Para realizar un seguimiento de los cambios realizados, puede ver la página de modelo en **Referencias** y compararla con su página de Live Copy:

1. En la consola **Sitios**, [vaya a un modelo o a una página de Live Copy y selecciónela.](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources)
1. Abra el panel **[Referencias](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)** y, según el contexto, seleccione:

   * **Modelo**
   * **Live Copies**

1. Seleccione la Live Copy específica en función del contexto, o bien:

   * **Comparar con el modelo**
   * **Comparar con Live Copy**

   Por ejemplo:

   ![Comparación de Live Copies](../assets/compare-live-copy.png)

1. Las páginas Live Copy y modelo se abrirán en paralelo.

   Para obtener información completa sobre el uso de la función de comparación, consulte [Diferencias de página](/help/sites-cloud/authoring/features/page-diff.md).

## Desasociar una Live Copy {#detaching-a-live-copy}

La acción de desasociar elimina permanentemente la relación activa entre una Live Copy y su página de origen/modelo. Todas las propiedades relevantes para MSM se eliminan de Live Copy y las páginas de Live Copy se convierten en una copia independiente.

>[!CAUTION]
>
>No puede restablecer la relación activa después de desasociar Live Copy.
>
>Para eliminar la relación activa con la opción de reinstalarla más adelante, puede [cancelar la herencia de Live Copy](#suspending-inheritance-for-a-page) para la página.

Hay implicaciones sobre dónde dentro del árbol que utiliza **Desasociar**:

* **Desasociar en una página raíz de una Live Copy**

   Cuando esta operación se realiza en la página raíz de una Live Copy, se elimina la relación activa entre todas las páginas del modelo y su Live Copy.

   Los cambios adicionales en las páginas del modelo **no afectarán** a Live Copy.

* **Desasociar en una subpágina de una Live Copy**

   Cuando esta operación se realiza en una subpágina (o rama) dentro de una Live Copy:

   * La relación activa se elimina para esa subpágina (o rama) y
   * Las páginas (sub)de la rama de Live Copy se tratan como si se hubieran creado manualmente.

   Sin embargo, las páginas secundarias siguen estando sujetas a la relación activa de la rama principal, por lo que una nueva implementación de las páginas de modelo:

   1. Cambie el nombre de las páginas separadas:

      * Esto se debe a que MSM los considera como páginas creadas manualmente que causan un conflicto, ya que tienen el mismo nombre que las páginas de Live Copy que intenta crear.
   1. Cree una nueva página de Live Copy con el nombre original, que contenga los cambios de la implementación.

   >[!NOTE]
   >
   >Consulte [Conflictos de despliegue de MSM](rollout-conflicts.md) para obtener más información sobre estas situaciones.

### Desasociar una página de Live Copy de las propiedades de página {#detach-a-live-copy-page-from-the-page-properties}

Para separar una Live Copy:

1. En la consola **Sitios**, seleccione la página Live Copy y pulse o haga clic en **Ver propiedades**.
1. Abra la pestaña **Live Copy**.
1. En la barra de herramientas, seleccione **Desasociar**.

   ![Botón Separar](../assets/detach-button.png)

1. Se mostrará un cuadro de diálogo de confirmación, seleccione **Desasociar** para completar la acción.

### Desasociar una página de Live Copy de la información general de Live Copy {#detach-a-live-copy-page-from-the-live-copy-overview}

La acción [Desasociar también está disponible en la Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview), cuando se selecciona una página de Live Copy.

1. Abra [Información general de Live Copy](live-copy-overview.md#using-the-live-copy-overview) y seleccione una página de Live Copy.
1. Seleccione **Separar** en la barra de herramientas.
1. Confirme la acción **Desasociar** en el cuadro de diálogo **Desasociar Live Copy**:

   ![Desasociar una Live Copy](../assets/detach-live-copy.png)
