---
title: Crear y organizar páginas
description: Crear y organizar páginas con AEM
exl-id: c57096ca-34fe-4b19-98e0-8f3cd43cf24e
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: ht
source-wordcount: '2561'
ht-degree: 100%

---

# Crear y organizar páginas {#creating-and-organizing-pages}

En este documento se describe cómo crear y administrar páginas con Adobe Experience Manager Cloud Service para luego poder [crear contenido](/help/sites-cloud/authoring/fundamentals/editing-content.md) en esas páginas.

>[!NOTE]
>
>Su cuenta necesita los derechos de acceso y permisos adecuados para realizar acciones en las páginas, como crear, copiar, mover, eliminar o editar.
>
>Si se producen problemas, le sugerimos que se ponga en contacto con el administrador del sistema.

<!--
>Your account needs the [appropriate access rights](/help/sites-administering/security.md) and [permissions](/help/sites-administering/security.md#permissions) to take action on pages such as create, copy, move, edit, and delete.
-->

>[!TIP]
>
>Existen varios [métodos abreviados del teclado](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md) que puede utilizar desde la consola de sitios web, y que le permitirán organizar las páginas de forma más eficaz.

## Organizar el sitio web {#organizing-your-website}

Como creador, deberá organizar el sitio web dentro de AEM. Esto implica crear y dar nombre a las páginas de contenido para que:

* Pueda encontrarlas con facilidad en el entorno de creación
* Los usuarios que visiten el sitio web puedan explorarlas fácilmente en el entorno de publicación

También puede usar [carpetas](#creating-a-new-folder) para organizar el contenido.

La estructura de un sitio web se puede considerar como un árbol que alberga las páginas de contenido. Los nombres de estas páginas de contenido se usan para formar las URL, y los títulos se muestran cuando se visualiza el contenido de la página.

A continuación se muestra un ejemplo del sitio [WKND Tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=es), donde se accede a un artículo sobre parques de patinaje (`la-skateparks`):

`http://<host>:<port>/editor.html/content/wknd/en/sports/la-skateparks.html`

```xml
 /content
 /wknd
  /en
   /music
    /...
   /sports
    /la-skateparks
    /five-gyms-la
    /mountain-bike-routes
   /shopping
    /...
   /art
    /...
   /...
```

Esta estructura puede verse desde la consola **Sitios**, donde puede [desplazarse por las páginas de su sitio web](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) y llevar a cabo acciones en las páginas. También puede crear sitios nuevos y [páginas nuevas](#creating-a-new-page).

Desde cualquier punto, podrá ver la rama hacia arriba desde las rutas en la barra de encabezado:

![Uso de rutas de exploración para navegar](/help/sites-cloud/authoring/assets/organizing-breadcrumbs.png)

### Convenciones de nomenclatura de páginas {#page-naming-conventions}

Cuando se crea una nueva página aparecen dos campos clave:

* **[Título](#title)**:

   * Se muestra al usuario en la consola, en la parte superior del contenido de la página al editar. 
   * Este campo es obligatorio.

* **[Nombre](#name)**:

   * Se usa para generar la URI.
   * Es opcional que el usuario especifique algo en este campo. Si no se especifica, el nombre se deriva del título. Consulte la siguiente sección [Restricciones de nombres de páginas y Prácticas recomendadas](#page-name-restrictions-and-best-practices) para obtener más detalles.

#### Restricciones de nombres de páginas y prácticas recomendadas {#page-name-restrictions-and-best-practices}

El **título** y el **nombre** de la página se pueden crear por separado, pero están relacionados:

* Al crear una página, solo es necesario el campo **Título**. Si no se proporciona ningún **nombre** durante la creación de la página, AEM genera un nombre a partir de los 64 primeros caracteres del título (observe el conjunto de validación a continuación). Solo se utilizan los 64 primeros caracteres para ofrecer compatibilidad con la práctica recomendada de nombres de página cortos.
* Si el autor especifica manualmente un nombre de página, el límite de 64 caracteres no se aplica. Sin embargo, es posible que se produzcan otras limitaciones técnicas en la longitud del nombre de la página.

>[!TIP]
>
>Al definir un nombre de página, se recomienda que sea lo más corto y expresivo posible para que el lector pueda entenderlo con facilidad. Para obtener más información, consulte la [guía de estilo W3C](https://www.w3.org/Provider/Style/TITLE.html) para el elemento de `title`.
>
>Además, recuerde que algunos exploradores (por ejemplo, las versiones anteriores de IE) solo aceptan URL con una longitud determinada, por lo que también existen motivos técnicos para mantener los nombres de las páginas cortos. 

Al crear una página nueva, AEM [valida su nombre según las convenciones](/help/implementing/developing/introduction/naming-conventions.md) que establecen tanto AEM como JCR.

El mínimo permitido de caracteres es:

* `a` hasta `z`
* `A` hasta `Z`
* `0` hasta `9`
* `_` (guion bajo)
* `-` (guion/signo menos)

Para obtener toda la información sobre los caracteres permitidos, consulte las [convenciones de nomenclatura](/help/implementing/developing/introduction/naming-conventions.md).

>[!NOTE]
>
>Los nombres de las páginas están limitados a 150 caracteres.

#### Título {#title}

Si proporciona solo un **título** de página al crear una nueva página, AEM derivará el **nombre** de página de esta cadena y lo [validará según las convenciones](/help/implementing/developing/introduction/naming-conventions.md) impuestas por AEM y JCR.

Se acepta un campo de **Título** con caracteres no válidos, pero los caracteres no válidos se sustituirán en el nombre derivado. Por ejemplo:

| Título | Nombre derivado |
|---|---|
| Schön | `schoen.html` |
| SC%&amp;&#42;ç+ | `sc---c-.html` |

#### Nombre {#name}

Al indicar un valor **Nombre** cuando se crea una página, AEM [validará el nombre según las convenciones](/help/implementing/developing/introduction/naming-conventions.md) impuestas por AEM y JCR. No se pueden enviar caracteres no válidos desde el campo **Nombre**. Cuando AEM detecta caracteres que no son válidos en el campo, se resaltarán con un mensaje explicativo.

![Ejemplo de introducción de un nombre de página no válido](/help/sites-cloud/authoring/assets/organizing-invalid-name.png)

>[!TIP]
>
>Evite utilizar un código de dos letras como nombre de página, tal como se indica en la norma ISO-639-1, a menos que sea la raíz de un idioma.
>
>Consulte [Preparación de contenido para su traducción](/help/sites-cloud/administering/translation/preparation.md) para obtener más información.

### Plantillas {#templates}

En AEM, una plantilla especifica un tipo de página especializado. Todas las páginas nuevas se basarán en una plantilla.

La plantilla define la estructura de una página (así como una imagen en miniatura y otras propiedades). Por ejemplo, puede tener plantillas diferentes para páginas de producto, mapas del sitio e información de contacto. Las plantillas están compuestas de [componentes](#components).

AEM incluye varias plantillas listas para usar. Las plantillas disponibles dependen del sitio web individual. Los campos principales son:

* **Título** El título se muestra en la página web resultante.

* **Nombre** Se utiliza al dar nombre a la página.

* **Plantilla** Una lista de plantillas disponibles para usar durante la generación de la nueva página.

>[!TIP]
>
>Si así se ha configurado en la instancia, los [autores de plantillas podrán crear plantillas con el editor de plantillas](/help/sites-cloud/authoring/features/templates.md).  

### Componentes {#components}

Componentes son los elementos ofrecidos por AEM para que pueda añadir tipos de contenido específicos. AEM incorpora una serie de componentes integrados que proporcionan amplias funcionalidades, como por ejemplo:

* Texto
* Imagen
* Título
* Carrusel
* Y muchos más

Una vez que haya creado y abierto una página, puede [añadir contenido mediante los componentes](/help/sites-cloud/authoring/fundamentals/editing-content.md#inserting-a-component), que están disponibles [en el explorador de componentes](/help/sites-cloud/authoring/fundamentals/environment-tools.md#components-browser).

>[!TIP]
>
>La [consola Componentes](/help/sites-cloud/authoring/features/components-console.md) aporta una visión general de los componentes de la instancia.

## Administrar páginas {#managing-pages}

### Creación de una nueva página {#creating-a-new-page}

A menos que se hayan creado todas las páginas por adelantado, debe crear una página para poder empezar a crear contenido:

1. Abra la consola Sitios (por ejemplo, `https://<host>:<port>/sites.html/content`).
1. Desplácese hasta la ubicación en la que desee crear la nueva página.
1. Abra el selector desplegable seleccionando **Crear** en la barra de herramientas y, a continuación, seleccione **Página** en la lista:

   ![Creación de una página](/help/sites-cloud/authoring/assets/organizing-create-page.png)

1. En el primer paso del asistente puede realizar una de las acciones siguientes:

   * Seleccione la plantilla que desea utilizar para crear la nueva página y, a continuación, toque o haga clic en **Siguiente** para continuar.

   * **Haga clic en Cancelar** para anular el proceso.

   ![Selección de una plantilla para una nueva página](/help/sites-cloud/authoring/assets/organizing-create-page-template.png)

1. En el último paso del asistente puede realizar una de las acciones siguientes:

   * Utilice las tres pestañas para especificar las [propiedades de página](/help/sites-cloud/authoring/fundamentals/page-properties.md) que desee asignar a la nueva página; a continuación, pulse o haga clic en **Crear** para crear la página.

   * Utilice **Atrás** para volver a la selección de plantillas.

   Los campos clave son:

   * **Título**:

      * Se muestra al usuario y es obligatorio.
   * **Nombre**:

      * Se usa para generar la URI. Si no se especifica, el nombre se deriva del título.
      * Al indicar un valor **Nombre** cuando se cree una página, AEM [validará el nombre según las convenciones](/help/implementing/developing/introduction/naming-conventions.md) impuestas por AEM y JCR.
      * No **se pueden enviar caracteres no válidos** desde el campo **Nombre**. Cuando AEM detecte caracteres no válidos, el campo se resaltará y aparecerá un mensaje explicativo para indicar qué caracteres se deben eliminar o reemplazar.

   >[!TIP]
   >
   >Consulte [Convenciones de nomenclatura para las páginas](#page-naming-conventions).

   La información mínima necesaria para crear una página nueva es el **Título**.

   ![Proporcionar título de página](/help/sites-cloud/authoring/assets/organizing-create-page-title.png)

1. Utilice **Crear** para completar el proceso y crear la nueva página. El cuadro de diálogo de confirmación le preguntará si desea **abrir** la página inmediatamente o volver a la consola (**Listo**): 

   ![Éxito en la creación de páginas](/help/sites-cloud/authoring/assets/organizing-create-page-success.png)

   >[!NOTE]
   >
   >Si crea una página con un nombre que ya existe en la ubicación, el sistema generará automáticamente una variación del nombre añadiéndole un número. Por ejemplo, si `beach` ya existe, la página nueva pasará a llamarse `beach1`.

1. Al volver a la consola, podrá ver la nueva página:

   ![Nueva página resultante](/help/sites-cloud/authoring/assets/organizing-create-page-result.png)

>[!CAUTION]
>
>Después de crear una página, su plantilla no se puede modificar, a menos que [cree un lanzamiento con una plantilla nueva](/help/sites-cloud/authoring/launches/creating.md#create-launch-with-new-template), aunque así se pierda el contenido existente.

### Abrir una página para su edición {#opening-a-page-for-editing}

Tras crear una página o desplazarse a una página existente (en la consola), puede abrirla para editarla:

1. Abra la consola **Sitios**.
1. Desplácese hasta que encuentre la página que desea editar.
1. Seleccione la página mediante:

   * [Acciones rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [El modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) y la barra de herramientas

   A continuación, seleccione el icono **Editar**:

   Botón ![Editar](/help/sites-cloud/authoring/assets/edit.png)

1. Se abrirá la página, y podrá [editarla](/help/sites-cloud/authoring/fundamentals/editing-content.md) si es necesario.

>[!NOTE]
>
>Solo se puede navegar a otras páginas desde el editor de páginas en el modo de previsualización, ya que los vínculos no están activos en el modo Editar.

### Copiar y pegar una página    {#copying-and-pasting-a-page}

Puede copiar una página y todas sus páginas secundarias en una nueva ubicación:

1. En la consola **Sitios**, desplácese hasta que encuentre la página que desea copiar.
1. Seleccione la página mediante una de las acciones siguientes:

   * [Acciones rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [El modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) y la barra de herramientas

   A continuación, seleccione el icono de la página **Copiar**:

   ![Copiar](/help/sites-cloud/authoring/assets/copy.png)

1. Desplácese hasta la ubicación de la copia nueva de la página.
1. Pulse o haga clic en el botón **Pegar** que está disponible.

   ![Pegar](/help/sites-cloud/authoring/assets/paste.png)

1. El cuadro de diálogo de pegado presenta un resumen de la operación de pegado y las capacidades siguientes:
   * **Nuevo nombre del sitio:** cambie el nombre de la página pegada
   * **Pegar sin elementos secundarios:** omita las páginas secundarias de la página seleccionada al pegar (de forma predeterminada, se pegan)

   ![Cuadro de diálogo de pegado](/help/sites-cloud/authoring/assets/paste-dialog.png)

1. Pulse o haga clic en el botón **Pegar** para confirmar la operación de pegado y crear las páginas nuevas.

>[!NOTE]
>
>Si copia la página en una ubicación en la que ya existe una página con el mismo nombre que el original, el sistema generará automáticamente una variación del nombre adjuntándole un número. Por ejemplo, si `beach` ya existe, una nueva página con el nombre `beach` se convierte en `beach1`.

>[!NOTE]
>
>Si inicia la acción de pegar en el modo de selección, este se abandona automáticamente en cuanto se copia la página.

### Mover una página o cambiarle el nombre {#moving-or-renaming-a-page}

El procedimiento para mover o cambiar el nombre de una página es básicamente el mismo y ambas acciones las controla el asistente para desplazar páginas. Con este asistente puede:

* Cambiar el nombre de una página sin moverla
* Mover la página sin cambiar su nombre
* Moverla y cambiarle el nombre al mismo tiempo

AEM le ofrece la funcionalidad de actualizar los vínculos internos que hagan referencia a la página que está moviendo o cuyo nombre está cambiando. Esto puede hacerse página por página para proporcionar flexibilidad completa.

1. Desplácese hasta encontrar la página que desee mover.
1. Seleccione la página mediante una de las acciones siguientes:

   * [Acciones rápidas](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions)
   * [El modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources) y la barra de herramientas

   A continuación, seleccione el icono **Mover página**:

   ![Botón Mover](/help/sites-cloud/authoring/assets/move.png)

   Esta acción abrirá el asistente para desplazar páginas.

1. En el paso **Cambiar nombre** del asistente puede efectuar una de las acciones siguientes:

   * Especifique el nombre que desea que tenga la página cuando se haya desplazado y, a continuación, toque o haga clic en **Siguiente** para continuar.
   * **Haga clic en Cancelar** para anular el proceso.

   ![Mover y cambiar el nombre de la página](/help/sites-cloud/authoring/assets/move-page-rename.png)

   El nombre de la página puede seguir siendo el mismo si solo va a mover la página.

   >[!NOTE]
   >
   >Si mueve una página a una ubicación en la que ya existe una página con el mismo nombre, el sistema generará automáticamente una variación del nombre adjuntándole un número. Por ejemplo, si `beach` ya existe, una nueva página con el nombre `beach` se convierte en `beach1`.

1. En el paso **Seleccionar destino** del asistente puede realizar una de las acciones siguientes:

   * Utilice la [vista de columna](/help/sites-cloud/authoring/getting-started/basic-handling.md#column-view) para desplazarse a la nueva ubicación de la página:

      * Seleccione el destino haciendo clic en la miniatura de destino.
      * Haga clic en **Siguiente** para continuar.
   * Utilice **Volver** para volver al apartado para especificar el nombre de la página.

   >[!NOTE]
   >
   >De forma predeterminada, el elemento principal de la página que está moviendo o cuyo nombre va a cambiar se selecciona como destino.

   ![Seleccionar destino de movimiento de página](/help/sites-cloud/authoring/assets/move-page-destination.png)

   >[!NOTE]
   >
   >Si mueve una página a una ubicación en la que ya existe una página con el mismo nombre, el sistema generará automáticamente una variación del nombre adjuntándole un número. Por ejemplo, si `winter` ya existe, `winter` pasa a llamarse `winter1`.

1. Si la página está vinculada, si se hace referencia a ella o si se ha publicado, los detalles aparecen en el paso **Ajustar/Volver a publicar**.

   Puede indicar qué debería ajustarse o volverse a publicar, según proceda.

   >[!NOTE]
   >
   >Si la página no está vinculada ni se hace referencia a ella, este paso no estará disponible.

   ![Volver a publicar la página al moverla](/help/sites-cloud/authoring/assets/move-page-republish.png)

1. Si selecciona **Mover**, se completará el proceso y la página se moverá o cambiará de nombre, según el caso.

>[!NOTE]
>
>Si la página ya se ha publicado, al mover la página se cancelará la publicación automáticamente. De forma predeterminada, se vuelve a publicar una vez finalizado su desplazamiento, pero esto puede cambiar si se desmarca el campo **Volver a publicar** en el paso **Ajustar/volver a publicar**.

>[!NOTE]
>
>Si no se hace referencia a la página, se omitirá el paso **Ajustar/volver a publicar**.

>[!NOTE]
>
>A la hora de especificar un nombre nuevo, las opciones para cambiar el nombre de una página también están sujetas a las [convenciones de nomenclatura para las páginas](#page-naming-conventions).

>[!NOTE]
>
>Las páginas solo se pueden mover a ubicaciones en las que se permitan las plantillas en las que está basada dicha página. Consulte [Disponibilidad de plantillas](/help/implementing/developing/components/templates.md#template-availability) para obtener más información.

#### Acciones asincrónicas {#asynchronous-actions}

Normalmente, una acción de mover o cambiar el nombre de una página se realiza de inmediato. Esto se considera un procesamiento sincrónico y las acciones posteriores en la IU se bloquean hasta que se complete la acción.

Sin embargo, si el número de páginas afectadas supera un límite definido, la acción se procesará asincrónicamente, lo que permitirá al usuario continuar la creación en la IU sin impedimentos por la acción de mover o cambiar el nombre de la página.

* Al hacer clic en **Mover** en el último paso anterior, AEM comprueba el límite configurado.
* Si el número de páginas afectadas es inferior al límite, realiza una operación sincrónica.
* Si el número de páginas afectadas supera el límite, realiza una operación asincrónica.
   * El usuario debe definir cuándo se debe realizar la operación asincrónica
      * **Ahora** comienza la ejecución del trabajo asincrónico de inmediato.
      * **Más tarde** permite al usuario definir cuándo se iniciará el trabajo asincrónico.

         ![Movimiento asincrónico de página](/help/sites-cloud/authoring/assets/asynchronous-page-move.png)

El estado de los trabajos asincrónicos se puede comprobar en el panel [**Estado de los trabajos asincrónicos** ](/help/operations/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)en **Navegación global** -> **Herramientas** -> **Operaciones** -> **Trabajos**

>[!NOTE]
>
>Para obtener más información sobre el procesamiento asincrónico de trabajos y cómo configurar el límite para las acciones de mover y cambiar el nombre de la página, consulte el documento [Trabajos asincrónicos](/help/operations/asynchronous-jobs.md) en la guía del usuario Operaciones.

### Eliminar una página {#deleting-a-page}

1. Desplácese hasta que vea la página que desee eliminar.
1. Utilice el [modo de selección](/help/sites-cloud/authoring/getting-started/basic-handling.md#viewing-and-selecting-resources) para seleccionar la página necesaria; luego, utilice **Eliminar** de la barra de herramientas:

   ![Botón Eliminar](/help/sites-cloud/authoring/assets/delete.png)

   >[!NOTE]
   >
   >Como medida de seguridad, el icono **Eliminar** página no está disponible como acción rápida.

1. Aparecerá un cuadro de diálogo que le pedirá que confirme la acción.

   ![Cuadro de diálogo Eliminar](/help/sites-cloud/authoring/assets/delete-page.png)

   * **¿Quiere archivar las páginas antes de la eliminación?** - Si se selecciona, las versiones de las páginas seleccionadas para su eliminación se crearán al eliminarlas.
      * [Las versiones se pueden restaurar más adelante.](/help/sites-cloud/authoring/features/page-versions.md)
      * Las páginas eliminadas sin versiones anteriores no se pueden restaurar.
   * Seleccione **Cancelar** para cancelar la acción.
   * Seleccione **Eliminar** para confirmar la acción:

      * Si la página no dispone de referencias, se eliminará.
      * Si la página dispone de referencias, un cuadro de mensaje le informa de que **Se hace referencia a una o varias páginas.** Puede seleccionar **Forzar eliminación** o **Cancelar**.

>[!NOTE]
>
>Si la página ya se ha publicado, se cancela su publicación automáticamente antes de eliminarla.

### Bloquear una página   {#locking-a-page}

Puede [bloquear o desbloquear una página](/help/sites-cloud/authoring/fundamentals/editing-content.md#locking-a-page) desde una consola o bien editando una página en concreto. En ambas ubicaciones también se mostrará información sobre si una página está bloqueada o no.

![Botón Bloquear](/help/sites-cloud/authoring/assets/lock.png)
![Botón Desbloquear](/help/sites-cloud/authoring/assets/unlock.png)

### Crear una nueva carpeta {#creating-a-new-folder}

Puede crear carpetas para organizar archivos y páginas.

1. Abra la consola **Sitios** y vaya hasta la ubicación deseada.
1. Para abrir la lista de opciones, seleccione **Crear** en la barra de herramientas.
1. Seleccione **Carpeta** para abrir el cuadro de diálogo. Aquí puede indicar el **Nombre** y el **Título**:

   ![Crear carpeta](/help/sites-cloud/authoring/assets/organizing-create-folder.png)

1. Seleccione **Crear** para crear la carpeta.

>[!NOTE]
>
>A la hora de especificar un nombre nuevo, las opciones para cambiar el nombre de las carpetas están también sujetas a las [convenciones de nomenclatura de páginas](#page-naming-conventions).

>[!CAUTION]
>
>* Las carpetas solo se pueden crear directamente en **Sitios** o en otras carpetas. No se pueden crear en una página.
>* Las acciones estándar mover, copiar, pegar, eliminar, publicar, cancelar publicación y las propiedades de ver/editar se pueden ejecutar en una carpeta.
>* Las carpetas no están disponibles para la selección en una Live Copy.

