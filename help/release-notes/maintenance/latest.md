---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: c9e9664b8dd17946a340fbf58318b9e6f11a4ff0
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 10%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 16357 {#release-16357}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 16357, que se publicó el jueves, 22 de mayo de 2024. La versión de mantenimiento anterior fue la 16145.

La activación de funcionalidades 2024.5.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-16357}

* ASSETS-30379: la comprobación de la licencia de DRM recorre todo el árbol de recursos que se descargan.
* ASSETS-35535: [Error del adaptador DataSet] Las descargas de recursos vacías deben ignorarse para los eventos de la versión 1.
* CQ-4356445: Productor de eventos e implementación de esquemas.
* CQ-4356625: mejore la comprobación de autorización en languageCopyrendercondition.jsp.
* CQ-4356629: mejorar la comprobación de autorización en isWorkflowUser rendercondition.
* CQ-4356934: Simplifique la API RequestProcessor al trabajar con ResponseEntities.
* CQ-4357214: los procesadores de solicitudes no deben depender de la lógica del servlet.
* FORMS-11295: compatibilidad añadida para SHA256 con el algoritmo ECDSA para la firma digital de AEM Forms.
* FORMS-12052: un autor de formularios ahora puede aplicar funciones personalizadas para preprocesar datos antes del envío.
* FORMS-13209: se incluye un controlador para anular los controladores de éxito y de error de envío predeterminados de Forms adaptable. Puede configurar estos controladores mediante el editor de reglas de Forms adaptable.
* FORMS-13612: Los lectores de pantalla ahora leen mensajes de error, descripciones cortas y descripciones largas de los campos de la Forms adaptable basada en componentes principales. Además, se ha agregado compatibilidad para invalidar las entradas del formulario adaptable cuando el formulario contiene errores y no es válido para el envío.
* FORMS-7483: El analizador de esquemas JSON de AEM Forms ahora admite el esquema JSON (2020-12).
* FORMS-9432: se ha agregado un tipo de contenido adicional (extremo REST) a la configuración de nube de la fuente de datos. Permite el envío de datos en pares clave-valor a un extremo autenticado.
* SITES-16392: La creación fallida del inicio no debe dejar contenido de basura.
* SITES-17854: admite UUID para referencias de CF y recursos (MVP de Pfizer).
* SITES-19555: API de modelo simple para el esquema de la IU.
* SITES-19579: la API de Java para migrar fragmentos de contenido de un modelo a otro.
* SITES-19611: [Abrir API] Cree una operación de escritura/actualización para administrar un esquema de interfaz de usuario por modelo en la definición de OpenAPI.
* SITES-19614: [Xwalk] Paginación de hoja de cálculo/desplazamiento infinito.
* SITES-19698: [Abrir API] Cree una operación de lectura para administrar un esquema de interfaz de usuario por modelo en la definición de OpenAPI.
* SITES-19834: Faltan ID para el evento de Adobe I/O para la publicación/cancelación de publicación.
* SITES-19973: Implementación de la API de búsqueda CFM.
* SITES-20005: la canalización de creación debe tener un retraso de evento configurable.
* SITES-20121: permitir defaultValue para campos de enumeración.
* SITES-20146: Habilitar la vista previa de la versión/comparación para páginas movidas.
* SITES-20149: RTC: [cq-wcm-launches-core] Exportar nueva API para inicios para archivos CF.
* SITES-20150: RTC: [cq-command] Añada nuevos métodos a la API existente.
* SITES-20238: [RTC] MVP de Pfizer: Añada la API de CF para resolver las rutas de CF en los ID y viceversa.
* SITES-20333: mejore la validación al crear fragmentos de contenido.
* SITES-20334: mejore la validación al editar modelos de fragmentos de contenido.
* SITES-20342: [Servidor] Publicar en el nivel de carpeta: agregue un filtro para publicar solo archivos CF.
* SITES-20355: elimine modelos de fragmentos de contenido y permisos de servlets de API.
* SITES-20387: La navegación por el administrador de etiquetas siempre calcula el uso de etiquetas.
* SITES-20405: [Xwalk] Compatibilidad con mimeType para contraer el campo.
* SITES-20451: Agregue el complemento sidecar a wcm-commons.
* SITES-20495: [SER] Capacidad para obtener permiso para publicar en el nivel de carpeta.
* SITES-20499: [MSM][Async] Extraiga el código de AsyncOperationServlet a una clase de utilidad.
* SITES-20583: Agregar etiqueta como propiedad en `LIST`/buscar fragmentos.
* SITES-20585: mejore la API de búsqueda de fragmentos de contenido para filtrar por configuración regional.
* SITES-20594: devuelve el nombre completo del usuario que crea, modifica o replica un recurso.
* SITES-20601: [OpenAPI] Actualice la API de búsqueda de CF para permitir recuperar solo los fragmentos de contenido secundarios directos.
* SITES-20653: [Xwalk] agregue experiment-start-date y -end-date.
* SITES-20656: [SER] Proporcione una opción que coincida con las mayúsculas y minúsculas al reemplazar una cadena.
* SITES-20666: [Xwalk] la del experimento debe desactivarse de forma predeterminada durante la creación.
* SITES-20752: [cq-wcm-core] Apple se inicia para los CF.
* SITES-20763: actualice los puntos finales de la API de envío en la integración de sitios.
* SITES-20946: agregue la etiqueta como propiedad en el extremo de modelos LIST.
* SITES-20947: [persistencia] recuperar subtarea por id de fragmento de contenido.
* SITES-21012: Combinar el esquema de metadatos del modelo con el producto.
* SITES-21043: [CF][launches] Mejoras de rendimiento de puerto lateral para Cloud Service.
* SITES-21044: [CF][launches] Implementación de carga útil de edición asincrónica de puerto lateral al Cloud Service.
* SITES-21550: [Xwalk] Metadatos personalizados: campos de número, fecha, hora, hora.
* SITES-21769: utilice el prefijo de ruta /jcr:id/ para la recuperación de recurso por ID.

