---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: d07fc976fe9c8e7872468048f80e525fe8484339
workflow-type: tm+mt
source-wordcount: '2584'
ht-degree: 8%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 15787 {#release-15787}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 15787, que se publicó el viernes, 04 de abril de 2024. La versión de mantenimiento anterior era 15575.

La activación de funcionalidades 2024.3.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-15787}

* SITES-19059: fragmentos de contenido, OpenAPI: permitir defaultValue para campos de enumeración
* SITES-20013: fragmentos de contenido, OpenAPI: WCMScriptHelper debe cancelar el procesamiento cuando no haya ServletResolver
* SITES-19926 - Fragmentos de contenido - OpenAPI - Mejoras en OnOffTriggerProcessor
* SITES-17945: fragmentos de contenido, OpenAPI: obtenga los últimos metadatos modificados para cada versión
* SITES-17298 - Fragmentos de contenido - OpenAPI - Permisos de modelos de fragmentos de contenido
* SITES-14255: fragmentos de contenido, OpenAPI: validar la exclusividad del campo de texto si se establece un indicador único en el modelo de fragmento
* SITES-15557: fragmentos de contenido, OpenAPI: permitir defaultValue para campos de enumeración
* SITES-1559: fragmentos de contenido, OpenAPI: actualice la API de lista CF para permitir recuperar solo fragmentos de contenido secundarios directos (BE)
* SITES-16052: fragmentos de contenido, OpenAPI: agregue la URL de la instancia en la que se podría consumir un recurso
* SITES-17944: fragmentos de contenido, OpenAPI: asignación adecuada de ACL de JCR al punto de conexión de permisos de CF
* SITES-17513: plano de control de fragmentos de contenido: cancelar la publicación de fragmentos de contenido
* SITES-8831: plano de control de fragmentos de contenido, PUT: actualizar un fragmento con información completa
* SITES-8836: fragmentos de contenido, OpenAPI, plano de control, referencias de GET, obtener referencias principales de un fragmento (por UUID)
* SITES-8986: fragmentos de contenido, OpenAPI: publicar modelo de fragmento de contenido
* SITES-18073 - Fragmentos de contenido - OpenAPI - Previsualizar patrón de URL para un CFM
* SITES-15242: fragmentos de contenido, OpenAPI: amplíe los eventos de publicación para proporcionar información sobre el nivel
* SITES-18702: fragmentos de contenido: OpenAPI [Servidor] Capacidad de publicación en el nivel de carpeta
* SITES-20020 - Fragmentos de contenido - OpenAPI - Eliminar `X-Adobe-Accept-Unsupported-API` antes de GA
* SITES-16066 - Fragmentos de contenido - Editor de fragmentos - Cambiar la URL de JS del selector de recursos
* SITES-19326: fragmentos de contenido, editor de fragmentos: actualice los vínculos en la interfaz de usuario de Assets para abrir CF en el nuevo editor CF
* SITES-10515 - Fragmentos de contenido - API de GraphQL - GraphQL - Problema de rendimiento de AbstractFetcher Carga de fragmentos de contenido referenciados
* SITES-17364: fragmentos de contenido, API de GraphQL: devolver nombre completo de las propiedades Modificado por y Publicado por
* SITES-19165: fragmentos de contenido, API de GraphQL: permitir que los modelos globales se utilicen, se haga referencia y se puedan consultar en todos los extremos de GraphQL
* SITES-17768: fragmentos de contenido, API de GraphQL: exponer la URL de Dynamic Media para imágenes mediante _dmS7Url
* SITES-11057: servidor principal: evite cargar todas las versiones al abrir Cronología > Versiones
* SKYOPS-63033 - HTTPD: Recorte los espacios en blanco de las variables de entorno de Dispatcher
* SKYOPS-65518 - HTTPD: error del validador si hay nombres de archivo no válidos en la carpeta de Dispatcher
* SITES-19626 - Lanzamientos: combinar los campos de última actualización DAM-CFM en el principal
* SITES-19251: sitio rápido, asistente de creación, carril lateral de la interfaz de usuario de administración de sitios de soporte cuando la referencia de tema no es igual al nombre del sitio
* AEM SITES-15430 - Editor universal - Editor universal bajo dominio de la
* CQ-4344966 - WCM: traducción: crear un marco básico para la actualización estructural de sitios y actualizar el existente para recursos
* CQ-4347312 - WCM - Traducción: cree un flujo de trabajo para asociar &quot;cq:translationsourcejcruuid&quot; en las copias de origen e idioma existentes
* CQ-4354509 - WCM - Traducción - Publicar eventos de trabajo de traducción [OSGi EventAdmin]
* AEM SITES-16318 - Cross-Swalk - Creación basada en el uso de la con Edge Delivery Services
* FORMS-9889: El usuario puede agregar la URL del POST y la configuración de la nube al configurar la acción de envío para Enviar al extremo REST
* En el editor de reglas, los usuarios pueden:
   * FORMS-12160: valide un campo, panel o formulario en la sección Entonces de la condición Cuándo.
   * FORMS-12570: restablezca un campo, panel o formulario en la sección Entonces de la condición Cuándo.
   * FORMS-11541: utilice objetos de campo y objetos globales en el editor de reglas a través de las funciones personalizadas.
   * FORMS-11714: defina los parámetros como opcionales en la función personalizada. De forma predeterminada, los parámetros declarados en funciones personalizadas son obligatorios.
   * FORMS-11756: utilice el almacenamiento en caché para funciones personalizadas para mejorar el tiempo de respuesta al recuperar la lista de funciones personalizadas en el editor de reglas.
   * FORMS-12053: Agregue una instrucción &#39;else&#39; en la condición &#39;When&#39; para implementar condiciones anidadas.
   * FORMS-11269: utilice funciones modernas de JavaScript ES10, como las funciones de izquierda y flecha, en la función personalizada para formularios basados en componentes principales.

