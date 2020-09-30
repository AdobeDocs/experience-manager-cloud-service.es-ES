---
title: Accesibilidad en [!DNL Experience Manager Assets].
description: Know how accessibility features in [!DNL Adobe Experience Manager] as a Cloud Service help disabled users.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0bb58d910fed91e4627e1fd8e1f9af47a1b2f4df
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


<!--
Original scope of this article for Core Assets for all a11y topics is around the following topics. This has changed since then but keeping this list of topics for posterity's sake.

* Convert the absolute doc links to relative links.
* Add an overview
* Compile a list of enhancements done in the last ~1 year.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, popup dialogs, etc.)
* Specific user tasks supported, such as, download assets, datepicker, editing metadata, etc.
* Support matrix of user tasks with browsers and screen readers + OSes combinations
* Exceptions that users should be aware of.
* CTA – what is next and more info from AEM team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Examples of other a11y DX Docs from Elle.
  * Link to a11y-specific channels to report issues, seek support, or request enhancements, if any. Available info from Elle.
-->

# Accessibility in [!DNL Adobe Experience Manager Assets] as a Cloud Service {#accessibility-in-aem-assets}

Adobe se compromete a fabricar productos para todos los usuarios, incluidas las personas con discapacidad. [!DNL Adobe Experience Manager] se mejora continuamente para satisfacer las necesidades de todos los tipos de usuarios. [!DNL Experience Manager] publica información de conformidad que detalla los estándares a los que se adhiere, describe las características de accesibilidad del producto y describe el nivel de cumplimiento. Ayuda a los usuarios a comprender el alcance de la adherencia.

[!DNL Adobe Experience Manager] proporciona distintos niveles de soporte para los siguientes estándares:

