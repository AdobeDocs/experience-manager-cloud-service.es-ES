---
title: Administración de proyectos de traducción
description: Aprenda a crear y administrar proyectos de traducción automática y humana en AEM.
feature: Language Copy
role: Admin
exl-id: dc2f3958-72b5-4ae3-a224-93d8b258bc80
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '4077'
ht-degree: 96%

---

# Administración de proyectos de traducción {#managing-translation-projects}

Los proyectos de traducción le permiten administrar la traducción del contenido de AEM. Un proyecto de traducción es un tipo de [proyecto](/help/sites-cloud/authoring/projects/overview.md) de AEM que contiene recursos que se van a traducir a otros idiomas. Estos recursos son las páginas y activos de las [copias de idioma](preparation.md) que se crean a partir del idioma principal.

>[!TIP]
>
>Si acaba de empezar a traducir contenido, consulte [Recorrido de traducción de sitios,](/help/journey-sites/translation/overview.md) que es una ruta guiada a través de la traducción del contenido de AEM Sites mediante herramientas de traducción potentes, ideales para aquellos que no tienen experiencia en traducción o en la traducción de contenido de AEM AEM, y que utilizan herramientas de traducción potentes, que son ideales para aquellos que no tienen experiencia con la traducción o la traducción de contenido en la mayoría de los casos.

Cuando se añaden recursos a un proyecto de traducción, se crea un trabajo de traducción para ellos. Los trabajos proporcionan comandos e información de estado que se utilizan para administrar los flujos de trabajo de traducción humana y traducción automática que se ejecutan en los recursos.

Los proyectos de traducción son elementos de larga duración, definidos por el idioma y el método/proveedor de traducción para alinearse con la gobernanza organizativa para la globalización. Deben iniciarse una vez, ya sea durante la traducción inicial o a mano, y permanecer en vigor durante todas las actividades de actualización de contenido y traducción.

Los proyectos y trabajos de traducción se crean con los flujos de trabajo de preparación de la traducción. Estos flujos de trabajo tienen tres opciones, tanto para la traducción inicial (Crear y traducir) como para las actualizaciones (Actualizar traducción):

