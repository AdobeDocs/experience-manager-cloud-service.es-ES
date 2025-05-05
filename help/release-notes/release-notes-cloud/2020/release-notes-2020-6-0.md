---
title: Notas de la versión de Adobe Experience Manager as a Cloud Service para 2020.6.0
description: "[!DNL Adobe Experience Manager] notas de la versión as a Cloud Service para 2020.6.0."
exl-id: fd6ebe2b-6d98-498c-a45d-b9a9c34e6be7
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 92%

---

# Notas de la versión de AEM as a Cloud Service 2020.6.0 {#release-notes}

Esta página describe las notas de la versión generales de Experience Manager as a Cloud Service 2020.6.0.

## Fecha de lanzamiento {#release-date}

La fecha de la versión de [!DNL Experience Manager] as a Cloud Service 2020.6.0 es el 4 de junio de 2020.

## Novedades de AEM Sites. {#aem-sites}

Siga esta sección para conocer las novedades y las actualizaciones de AEM Sites en AEM as a Cloud Service versión 2020.6.0.

### Novedades {#whats-new-2020.6.0}

La versión 2.9.0 de los [componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=es) ya está disponible como parte de AEM Sites, incluidos:

* Integración entre [Adobe Client Data Layer](https://github.com/adobe/adobe-client-data-layer) y los componentes principales.
* Atributos de ID HTML configurables para todos los componentes.
* Un nuevo componente de barra de progreso.
* Muchas correcciones de errores.

### Correcciones de errores {#sites-bug-fixes}

* Los componentes dentro del contenedor de diseño no están visibles cuando el contenedor de diseño se copia y se vuelve a pegar en una página.

* Se ha corregido un problema con el cambio de tamaño del componente de diseño.

* Capacidad añadida para administrar las páginas solo de enrutamiento angular y páginas de AEM/Angular.

### Accesibilidad {#accessibility}

* La función y el estado de narración ahora son posibles para los elementos de la colección en el cuadro de diálogo **Crear página** mientras se navega en el modo de exploración con la flecha hacia abajo.

* Se añadió un vínculo en la navegación para permitir a los usuarios saltar al contenido principal.

* Mejoras en el lector de pantalla.

## Novedades de Foundations en AEM as a Cloud Service {#foundations}

AEM AEM Los tiempos de generación de proyectos mejorarán si se eliminan todas las referencias del archivo pom.xml del proyecto de la al repositorio remoto `https://downloads.experiencecloud.adobe.com/content/maven/public`.

El Jar de API de SDK de AEM as a Cloud Service, que anteriormente estaba alojado en esa ubicación, ahora se encuentra en Maven Central, que es el repositorio de artefactos predeterminado de Maven.

## Novedades de Cloud Manager. {#cloud-manager}

Siga esta sección para conocer las novedades y las actualizaciones de Cloud Manager en AEM as a Cloud Service versión 2020.6.0.

### Novedades {#what-is-new-cloud-manager}

* Un usuario con el rol de *Propietario del negocio* en Cloud Manager ahora puede eliminar un programa de zona protegida para pruebas de la página de aterrizaje (con el botón de acción rápida en tarjeta de programa) o desde el programa.

  Consulte [Eliminación de un programa de zona protegida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html?lang=es) para obtener más información.

* Un usuario de programa de zona protegida en el rol de *Propietario del negocio* o *Administrador de implementación* en Cloud Manager ahora puede eliminar su conjunto de entornos de producción y ensayo en la interfaz de usuario de Cloud Manager. La opción Eliminar ya está disponible en la tarjeta de entorno de la página **Información general de Programas** y en la página **Entornos**. Al seleccionar la opción de eliminación en producción o fase también se eliminan las otras del conjunto.

  Consulte [Eliminación de un programa de zona protegida](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html?lang=es) para obtener más información.

* Marcas de entrenador en la página de aterrizaje para informar e instruir al usuario sobre la navegación básica.

* Marcas de entrenador en la página de **Información general de Programa** para informar e instruir al usuario sobre la navegación básica dentro de Cloud Manager para los primeros pasos.

* Ahora hay disponible una página **LEARN** en Cloud Manager, a la que se puede acceder desde la barra de navegación superior. Esta página incluye recursos para ayudar a los usuarios a conocer los flujos de trabajo utilizados con más frecuencia según su rol asignado en Cloud Manager.

* Los Programas de zona protegida ahora se identifican mediante un distintivo de **Zona protegida** que se muestra en la tarjeta de programa de la página de aterrizaje junto al nombre del programa en la página **Información general del Programa**.

* Un usuario con el rol de SysAdmin ahora tiene acceso con un solo clic a la ubicación de Admin Console desde la que se pueden administrar los roles de los usuarios o los permisos de Cloud Manager. Ahora está disponible el botón **Administrar acceso** en la página de aterrizaje junto al botón **Agregar Programa**.

  Consulte [Tareas de SysAdmin](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=es#sysadmin-tasks) para obtener más información.

* Un usuario con el rol de SysAdmin ahora tiene acceso con un solo clic a la instancia de autor directamente desde Cloud Manager.

  Consulte [Administración del acceso a la instancia de autor](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=es#manage-access-aem) para obtener más información.

* El registro de generación ahora incluye la lista de artefactos descubiertos, incluidos los paquetes de contenido omitido.

* El paso Generar ahora valida que todos los paquetes de contenido generados incluyen todas las propiedades obligatorias: nombre, grupo y versión.

* El paso Generar ahora valida que la generación produjo al menos un paquete de contenido.

### Correcciones de errores {#bug-fixes-cm}

* En determinadas situaciones, los iconos del cuadro de diálogo **Crear Programa** estaban desalineados.

* El identificador de la versión de AEM no se mostraba de forma coherente en la página **Información general de Programas**.

* Al configurar la canalización de producción, la opción **Implementación programada** no estaba visible para algunos clientes.

### Problemas conocidos {#known-issues-cm}

* Los entornos dentro de un programa de zona protegida hibernan cuando no se detecte ninguna actividad durante un tiempo determinado. Este estado no se observa en Cloud Manager. Sin embargo, el estado se puede observar a través de Developer Console. Esto se solucionará en una próxima versión.

* El vínculo a Developer Console directamente desde Cloud Manager no mostrará la opción de anular la hibernación o hibernar el entorno de un programa de zona protegida para pruebas. Para solucionarlo, una vez en Developer Console, agregue el patrón `#release-cm-p1234-e5678` al final de la dirección URL, donde *1234* es el ID de Programa y *5678* es el ID del entorno. Esto se solucionará en una próxima versión.

## Novedades de [!DNL Adobe Experience Manager Assets] {#aem-assets}

**Experiencia del usuario guiada para etiquetas inteligentes mejoradas, con tecnología Adobe Sensei**

Las etiquetas inteligentes mejoradas permiten a las organizaciones formar modelos de etiquetado inteligente para reconocer imágenes basadas en etiquetas comerciales específicas del cliente, además de las etiquetas inteligentes genéricas.

Con esta versión, existe una experiencia del usuario nueva y guiada que configura la formación sobre etiquetas inteligentes para conjuntos de etiquetas específicas del cliente y a formarlas con recursos que se deben reconocer y etiquetar con ellas en el futuro. La experiencia es ahora más intuitiva.
Capacite las etiquetas inteligentes mejoradas para obtener una formación más intuitiva sobre las etiquetas inteligentes. Consulte [cómo agregar etiquetas inteligentes a los recursos](/help/assets/smart-tags.md).

**Compatibilidad con la ingesta, previsualización y envío de contenido 3D**

Las organizaciones ahora pueden almacenar y utilizar archivos 3D en AEM Assets. El usuario puede cargar, previsualizar y aprovechar diferentes archivos 3D principales, incluidos los archivos OBJ, STL, GLTF y GLB. Con la adición de [!DNL Dynamic Media], puede configurar y entregar experiencias 3D mediante direcciones URL o visores agnósticos. Esto incluye un [!DNL Dynamic Media] visualizador de experiencias 3D, un componente de visualizador 3D de sitios y la capacidad de distribuir archivos 3D a través [!DNL Dynamic Media] (AR/VR). Consulte [Uso de recursos 3D en Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

**Compatibilidad con Adobe Asset Link para Adobe XD**

Con la última versión, [!DNL Experience Manager Assets] ofrece compatibilidad con un nuevo complemento [!DNL Adobe Asset Link] que se incluye en la versión [!DNL Adobe XD] v29.3. La integración permite a los diseñadores acceder y utilizar recursos desde [!DNL Experience Manager] en sus diseños, sin necesidad de salir de la aplicación [!DNL Adobe XD]. Consulte [Adobe Asset Link para obtener la documentación de Adobe XD](https://helpx.adobe.com/es/enterprise/using/adobe-asset-link-for-xd.html).

Con esta versión, los usuarios y diseñadores creativos ahora pueden trabajar con recursos gestionados en [!DNL AEM Assets] el uso [!DNL Adobe Asset Link] en una serie de aplicaciones de escritorio de Creative Cloud, incluidas [!DNL Adobe XD], [!DNL Photoshop], [!DNL Illustrator]y [!DNL InDesign].

**Mejoras de accesibilidad**

[!DNL Adobe Experience Manager Assets] ahora es más accesible de acuerdo con las directrices de accesibilidad de contenido web (WCAG) v2.1. La accesibilidad ha mejorado en los siguientes casos de uso o interfaces:

Los elementos de la interfaz de usuario son fáciles de leer en pantalla, son accesibles mediante un teclado y tienen un mejor contraste. A continuación se muestra una lista detallada de las mejoras:

* El lector de pantalla no lee las barras de progreso de [!UICONTROL Opciones], [!UICONTROL Ámbito] y [!UICONTROL Flujos de trabajo] en la página [!UICONTROL Administrar publicación] como indicadores de progreso. En su lugar, los usuarios de lectores de pantalla perciben estos indicadores de estado como una lista de pestañas. (CQ-4273015)

* Al añadir etiquetas en la página [!UICONTROL Propiedades] de un recurso, los usuarios navegan por una estructura de árbol de etiquetas. No se puede acceder a la estructura de árbol porque los usuarios del lector de pantalla no escuchan nada al navegar. (CQ-4272964)

* En el cuadro de diálogo de uso compartido de vínculos, al navegar en el modo de exploración, el lector de pantalla,

   * Narra la información de la tabla inmediatamente cuando se carga el cuadro de diálogo.
   * No puede navegar a todas las sugerencias automáticas de la lista.
   * No narra las sugerencias automáticas mostradas para el cuadro combinado [!UICONTROL Añadir dirección de correo electrónico/Buscar]. (CQ-4294232)

* Ahora se puede acceder a la página del [!UICONTROL Editor de Esquemas de metadatos] y a sus elementos con un teclado, y es fácil leerlos en la pantalla. (CQ-4272953) Los usuarios pueden arrastrar los componentes mediante el teclado en el modo de exploración NVDA. (CQ-4296326)

* En la interfaz de usuario de Assets, no se puede acceder a la configuración de vista mediante el teclado. (CQ-4289038)

* La proporción de luminosidad es inferior a 3:1 para los iconos de clasificación de color amarillo. No es útil para usuarios con visión limitada y sin percepción del color. Las estrellas de clasificación se muestran en la pestaña del recurso o en la vista de la tarjeta.

* El color y el contraste de algunos elementos de la interfaz de usuario se actualizan para que los usuarios con visión limitada o los usuarios sin percepción del color puedan distinguir estos elementos de la interfaz de usuario. Por ejemplo, el color de los iconos de clasificación por estrellas en la sección [!UICONTROL Clasificación] de la pestaña [!UICONTROL Avanzada] de las [!UICONTROL Propiedades] de un recurso y en la vista de tarjetas se cambia para obtener el contraste adecuado. (CQ-4295106)

* Los lectores de pantalla ahora pueden leer las entradas del menú emergente del cuadro de lista del cuadro combinado (en distintos campos de diferentes páginas) como una lista de opciones. (CQ-4294017)

* Para aplicar un flujo de trabajo a un recurso, se puede acceder a la flecha de cheurón de la [!UICONTROL cronología] mediante un teclado. (CQ-4289268)

* Los usuarios pueden eliminar las etiquetas seleccionadas en el campo [!UICONTROL Etiquetas] de la pestaña [!UICONTROL Básico] de la página [!UICONTROL Propiedades] de un recurso con `x` un símbolo. Los lectores de pantalla ahora anuncian el propósito y el número de etiquetas seleccionadas (CQ-4273033).

* Los campos de formulario de solo lectura se pueden centrar en el uso de un teclado. Por ejemplo, los campos desactivados en la ficha [!UICONTROL Básico] de la página [!UICONTROL Propiedades] de un recurso. (CQ-4273031)

* Acceda ahora a las opciones para filtrar recursos en la barra lateral izquierda con un teclado. (CQ-4273018)

* El lector de pantalla anuncia el propósito de varios elementos de cuadro combinado, como el campo Ruta y la opción de abrir el cuadro de diálogo Selección en la ficha [!UICONTROL Básico] de la página [!UICONTROL Propiedades] de un recurso. (CQ-4273016)

* Se puede acceder a los controles de volumen de los vídeos mediante un teclado. (CQ-4272696)

* Muchas opciones procesables en la interfaz de usuario de Assets no indican el enfoque al utilizar el teclado. (CQ-4272694)

* Los usuarios del lector de pantalla ahora pueden saber cuándo se pueden seleccionar las filas de la vista de lista mediante un teclado. La información se anuncia cuando se sitúa el puntero sobre las filas. (CQ-4271824)

* Algunos campos de formulario, como el nombre de usuario y los campos de contraseña de la página de inicio de sesión, dependen de los valores de marcador de posición para proporcionar una etiqueta accesible. (CQ-4271716)

* Ahora se puede acceder a los elementos interactivos de la interfaz de usuario, como los vínculos y las opciones de encabezado y zoom de la página de recursos o la navegación por carpetas mediante un teclado. (CQ-4271412)

* Los títulos de todas las páginas exploradas en [!DNL Adobe Experience Manager] Assets hora son únicos. (CQ-4271409)

**Otras mejoras**

La versión incorpora las siguientes mejoras adicionales:

* Capacidad para volver a procesar recursos con perfiles de procesamiento de recursos, lo que permite que los usuarios tengan un control total del proceso (ejecute el procesamiento completo de recursos, aplique perfiles de procesamiento específicos y decida si se debe ejecutar el flujo de trabajo posterior al procesamiento).
* Las consultas de búsqueda devuelven los resultados más rápido ahora que la instancia de clúster subyacente se ha reiniciado entre bastidores (la ejecución de búsqueda inicial podría durar más en un caso anterior).
* Ordene por &quot;Nombre&quot; cuando visualice recursos en la vista de listas en la interfaz de recursos y en los resultados de búsqueda. Consulte [Búsqueda de recursos](/help/assets/search-assets.md#sort).
* Ordene en &quot;Creado&quot; (Fecha) cuando visualice recursos en la vista de listas en la interfaz de Assets y en los resultados de búsqueda. Consulte [Búsqueda de recursos](/help/assets/search-assets.md#sort).
* Compatibilidad para convertir archivos EPS en imágenes mediante microservicios de recursos.

### Correcciones de errores {#assets-bug-fixes}

Además de las nuevas funciones anteriores, la versión actual proporciona las siguientes correcciones de errores en función de los comentarios de los clientes para [!DNL Assets].

* Para archivos de música MP3, el botón de reproducción mostrado en la miniatura en la previsualización DAM no funciona. (CQ-4294731)
* Al pasar el puntero sobre la vista de la tarjeta, la pantalla se desplaza como resultado del enfoque (automático) en las acciones rápidas disponibles en la tarjeta. (GRANITE-26895)
* La visualización de demasiadas imágenes después de desplazarse por un gran número de resultados de búsqueda provoca el bloqueo del explorador. (GRANITE-26432)
* Al descargar un recurso, si se selecciona la opción de correo electrónico e incluso si se proporciona un ID de correo electrónico válido, la opción de descarga no está disponible. (CQ-4296535)
* Los filtros personalizados guardados como colecciones inteligentes no se aplican correctamente a los recursos. (CQ-4294942)
* Varias mejoras en la búsqueda y la indexación y correcciones de errores para mejorar el rendimiento. (CQ-4286373)
* No se puede acceder a la pestaña de propiedades de la carpeta en Assets y devuelve el error 500. (CQ-4295701)
