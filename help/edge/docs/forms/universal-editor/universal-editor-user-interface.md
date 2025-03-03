---
title: 'Descripción del editor universal: tutorial para desarrolladores'
description: Este tutorial le ayuda a familiarizarse con la interfaz del editor universal. Le guía para conocer la interfaz de usuario y crear sus propios formularios de Edge Delivery Services en el editor universal.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: 744f505c8e97b6ca6947b685ddb1eba41b370cfa
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 96%

---

# Exploración de la interfaz (WYSIWYG) del editor universal

El [Editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) ofrece una interfaz de What You See Is What You Get (WYSIWYG) simple, visual e intuitiva para Adobe Edge Delivery Services Forms. Proporciona una interfaz moderna e intuitiva para la creación eficiente de formularios.

![Interfaz de usuario del editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## Descripción de la interfaz de editor universal

Cuando el autor del formulario edita el formulario mediante el editor universal, la consola abre una interfaz interactiva WYSIWYG, lo que permite al usuario empezar a editar el formulario.

>[!NOTE]
>
> Para obtener información sobre cómo crear formularios mediante el editor universal, consulte el artículo [Introducción a Edge Delivery Services para AEM Forms con el editor universal (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

![Interfaz de usuario del Editor de reglas](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

La interfaz del editor universal se divide en cuatro partes:

* **[A: encabezado de Experience Cloud](#experience-cloud-header)**
* **[B: barra de herramientas del editor universal](#universal-editor-toolbar)**
* **[C: panel Propiedades](#properties-panel)**
* **[D: editor](#editor)**

### Encabezado de Experience Cloud

El encabezado de Experience Cloud siempre se encuentra en la parte superior de la pantalla. Ofrece información sobre la ubicación actual en Experience Cloud. También le permite ir a otras aplicaciones de Experience Cloud.

![Encabezado de Experience Cloud del editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)


Vamos a entender cada uno de sus componentes.

* **Adobe Experience Cloud**

  Puede hacer clic en el vínculo de **Adobe Experience Cloud** en la parte izquierda de la pantalla para ir a la raíz de la solución de Experience Manager y acceder a herramientas como Experience Manager Sites, Experience Manager Assets y Experience Manager Guides.

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png){width=50%,height=50%}

* **Nombre de la organización**

  **Nombre de la organización** muestra el nombre de la organización de IMS en la que inició sesión actualmente. Puede cambiar a otra organización de IMS, si tiene acceso a otras organizaciones, seleccionando en la lista desplegable. Por ejemplo, el nombre de organización de IMS seleccionado actualmente es `AEM Forms Internal01`.

  ![Organización](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png){width=50%,height=50%}


* **Ayuda**

  El icono de ayuda proporciona acceso rápido a los recursos de aprendizaje y asistencia. El autor del formulario también puede añadir los comentarios en la sección **Ayuda**.
  ![Ayuda](/help/edge/docs/forms/universal-editor/assets/ue-help.png){width=50%,height=50%}


* **Notificaciones**

  La sección **Notificación** muestra el número de notificaciones incompletas asignadas actualmente, las solicitudes y las tareas actuales en la organización IMS.

  ![Notificación](/help/edge/docs/forms/universal-editor/assets/ue-notification.png){width=50%,height=50%}


* **Soluciones**

  Puede ir a otras soluciones de Experience Cloud mediante el vínculo **Soluciones**.
  ![Soluciones](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png){width=50%,height=50%}


* **Autor**
El icono representa los detalles del autor del formulario, junto con el nombre de la organización IMS en la que el autor ha iniciado sesión actualmente.
  ![Autor](/help/edge/docs/forms/universal-editor/assets/ue-author.png){width=50%,height=50%}

### Barra de herramientas del editor universal

La barra de herramientas permite desplazarse a otros formularios y editarlos. También permite publicar o cancelar la publicación del formulario, editar sus propiedades y acceder al editor de reglas.
![Barra de herramientas del editor universal](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

Vamos a entender cada uno de sus componentes.

* **Botón de inicio**
El botón de inicio le permite navegar hasta la página de inicio del editor universal. También puede introducir directamente la dirección URL del formulario que desean editar mediante el editor universal.
  ![Inicio del editor universal](/help/edge/docs/forms/universal-editor/assets/ue-home.png)



* **Barra de ubicación**
La **barra de ubicación** muestra la dirección del formulario que está editando el autor. También puede introducir otra URL de formulario haciendo clic en la barra de ubicación. La tecla de método abreviado para abrir la barra de ubicación es la tecla `l`.
  ![Barra de ubicación](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png){width=50%,height=50%}



* **Editor de reglas**

  El **Editor de reglas** ofrece una interfaz visual intuitiva para crear y administrar reglas. Puede añadir el comportamiento de formulario dinámico mediante el editor de reglas.

  ![Editor de reglas](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > * En el editor universal, la extensión del Editor de reglas no está habilitada de forma predeterminada. Para habilitar la extensión del editor de reglas, escríbanos a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) desde su ID de correo electrónico oficial.
  > * Para aprender a crear reglas, consulte el artículo [Introducción al editor de reglas en la creación de WYSIWYG](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

* **Editar propiedades de formulario**
Puede editar las propiedades del formulario, como el modelo de datos de formulario y la fecha de publicación, haciendo clic en la opción **Editar propiedades del formulario**.
  ![Editar propiedades del formulario](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)



* **Configuración del encabezado de autenticación**
La **configuración del encabezado de autenticación** permite al autor establecer un encabezado de autenticación personalizado para el desarrollo local.
  ![encabezado de autenticación](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png){width=50%,height=50%}



* **Modo adaptable**
  La opción **Modo adaptable** le permite definir cómo el Editor universal procesa el formulario. De forma predeterminada, el editor se abre en un diseño de escritorio en el que el explorador define automáticamente la altura y la anchura. También puede optar por emular un dispositivo móvil y comprobar cómo aparece el formulario en los dispositivos móviles.

  ![Modo adaptable](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png){width=50%,height=50%}


* **Modo de vista previa**
En el modo de vista previa, el formulario aparecerá en el editor exactamente tal como se publica. Esto permite al autor navegar por el formulario haciendo clic en vínculos y botones. Cuando esté contento con las ediciones, el autor puede publicar el formulario para usuarios activos. La tecla de método abreviado para conmutar entre el modo de edición y vista previa es `p`.
  ![Previsualizar](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

* **Abrir página**
La opción **Abrir página** abre el formulario en una nueva pestaña para previsualizarlo. La tecla de método abreviado para abrir el formulario en el modo de vista previa en una nueva pestaña es `o`.
  ![Abrir página](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

* **Publicar**

  Puede hacer que el formulario esté disponible para los usuarios activos mediante el botón **Publicar**.
  ![Publicar](/help/edge/docs/forms/universal-editor/assets/ue-publish.png){width=50%,height=50%}

* **Puntos suspensivos**
Cuando el autor hace clic en la opción de puntos suspensivos (...), aparece la opción **Cancelar la publicación**. Puede cancelar la publicación de un formulario usando la opción **Cancelar la publicación**.
  ![Puntos suspensivos](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png){width=50%,height=50%}

### Panel Propiedades

El **Panel Propiedades** se encuentra en el lado derecho del editor. Muestra los detalles del componente seleccionado en la jerarquía del formulario. Es la estructura predeterminada cuando no se selecciona ningún componente.
![panel ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png){width=50%,height=50%}


Vamos a entender cada uno de sus componentes.


* **Modo Propiedades**
En la opción **Propiedades** se muestran las propiedades del componente seleccionado en el editor. Por ejemplo, la imagen muestra las propiedades del componente de entrada de número seleccionado. Puede modificar las propiedades del componente mediante esta opción. La tecla de método abreviado para abrir las propiedades del componente es `d`.

  ![ue-properties](/help/edge/docs/forms/universal-editor/assets/ue-properties.png){width=50%,height=50%}


* **Árbol de contenido**
La opción **Árbol de contenido** muestra la jerarquía del formulario. Cuando el autor hace clic en un elemento del árbol de contenido, el editor lo selecciona y se desplaza a ese componente. La tecla de método abreviado para conmutar entre la vista del árbol de contenido es la tecla `f`.

  ![Árbol de contenido](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png){width=50%,height=50%}


* **Generar variaciones**
  **Generar variaciones** usa la inteligencia artificial para producir distintas versiones de formularios en función de indicaciones específicas. Estas indicaciones las puede proporcionar Adobe o las puede crear y administrar el autor del formulario.

  ![variación](/help/edge/docs/forms/universal-editor/assets/ue-variations.png){width=50%,height=50%}


  >[!NOTE]
  >
  > Para obtener instrucciones sobre cómo usar Generar variaciones para formularios, consulte el artículo [Generar variaciones](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/generative-ai/generate-variations)

* **Experimentación**:

  **Experimentación** hace referencia a técnicas que se utilizan para probar diferentes variaciones de formularios y diseños con el fin de optimizar la experiencia del usuario y el rendimiento.
  ![experimentación](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png){width=50%,height=50%}


* **Personalización**
La opción **Personalización** configura los ajustes para establecer una conexión entre los formularios y Adobe Experience Platform (AEP) que forman parte del ecosistema de Adobe o de aplicaciones externas.
  ![Personalización](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png){width=50%,height=50%}


* **Pruebas A/B**:
  **Pruebas A/B** se refieren a técnicas que se utilizan para probar diferentes variaciones de formularios y diseño para optimizar la experiencia del usuario y el rendimiento.
  ![Pruebas A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png){width=50%,height=50%}



* **Administración de tareas**:
La característica **Administración de tareas** le permite optimizar los flujos de trabajo y mejorar la colaboración al permitir que los equipos administren, realicen un seguimiento y ejecuten tareas relacionadas con la personalización y optimización de los formularios
  ![administración de tareas](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png){width=50%,height=50%}

.
* **Borradores de contenido**

  La opción **Borradores de contenido** le permite crear borradores para elementos de texto enriquecido. Los borradores se pueden crear utilizando el texto de formulario existente o desde cero. Puede editar o eliminar borradores según sea necesario. De manera predeterminada, solo están visibles tres borradores, pero al hacer clic en **Mostrar todo** se muestra el resto.

  ![administración de tareas](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png){width=50%,height=50%}


* **Fuente de datos**

  La opción **Fuente de datos** le permite configurar fuentes de datos y seleccionarlas al crear un modelo de datos de formulario (FDM). Permite usar todos los objetos, propiedades y servicios del modelo de datos de las fuentes de datos seleccionados en el modelo de datos de formulario.
  ![Fuente de datos](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png){width=50%,height=50%}

* **Añadir**

  La opción **Añadir** abre una lista desplegable de componentes que se pueden añadir al contenedor seleccionado. Por ejemplo, en una sección de un formulario adaptable, la lista muestra los componentes disponibles que se pueden añadir a un formulario. La tecla de método abreviado para abrir la lista de componentes es `a`.
  ![Icono de Añadir](/help/edge/docs/forms/universal-editor/assets/ue-add.png){width=50%,height=50%}

* **Duplicar**

  La opción **Duplicar** crea una copia del componente, que se selecciona en el árbol de contenido o en el editor.
  ![Icono de Duplicar](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png){width=50%,height=50%}


* **Eliminar**
La opción **Eliminar** elimina un componente, que está seleccionado en el árbol de contenido o en el editor.

  ![Eliminar](/help/edge/docs/forms/universal-editor/assets/ue-delete.png){width=50%,height=50%}

### Editor

El editor le permite editar el formulario, y el formulario especificado en la barra de ubicación se procesa en el área de edición. Si el editor se encuentra en el modo de vista previa, puede desplazarse por el formulario mediante los botones y vínculos disponibles.
![Editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png){width=50%,height=50%}

## Véase también

{{universal-editor-see-also}}