1. [Creación de un nuevo proyecto](#creating-translation-projects-using-the-references-panel)
1. [Adición a un proyecto existente](#adding-pages-to-a-translation-project)
1. [Solo estructura de contenido](#creating-the-structure-of-a-language-copy)

AEM detecta si se está creando un proyecto de traducción para la traducción inicial del contenido o para actualizar las copias de idioma ya traducidas. Cuando se crea un proyecto de traducción para una página y se indican las copias de idioma para las que se está traduciendo, AEM detecta si la página de origen ya existe en las copias de idioma de destino:

* **La copia de idioma no incluye la página:** AEM trata esta situación como la traducción inicial. La página se copia inmediatamente en el texto del idioma y se incluye en el proyecto. Cuando la página traducida se importa a AEM, AEM la copia directamente en la copia del idioma.
* **La copia de idioma ya incluye la página:** AEM trata esta situación como una traducción actualizada. Se crea un lanzamiento, se añade una copia de la página a este y se incluye en el proyecto. Los lanzamientos permiten revisar las traducciones actualizadas antes de enviarlas a la copia de idioma:

   * Cuando la página traducida se importa a AEM, sobrescribe la página en el lanzamiento.
   * La página traducida sobrescribe la copia de idioma solo cuando se promociona el lanzamiento.

Por ejemplo, la raíz lingüística `/content/wknd/fr` se crea para la traducción al francés del idioma principal `/content/wknd/en`. No hay más páginas en la copia en francés.

* Se crea un proyecto de traducción para la página `/content/wknd/en/products` y todas las secundarias, destinado a la copia en francés. Como la copia de idioma no incluye la página `/content/wknd/fr/products`, AEM copia inmediatamente la página `/content/wknd/en/products` y todas las secundarias a la copia en francés. Las copias también se incluyen en el proyecto de traducción.
* Se crea un proyecto de traducción para la página `/content/wknd/en` y todas las secundarias, destinado a la copia en francés. Como la copia de idioma incluye la página que corresponde con la página `/content/wknd/en` (la raíz del idioma), AEM copia la página `/content/wknd/en` y todas las secundarias y las añade a un lanzamiento. Las copias también se incluyen en el proyecto de traducción.

## Traducción desde la consola Sites {#performing-initial-translations-and-updating-existing-translations}

Los proyectos de traducción se pueden crear o actualizar directamente desde la consola Sites.

### Creación de proyectos de traducción mediante el panel Referencias {#creating-translation-projects-using-the-references-panel}

Cree proyectos de traducción para poder ejecutar y administrar el flujo de trabajo de traducción de los recursos del idioma principal. Cuando cree proyectos, especifique la página en el idioma principal que está traduciendo y las copias de idioma para las que va a hacer la traducción:

* La configuración de nube del marco de trabajo de integración de traducciones asociado a la página seleccionada determina muchas propiedades de los proyectos de traducción, como el flujo de trabajo de traducción que se va a utilizar.
* Se crea un proyecto para cada copia de idioma seleccionada.
* Se genera una copia de la página seleccionada y de los recursos asociados, que se añaden a cada proyecto. Estas copias se envían después al proveedor de traducciones para que las traduzca.

Puede especificar que las páginas secundarias de la página seleccionada también estén seleccionadas. En este caso, también se añaden copias de las páginas secundarias a cada proyecto para que se traduzcan. Cuando alguna página secundaria está asociada con diferentes configuraciones del marco de trabajo de integración de traducciones, AEM crea proyectos adicionales.

También puede [crear proyectos de traducción manualmente](#creating-a-translation-project-using-the-projects-console).

>[!NOTE]
>
>Para crear un proyecto, la cuenta debe ser miembro del grupo `project-administrators`.

### Traducciones iniciales y actualización de traducciones {#initial-and-updating}

El panel Referencias indica si está actualizando las copias de idioma existentes o creando la primera versión de estas. Cuando existe una copia de idioma para la página seleccionada, aparece la pestaña Actualizar copias de idioma para proporcionar acceso a los comandos relacionados con el proyecto.

![Actualizar copias de idioma](../assets/update-language-copies.png)

Después de traducir, puede [revisar la traducción](#reviewing-and-promoting-updated-content) antes de sobrescribir la copia de idioma con ella. Cuando no existe ninguna copia de idioma para la página seleccionada, aparece la pestaña Crear y traducir para dar acceso a los comandos relacionados con el proyecto.

![Crear y traducir](../assets/create-and-translate.png)

### Creación de proyectos de traducción para una copia de idioma nueva {#create-translation-projects-for-a-new-language-copy}

1. Utilice la consola Sites para seleccionar la página que está añadiendo a los proyectos de traducción.

1. En la barra de herramientas, abra el carril **Referencias**.

   ![Referencias](../assets/references.png)

1. Seleccione **Copias de idioma** y, a continuación, las copias de idioma para las que está traduciendo las páginas de origen.
1. Pulse o haga clic en **Crear y traducir** y configure el trabajo de traducción:

   * Utilice la lista desplegable **Idiomas** para seleccionar la copia de idioma que desea traducir. Seleccione otros idiomas según sea necesario. Los idiomas que aparecen en la lista se corresponden con las [raíces de idioma que ha creado](preparation.md#creating-a-language-root).
      * Al seleccionar varios idiomas, se crea un proyecto con un trabajo de traducción para cada uno.
   * Para traducir la página seleccionada y todas las secundarias, escoja **Seleccionar todas las páginas secundarias**. Para traducir solo la página que ha seleccionado, desactive la opción.
   * En **Proyecto**, seleccione **Crear proyecto de traducción**.
   * De forma opcional, para **Maestro del proyecto**, seleccione un proyecto del que heredar funciones de usuario y permisos.
   * En **Título**, escriba un nombre para el proyecto.

   ![Creación del proyecto de traducción](../assets/create-translation-project.png)

1. Haga clic o pulse **Crear**.

### Creación de proyectos de traducción para una copia de idioma existente {#create-translation-projects-for-an-existing-language-copy}

1. Utilice la consola Sites para seleccionar la página que está añadiendo a los proyectos de traducción.

1. En la barra de herramientas, abra el carril **Referencias**.

   ![Referencias](../assets/references.png)

1. Seleccione **Copias de idioma** y, a continuación, las copias de idioma para las que está traduciendo las páginas de origen.
1. Pulse o haga clic en **Actualizar copias de idioma** y, a continuación, configure el trabajo de traducción:

   * Para traducir la página seleccionada y todas las secundarias, escoja **Seleccionar todas las páginas secundarias**. Para traducir solo la página que ha seleccionado, desactive la opción.
   * En **Proyecto**, seleccione **Crear proyecto de traducción**.
   * De forma opcional, para **Maestro del proyecto**, seleccione un proyecto del que heredar funciones de usuario y permisos.
   * En **Título**, escriba un nombre para el proyecto.

   ![Creación de un proyecto para actualizar copias de idioma](../assets/create-update-language-copies-project.png)

1. Haga clic o pulse **Crear**.

### Adición de páginas a un proyecto de traducción {#adding-pages-to-a-translation-project}

Una vez creado un proyecto de traducción, puede usar el carril **Recursos** para añadir páginas al proyecto. Agregarlas resulta útil cuando se incluyen páginas de distintas ramas en el mismo proyecto.

Al añadir páginas a un proyecto de traducción, estas se incluyen en un nuevo trabajo de traducción. También puede [agregar páginas a un trabajo existente](#adding-pages-assets-to-a-translation-job).

Al igual que al crear un nuevo proyecto, al anexar páginas, se añaden copias de estas a un lanzamiento cuando es necesario para evitar sobrescribir las copias de idioma existentes. Consulte [Creación de proyectos de traducción para copias de idiomas existentes](#performing-initial-translations-and-updating-existing-translations).

1. Utilice la consola Sites para seleccionar la página que está agregando al proyecto de traducción.

1. En la barra de herramientas, abra el carril **Referencias**.

   ![Referencias](../assets/references.png)

1. Seleccione **Copias de idioma** y, a continuación, las copias de idioma para las que está traduciendo las páginas de origen.

   ![Actualización de las copias de idiomas desde el carril de referencias](../assets/update-language-copies-references.png)

1. Pulse o haga clic en **Actualizar copias de idioma** y, a continuación, configure las propiedades:

   * Para traducir la página seleccionada y todas las secundarias, escoja **Seleccionar todas las páginas secundarias**. Para traducir solo la página que ha seleccionado, desactive la opción.
   * En **Proyecto**, seleccione **Añadir a un proyecto de traducción existente**.
   * Seleccione el proyecto en **Proyecto de traducción existente**.

   >[!NOTE]
   >
   >El idioma de destino definido en el proyecto de traducción debe coincidir con la ruta de la copia de idioma, como se muestra en el carril de referencias.

1. Haga clic o pulse en **Actualizar**.

### Creación de la estructura de una copia de idioma {#creating-the-structure-of-a-language-copy}

Es posible crear únicamente la estructura de la copia de idioma, lo que le permite copiar el contenido y los cambios estructurales del idioma principal en copias de idioma (no traducidas). Esto no está relacionado con un trabajo o proyecto de traducción. Puede usar esto para mantener a los maestros de idiomas sincronizados, incluso sin traducción.

Rellene la copia de idioma para que albergue contenido de la lengua principal que está traduciendo. Antes de rellenar la copia de idioma, debe tener [creada su raíz del idioma](preparation.md#creating-a-language-root).

1. Utilice la consola Sites para seleccionar la raíz de idioma del idioma principal que está utilizando como origen.
1. Abra el carril de referencias tocando o haciendo clic en **Referencias** en la barra de herramientas.

   ![Referencias](../assets/references.png)

1. Seleccione **Copias de idioma** y, a continuación, las copias de idioma que desee rellenar.

   ![Selección de copias de idioma](../assets/language-copy-structure-select.png)

1. Pulse o haga clic en **Actualizar copias de idioma** para mostrar las herramientas de traducción y configurar las propiedades:

   * Seleccione la opción **Seleccionar todas las páginas secundarias**.
   * Para **Proyecto**, seleccione **Crear solo estructura**.

   ![Solo estructura](../assets/language-copy-structure-only.png)

1. Haga clic o pulse en **Actualizar**.

### Actualización de la memoria de traducción {#updating-translation-memory}

Las ediciones manuales del contenido traducido se pueden sincronizar de nuevo con el sistema de gestión de traducciones (TMS) para mejorar su memoria de traducción.

1. Desde la consola Sites, después de actualizar el contenido de texto en una página traducida, seleccione **Actualizar memoria de traducción**.
1. Una vista de lista muestra una comparación en paralelo de la fuente y la traducción de cada componente de texto editado. Seleccione qué actualizaciones de traducción deben sincronizarse con la memoria de traducción y **Actualizar memoria**.

![Comparación de cambios de la memoria de traducción](../assets/update-translation-memory-compare.png)

AEM actualiza la traducción de las cadenas existentes en la memoria de traducción del sistema de administración de etiquetas configurado.

* La acción actualiza la traducción de cadenas existentes en la memoria de traducción del sistema de administración de etiquetas configurado.
* No crea nuevos trabajos de traducción.
* Envía las traducciones de vuelta al sistema de administración de etiquetas, a través de la API de traducción de AEM (se muestra a continuación).

Para usar esta función, haga lo siguiente:

* Configure un sistema de administración de etiquetas para su uso con AEM.
* El conector debe implementar el método [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html).
   * El código dentro de este método determina qué sucede con la solicitud de actualización de memoria de traducción.
   * El marco de traducción de AEM envía los pares de valor de cadena (traducción original y actualizada) al sistema de gestión de etiquetas mediante esta implementación de método.

Las actualizaciones de la memoria de traducción se pueden interceptar y enviar a un destino personalizado, en los casos en que se utilice una memoria de traducción propia.

### Comprobación del estado de traducción de una página {#check-translation-status}

Se puede seleccionar una propiedad en la vista de lista de la consola Sites que muestre si una página se ha traducido, está en proceso de traducción o aún no se ha traducido.

1. En la consola del sitio, cambie a la [vista de lista](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources).
1. Pulse o haga clic en **Configuración de vista** en la lista desplegable de vista.
1. En el cuadro de diálogo, marque la propiedad **Traducido** y pulse o haga clic en **Actualizar**.

La consola Sites ahora muestra la columna **Traducido** con el estado de traducción de las páginas enumeradas.

![Estado de traducción en la vista de lista](../assets/translation-status-list-view.png)

## Administración de proyectos de traducción desde la consola Proyectos

Se puede acceder a muchas tareas de traducción y a muchas opciones avanzadas en la consola Proyectos.

### Explicación de la consola Proyectos

Los proyectos de traducción, en AEM, utilizan la [consola Proyectos AEM estándar](/help/sites-cloud/authoring/projects/overview.md). AEM Si no está familiarizado con proyectos de, revise esa documentación.

Como cualquier otro proyecto, un proyecto de traducción está compuesto por mosaicos que presentan una visión general de las tareas del proyecto.

![Proyecto de traducción](../assets/translation-project.png)

* **Resumen**: una visión general del proyecto
* **Tareas**: una o más tareas de traducción
* **Equipo**: usuarios que colaboran en el proyecto de traducción
* **Tareas**: elementos que deben completarse como parte del esfuerzo de traducción

Utilice los botones de comandos y elipsis de la parte superior e inferior de los mosaicos (respectivamente) para acceder a los controles y las opciones de los distintos mosaicos.

![Botón de comandos](../assets/context.png)

![Botón de puntos suspensivos](../assets/ellipsis.png)

### Creación de un proyecto de traducción mediante la consola Proyectos {#creating-a-translation-project-using-the-projects-console}

Puede crear manualmente un proyecto de traducción si prefiere usar la consola Proyectos en lugar de la consola Sites.

>[!NOTE]
>
>Para crear un proyecto, la cuenta debe ser miembro del grupo `project-administrators`.

Cuando cree manualmente un proyecto de traducción, debe proporcionar valores para las siguientes propiedades relacionadas con la traducción, además de las [propiedades básicas](/help/sites-cloud/authoring/projects/managing.md#creating-a-project):

* **Nombre:** nombre del proyecto
* **Idioma de origen:** el idioma del contenido de origen
* **Idioma de destino:** idioma o idiomas a los que se traduce el contenido
   * Si se seleccionan varios idiomas, se crea un trabajo para cada idioma dentro del proyecto.
* **Método de traducción:** seleccione **Traducción humana** para indicar que la traducción se debe llevar a cabo manualmente.

1. En la barra de herramientas de la consola Proyectos, pulse o haga clic en **Crear**.
1. Seleccione la plantilla **Proyecto de traducción** y, a continuación, haga clic o pulse en **Siguiente**.
1. Introduzca valores en la pestaña de propiedades **Básicas**.
1. Pulse o haga clic en **Avanzadas** y proporcione valores para las propiedades relacionadas con la traducción.
1. Haga clic o pulse **Crear**. En el cuadro de confirmación, toque o haga clic en **Listo** para volver a la consola de proyectos, o toque o haga clic en **Abrir proyecto** para abrir y comenzar a administrar el proyecto.

### Adición de páginas y activos a un trabajo de traducción {#adding-pages-assets-to-a-translation-job}

Puede agregar páginas, activos o etiquetas al trabajo de su proyecto de traducción. Para agregar páginas o activos:

1. En la parte inferior del mosaico del trabajo de traducción del proyecto de traducción, toque o haga clic en los puntos suspensivos.

   ![Mosaico de trabajo de traducción](../assets/translation-job.png)

1. En la siguiente ventana, toque o haga clic en el botón **Agregar** en la barra de herramientas y, a continuación, seleccione **Activos/Páginas**.

   ![Agregar páginas](../assets/add-to-project.png)

1. En la ventana modal, seleccione el elemento superior de la rama que desea agregar y, a continuación, toque o haga clic en el icono de marca de verificación. La selección múltiple está habilitada en esta ventana.

   ![Seleccionar páginas](../assets/select-pages.png)

1. También puede seleccionar el icono de búsqueda para buscar fácilmente páginas o activos que desee agregar a su trabajo de traducción.

   ![Buscar contenido](../assets/search-for-content.png)

1. Una vez seleccionado, toque o haga clic en **Seleccionar**. Sus páginas o activos se añaden al trabajo de traducción.

>[!TIP]
>
>Este método agrega páginas/activos y sus tareas secundarias al proyecto. Seleccione **Activo/Página (sin tareas secundarias)** si solo desea agregar los elementos principales.

### Adición de etiquetas a un trabajo de traducción {#adding-tags-to-a-translation-job}

Puede añadir etiquetas a un proyecto de traducción similar a [cómo agregar activos y páginas a un proyecto](#adding-pages-assets-to-a-translation-job). Solo seleccione **Etiquetas** en el menú **Agregar**, a continuación, siga los mismos pasos.

### Ver detalles del proyecto de traducción {#seeing-translation-project-details}

Se puede acceder a las propiedades del proyecto de traducción mediante el botón de puntos suspensivos del mosaico resumen del proyecto. Además de la [información del proyecto](/help/sites-cloud/authoring/projects/overview.md#project-info) genérica, las propiedades del proyecto de traducción contienen características específicas de la traducción.

En el proyecto de traducción, toque o haga clic en los puntos suspensivos en la parte inferior del mosaico Resumen de traducción. La mayoría de las propiedades específicas del proyecto se encuentran en la pestaña **Avanzadas**.

* **Idioma de origen:** el idioma de las páginas que se están traduciendo
* **Idioma de destino:** el o los idiomas a los que se traducen las páginas
* **Configuración de nube:** la configuración de nube para el conector del servicio de traducción que se utiliza para el proyecto
* **Método de traducción:** el flujo de trabajo de traducción, ya sea **Traducción humana** o **Traducción automática**
* **Proveedor de traducción:** el proveedor de servicios de traducción que realiza la traducción
* **Categoría de contenido** (traducción automática): la categoría de contenido que se utiliza para la traducción
* **Credencial del proveedor de traducción:** las credenciales para iniciar sesión en el proveedor
* **Promocionar automáticamente los lanzamientos de traducción:** después de recibir contenido traducido, los lanzamientos de traducción se promocionan automáticamente
   * **Eliminar lanzamiento después de la promoción:** si los lanzamientos de traducción se promocionan automáticamente, se elimina el lanzamiento después de la promoción
* **Aprobar traducciones automáticamente:** después de recibir el contenido traducido, los trabajos de traducción se aprueban automáticamente
* **Repetir traducción:** configurar la ejecución recurrente de un proyecto de traducción, seleccionando la frecuencia con la que el proyecto creará y ejecutará automáticamente los trabajos de traducción

Cuando se crea un proyecto utilizando el carril de referencias de una página, estas propiedades se configuran automáticamente en función de las propiedades de la página de origen.

![Propiedades del proyecto de traducción](../assets/translation-project-properties.png)

### Monitorización del estado de un trabajo de traducción {#monitoring-the-status-of-a-translation-job}

El mosaico de trabajo de traducción de un proyecto de traducción proporciona el estado de un trabajo de traducción y la cantidad de páginas y activos en el trabajo.

![Trabajo de traducción](../assets/translation-job.png)

En la tabla siguiente se describe cada estado que puede tener un trabajo o elemento del trabajo:

| Estado | Descripción |
|---|---|
| **Borrador** | El trabajo de traducción no se ha iniciado. Los trabajos de traducción están en el estado **Borrador** cuando se crean. |
| **Enviado** | Los archivos del trabajo de traducción tienen este estado cuando se han enviado correctamente al servicio de traducción. Este estado se puede producir después de que el comando **Ámbito de la solicitud** o **Inicio** se emita. |
| **Previsión solicitada** | Para el flujo de trabajo de traducción humana, los archivos del trabajo se han enviado al proveedor de traducción para que los examine. Este estado aparece después de que el comando **Ámbito de la solicitud** se emita. |
| **Previsión finalizada** | El proveedor ha creado un ámbito para el trabajo de traducción. |
| **Asignado para traducción** | El propietario del proyecto ha aceptado el ámbito. Este estado indica que el proveedor de traducción debe empezar a traducir los archivos del trabajo. |
| **Traducción en progreso** | Para un trabajo, la traducción de uno o más archivos del trabajo aún no está completa. Para un elemento del trabajo, el artículo se está traduciendo. |
| **Traducido** | Para un trabajo, se ha completado la traducción de todos los archivos del trabajo. Para un artículo del trabajo, el artículo se traduce. |
| **Listo para revisión** | El elemento del trabajo se traduce y el archivo se ha importado a AEM. |
| **Completar** | El propietario del proyecto ha indicado que el contrato de traducción ha concluido. |
| **Cancelar** | Indica que el proveedor de traducción debe dejar de trabajar en un trabajo de traducción. |
| **Actualización de errores** | Se ha producido un error al transferir archivos entre AEM y el servicio de traducción. |
| **Estado desconocido** | Se ha producido un error desconocido. |

Para ver el estado de cada archivo en el trabajo, toque o haga clic en los puntos suspensivos en la parte inferior del mosaico.

### Configuración de la fecha de entrega de los trabajos de traducción {#setting-the-due-date-of-translation-jobs}

Especifique la fecha antes de la cual el proveedor de traducción debe devolver los archivos traducidos. La configuración de la fecha de entrega funciona correctamente solo cuando el proveedor de traducción que está utilizando admite esta función.

1. Toque o haga clic en los puntos suspensivos en la parte inferior del mosaico de resumen de la traducción.

   ![Mosaico de resumen de traducción](../assets/translation-summary-tile.png)

1. En la pestaña **Básico**, utilice el selector de fechas de la propiedad **Fecha de entrega** para seleccionar la fecha de entrega.

   ![Propiedades del proyecto de traducción](../assets/translation-project-properties-basic.png)

1. Haga clic o pulse **Guardar y cerrar**.

### Creación de ámbitos para un trabajo de traducción {#scoping-a-translation-job}

Defina un trabajo de traducción para obtener una estimación del coste de su proveedor de servicios de traducción. Cuando se define un trabajo, los archivos de origen se envían al proveedor de traducción que compara el texto con su grupo de traducciones almacenadas (memoria de traducción). Normalmente, el ámbito es el número de palabras que se deben traducir.

Para obtener más información sobre los resultados de ámbito, póngase en contacto con el proveedor de traducción.

>[!NOTE]
>
>El ámbito es opcional y solo se aplica a la traducción humana. Puede comenzar un trabajo de traducción sin ámbitos.

Cuando se define un trabajo de traducción, el estado del trabajo es **Ámbito solicitado**. Cuando el proveedor de traducción devuelve el ámbito, el estado se cambia a **Ámbito completado**. Cuando finalice el ámbito, puede utilizar el comando **Mostrar ámbito** para revisar los resultados de creación de ámbitos.

El ámbito funciona correctamente solo cuando el proveedor de traducción que está utilizando admite esta función.

1. En la consola de proyectos, abra el proyecto de traducción.
1. En el título del trabajo de traducción, pulse o haga clic en el menú de comandos y, a continuación, pulse o haga clic en **Ámbito de la solicitud**.
1. Cuando el estado del trabajo cambia a **Ámbito completado**, toque o haga clic en el menú de comandos y, a continuación, toque o haga clic en **Mostrar ámbito**.

### Inicio de trabajos de traducción {#starting-translation-jobs}

Inicie un trabajo de traducción para traducir las páginas de origen al idioma de destino. La traducción se realiza según los valores de propiedad del mosaico resumen de la traducción.

Puede comenzar un trabajo individual desde el proyecto.

1. En la consola de proyectos, abra el proyecto de traducción.
1. En el mosaico del trabajo de traducción, toque o haga clic en el menú de comandos y, a continuación, toque o haga clic en **Inicio**.
1. En el cuadro de diálogo de acción que confirma el inicio de la traducción, toque o haga clic en **Cerrar**.

Después de iniciar el trabajo de traducción, el mosaico del trabajo de traducción muestra la traducción en estado **En progreso**.

También puede iniciar todos los trabajos de traducción de un proyecto.

1. En la consola del proyecto, seleccione el proyecto de traducción.
1. En la barra de herramientas, toque o haga clic en **Iniciar trabajos de traducción**.
1. En el cuadro de diálogo, revise la lista de trabajos que se han iniciado y, a continuación, confirme con **Inicio** o cancelar con **Cancelar**.

### Cancelación de un trabajo de traducción {#canceling-a-translation-job}

Cancelar un trabajo de traducción para detener el proceso de traducción e impedir que el proveedor de traducción realice más traducciones. Puede cancelar un trabajo cuando el trabajo tenga el estado **Comprometido para traducción** o **Traducción en curso**.

1. En la consola de proyectos, abra el proyecto de traducción.
1. En el mosaico del trabajo de traducción, toque o haga clic en el menú de comandos y, a continuación, toque o haga clic en **Cancelar**.
1. En el cuadro de diálogo de acción que confirma la cancelación de la traducción, toque o haga clic en **OK**.

### Aceptar y rechazar flujo de trabajo {#accept-reject-workflow}

Cuando el contenido regresa después de la traducción y se encuentra en el estado **Listo para revisión**, puede ir al trabajo de traducción y aceptar/rechazar contenido.

Si selecciona **Rechazar traducción**, tiene la opción de agregar un comentario.

El rechazo de contenido lo devuelve al proveedor de traducción, donde puede ver el comentario.

### Finalización y archivado de trabajos de traducción {#completing-and-archiving-translation-jobs}

Complete un trabajo de traducción después de haber revisado los archivos traducidos del proveedor.

1. En la consola de proyectos, abra el proyecto de traducción.
1. En el mosaico del trabajo de traducción, toque o haga clic en el menú de comandos y, a continuación, toque o haga clic en **Completar**.
1. El trabajo ahora tiene el estado **Completo**.

Para los flujos de trabajo de traducción humana, completar una traducción indica al proveedor que el contrato de traducción se ha cumplido y que debe guardar la traducción en su memoria de traducción.

Archive el trabajo de traducción una vez completado para ya no ver los detalles del estado del trabajo.

1. En la consola de proyectos, abra el proyecto de traducción.
1. En el mosaico del trabajo de traducción, toque o haga clic en el menú de comandos y luego, en **Archivo**.

Al archivar el trabajo, el mosaico del trabajo de traducción se elimina del proyecto.

## Revisión y uso del contenido traducido {#reviewing-and-promoting-updated-content}

Puede utilizar la consola Sitios para revisar contenido, comparar copias de idiomas y activar el contenido.

### Promocionar contenido actualizado {#promoting-updated-content}

Cuando el contenido se traduce para una copia de idioma existente, revise las traducciones, realice cambios si es necesario y, a continuación, promueva las traducciones para moverlo a la copia de idioma. Puede revisar los archivos traducidos cuando el trabajo de traducción muestre el estado **Listo para revisión**.

![Trabajo listo para revisión](../assets/job-ready-for-review.png)

1. Seleccione la página en el patrón de idioma, toque o haga clic en **Referencias** y luego, en **Copias de idioma**.
1. Toque o haga clic en la copia de idioma para revisarla.

   ![Copia de idioma lista para revisión](../assets/language-copy-ready-for-review.png)

1. Toque o haga clic en **Lanzamiento** para mostrar los comandos relacionados con el lanzamiento.

   ![Lanzamiento](../assets/language-copy-launch.png)

1. Para abrir la copia de lanzamiento de la página para revisar y editar el contenido, haga clic en **Abrir página**.
1. Después de revisar el contenido y de realizar los cambios necesarios, para promocionar la copia de lanzamiento, haga clic en **Promocionar**.
1. En la página **Promocionar lanzamiento**, especifique qué páginas promocionar y, a continuación, toque o haga clic en **Promocionar**.

### Comparación de copias de idioma {#comparing-language-copies}

Para comparar las copias de idioma con el maestro de idioma:

1. En la consola Sites, vaya a la copia de idioma que desee comparar.
1. Abra el [Carril referencias](/help/sites-cloud/authoring/getting-started/basic-handling.md#references).
1. En el encabezado **Copias**, seleccione **Copias de idioma.**
1. Seleccione la copia de idioma específica y, a continuación, puede hacer clic en **Comparar con maestro** o **Comparar con anterior** si procede.

   ![Comparar copias de idioma](../assets/language-copy-compare.png)

1. Las dos páginas (inicio y origen) se abren en paralelo.
   * Para obtener información completa sobre el uso de esta funcionalidad, consulte [Diferencias de página](/help/sites-cloud/authoring/features/page-diff.md).

## Mover una página de origen o cambiarle el nombre {#move-source}

Si una página de origen ya traducida necesita ser [cambiada de nombre o movida](/help/sites-cloud/authoring/fundamentals/organizing-pages.md#moving-or-renaming-a-page), volver a traducir la página después del traslado creará una nueva copia de idioma basada en el nuevo nombre/ubicación de la página. La copia de idioma antigua basada en el nombre/ubicación anterior seguirá ahí.

La práctica recomendada en este escenario es seguir este procedimiento:
1. Cancele la publicación de las copias de idioma asociadas con la página de origen que desee mover.
1. Elimínelas.
1. Cree nuevas copias de idioma a partir de la página de origen que acaba de mover.
1. Publique las copias de idioma recién creadas.

## Importación y exportación de trabajos de traducción {#import-export}

Aunque AEM ofrece varias soluciones de traducción e interfaces, también es posible importar y exportar manualmente la información del trabajo de traducción.

### Exportación de un trabajo de traducción {#exporting-a-translation-job}

Puede descargar el contenido de un trabajo de traducción, por ejemplo, para enviarlo a un proveedor de traducción que no esté integrado con AEM a través de un conector o para revisar el contenido.

1. En el menú desplegable del mosaico del trabajo de traducción, toque o haga clic en **Exportar**.
1. En el cuadro de diálogo, toque o haga clic en **Descargar archivo exportado**, y si es necesario, utilice el cuadro de diálogo del explorador web para guardar el archivo.
1. En el cuadro de diálogo, toque o haga clic en **Cerrar**.

### Importación de un trabajo de traducción {#importing-a-translation-job}

Puede importar contenido traducido a AEM, por ejemplo, cuando el proveedor de traducción se lo envía porque no están integrados con AEM a través de un conector.

1. En el menú desplegable del mosaico del trabajo de traducción, toque o haga clic en **Importar**.
1. Utilice el cuadro de diálogo del explorador web para seleccionar el archivo que desea importar.
1. En el cuadro de diálogo, pulse o haga clic en **Cerrar**.
