---
title: Explicación del editor universal
description: Este tutorial le ayuda a familiarizarse con la interfaz del editor universal. Le guía para conocer la interfaz de usuario y crear sus propios formularios de Edge Delivery Services en el editor universal.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 90321e81-bb55-48b2-b329-4944bf926309
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1706'
ht-degree: 10%

---


# Exploración de la interfaz (WYSIWYG) del editor universal

El [Editor universal](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) ofrece una interfaz de What You See Is What You Get (WYSIWYG) simple, visual e intuitiva para Adobe Edge Delivery Services Forms. Proporciona una interfaz moderna e intuitiva para la creación eficiente de formularios.

![Interfaz de usuario del editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface.png)

## Lo que aprenderá

Al final de este tutorial, deberá hacer lo siguiente:

- Explicación de los componentes principales de la interfaz de editor universal
- Navegar con seguridad por las diferentes secciones de la interfaz
- Saber cómo acceder y utilizar herramientas esenciales de creación de formularios
- Familiarícese con los métodos abreviados del teclado que aumentan la productividad

## Explicación de la interfaz del editor universal

Cuando edita un formulario con el Editor universal, la consola abre una interfaz interactiva de WYSIWYG que le permite iniciar la edición inmediatamente. Esta interfaz proporciona comentarios visuales en tiempo real mientras trabaja, mostrando exactamente cómo aparecerá el formulario para los usuarios finales.

>[!NOTE]
>
> Para obtener información sobre cómo crear formularios mediante el editor universal, consulte el artículo [Introducción a Edge Delivery Services para AEM Forms con el editor universal (WYSIWYG)](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md).

![Interfaz de usuario del Editor de reglas](/help/edge/docs/forms/universal-editor/assets/universal-editor-interface1.png)

La interfaz del editor universal se divide en cuatro partes lógicas:

