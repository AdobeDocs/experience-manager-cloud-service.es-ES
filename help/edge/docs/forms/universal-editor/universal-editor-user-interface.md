---
title: 'Comprender el editor universal: tutorial para desarrolladores'
description: Este tutorial le ayuda a ponerse en marcha con la interfaz del editor universal. Le guía para comprender la interfaz de usuario y crear sus propios formularios Edge Delivery Services en el editor universal.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 0c6f024594e1b1fd98174914d2c0714dffecb241
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 0%

---

# Exploración de la interfaz del Editor universal (WYSIWYG)

El [Editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) ofrece una interfaz de What You See Is What You Get (WYSIWYG) sencilla, visual e intuitiva para Forms de Adobe Edge Delivery Services (EDS). Proporciona una interfaz moderna con la funcionalidad de arrastrar y soltar para crear formularios de forma eficaz.

![Interfaz de usuario del editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## Explicación de la interfaz de editor universal

Cuando el autor del formulario edita el formulario con el Editor universal, la consola abre una interfaz interactiva de WYSIWYG, lo que permite al usuario empezar a editar el formulario.

>[!NOTE]
>
> Para obtener información sobre cómo crear formularios con el Editor universal, consulte el artículo [Introducción a Edge Delivery Services para AEM Forms con el Editor universal (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

![Interfaz de usuario del editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

La interfaz del editor universal se divide en cuatro partes:

* **[A: encabezado de Experience Cloud](#experience-cloud-header)**
* **[B: barra de herramientas del editor universal](#universal-editor-toolbar)**
* **[C: panel Propiedades](#properties-panel)**
* **[D: Editor](#editor)**

### Encabezado Experience Cloud

El encabezado de Experience Cloud se encuentra en la parte superior de la consola. Proporciona información sobre la ubicación actual en Experience Cloud. También le permite navegar a otras aplicaciones de Experience Cloud.

![Encabezado Experience Cloud de editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)


Vamos a entender cada uno de sus componentes.

* **Adobe Experience Cloud**

  Puede hacer clic en el vínculo **Adobe Experience Cloud** en la parte izquierda de la pantalla para ir a la raíz de la solución de Experience Manager y acceder a herramientas como Experience Manager Sites, Experience Manager Assets y Experience Manager Guides.

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png){width=50%,height=50%}

* **Nombre de organización**

  **Organization name** muestra el nombre de la organización de IMS en la que inició sesión actualmente. Puede cambiar a otra organización de IMS, si tiene acceso a otras organizaciones, seleccionando en la lista desplegable. Por ejemplo, el nombre de organización de IMS seleccionado actualmente es `AEM Forms Internal01`.

  ![Organización](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png){width=50%,height=50%}


* **Ayuda**

  El icono de ayuda proporciona acceso rápido a los recursos de aprendizaje y asistencia. El autor del formulario también puede agregar comentarios en la sección **Ayuda**.
  ![Ayuda](/help/edge/docs/forms/universal-editor/assets/ue-help.png){width=50%,height=50%}


* **Notificaciones**

  La sección **Notificación** muestra el número de notificaciones incompletas asignadas actualmente, las solicitudes y las tareas actuales en la organización IMS.

  ![Notificación](/help/edge/docs/forms/universal-editor/assets/ue-notification.png){width=50%,height=50%}


* **Soluciones**

  Puede cambiar a otras soluciones de Experience Cloud mediante el vínculo **Soluciones**.
  ![Soluciones](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png){width=50%,height=50%}


* **Autor**
El icono representa los detalles del autor del formulario, junto con el nombre de la organización IMS en la que el autor ha iniciado sesión actualmente.
  ![Autor](/help/edge/docs/forms/universal-editor/assets/ue-author.png){width=50%,height=50%}

### Barra de herramientas del editor universal

La barra de herramientas permite desplazarse a otros formularios y editarlos. También les permite publicar o cancelar la publicación del formulario, editar sus propiedades y acceder al editor de reglas.
![Barra de herramientas del editor universal](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

Vamos a entender cada uno de sus componentes.

* **Botón de inicio**
El botón de inicio le permite navegar a la página de inicio del Editor universal. También puede introducir directamente la dirección URL del formulario que desea editar con el editor universal.
  ![Página principal del editor universal](/help/edge/docs/forms/universal-editor/assets/ue-home.png)



* **Barra de ubicación**
La **barra de ubicación** muestra la dirección del formulario que está editando el autor. También puede introducir otra URL de formulario haciendo clic en en la barra de ubicación. La tecla de método abreviado para abrir la barra de ubicación es la tecla `l`.
  ![Barra de ubicación](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png){width=50%,height=50%}



* **Editor de reglas**

  El **Editor de reglas** ofrece una interfaz visual intuitiva para crear y administrar reglas. Puede agregar el comportamiento de formulario dinámico mediante el Editor de reglas.

  ![Editor de reglas](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > * En el Editor universal, la extensión del Editor de reglas no está habilitada de forma predeterminada. Para habilitar la extensión del Editor de reglas, escríbanos a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) desde su ID de correo electrónico oficial.
  > * Para aprender a crear reglas, consulte el artículo [Introducción al Editor de reglas en la creación de WYSIWYG](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

* **Editar propiedades de formulario**
Puede editar las propiedades del formulario, como el modelo de datos de formulario y la fecha de publicación, haciendo clic en la opción **Editar propiedades del formulario**.
  ![Editar propiedades de formulario](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)



* **Configuración del encabezado de autenticación**
La **configuración del encabezado de autenticación** permite al autor establecer un encabezado de autenticación personalizado con fines de desarrollo local.
  ![encabezado de autenticación](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png){width=50%,height=50%}



* **Modo interactivo**
  La opción **Modo interactivo** le permite definir cómo el Editor universal procesa el formulario. De forma predeterminada, el editor se abre en un diseño de escritorio, donde el explorador determina automáticamente la altura y la anchura. También puede optar por emular un dispositivo móvil y comprobar cómo aparece el formulario en los dispositivos móviles.

  ![Modo interactivo](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=50%,height=50%}


* **Modo de vista previa**
En el modo de vista previa, el formulario aparecerá en el editor exactamente como se publica. Esto permite al autor navegar por el formulario haciendo clic en vínculos y botones. Una vez satisfecho con las ediciones, el autor puede publicar el formulario para usuarios activos. La tecla de método abreviado para alternar entre el modo de edición y vista previa es `p`.
  ![Previsualizar](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

* **Abrir página**
La opción **Abrir página** abre el formulario en una nueva pestaña para previsualizarlo. La tecla de método abreviado para abrir el formulario en el modo de vista previa en una nueva pestaña es `o`.
  ![Abrir página](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

* **Publicar**

  Puede hacer que el formulario esté disponible para los usuarios activos mediante el botón **Publicar**.
  ![Publicar](/help/edge/docs/forms/universal-editor/assets/ue-publish.png){width=50%,height=50%}

* **Puntos suspensivos**
Cuando el autor hace clic en la opción de puntos suspensivos (...), aparece la opción **Cancelar la publicación**. Puede cancelar la publicación de un formulario usando la opción **Cancelar publicación**.
  ![Puntos suspensivos](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png){width=50%,height=50%}

### Panel Propiedades

El **Panel de propiedades** se encuentra a la derecha del editor. Muestra los detalles del componente seleccionado en la jerarquía del formulario. Es la estructura predeterminada cuando no se selecciona ningún componente.
![panel de propiedades de uso](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png){width=50%,height=50%}


Vamos a entender cada uno de sus componentes.


* **Modo Propiedades**
En la opción **Propiedades** se muestran las propiedades del componente seleccionado en el editor. Por ejemplo, la imagen muestra las propiedades del componente de entrada de número seleccionado. Puede modificar las propiedades del componente con esta opción. La tecla de método abreviado para abrir las propiedades del componente es `d`.

  ![ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties.png){width=50%,height=50%}


* **Árbol de contenido**
La opción **Árbol de contenido** muestra la jerarquía del formulario. Cuando el autor hace clic en un elemento del árbol de contenido, el editor lo selecciona y se desplaza a ese componente. La tecla de método abreviado para alternar entre la vista del árbol de contenido es la tecla `f`.

  ![Árbol de contenido](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png){width=50%,height=50%}


* **Generar variaciones**
  **Generar variaciones** usa inteligencia artificial para producir distintas versiones de formularios en función de peticiones de datos específicas. Estos indicadores los puede proporcionar Adobe o los puede crear y administrar el autor del formulario.

  ![variación](/help/edge/docs/forms/universal-editor/assets/ue-variations.png){width=50%,height=50%}


  >[!NOTE]
  >
  > Para obtener instrucciones sobre cómo usar Generar variaciones para formularios, consulte el artículo [Generar variaciones](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

* **Experimentación**:

  **Experimentación** hace referencia a técnicas utilizadas para probar diferentes variaciones de formularios y diseños con el fin de optimizar la experiencia del usuario y el rendimiento.
  ![experimentación](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png){width=50%,height=50%}


* **Personalization**
La opción **Personalization** configura las opciones para establecer una conexión entre los formularios y Adobe Experience Platform (AEP) que forman parte del ecosistema de Adobe o aplicaciones externas.
  ![Personalization](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png){width=50%,height=50%}


* **Prueba A/B**:
  **Pruebas A/B** se refieren a técnicas utilizadas para probar diferentes variaciones de formularios y diseño para optimizar la experiencia del usuario y el rendimiento.
  ![Prueba A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png){width=50%,height=50%}



* **Administración de tareas**:
La característica **Administración de tareas** le permite optimizar los flujos de trabajo y mejorar la colaboración al permitir que los equipos administren, realicen un seguimiento y ejecuten tareas relacionadas con la personalización y optimización de los formularios
  ![administración de tareas](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png){width=50%,height=50%}

.
* **Borradores de contenido**

  La opción **Borradores de contenido** le permite crear borradores para elementos de texto enriquecido. Los borradores se pueden crear utilizando el texto de formulario existente o desde cero. Puede editar o eliminar borradores según sea necesario. De manera predeterminada, solo están visibles tres borradores, pero al hacer clic en **Mostrar todo** se muestra el resto.

  ![administración de tareas](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png){width=50%,height=50%}


* **Source de datos**

  La opción **Data Source** le permite configurar las fuentes de datos y seleccionarlas al crear un modelo de datos de formulario (FDM). Hace que todos los objetos, propiedades y servicios del modelo de datos de las fuentes de datos seleccionadas estén disponibles para su uso en el modelo de datos de formulario.
  ![Source de datos](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png){width=50%,height=50%}

* **Agregar**

  La opción **Agregar** abre una lista desplegable de componentes que se pueden agregar al contenedor seleccionado. Por ejemplo, en una sección de un formulario adaptable, la lista muestra los componentes disponibles que se pueden agregar a un formulario. La tecla de método abreviado para abrir la lista de componentes es `a`.
  ![Agregar icono](/help/edge/docs/forms/universal-editor/assets/ue-add.png){width=50%,height=50%}

* **Duplicado**

  La opción **Duplicate** crea una copia del componente, que se selecciona en el árbol de contenido o en el editor.
  ![Icono duplicado](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png){width=50%,height=50%}


* **Eliminar**
La opción **Delete** elimina un componente, que está seleccionado en el árbol de contenido o en el editor.

  ![Eliminar](/help/edge/docs/forms/universal-editor/assets/ue-delete.png){width=50%,height=50%}

### Editor

El editor permite editar el formulario, y el formulario especificado en la barra de ubicación se procesa en el área de edición. Si el editor se encuentra en el modo de vista previa, puede desplazarse por el formulario mediante los botones y vínculos disponibles.
![Editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png){width=50%,height=50%}

## Ver también

{{universal-editor-see-also}}