### Problemas corregidos {#fixed-issues-16357}

* ASSETS-37611: El flujo de trabajo &quot;Solicitud para completar la operación de movimiento&quot; se activa para los recursos no publicados.
* ASSETS-38723: NPE producido por MetadataRulesProviderImpl cuando se llama a getReadRulesForMetadataChildNodes() antes de que se inicialice this.readRules.
* AEM CQ-4357161: la pantalla de carga útil de la bandeja de entrada de AEM devuelve 404.
* CQ-4357278: DispatcherServlet emite NPE si getRequestBodyType devuelve un valor nulo.
* CQ-4357279: el procesamiento de solicitudes falla cuando no hay pathInfo para una solicitud.
* FORMS-11589: Para usuarios con solo la solución AEM Forms (sin ninguna otra solución), la canalización de front-end no funciona.
* FORMS-11952: cuando se envía un formulario, la dirección URL de envío generada por el formulario comienza con /content/ en lugar de /portale/, lo que produce un enrutamiento incorrecto de la solicitud. Esto evita que la solicitud llegue a los servidores deseados.
* FORMS-13587: en el editor de Forms adaptable, la función del emulador de dispositivos no funciona correctamente para los componentes principales basados en Forms adaptable.
* FORMS-13616: el selector de fechas muestra la fecha actual como un día por detrás, probablemente debido a un problema de zona horaria, y hay dificultades para establecer el formato de fecha correcto debido a esta incoherencia y a un problema adicional de patrón de visualización.
* FORMS-13786: en el editor de reglas de Forms adaptable, la funcionalidad de arrastrar y soltar no funciona para las funciones personalizadas.
* FORMS-13801: Incluso si el componente Términos y condiciones está desactivado, la casilla de verificación correspondiente permanece activada.
* FORMS-13827: en el editor de reglas de Forms adaptable, la operación CUANDO no admite actualmente diferentes tipos de campos con selectores de fechas.
* FORMS-13829: la lista desplegable, controlada por reglas para imitar la funcionalidad del botón de radio, no se rellena correctamente después de borrar y volver a seleccionar una selección. El comportamiento deseado es que las casillas de verificación individuales actúen como botones de opción, lo que permite realizar una sola selección a la vez y anular la selección de todas las opciones.
* FORMS-13896: en la salida del documento de registro, las fechas y los números se muestran en árabe, independientemente de si los datos de entrada se combinan con números gregorianos.
* FORMS-14244: en un formulario adaptable basado en un XDP con scripts incrustados en las casillas de verificación, los scripts no se ejecutan para los elementos después de dichas casillas de verificación.
* FORMS-14267: Los usuarios están experimentando errores de tiempo de espera coherentes al enviar solicitudes de API a través de entornos de desarrollo, fase y producción. Estas solicitudes están relacionadas con la generación de PDF, a veces con datos rellenados previamente mediante enlaces de datos. El problema resulta en un proceso de bloqueo que finalmente se agota el tiempo de espera, pero tiene éxito al reintentar después del error.
* FORMS-14376 Cuando un usuario presiona el botón Restablecer, se producen errores de consola si el texto estático está marcado como no enlazado.
* SCRNS-3945: Skyline: Cadena &quot;programada&quot; no localizada en Screens.
* SITES-11727: [GQL] Faltan datos para la hidratación completa de las referencias de fragmentos de contenido.
* SITES-16674: La casilla de verificación Heredar configuraciones de despliegue no funciona en las propiedades de Live Copy.
* AEM SITES-17772:: el usuario con un grupo de administradores no puede desbloquear la página que otro usuario ha bloqueado.
* SITES-18680: no se pueden extraer las variaciones de referencia en la consulta de graphql (Apple).
* AEM SITES-19462: La búsqueda de recursos no funciona correctamente en Cloud.
* SITES-19554: [Xwalk] Editor de hoja de cálculo: No se puede vaciar una celda.
* SITES-19971: Al aplicar parches a una CFM que contiene pestañas, se cambia el orden de los campos.
* SITES-19994: cierra el reloj del botón cuando los usuarios intentan cerrar el fragmento de contenido.
* SITES-20023: La carga de archivos no funciona para recursos remotos (de próxima generación) en varios campos.
* SITES-20029: las versiones de fragmentos de contenido se crean justo después de cerrarlo sin cambiar el contenido.
* SITES-20168: modelo de fragmento de contenido `locked` el campo no se ha actualizado correctamente.
* AEM SITES-20214: Problema de secuencia de configuración de despliegue de al guardar.
* SITES-20364: 302 Redirecciones que no funcionan con el selector de URL.
* AEM SITES-20367: Problema con la eliminación de lanzamientos en la.
* SITES-20401: [Xwalk] Los metadatos de sección no admiten propiedades de varios valores.
* SITES-20496: [Xwalk] No hay opción de propiedades al seleccionar hoja de cálculo en administración del sitio.
* SITES-20522: Los fragmentos de contenido dañados rompen el punto de conexión /adobe/sites/cf/fragments.
* AEM SITES-20547: Rutas truncadas en la lista de rutas excluidas de Live Copy en las rutas as a Cloud Service.
* SITES-20559: [MSM][XF][Lufthansa] El despliegue de fragmentos de experiencias de formatos/idiomas a países/idiomas no actualiza las referencias.
* SITES-20582: la búsqueda y la lista de fragmentos de contenido deben permitir la profundidad 0.
* SITES-20586: La marca de tiempo de la plantilla &quot;Publicada&quot; no se ha actualizado.
* SITES-20608: La segmentación de fragmentos de experiencias con personalización habilitada cuando se incluye en una plantilla provoca un bucle infinito.
* SITES-20691: La restricción de la plantilla del fragmento de experiencia no respeta cq:allowedTemplates.
* SITES-20816: CF OpenAPI: genera incoherencia con el modelo que falta para el fragmento al que se hace referencia.
* AEM SITES-21122: Defecto de Live Copy de CS con fragmentos de contenido.
* SITES-21233: [CoreCmp] Acordeón roto para GS1 EE. UU. después de actualizar a 15860.
* SITES-21239: Quitar la dependencia circular ContentFragmentSearchService.
* SITES-21316: Vista previa de fragmentos: la vista previa falla debido a cambios de código de SITES-11727.
* SITES-21391: [Evento OpenAPI] No se activó ningún evento al modificar el título o las etiquetas (propiedades) de un modelo de fragmento de contenido.
* SKYOPS-73234: aumento del error de registro en la actualización del programa AEM Assets AEM Global DAM a la versión de la versión de la versión de la 15553 y el ID de PR 35362.
* SKYOPS-75341: NoSuchMethodError en el paquete de distribución Crosswalk.

### Problemas conocidos {#known-issues-16357}

Ninguna.

### Funciones y API obsoletas {#deprecated-16357}

Para saber qué es lo que está en desuso o se ha eliminado en AEM as a Cloud Service, consulte [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Tecnologías integradas {#embedded-tech-16357}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.62.0 | [API Oak 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html?lang=es) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.25.4 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