* FORMS-9014: varias mejoras relacionadas con la accesibilidad del componente Firma manuscrita


### Problemas corregidos {#fixed-issues-15787}

* Se han corregido varios problemas de accesibilidad e internacionalización
* AEM SITES-16966 -: Unlocalized &quot;No tiene versiones&quot; en Sitios > Restaurar > Restaurar árbol
* SITES-16208: ContentFragmentModelIdentifier expone una propiedad de título engañosa
* SITES-18024: cuando falta el encabezado If-Match, la respuesta debe ser 428
* SITES-18003: el usuario que creó una versión no se devuelve correctamente
* SITES-17937: el evento de fragmento de contenido creado se emite antes de que se hayan sincronizado los pods de creación
* SITES-18029: la canalización de procesamiento de eventos se bloquea cuando la observación JCR la notifica simultáneamente
* SITES-17882: elimina el límite de longitud máxima del campo de texto del fragmento del esquema
* SITES-19252: corrija las incoherencias relacionadas con el código de estado HTTP 406 y 415
* SITES-16964 - [Servidor] La ordenación por &quot;Modificado por&quot; no funciona correctamente
* SITES-17519: editor de propiedades de página de sitios . El nombre de página largo hace que los botones no se puedan seleccionar
* SITES-16852: la API de publicación publica referencias con el estado NUEVO
* SITES-18833: la restricción de unicidad no es visible en los extremos de OpenAPI
* SITES-15553: el panel lateral de XF no se pudo cargar si la dirección URL de XF contiene un selector
* SITES-14340: NPE en VersioningTimelineEventProvider.accept
* SITES-1605 - [Sites] DeletePageCommand inicia NPE en el caso de una ruta de origen nula
* SITES-16308 - [GB18030]: mensaje de advertencia que aparece al crear una nueva carpeta de Sites denominada con caracteres GB18030
* SITES-16304 - [GB18030]: mensaje de advertencia que aparece al crear una nueva carpeta de fragmentos de experiencias con caracteres GB18030
* SITES-8769: mejore el rendimiento de StyleImpl
* CQ-4343815 - Campaign - Segmentación - La variante predeterminada de un teaser tiene una URL vacía
* CQ-4355889 - Campaign - Segmentación - La solicitud de creación de audiencia falla con la configuración de IMS.
* SITES-12460: integración de Campaign: integración de Campaign y AEM Cloud Service dañada
* SITES-11571: fragmentos de contenido, API de GraphQL: PersistedQueryServlet debe enviar 400 en direcciones URL con formato incorrecto
* SITES-19946: fragmentos de contenido, API de GraphQL: los modelos ya no se analizan al inicio
* SITES-1605: servidor principal: DeletePageCommand inicia NPE en caso de que la ruta de origen sea nula
* SITES-5429: servidor principal: ChildrenListServlet itemResourceType permite la ejecución directa de código
* SITES-15553: fragmentos de experiencias: el panel lateral de XF no se pudo cargar si la dirección URL de XF contenía un selector
* SITES-13666 - Headless - Admin - Registro de errores falso positivo &quot;com.adobe.cq.dam.cfm.headless.ui.impl.models.CFHomeCardModelImpl Config Id no debe ser nulo&quot;
* SITES-17164 - Editor de páginas - [Cloud, 6.5 Forms] La previsualización del editor de temáticas AF está dañada
* SITES-14340: IU de administración de sitios (NPE) en VersioningTimelineEventProvider.accept
* SKYOPS-68611 - Sling - repoinit - Port sling repoinit crear corrección de ruta en la rama de mantenimiento
* CQ-4354678 - WCM - Traducción: los trabajos de traducción exportan el contenido traducido
* CQ-4355167 - WCM - Traducción: no aparece al marcar un trabajo de traducción como Completado o Archivado
* CQ-4355913 - WCM - Traducción - Traducción de tarjetas de idioma del proyecto erróneas
* GRANITE-47694 - Flujo de trabajo: no se pueden obtener subtareas en un flujo de trabajo en la nube para un usuario no administrador
* ASSETS-31097 - Assets Cloud: Registros rellenados con índices de advertencias cruzadas para /bin/numberofentitiesinfolders.json
* ASSETS-35860 - Nube de recursos: conversión de huso horario incorrecta en la vista de columna de AEM Assets
* SITES-15260: IU clásica (heredada): Bulkedit añade propiedades VACÍAS en la página si se utiliza la importación de hojas
* SITES-16834: IU clásica (heredada): falta texto después de editar el texto con el Editor por lotes cuando el texto tiene comas
* SITES-17767 - Fragmentos de contenido - Administrador - Compatibilidad permitida con modelos cf también para carpetas sin un nodo jcr:content
* SITES-17683: fragmentos de contenido: back-end principal: los fragmentos de contenido no se pueden serializar con el exportador Jackson
* SITES-18797: Fragmentos de contenido: servidor principal: resultados de GraphQL duplicados tras la personalización del índice
* SITES-18076: fragmentos de contenido: back-end principal: el texto de varios valores tiene un @TypeHint incorrecto
* SITES-17856: fragmentos de contenido: editor de modelos y modelos: los modelos CF no se muestran si la configuración no es una carpeta
* SITES-17071: servidor principal: la página específica no muestra la versión en la cronología
* SITES-17285: componentes principales: el recorte de imágenes en línea es diferente en Autor y Publicación en AEMaCS
* SITES-19187: componentes principales: dos métodos de colocar recursos en un componente de imagen proporcionan resultados diferentes en el cuadro de diálogo
* SITES-20077: componentes principales, recorte de imágenes en línea: el recorte es incorrecto y las imágenes están borrosas
* SITES-17211: fragmentos de experiencias, cuadro de diálogo del selector de rutas de componentes de fragmentos de experiencias que muestra los fragmentos de experiencias eliminados
* SITES-17894 - Lanzamientos: la promoción de lanzamientos anidados revierte el contenido de lanzamiento a una versión desde su antecesor
* SITES-16042 - MSM - Live Copies: las anotaciones se muestran incorrectamente en la Live Copy después de los despliegues
* SITES-16691 - MSM - Live Copies: cuando el cliente selecciona &quot;Despliegue&quot; o &quot;Despliegue a&quot; desde el icono &quot;Despliegue&quot; de un componente, el botón &quot;Continuar&quot; aparece atenuado.
* SITES-16733 - MSM - Live Copies - La página de índice de modelo no se puede desplegar cuando se aplica rep:policy al nodo
* SITES-17155 - MSM - Live Copies: los encabezados y pies de página se traducen de nuevo al inglés cuando se cambia el nombre de LiveCopy
* AEM SITES-17492 - MSM - Live Copies - Incoherencias en el diseño de la Live Copy de la página de
* SITES-19316 - MSM - Live Copies: el vínculo de referencia al fragmento de experiencia no se actualiza en la copia de idioma
* SITES-19347 - MSM - Live Copies - Lentitud del autor del producto y mensajes de interrupción del servicio - pods que se reinician con frecuencia - alertas de estado
* SITES-19790 - MSM - Live Copies: información de vista previa incorrecta después de la creación de LiveCopy
* SITES-20086: MSM: Live Copies: el despliegue de MSM para CF en Assets desplegará todas las Live Copies aunque se seleccione una Live Copy para su despliegue
* AEM SITES-20088 - MSM - Live Copies - Despliegue de XF de publicación de problema de página en blanco en Propiedades - as a Cloud Service
* SITES-16854 - Editor de páginas - La superposición de destino de colocación cubre parsys en componentes con la función &quot;Seleccionar panel&quot;
* CQ-4355563 - Proyectos: el parámetro de ruta es incorrecto. Rellenando &quot;?appId=aemshell&quot; para el script de búsqueda de la bandeja de entrada del proyecto
* SITES-16876 - Sitio rápido - Implementación del tema - Falta CSS y JS en las páginas de vista previa 2
* SITES-18418: interfaz de usuario de administración de sitios . La funcionalidad de mostrar/ocultar del widget de campo de ruta no funciona correctamente cuando se requiere un campo
* AEM SITES-19534: interfaz de usuario de administración de sitios. No se puede abrir el cuadro de diálogo Permisos efectivos después de la actualización a la versión 6.5.19 de
* SITES-19203: Editor de plantillas: políticas de plantilla editables Botón de eliminación de texto desalineado y superposición de estilos
* CQ-4354881 - WCM - Traducción: la ruta de fragmentos de contenido se establece en origen (en-us) cuando los fragmentos de contenido se traducen como parte de una página
* CQ-4355289 - WCM - Traducción: solo se muestran los primeros 40 elementos en los Cloud Service de traducción
* CQ-4355866 - WCM - Traducción: error de lanzamiento del flujo de trabajo de traducción para páginas existentes
* CQ-4355797: flujo de trabajo: no se puede usar el paso de flujo de trabajo OOTB
* GRANITE-48938: flujo de trabajo: la visualización del autor se detiene en un estado de &quot;publicación pendiente&quot; para los recursos. Problema en la nueva caché de mapa de carga útil persistente.
* GRANITE-49036 - Flujo de trabajo - Solicitud de función | Capacidad para programar y configurar la depuración de paquetes de flujo de trabajo
* SITES-17393: extensiones de flujo de trabajo: el árbol de contenido de publicación falla al utilizar iniciadores de flujo de trabajo para cq:Tag
* SITES-17759: extensiones de flujo de trabajo: Tree-Activation-Workflow para etiquetas que no funcionan en AEMaaCS
* FORMS-12411: En dispositivos Android, la variable `Maximum Number of Characters Validation` Esta opción no funciona para el componente Cuadro de texto del formulario adaptable.
* FORMS-13377: Cuando un usuario intenta agregar la fuente personalizada y ejecutar la canalización para configurarla, se produce el error &quot;ContainersNotReady&quot;
* FORMS-13267: Cuando un usuario agrega un componente desplegable de formulario adaptable, el ID de la lista desplegable no se genera
* FORMS-13544: Cuando un usuario agrega un componente Contenedor de formulario adaptable con una presentación de asistente, no funciona correctamente durante la creación del formulario
* FORMS-13091, FORMS-13414: Si el usuario intenta configurar una URL de dominio personalizado en el almacenamiento del blob de Azure, se producirá un error
* FORMS-13595: Cuando un usuario intenta guardar el formulario en una ubicación diferente, no puede ver los botones &quot;Seleccionar carpeta&quot; y &quot;Cancelar&quot; si la resolución del explorador está establecida en 100 %. Sin embargo, la opción está visible cuando la resolución se establece en 75 %
* FORMS-10952: Cuando un usuario agrega un componente desplegable de formulario adaptable a un formulario adaptable y utiliza la propiedad &quot;Set Options&quot; basada en varias reglas personalizadas, la propiedad &quot;Set Options&quot; funciona solo para la última regla
* FORMS-11471: La carga diferida de un fragmento falla cuando la llamada &quot;emisor.json&quot; falla debido a una interrupción de la red.
* FORMS-11786: cuando un usuario cambia entre meses en el widget de calendario, el componente selector de fechas muestra una fila adicional.
* FORMS-12093, FORMS-12093: Cuando un usuario marca la casilla de verificación del formulario adaptable para enviar un formulario, el valor incorrecto con un  `\` se almacena en el cuadro de texto
* FORMS-11993: Cuando un usuario hace clic en una imagen mediante &quot;Tomar una foto&quot; en el componente Datos adjuntos en un dispositivo iOS, todas las imágenes se añaden a la carpeta con el mismo nombre
* FORMS-12555: Cuando un usuario intenta integrar AEM Forms AEM en una plataforma de correo con una URL publicada en el sitio, AEM Forms no agrega method=post al procesar la página. Este problema se produce aunque el POST esté establecido en la acción de envío con la dirección URL. Esto hace que la plataforma de correo no reconozca este formulario
* FORMS-12938: los formularios de HTML5 no funcionan o no se cargan correctamente en el explorador Microsoft Edge con el modo de compatibilidad con IE
* FORMS-12032: cuando un usuario envía un formulario, la ruta de la acción de envío no señala correctamente
* FORMS-12445: Se capturan valores incorrectos en el modelo de datos de formulario después de cambiar el orden de las opciones del botón de opción y de publicar el formulario.
* FORMS-12947: Cuando un usuario agrega un idioma nuevo a un diccionario existente, no se puede combinar ni agregar
* FORMS-11363: Cuando un usuario envía un formulario a través de Workspace, se produce un problema de visualización en las tablas mientras se procesa
* FORMS-11756: Cuando un usuario agrega las funciones de JavaScript ES6 como `let` y `const` en las funciones personalizadas, el editor de reglas no se puede abrir. Esta versión de mantenimiento admite ES10
* FORMS-13164: si el usuario genera un PDF, se le añaden líneas en blanco inesperadas después del envío
* FORMS-13789: Cuando el usuario intenta generar varios PDF, la API por lotes de salida falla
* FORMS-11483: Cuando un usuario convierte PDF en PDF/A-2B o PDF/A-3B, no se convierte y muestra un error de validación
* FORMS-10501: Cuando un usuario invoca el HSM, los documentos se certifican, pero no habilita el LTV
* FORMS-11546: Cuando un autor de formularios utiliza paneles repetidos en un formulario adaptable, el atributo ARIA no aparece en las etiquetas de HTML. Esto mejora la accesibilidad de los paneles repetidos del formulario adaptable
* FORMS-11826: Debido a las etiquetas coincidentes Arial® etiquetadas por y Arial®, los lectores de pantalla no pueden distinguir entre estas dos. Para resolver el problema, la etiqueta &quot;aria-labelledby&quot; se sustituye por &quot;aria-describedby&quot; en los campos del formulario. (F). Esto mejora la accesibilidad del Forms adaptable
* FORMS-12626, FORMS-13094: Los usuarios no pueden acceder a la barra de herramientas mediante el teclado para guardar o editar contenido en la página del editor de formularios. Este problema de accesibilidad se ha corregido
* FORMS-13102: Durante el proceso de creación de formularios, los iconos disponibles en la página Forms y Documentos carecen de funciones descriptivas para personas con capacidades diferentes. Este problema de accesibilidad se ha corregido

### Problemas conocidos {#known-issues-15787}

* SITES-17934: fragmentos de contenido: la vista previa falla debido a la protección DoS para un árbol grande de fragmentos. Consulte [KB](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23945)

### Funciones y API obsoletas {#deprecated-15787}

* [Credenciales JWT de Adobe Developer Console en desuso](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Eche un vistazo a [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md) AEM para saber qué se ha desaprobado o eliminado en el as a Cloud Service de la.

### Aviso de cambio {#change-notice-15787}

**Acción necesaria**

#### Establecer la versión de CM Java en 11 {#set-java-version-11}

La nueva versión de aem-sdk-api contiene clases compiladas con un destino Java 11, que no es compatible con la versión 1.8 JDK predeterminada del entorno de compilación de Cloud Manager. Esta actualización requiere que Maven se ejecute con JDK 11.

Se recomienda a los clientes que añadan un archivo `.cloudmanager/java-version` a la raíz de su repositorio de Git con el contenido: `11`. Consulte [Entorno de compilación / Configuración de la versión del JDK de Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).


### Tecnologías integradas {#embedded-tech-15787}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html?lang=es) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.24.4 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