* [Directrices de accesibilidad del contenido web (WCAG) 2.1](https://www.w3.org/TR/WCAG/).
* [Sección 508](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)revisada.
* [WAI-ARIA](https://www.w3.org/WAI/standards-guidelines/aria/).
* [ES 301 549](https://en.wikipedia.org/wiki/EN_301_549).

Para acceder al informe que detalla los niveles de cumplimiento, consulte la página Informes de conformidad de [accesibilidad ](https://www.adobe.com/accessibility/compliance.html) (ACR) para todas las soluciones de Adobe.

## Tecnologías de asistencia {#at-support}

Los usuarios con discapacidades suelen utilizar hardware y software para acceder al contenido web. Estas herramientas se conocen como tecnologías de asistencia. [!DNL Adobe Experience Manager Assets] trabajar con las siguientes tecnologías de asistencia para permitir que los usuarios utilicen las funciones principales:

* Lectores de pantalla.
* Software de reconocimiento de voz.
* Uso del teclado: navegación y accesos directos.
* Herramientas de ampliación de la interfaz de usuario.

## [!DNL Experience Manager Assets] casos de uso accesibles {#accessible-assets-use-cases}

En [!DNL Experience Manager]concreto, las funciones de accesibilidad satisfacen dos requisitos clave de [!DNL Experience Manager] los usuarios y sus clientes.

Para los diseñadores y creadores de contenido, existen funciones para crear y publicar contenido accesible que sus clientes y visitantes de sitios web utilizan a su vez. El contenido puede ser utilizado por personas con discapacidades con la ayuda de tecnologías de asistencia. Para obtener más información, consulte las directrices [de accesibilidad](/help/onboarding/accessibility/web-accessibility.md)web.

Además, [!DNL Experience Manager] permite a los usuarios y administradores con discapacidades acceder a la interfaz de usuario y a los controles para crear y administrar contenido. Las personas con discapacidades pueden utilizar tecnologías de asistencia para navegar, utilizar y administrar la [!DNL Assets] capacidad.

Las funciones principales de [!DNL Assets] son más accesibles que antes y se actualizan periódicamente para mejorar el cumplimiento de las normas mundiales. Las operaciones de CRUD en Assets tienen cierto grado de accesibilidad incorporada en ellas. Se puede acceder a flujos de trabajo DAM como agregar, administrar, buscar y distribuir recursos con la ayuda de métodos abreviados de teclado, texto del lector de pantalla, contraste de color, etc.

## Compatibilidad con el uso del teclado {#keyboard-use}

Muchos elementos de la interfaz de usuario en los que se puede hacer clic o en los que se puede realizar una acción con un puntero también se pueden utilizar con el teclado. Con un teclado, los usuarios pueden centrarse en los elementos de la interfaz de usuario y realizar una acción adecuada. Los usuarios pueden utilizar directamente los métodos abreviados de teclado para activar un comando o una acción sin tener que centrarse en los elementos de la interfaz de usuario y activarlos con el teclado. Por ejemplo, los usuarios pueden abrir la línea de tiempo de un recurso en el lado izquierdo navegando hasta el control de la interfaz de usuario mediante un teclado, pulsando Retorno y pulsando `alt + 2` el método abreviado de teclado.

<!-- TBD items:

* The button/menu to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* How to open and browse through the profile popup dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the buttons like delete tag? This info can go into ‘basic handling’ info aka article to ‘understand and use the workspace’.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### Métodos abreviados de teclado en Recursos {#keyboard-shortcuts}

<!-- TBD: Add here only those keyboard shortcuts that work for/with Assets. Do with Oct release.
-->

| Interfaz de usuario o escenario | Método abreviado de teclado | Acción |
|---|---|---|
| Vista de columnas en la interfaz de usuario de Recursos | Teclas de flecha arriba y abajo | Navegue a archivos y carpetas dentro de la misma jerarquía. |
| Vista de columnas en la interfaz de usuario de Recursos | Teclas de flecha izquierda y derecha | Vaya a los archivos y carpetas situados encima o debajo de la carpeta actual. |
| Exploración de carpetas en Recursos | `/` | Invocar la búsqueda abriendo el cuadro Omnisearch. |
| Consola de recursos | ` | Conmutar raíles laterales |
| Consola de recursos | Alt + 1 | Abra el árbol de contenido. |
| Consola de recursos | Alt + 2 | Abra [!UICONTROL Navegación] en el lateral. |
| Consola de recursos | Alt + 3 | Mostrar [!UICONTROL cronología] de un recurso seleccionado. |
| Consola de recursos | Alt + 4 | Abra las referencias de Live Copy del recurso seleccionado. |
| Consola de recursos | Alt + 5 | Invocar la búsqueda dentro de la carpeta seleccionada. |
| El recurso o la carpeta están seleccionados | Retroceso | Elimine el recurso o la carpeta seleccionados. |
| El recurso o la carpeta están seleccionados | `p` | Abra la página Propiedades del recurso seleccionado. |
| El recurso o la carpeta están seleccionados | `e` | Edite el recurso seleccionado. |
| El recurso o la carpeta están seleccionados | `m` | Mueva el recurso seleccionado. |
| El recurso o la carpeta están seleccionados | Ctrl+c | Copie el recurso seleccionado. |
| El recurso o la carpeta están seleccionados | Esc | Anule la selección. |
| Se abre el cuadro de diálogo y está en el foco | Esc | Cerrar. |
| Dentro de una carpeta en DAM | Ctrl+v | Pegue el recurso copiado. |
| Consola de recursos | Ctrl + A | Seleccione todos los recursos. |
| Páginas de propiedades de recursos | Ctrl + S | Guarde los cambios. |
| Consola de recursos | `?` | Consulte una lista de métodos abreviados de teclado. |

La mayoría de los métodos abreviados de teclado que se aplican a las [!DNL Experience Manager] consolas también se aplican a los recursos. See [Keyboard Shortcuts for Consoles](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/essentials/keyboard-shortcuts.html). Consulte cómo [habilitar o deshabilitar los métodos abreviados](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)de teclado.

## Inicio de sesión y navegación por la interfaz [!DNL Assets] de usuario {#login}

Los usuarios pueden utilizar el teclado para desplazarse hasta el campo de inicio de sesión y rellenarlo para iniciar sesión. Los mensajes de error debido a combinaciones incorrectas de nombre de usuario y contraseña en la página de inicio de sesión son anunciados por los lectores de pantalla cada vez que se produce el error.

Después de iniciar sesión, los usuarios de DAM pueden navegar a la interfaz [!DNL Assets] de usuario mediante el teclado. El orden de navegación del teclado es de izquierda a derecha y de arriba abajo. Al navegar con un teclado, cualquier opción procesable enfocada se resalta con mejor contraste de color y es narrada por un lector de pantalla. Un lector de pantalla anuncia el estado (expandido o contraído) de las opciones enfocadas del menú.

Si un usuario expande la opción de ayuda o perfil del usuario desde el menú, el lector de pantalla anunciará la opción o el estado correspondientes. Si un usuario expande la opción de perfil de usuario, las opciones disponibles se pueden seleccionar con un teclado. Por ejemplo, un usuario puede hacerse pasar por otro usuario. La opción de interfaz de usuario y el mensaje de error

![Navegación por teclado de las opciones principales en la interfaz de usuario del Experience Manager](assets/keyboard-navigation-in-aem.gif)

*Figura: Desplazarse por las opciones en la parte superior de la interfaz de usuario Experience Manager mediante`Tab`la tecla .*

Si un usuario busca una cadena desde la opción [!UICONTROL Ayuda] , un narrador anuncia &#39;Búsqueda de ayuda&#39; para indicar que se está realizando una búsqueda.

## Examinar los recursos existentes y la información relacionada con la vista {#browse}

En la interfaz de usuario, los usuarios pueden utilizar el teclado para explorar la lista de recursos digitales existentes en el repositorio de DAM, realizar la previsualización o descarga de un recurso, ver las representaciones generadas, cambiar de vista, ver las representaciones generadas, ver la línea de tiempo y el historial de versiones, ver comentarios y referencias, y vista y administración de metadatos. [!DNL Assets]

<!-- TBD: Not sure about the following list items mean:

In Experience Manager header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close button in a coral-dialog wasn't accessible through keyboard, due to which user cannot trigger close button through keyboard press in version preview dialog. After fix, user can close dialog through close button using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

Al explorar el repositorio de recursos, la siguiente funcionalidad mejora la accesibilidad:

* El lector de pantalla anuncia alternativas de texto que ilustran el propósito o la funcionalidad de los iconos en lugar de sus nombres.
* Los usuarios pueden acceder a las opciones interactivas de la interfaz de usuario y centrarlas en la lista Referencias de los recursos con las teclas del teclado.
* Los elementos de cada fila de la vista de lista son anunciados como los elementos de la misma fila por los lectores de pantalla.
* El enfoque del usuario al navegar con `Tab` la tecla puede moverse a la opción de cierre en la previsualización de la versión.
* Cuando se utiliza el teclado para examinar, las opciones de interfaz de usuario activables resaltadas tienen un enfoque visual más prominente con un contraste mejorado. Hace que el área enfocada sea más identificable para el usuario.
* El uso de la `Esc` tecla para eliminar los iconos de acción rápida de la vista de miniaturas no elimina el enfoque del teclado del último elemento seleccionado.
* Con un recurso seleccionado, al pulsar Alt + 4 se abre la lista Referencias. Con `Tab` la tecla , los usuarios pueden navegar por las entradas de referencia de ninguno.
* Los comentarios de un recurso están disponibles en la línea de tiempo del recurso. Se puede acceder a ella mediante el teclado.
* Los ajustes de vista en Experience Manager son accesibles mediante el teclado. El usuario puede navegar por los tamaños de tarjeta disponibles con las teclas de flecha y seleccionar y desplazarse por los tabuladores para navegar y establecer otros elementos en la vista de configuración de Vista existente.

<!-- TBD: Gradually,  as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?

-->

## Administre recursos digitales {#manage-assets}

Muchas tareas de administración de recursos, como las operaciones de CRUD, la descarga de recursos y la adición de metadatos, son accesibles en diversos grados. Assets permite realizar las tareas mediante diversas tecnologías de asistencia, especialmente un lector de pantalla y un teclado.

Vea una demostración en vídeo de cómo utilizar un teclado para [examinar el repositorio y descargar un recurso](https://youtu.be/K3dgqMRQJys).

Para las operaciones de metadatos que normalmente realizan funciones como los especialistas en marketing y los administradores, las siguientes funciones mejoran la accesibilidad:

* [!UICONTROL Ahora se puede acceder a la opción Guardar y cerrar] de la página Propiedades del recurso mediante el teclado.
* Los lectores de pantalla anuncian las opciones para eliminar las etiquetas seleccionadas en la ficha Básico de los botones Propiedades del recurso para eliminar las etiquetas seleccionadas.
* El cuadro de diálogo emergente Selector de fecha se puede utilizar con un teclado. Datepicker se utiliza para establecer tiempos de activación y de desactivación.
* La funcionalidad de arrastrar mediante el teclado funciona correctamente en el Editor de Esquemas de metadatos en el modo de exploración del lector de pantalla.
* Un usuario puede mover el enfoque mediante el teclado al campo Añadir usuario o grupo en Grupo cerrado de usuarios en la ficha Permisos de Propiedades de la carpeta.

## Buscar recursos digitales {#search}

Una experiencia de búsqueda de recursos rápida y fluida aumenta la velocidad de contenido. Los casos de uso de velocidad de contenido son parte de la funcionalidad principal [!DNL Assets] . Para realizar el inicio de una búsqueda desde la barra de Omniture, los usuarios pueden utilizar la combinación de teclas `/` o utilizar junto `Tab` con los lectores de pantalla para localizar rápidamente la opción de búsqueda. El lector de pantalla narra el nombre de la opción como Botón [!UICONTROL de] búsqueda cuando el enfoque está en la opción ![de](assets/do-not-localize/search_icon.png)búsqueda de opciones de búsqueda. Los usuarios pueden presionar `Return` para abrir el cuadro Omniture Search. El lector de pantalla no sólo narra la palabra clave escrita en el cuadro de búsqueda, sino que también narra las sugerencias de autocompletar ofrecidas por [!DNL Experience Manager Assets]. Los usuarios pueden utilizar una combinación de teclas de flecha `Return`, y `Tab` acceder a las distintas opciones para activar una búsqueda.

La funcionalidad de búsqueda se hace más accesible gracias a las siguientes funciones:

* El título de la página, según esté disponible para un lector de pantalla, ayuda a identificar la página como página de búsqueda de recursos.
* Los usuarios buscan recursos desde la barra de Omniture. Utilice las teclas del teclado o la combinación de teclas `/` para acceder a la barra de Omniture.
* Inicio escribiendo la palabra clave de búsqueda y utilice el teclado para seleccionar las sugerencias automáticas. Pulse la tecla Retorno para aceptar una cadena sugerida automáticamente y buscar recursos para ella.
* Los lectores de pantalla pueden identificar y anunciar las casillas de verificación de estado mixto (en las que, a menos que se seleccionen todos los predicados anidados, las casillas de verificación de primer nivel no se seleccionan y se rompen) en el panel Filtros al filtrar los resultados de búsqueda.
* El enfoque del usuario pasa a las opciones de búsqueda después de que se cierre el cuadro de búsqueda de Omniture.

Al filtrar los resultados de búsqueda:

* La página de resultados de la búsqueda tiene títulos informativos para comprender mejor a los usuarios de lectores de pantalla.
* Un lector de pantalla anuncia las opciones del filtro de búsqueda como acordeones ampliables.
* Los lectores de pantalla anuncian los predicados con botones de estado mixto.

## Compartir recursos {#share-assets}

<!-- TBD: Accessibility in DA, BP, AAL? Asked CCE team for AAL content?
-->

Al compartir recursos, las siguientes funciones mejoran la accesibilidad:

* Un usuario puede mover el enfoque mediante el teclado en el campo Buscar y Añadir dirección de correo electrónico del cuadro de diálogo de uso compartido de vínculos.

* En el cuadro de diálogo de uso compartido de vínculos, al navegar en el modo Examinar, los lectores de pantalla,

   * No anote la información de la tabla en cuanto se cargue el cuadro de diálogo.
   * Puede navegar a todas las sugerencias automáticas de la lista.
   * Narre las sugerencias automáticas que se muestran para Añadir la dirección de correo electrónico y los campos de búsqueda.

## Accesibilidad en [!DNL Dynamic Media] {#dynamic-media-accessibility}

Al utilizar Dynamic Media, la siguiente funcionalidad ayuda a que sea accesible:

* Un usuario puede centrarse en `Flyout`las opciones, `InlineZoom`, `Shoppable_Banner`, `Zoom_dark`, `Zoom_light``ZoomVertical_dark`y `ZoomVertical_light` mediante `Tab` la clave en los detalles de recursos. Los visores de [!DNL Dynamic Media].

## Documentación accesible {#accessible-docs}

[!DNL Experience Manager] proporciona documentación accesible que puede ser consumida por personas con discapacidades. Lo siguiente ayuda a hacer accesible la oferta de contenido por ahora, mientras que Adobe sigue mejorando la plantilla y el contenido:

* Los lectores de pantalla pueden leer el texto.
* Las imágenes y las ilustraciones tienen texto alternativo disponible.
* Se puede navegar con el teclado.
* Las tasas de contraste ayudan a resaltar algunas partes del sitio web de documentación.

<!-- 
## More resources for accessibility {#a11y-resources}

TBD: If anyone is aware of AEM-specific resources that help users leverage any accessibility features or use any assistive technology with AEM, please share or leave a link here.
-->

## Mejoras en las [!DNL Experience Manager Assets] versiones {#rn-fixes}

Para obtener una lista de las mejoras específicas realizadas en cada versión individual, consulte las notas de la [versión](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/release-notes/home.html) de las respectivas versiones.

>[!MORELIKETHIS]
>
>* [AEM de accesibilidad](/help/onboarding/accessibility/web-accessibility.md)
>* [Informes de conformidad para soluciones de Adobe](https://www.adobe.com/accessibility/compliance.html)