- **[A: encabezado de Experience Cloud](#experience-cloud-header)**
- **[B: barra de herramientas del editor universal](#universal-editor-toolbar)**
- **[C: panel Propiedades](#properties-panel)**
- **[D: editor](#editor)**

Exploremos cada sección en detalle.

### Encabezado de Experience Cloud

El encabezado de Experience Cloud aparece en la parte superior de la consola y proporciona un contexto de navegación dentro del ecosistema de Adobe Experience Cloud más amplio. Muestra su ubicación actual y permite un acceso rápido a otras aplicaciones de Experience Cloud.

![Encabezado de Experience Cloud del editor universal](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager-header.png)

Veamos cada componente:

- **Adobe Experience Cloud**

  Si hace clic en el vínculo **Adobe Experience Cloud** en la parte izquierda de la pantalla, podrá navegar a la raíz de la solución de Experience Manager. Desde allí, puede acceder a otras herramientas como Experience Manager Sites, Experience Manager Assets y Experience Manager Guides.

  ![Adobe Experience Manager](/help/edge/docs/forms/universal-editor/assets/universal-editor-experience-manager.png)

- **Nombre de organización**

  **Organization Name** muestra el nombre de la organización de Identity Management System (IMS) en la que inició sesión actualmente. Si tiene acceso a varias organizaciones, puede cambiar entre ellas mediante este menú desplegable. Por ejemplo, en la captura de pantalla, la organización de IMS seleccionada actualmente es &quot;AEM Forms Internal01&quot;.

  ![Organización](/help/edge/docs/forms/universal-editor/assets/universal-editor-organization.png)

- **Ayuda**

  El icono Ayuda proporciona un acceso rápido a los recursos de aprendizaje y asistencia. Esto es especialmente útil cuando se encuentran desafíos o cuando se necesita orientación sobre características específicas. También puede enviar comentarios a través de esta sección.

  ![Ayuda](/help/edge/docs/forms/universal-editor/assets/ue-help.png)

- **Notificaciones**

  La sección **Notificaciones** muestra el número de notificaciones, solicitudes y tareas actuales incompletas asignadas actualmente en su organización IMS. Esta sección le ayuda a mantenerse al día con el flujo de trabajo.

  ![Notificación](/help/edge/docs/forms/universal-editor/assets/ue-notification.png)

- **Soluciones**

  El menú **Soluciones** le permite cambiar a otras soluciones de Adobe Experience Cloud, lo que facilita el cambio entre distintas herramientas del flujo de trabajo.

  ![Soluciones](/help/edge/docs/forms/universal-editor/assets/ue-solutions.png)

- **Perfil de usuario**

  Este icono muestra la información de perfil, junto con el nombre de la organización IMS en la que ha iniciado sesión actualmente. Haga clic en este icono para acceder a la configuración de la cuenta y a las opciones de cierre de sesión.

  ![Autor](/help/edge/docs/forms/universal-editor/assets/ue-author.png)

### Barra de herramientas del editor universal

La barra de herramientas proporciona herramientas esenciales de navegación y edición. Con él, puede desplazarse entre formularios, publicar o cancelar la publicación de formularios, editar propiedades de formularios y acceder al editor de reglas para agregar comportamientos dinámicos.

![Barra de herramientas del editor universal](/help/edge/docs/forms/universal-editor/assets/ue-toolbar.png)

Esto es lo que ofrece cada componente:

- **Botón de inicio**

  El botón Inicio le devuelve a la página de inicio del Editor universal. Esto resulta útil cuando necesita empezar a trabajar en un formulario diferente. También puede introducir directamente una dirección URL en la barra de ubicación para desplazarse a cualquier formulario que desee editar.

  ![Inicio del editor universal](/help/edge/docs/forms/universal-editor/assets/ue-home.png)

- **Barra de ubicación**

  La **Barra de ubicación** muestra la dirección del formulario que está editando en ese momento. Para cambiar a un formulario diferente, simplemente haga clic en la barra de ubicación e introduzca su URL. El método abreviado de teclado para enfocar la barra de ubicación es `l`.

  ![Barra de ubicación](/help/edge/docs/forms/universal-editor/assets/ue-locationbar.png)

- **Editor de reglas**

  El **Editor de reglas** le permite agregar comportamientos dinámicos a los formularios a través de una interfaz visual intuitiva. Con él, puede crear condiciones, validaciones y acciones que respondan a los datos introducidos por el usuario, lo que hace que los formularios sean interactivos e inteligentes.

  ![Editor de reglas](/help/edge/docs/forms/universal-editor/assets/ue-ruleeditor.png)

  >[!NOTE]
  >
  > - La extensión del Editor de reglas no está habilitada de forma predeterminada en el Editor universal. Para habilitar esta característica, comuníquese con nosotros en [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com) desde su dirección de correo electrónico oficial.
  > - Para aprender a crear y administrar reglas, consulte el artículo [Introducción al Editor de reglas en la creación de WYSIWYG](/help/edge/docs/forms/universal-editor/rule-editor-universal-editor.md).

- **Editar propiedades del formulario**

  La opción **Editar propiedades del formulario** le permite configurar opciones de formulario importantes, como el modelo de datos de formulario (FDM) y la fecha de publicación. Estas propiedades influyen en el comportamiento del formulario y en la integración con los sistemas back-end.

  ![Editar propiedades del formulario](/help/edge/docs/forms/universal-editor/assets/ue-formproperties.png)

- **Configuración del encabezado de autenticación**

  La opción **Configuración del encabezado de autenticación** le permite establecer encabezados de autenticación personalizados con fines de desarrollo local. Esto resulta particularmente útil a la hora de probar formularios que requieren credenciales de autenticación.

  ![Encabezado de autenticación](/help/edge/docs/forms/universal-editor/assets/ue-authenticationheader.png)

- **Modo adaptable**

  La característica **Modo interactivo** le permite probar el aspecto del formulario en diferentes dispositivos. De forma predeterminada, el editor se abre con el diseño de escritorio, pero puede cambiar a la vista móvil para garantizar que el formulario se pueda utilizar y sea atractivo en pantallas más pequeñas.

  ![Modo interactivo](/help/edge/docs/forms/universal-editor/assets/ue-responsivemode.png)

- **Modo de vista previa**

  **Modo de vista previa** muestra el formulario exactamente como aparecerá cuando se publique. Esto le permite interactuar con el formulario haciendo clic en vínculos y botones, tal como lo harían los usuarios. Este es un paso esencial antes de publicar para comprobar que todo funciona según lo esperado. Alternar entre los modos de edición y vista previa mediante el método abreviado de teclado `p`.

  ![Previsualizar](/help/edge/docs/forms/universal-editor/assets/ue-preview.png)

- **Abrir página**

  El botón **Abrir página** abre el formulario en una nueva pestaña del explorador para previsualizarlo. Esto le proporciona una vista de pantalla completa del formulario sin la interfaz del editor. La combinación de teclas para esta acción es `o`.

  ![Abrir página](/help/edge/docs/forms/universal-editor/assets/ue-openpage.png)

- **Publicar**

  Una vez que el formulario esté listo para los usuarios, el botón **Publicar** lo activa y lo pone a disposición de la audiencia. Este es el último paso del flujo de trabajo de creación de formularios.

  ![Publicar](/help/edge/docs/forms/universal-editor/assets/ue-publish.png)

- **Menú de puntos suspensivos**

  Al hacer clic en los puntos suspensivos (...), se muestran opciones adicionales, como la posibilidad de **Cancelar la publicación** de un formulario que se encuentra activo. Esto resulta útil cuando necesita quitar temporalmente un formulario del acceso público o reemplazarlo por una versión actualizada.

  ![Puntos suspensivos](/help/edge/docs/forms/universal-editor/assets/ue-ellipsis.png)

### Panel Propiedades

El **Panel de propiedades** aparece a la derecha de la interfaz y muestra información contextual basada en lo que haya seleccionado en el formulario. Cuando no se selecciona ningún componente, se muestra la estructura general del formulario.

![Panel Propiedades](/help/edge/docs/forms/universal-editor/assets/ue-properties-panel.png)

Vamos a explorar sus componentes clave:

- **Modo Propiedades**

  El modo **Propiedades** muestra la configuración y las opciones del componente seleccionado actualmente. Aquí es donde se personalizan los elementos individuales del formulario para satisfacer sus necesidades específicas. El método abreviado de teclado para abrir las propiedades de un componente seleccionado es `d`.

  ![Propiedades](/help/edge/docs/forms/universal-editor/assets/ue-properties.png)

- **Árbol de contenido**

  El **Árbol de contenido** muestra la estructura jerárquica del formulario. Esta representación visual le ayuda a comprender cómo se anidan los componentes entre sí. Al hacer clic en cualquier elemento del árbol, se selecciona en el editor y se desplaza a su ubicación. Esto resulta especialmente útil en formularios complejos. Cambie la vista del árbol de contenido con el método abreviado de teclado `f`.

  ![Árbol de contenido](/help/edge/docs/forms/universal-editor/assets/ue-contenttree.png)

- **Generar variaciones**

  La característica **Generar variaciones** aprovecha la inteligencia artificial para crear distintas versiones del formulario basadas en indicaciones específicas. Esto le ayuda a experimentar con diferentes enfoques y diseños sin crear manualmente cada variación. Adobe puede proporcionar los indicadores o usted puede personalizarlos.

  ![Generar variaciones](/help/edge/docs/forms/universal-editor/assets/ue-variations.png)

  >[!NOTE]
  >
  > Para obtener instrucciones detalladas sobre el uso de Generar variaciones para formularios, consulte el artículo [Generar variaciones](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/generative-ai/generate-variations).

- **Experimentación**

  La característica **Experimentación** le permite ejecutar pruebas controladas comparando diferentes diseños de formulario. Al analizar cómo interactúan los usuarios con cada variante, puede tomar decisiones basadas en datos para optimizar las tasas de conversión y la experiencia del usuario.

  ![Experimentación](/help/edge/docs/forms/universal-editor/assets/ue-experimentation.png)

- **Personalización**

  La configuración de **Personalization** le permite conectar los formularios con Adobe Experience Platform (AEP) o aplicaciones externas. Esta conexión le permite crear experiencias de formulario adaptadas en función de los datos y comportamientos de los usuarios, lo que aumenta la relevancia y la participación.

  ![Personalización](/help/edge/docs/forms/universal-editor/assets/ue-personalizaton.png)

- **Pruebas A/B**

  **Pruebas A/B** le ayuda a comparar variaciones específicas de su formulario para determinar cuál tiene un mejor rendimiento. A diferencia de la experimentación más amplia, las pruebas A/B suelen centrarse en comparar elementos o cambios específicos para identificar la opción más eficaz.

  ![Pruebas A/B](/help/edge/docs/forms/universal-editor/assets/ue-abtesting.png)

- **Administración de tareas**

  La característica **Administración de tareas** optimiza la colaboración al ayudar a su equipo a organizar, rastrear y completar tareas relacionadas con la creación y optimización de formularios. Esto hace que los proyectos avancen de manera eficiente con una clara rendición de cuentas.

  ![Administración de tareas](/help/edge/docs/forms/universal-editor/assets/ue-taskmanagement.png)

- **Borradores de contenido**

  La característica **Borradores de contenido** le permite crear y guardar versiones preliminares de elementos de texto en el formulario. Puede crear borradores utilizando el texto de formulario existente o empezar desde cero y, a continuación, editarlos o eliminarlos según sea necesario. De manera predeterminada, verá tres borradores, pero al hacer clic en **Mostrar todo** se muestran borradores adicionales.

  ![Borradores de contenido](/help/edge/docs/forms/universal-editor/assets/ue-contentdraft.png)

- **Fuente de datos**

  La opción **Data Source** le permite configurar y seleccionar las fuentes de datos para su modelo de datos de formulario (FDM). Esta integración hace que todos los objetos, propiedades y servicios del modelo de datos de las fuentes seleccionadas estén disponibles para su uso en el formulario, lo que permite la recuperación y el envío dinámicos de datos.

  ![Fuente de datos](/help/edge/docs/forms/universal-editor/assets/ue-datasource.png)

- **Añadir**

  El botón **Agregar** muestra una lista desplegable de componentes que se pueden agregar al contenedor seleccionado actualmente. Por ejemplo, cuando se selecciona una sección de formulario adaptable, esta lista muestra todos los componentes que se pueden agregar a esa sección. La combinación de teclas para abrir esta lista de componentes es `a`.

  ![Agregar icono](/help/edge/docs/forms/universal-editor/assets/ue-add.png)

- **Duplicar**

  La opción **Duplicate** crea una copia exacta del componente seleccionado. Esto ahorra tiempo cuando necesita varios elementos similares, ya que puede duplicarlos y luego modificarlos en lugar de crear desde cero.

  ![Icono Duplicado](/help/edge/docs/forms/universal-editor/assets/ue-duplicate.png)

- **Eliminar**

  La opción **Eliminar** quita el componente seleccionado del formulario. Tenga cuidado al utilizar esta opción, ya que elimina inmediatamente el elemento sin un mensaje de confirmación.

  ![Eliminar](/help/edge/docs/forms/universal-editor/assets/ue-delete.png)

### Editor

El Editor es el espacio de trabajo central donde se crea y modifica el formulario. Muestra el formulario especificado en la barra de ubicación y proporciona una experiencia WYSIWYG que muestra exactamente cómo aparecerá el formulario para los usuarios. En el modo de vista previa, puede interactuar con el formulario del mismo modo que lo harían los usuarios, probando la navegación a través de botones y vínculos.

![Editor](/help/edge/docs/forms/universal-editor/assets/ue-editor.png)

El Editor es el lugar donde pasará la mayor parte del tiempo agregando componentes, configurando sus propiedades y organizándolos para crear una experiencia de formulario intuitiva y eficaz.

## Resumen de métodos abreviados de teclado

Para aumentar su productividad, recuerde estos métodos abreviados de teclado esenciales:

- `l` - Enfocar la barra de ubicación
- `p`: alternar entre los modos de edición y vista previa
- `o` - Abrir el formulario en una nueva pestaña
- `d` - Abrir propiedades del componente seleccionado
- `f` - Alternar la vista de árbol de contenido
- `a`: abra la lista de componentes que desea agregar


