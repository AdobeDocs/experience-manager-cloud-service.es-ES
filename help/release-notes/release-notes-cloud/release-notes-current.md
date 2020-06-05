---
title: Notas de la versión de Adobe Experience Manager as a Cloud Service para 2020.6.0
description: Notas de la versión de Experience Manager para 2020.6.0
translation-type: tm+mt
source-git-commit: 41684858f1fe516046b9601c1d869fff180320e0
workflow-type: tm+mt
source-wordcount: '1843'
ht-degree: 7%

---


# Notas de la versión de AEM as a Cloud Service 2020.6.0 {#release-notes}

En la siguiente sección se describen las notas de la versión generales de Experience Manager as a Cloud Service 2020.6.0.

## Fecha de la versión {#release-date}

The release date for [!DNL Experience Manager] as a Cloud Service 2020.6.0 is June 04, 2020.

## Novedades en AEM Sites {#aem-sites}

Siga esta sección para conocer las novedades y las actualizaciones de AEM Sites en AEM as a Cloud Service versión 2020.6.0.

### Novedades {#whats-new-2020.6.0}

La versión 2.9.0 de los componentes [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) principales ya está disponible como parte de los sitios de AEM, incluidos:

* Integración entre la capa [de datos del cliente de](https://github.com/adobe/adobe-client-data-layer) Adobe y los componentes principales
* Atributos de ID HTML configurables para todos los componentes
* Un nuevo componente de barra de progreso
* Muchas correcciones de errores

### Corrección de errores {#sites-bug-fixes}

* Los componentes dentro del contenedor de diseño no están visibles cuando el contenedor de diseño se copia y se vuelve a pegar en una página.

* Se ha corregido un problema con el cambio de tamaño del componente de diseño.

* Capacidad Añadida para administrar páginas solo de enrutamiento angular y páginas de AEM/Angular.

### Accesibilidad {#accessibility}

* La función y el estado de narración ahora son posibles para los elementos de la colección en el cuadro de diálogo **Crear página** mientras se navega en el modo de exploración con la flecha hacia abajo.

* Se Añadió un vínculo en la navegación para permitir a los usuarios saltar al contenido principal.

* Mejoras en el lector de pantalla.


## Novedades de las fundaciones en AEM como servicio de nube {#foundations}

Los tiempos de creación de proyectos de AEM mejorarán si se eliminan todas las referencias del archivo pom.xml del proyecto de AEM al repositorio remoto `https://downloads.experiencecloud.adobe.com/content/maven/public`.

AEM como Jar de API de SDK de servicio de nube, que anteriormente estaba alojado en esa ubicación, ahora se encuentra en Maven Central, que es el repositorio de artefactos predeterminado de Maven.

## Novedades de Cloud Manager {#cloud-manager}

Siga esta sección para conocer las novedades y las actualizaciones de Cloud Manager en AEM as a Cloud Service versión 2020.6.0.

### Novedades {#what-is-new-cloud-manager}

* Un usuario con la función Propietario ** empresarial en Cloud Manager ahora puede eliminar un Programa de Simulador para pruebas de la página de aterrizaje (mediante un botón de acción rápida en la tarjeta de Programa) o desde el programa.

   Consulte [Eliminación de un Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) de Simulador para pruebas para obtener más información.

* Un usuario de Programa de Simulador para pruebas en la función Propietario ** empresarial o Administrador *de* implementación en Cloud Manager ahora puede eliminar su conjunto de entornos de producción y de fase mediante la interfaz de usuario del Administrador de nube. La opción Eliminar ya está disponible en la tarjeta de Entorno de la página Información general **de** Programas y en la página **Entornos** . Al seleccionar la opción de eliminación en Producción o Etapa, también se elimina la otra del conjunto.

   Consulte [Eliminación de un Programa](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) de Simulador para pruebas para obtener más información.

* Marcas de entrenador en la página de aterrizaje para informar e instruir al usuario sobre la navegación básica.

* Marcas de entrenador en la página Información general **de** Programa para informar e instruir al usuario sobre la navegación básica dentro de Cloud Manager para iniciarla.

* Ahora hay disponible una página **APRENDIZAJE** en Cloud Manager, a la que se puede acceder desde la barra de navegación superior. Esta página incluye recursos para ayudar a los usuarios a conocer los flujos de trabajo utilizados con más frecuencia según su función asignada en Cloud Manager.

* Los Programas de Simulador para pruebas ahora se identifican mediante un distintivo de **Simulador para pruebas** que se mostrará en la tarjeta de programa de la página de aterrizaje y junto al nombre del programa en la página Información general **de** Programa.

* Un usuario con la función Administración de sistemas ahora tiene acceso de un solo clic a la ubicación de la Consola de administración desde la que se pueden administrar las funciones de usuario o los permisos de Cloud Manager. Ahora hay disponible un botón **Administrar acceso** en la página de aterrizaje junto al botón **Añadir Programa** .

   Consulte [Tareas](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks) de Administración de sistemas para obtener más detalles.

* Un usuario con la función Administración de sistemas ahora tiene acceso con un solo clic a la instancia de autor directamente desde Cloud Manager.

   Consulte [Administración del acceso a la instancia](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem) de autor para obtener más información.

* El registro de compilación ahora incluye la lista de artefactos descubiertos, incluidos los paquetes de contenido omitido.

* El paso Generar ahora valida que todos los paquetes de contenido generados incluyen todas las propiedades obligatorias: nombre, grupo y versión.

* El paso Generar ahora valida que la compilación produjo al menos un paquete de contenido.

### Corrección de errores {#bug-fixes-cm}

* En determinadas situaciones, los iconos del cuadro de diálogo **Crear Programa** estaban desalineados.

* El identificador de versión de AEM no se mostraba de forma coherente en la página Información general **de** Programas.

* Al configurar la canalización de producción, la opción Implementación **** programada no estaba visible para algunos clientes.

### Problemas conocidos {#known-issues-cm}

* Los Entornos dentro de un programa de Simulador para pruebas se hibernarán cuando no se detecte ninguna actividad durante un tiempo determinado. Este estado no se observará en Cloud Manager. Sin embargo, el estado se puede observar a través de la consola de desarrollador. Esto se solucionará en una próxima versión.

* El vínculo a la consola de desarrollador directamente desde Cloud Manager no mostrará la opción de deshibernar o hibernar el entorno de un Programa de Simulador para pruebas. Para solucionarlo, una vez en la consola de desarrollador, agregue el patrón `#release-cm-p1234-e5678` al final de la dirección URL, donde *1234* es el ID de Programa y *5678* es el ID de Entorno. Esto se solucionará en una próxima versión.

## Novedades de [!DNL Adobe Experience Manager Assets] {#aem-assets}

<!-- 
Assets RNs are being authored and are a work in progress.
PM/EM review required before publishing.
-->

**Experiencia de usuario guiada para etiquetas inteligentes mejoradas, con tecnología Adobe Sensei**

Las etiquetas inteligentes mejoradas permiten a las organizaciones formar modelos de etiquetado inteligente para reconocer imágenes basadas en etiquetas comerciales específicas del cliente, además de etiquetas inteligentes genéricas.

Con esta versión, existe una experiencia de usuario nueva y guiada que ayuda a configurar la formación sobre etiquetas inteligentes para conjuntos de etiquetas específicas del cliente y a formarlas con recursos que se deben reconocer y etiquetar con ellas en el futuro. Esta es una experiencia más intuitiva.
Capacite las etiquetas inteligentes mejoradas para obtener una formación más intuitiva sobre las etiquetas inteligentes. Consulte [cómo etiquetar](/help/assets/smart-tags.md) de forma inteligente y [configurar el etiquetado](/help/assets/smart-tags-configuration.md)inteligente.

**Compatibilidad con la ingestión, previsualización y envío de contenido 3D**

Las organizaciones ahora pueden almacenar y utilizar archivos 3D en Recursos AEM. El usuario puede cargar, previsualización y aprovechar una gran variedad de archivos 3D principales, incluidos archivos .obj, .stl, .gltf y .glb. Con la adición de [!DNL Dynamic Media], las experiencias 3D se pueden configurar y enviar mediante direcciones URL o visores agnósticos. Esto incluye un visor de experiencias [!DNL Dynamic Media] 3D, un componente de visor 3D de sitios y la capacidad de distribuir archivos 3D a través [!DNL Dynamic Media] (AR/VR). Consulte [Uso de recursos 3D en Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

<!-- Hiding this as the GA is at a later date. 
**Adobe Asset Link support for Adobe XD**

With the latest release, [!DNL Experience Manager Assets] provides support for a new [!DNL Adobe Asset Link] plug-in that is released with [!DNL Adobe XD] v29. The integration allows designers to access and use assets from [!DNL Experience Manager] in their designs, without the need to leave [!DNL Adobe XD] application. See [Adobe Asset Link documentation](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html).
-->

**Mejoras de accesibilidad**

[!DNL Adobe Experience Manager Assets] ahora es más accesible de acuerdo con las directrices de accesibilidad de contenido web (WCAG) v2.1. La accesibilidad ha mejorado en los siguientes casos de uso o interfaces:

* Los elementos, controles, páginas y cuadros de diálogo de la interfaz de usuario son fáciles de leer en pantalla.
* Los elementos de la interfaz de usuario, los controles y los campos del formulario de entrada son accesibles mediante el teclado.
* Cambiar el color o el contraste de algunos elementos de interfaz para hacerlos más distinguibles por usuarios con visión limitada y sin percepción del color. Por ejemplo, Recursos ahora tiene el contraste adecuado en los iconos de clasificación por estrellas de la página [!UICONTROL Propiedades] y de la vista de tarjeta.

**Otras mejoras**

La versión incorpora las siguientes mejoras adicionales:

* Capacidad para volver a procesar recursos con perfiles de procesamiento de recursos, lo que permite que los usuarios tengan un control total del proceso (ejecute el procesamiento completo de recursos, aplique perfiles de procesamiento específicos y decida si se debe ejecutar el flujo de trabajo posterior al procesamiento).
* Las consultas de búsqueda devuelven los resultados más rápido ahora que la instancia de clúster subyacente se ha reiniciado entre bastidores (la ejecución de búsqueda inicial podría durar más en un caso anterior).
* Ordene por &#39;Nombre&#39; cuando visualice recursos en la vista de listas en la interfaz de recursos y en los resultados de búsqueda. Consulte [Búsqueda de recursos](/help/assets/search-assets.md#sort).
* Ordena en &quot;Creación&quot; (fecha) cuando visualiza recursos en la vista de listas en la interfaz de Recursos y en los resultados de búsqueda. Consulte [Búsqueda de recursos](/help/assets/search-assets.md#sort).
* Compatibilidad para convertir archivos EPS en imágenes mediante microservicios de recursos.

### Corrección de errores {#assets-bug-fixes}

<!-- TBD: Add enhancements above and bug fixes below.
Seek DM bug fixes if any.
Add Nui update as shared on Slack: https://git.corp.adobe.com/nui/app/releases/tag/22
-->

Además de las nuevas funciones anteriores, la versión actual ofrece las siguientes mejoras y correcciones de errores en función de los comentarios de los clientes para [!DNL Assets].

* Para archivos de música MP3, el botón de reproducción mostrado en la miniatura en la previsualización DAM no funciona. (CQ-4294731)
* Al pasar el puntero sobre la vista de la tarjeta, la pantalla se desplaza como resultado del enfoque (automático) en las acciones rápidas disponibles en la tarjeta. (GRANITE-26895)
* La visualización de demasiadas imágenes después de desplazarse por un gran número de resultados de búsqueda provoca el bloqueo del explorador. (GRANITE-26432)
* El lector de pantalla no lee los indicadores de progreso de [!UICONTROL Opciones], [!UICONTROL Ámbito]y [!UICONTROL Flujos de trabajo] en la página [!UICONTROL Administrar publicación] como indicadores de progreso. En su lugar, los usuarios de lectores de pantalla perciben estos indicadores de estado como una lista de tabulación. (CQ-4273015)
* Al descargar un recurso, si se selecciona la opción de correo electrónico e incluso si se proporciona un ID de correo electrónico válido, la opción de descarga no está disponible. (CQ-4296535)

* Al agregar etiquetas en la página [!UICONTROL Propiedades] de un recurso, los usuarios navegan por una estructura de árbol de etiquetas. No se puede acceder a la estructura de árbol porque los usuarios del lector de pantalla no escuchan nada al navegar por ella. (CQ-4272964)
* En el cuadro de diálogo de uso compartido de vínculos, al navegar en el modo de exploración, el lector de pantalla,

   * narra la información de la tabla tan pronto como se carga el cuadro de diálogo.
   * no puede navegar a todas las sugerencias automáticas de la lista.
   * no narra las sugerencias automáticas mostradas para el cuadro combinado [!UICONTROL Añadir dirección de correo electrónico/Buscar] . (CQ-4294232)

* Las opciones de arrastrar no funcionan con el teclado en el modo de exploración NVDA en el editor de esquema de metadatos. (CQ-4296326)
* En la interfaz de usuario de Recursos, no se puede acceder a la configuración de vista mediante el teclado. (CQ-4289038)
* Los filtros personalizados guardados como colecciones inteligentes no se aplican correctamente a los recursos. (CQ-4294942)
* Varias mejoras en la búsqueda y la indexación y correcciones de errores para mejorar el rendimiento. (CQ-4286373)
* La proporción de luminosidad es inferior a 3:1 para los iconos de clasificación de color amarillo. No es útil para usuarios con visión limitada y sin percepción del color. Las estrellas de clasificación se muestran en la sección [!UICONTROL Clasificación] de la ficha [!UICONTROL Avanzado] en [!UICONTROL Propiedades] del recurso o en vista de tarjeta (CQ-4295106)
* La lista desplegable del cuadro combinado de cuadro de lista (en varios campos de diferentes páginas) ahora muestra las entradas como una lista de opciones que pueden anunciar los lectores de pantalla. (CQ-4294017)
* No se puede acceder a la flecha hacia arriba de la [!UICONTROL línea de tiempo] mediante un teclado para aplicar un flujo de trabajo a un recurso. (CQ-4289268)
* Ahora los lectores de pantalla pueden acceder a las opciones (con [!UICONTROL x]) para eliminar cada una de las etiquetas seleccionadas debajo del campo [!UICONTROL Etiquetas] de la ficha [!UICONTROL Básico] de [!UICONTROL Propiedades] . (CQ-4273033)
* Los campos de formulario de sólo lectura (por ejemplo, campos desactivados en la ficha  Básico de [!UICONTROL Propiedades]del recurso) ahora se pueden enfocar mediante el teclado. (CQ-4273031)
* Ahora se puede acceder a la opción para abrir la barra lateral del filtro mediante el teclado. (CQ-4273018)
* Los lectores de pantalla ahora anuncian correctamente el propósito de varios elementos de cuadro combinado (como el campo Ruta y la opción para abrir el cuadro de diálogo Selección en la ficha Básico de Propiedades del recurso). (CQ-4273016)
* [!UICONTROL No se puede acceder a la página Editor] de Esquemas de metadatos ni a sus elementos mediante el teclado y no es fácil de leer en pantalla. (CQ-4272953)
* Los controles de volumen de vídeo no son accesibles mediante un teclado. (CQ-4272696)
* Muchas opciones procesables en la interfaz de usuario de Recursos no indican el enfoque al utilizar el teclado. (CQ-4272694)
* Los usuarios del lector de pantalla no saben que las filas de la vista de lista se pueden seleccionar al utilizar un teclado. La información solo se anuncia cuando se sitúa el ratón sobre las filas. (CQ-4271824)
* Algunos campos de formulario, como el nombre de usuario y los campos de contraseña de la página de inicio de sesión, dependen únicamente de los valores de marcador de posición para proporcionar una etiqueta accesible. (CQ-4271716)
* Ahora se puede acceder a elementos interactivos de la interfaz de usuario, como vínculos y opciones (en las opciones de encabezado y zoom de la página de recursos, navegación por carpetas) mediante un teclado. (CQ-4271412)
* Los títulos de todas las páginas exploradas en [!DNL Adobe Experience Manager] Recursos ahora son únicos. (CQ-4271409)
