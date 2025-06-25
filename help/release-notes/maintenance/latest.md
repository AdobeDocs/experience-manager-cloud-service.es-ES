---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 7ae30d2053a17c2855c66b265c831ea27d19d535
workflow-type: tm+mt
source-wordcount: '1496'
ht-degree: 13%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 21331 {#21331}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 21331, que se publicó el miércoles, 24 de junio de 2025. La versión de mantenimiento anterior fue la 21193.

La activación de funcionalidades 2025.7.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-21331}

* CQ-4356522: optimización `WorkflowResourceStatusProvider`.
* FORMS-16458: interfaz de usuario para elegir propiedades de fuente (tipo de letra).
* FORMS-17707: El conector de AEP no funciona para la fase de plataforma de AEP.
* FORMS-19125: admite la asignación automática de fragmentos en el editor AF.
* FORMS-19336: búsqueda añadida en el árbol de Source de datos en el editor AF.
* FORMS-19417: Compatibilidad con botones de opción en la vista de jerarquía.
* FORMS-19603: admite la página maestra y la página de diseño en el editor de reglas.
* SITES-10575: &quot;MSM Blueprint Bloomfilter Loader&quot; intenta cargar más de 100000 filas.
* SITES-14542: al cambiar el nombre o mover una página de origen de Live Copy, se debe producir un déclencheur al publicar la página de Live Copy con el nombre o la que se movió en caso de que se publicara anteriormente.
* SITES-19754: Edge Delivery con editor universal: añada un mensaje de error legible en lenguaje natural cuando la integración tenga problemas.
* SITES-23499: Edge Delivery con editor universal: agregue compatibilidad con varios campos para utilizarlos en opciones de bloque.
* SITES-23518: Edge Delivery con editor universal: agregue compatibilidad con representaciones de recursos específicas de Edge Delivery.
* SITES-25913: API REST de fragmentos de contenido: validación de recursos con intervalo de tiempo antes de iniciar el flujo de trabajo de publicación.
* SITES-25976: Los vínculos dentro de los fragmentos de experiencias no se adaptan después del despliegue de MSM.
* SITES-26271: API REST de fragmentos de contenido: cambie a BFS Traversal para el punto final de variación de GET.
* SITES-27486: Editor universal: integración de AEM.
* SITES-27775: búsqueda de referencia optimizada durante la publicación (carga diferida de metadatos).
* SITES-27782: Edge Delivery con el editor universal: agregue una implementación específica de editor-suscriptor para publicar contenido en Edge Delivery (acceso anticipado).
* SITES-27792: Edge Delivery con editor universal: agregue la plantilla de configuración del servicio Edge Delivery.
* SITES-28683: permitir que las búsquedas de MSM LiveRelationship omitan el estado avanzado.
* SITES-29930: API REST de fragmentos de contenido: agregue métricas para el flujo de trabajo de publicación de fragmentos de contenido.
* SITES-29986: API REST de fragmentos de contenido: admite la nomenclatura técnica del modelo CF.
* SITES-30088: Fragmentos de contenido API REST: CF Publish: omitir recuperación de referencias cuando filterReferencesByStatus está vacío.
* SITES-30328: Edge Delivery con editor universal: agregue compatibilidad para obtener una vista previa desde Sidekick.
* SITES-30445: Fragmentos de contenido API REST: esquema de la interfaz de usuario del modelo CF: agregue una opción para controlar el estado inicial de contraíble.
* SITES-30604: API REST de fragmentos de contenido: admite la adopción de esquemas de metadatos de modelo en la nueva interfaz de usuario.
* SITES-30885: procesamiento JSON optimizado en consultas persistentes.
* SITES-30886: API REST de fragmentos de contenido: flujos de trabajo de GET para el extremo del fragmento de contenido en función de los uuid de fragmento almacenados en los metadatos del flujo de trabajo.
* SITES-31005: mejore la interfaz de usuario del trabajo de despliegue para mostrar el progreso.
* SITES-31020: mejore la interfaz de usuario del trabajo de creación de Live Copy para mostrar el progreso.
* SITES-31472: Eliminar lanzamiento puede hacer que el repositorio se detenga si el lanzamiento es masivo.
* SITES-31677: el espacio de trabajo personalizado admite la exportación de fragmentos de contenido de AEM a Target.
* SITES-31782: API REST de fragmentos de contenido: añada una descripción para los recursos locales.
* SITES-32175: permitir confirmaciones intermediarias tanto para la creación de Live Copy como para el despliegue de la página MSM.
* SITES-5358: API REST de fragmentos de contenido: copie archivos CF con elementos secundarios.

### Problemas solucionados {#fixed-issues-21331}

* CQ-4359756: Reglas de traducción ahora incluye propiedades de filtro en el nivel de componente.
* CQ-4359826: resuelve el estado incoherente en el panel de referencia de fragmentos de contenido.
* CQ-4359866: la clase LanguageUtils ahora admite la prueba unitaria sin agregar dependencia adicional.
* FORMS-13990: API de servicio de Forms: Generación de documentos : el campo de datos cuando se deja vacío después de seleccionarse da 200 cuando se espera 400.
* FORMS-14309: API del servicio Forms : Extraer rectificación del código de respuesta de datos.
* FORMS-18526: Cuando se copia una regla con varios campos en condiciones, el campo fijo no cambia.
* FORMS-18977: El servicio DOR no pasa el título del documento.
* FORMS-19047: Faltan traducciones después de publicar un formulario adaptable en AEM Forms en SP22.
* FORMS-19234: no se puede utilizar la función de cronología de los PDF en los formularios de AEM.
* FORMS-19628: en el documento de registro generado automáticamente, al excluir el título del panel anidado, también se oculta el título del panel raíz.
* FORMS-19651: La regla Fix cuando se hace clic en un botón se utiliza en una condición binaria y también se utiliza el mismo botón en la instrucción Then.
* FORMS-19808: FormsPortal: no se pueden extraer borradores cuando la carga diferida está habilitada.
* FORMS-19887: La propiedad de acceso no funciona en la vista previa de HTML5.
* SITES-15452: los elementos CF únicos no deben comprobarse con sus copias en el lanzamiento.
* SITES-24492: la lista de pestañas ARIA no tiene un nombre accesible.
* SITES-24623: API REST de fragmentos de contenido: corrija la discrepancia de ETag entre los extremos para el mismo CF.
* SITES-24668: Referencias La funcionalidad del carril se interrumpe cuando el zoom aumenta al 400 %.
* SITES-24678: el mensaje de estado del carril de referencias no se anuncia mediante el lector de pantalla.
* SITES-24697: El lector de pantalla no anuncia el estado de carga del modelo de imagen.
* SITES-24708: Filtros La funcionalidad del carril se interrumpe cuando el zoom se aumenta al 400 %.
* SITES-25235: el lector de pantalla no anuncia el mensaje de carga de contenido del carril de filtro.
* SITES-25254: la barra de desplazamiento horizontal aparece en modo carrusel cuando el contenido se ve a 320 píxeles.
* SITES-25433: Edge Delivery con editor universal: corrija la representación de versiones de páginas para estructuras de sitios en varios idiomas.
* SITES-26890: Al utilizar el teclado, el enfoque del teclado &quot;Encabezados de tabla&quot; del ámbito no está visible en la página Administrar publicación.
* SITES-29075: La información general de Live Copy no funciona para sitios web de gran volumen.
* SITES-29514: Edge Delivery con editor universal: haga que GitHub/URL del proyecto sea obligatorio al crear un nuevo sitio.
* SITES-29691: no se puede mover la página en un caso específico relacionado con lanzamientos.
* SITES-29745: API REST de fragmentos de contenido: implementa la hidratación de las variaciones de referencias en el recorrido de BFS.
* SITES-29748: corrija las condiciones de procesamiento para mostrar las acciones Administrar publicación/Publicación rápida dentro del editor CF.
* SITES-29789: problema con el cambio del vínculo del componente en las páginas raíz copiadas.
* SITES-29987: API REST de fragmentos de contenido: Crear y editar modelo de fragmento de contenido no es compatible con `previewUrlPattern`.
* SITES-30140: problema de doble ventana al crear la referencia de fragmento de contenido.
* SITES-30260: Fragmentos de contenido API de REST: error al actualizar/eliminar CF mediante la última ETag.
* SITES-30327: API REST de fragmentos de contenido: la publicación de CF sin permisos crea flujos de trabajo independientes para cada recurso de carga útil.
* SITES-30333: lea los metadatos de los recursos de jcr para evitar problemas de análisis de xmp.
* SITES-30353: GraphQL DataFetchingExceptions para el campo &quot;src&quot; en fragmentos de contenido de AEM.
* SITES-30377: Edge Delivery con el editor universal: Corrija los nombres de la organización y del sitio.
* SITES-30386: Edge Delivery con editor universal: quite UE duplicado y heredado `cors.js`.
* SITES-30583: API REST de fragmentos de contenido: la herramienta Buscar y reemplazar cambia todos los caracteres a minúsculas.
* SITES-30585: La API REST de fragmentos de contenido: `previewUrlPattern` no se estableció en la creación de CFM con referencias.
* SITES-30634: Imagen RTE Texto alternativo y alineación no funcionan de forma coherente.
* SITES-30660: problema de conformidad de ADA con el componente personalizado de AEM.
* SITES-30695: Edge Delivery con el editor universal: aumente la clasificación de la canalización de reescritura para no interferir con el código personalizado.
* SITES-30727: no se pueden arrastrar y soltar componentes en el editor de creación de producción.
* SITES-30752: no utilice encabezados `If-modified-since`/`last-modified` al generar una respuesta de consulta persistente.
* SITES-30871: DOM se actualiza después de activar el detector de postedición.
* SITES-30877: Estado de despliegue de página secundaria incorrecto.
* SITES-30899: la opción de despliegue &quot;Más tarde&quot; permite continuar sin seleccionar ninguna fecha.
* SITES-30947: excepción de puntero nulo debido a la propiedad &quot;behavior&quot; que falta en el modelo durante el despliegue.
* SITES-31157: API REST de fragmentos de contenido: el parche falla en un caso específico.
* SITES-31272: no se puede crear una copia de idioma de Assets mediante PageManager.copy.
* SITES-31327: API REST de fragmentos de contenido: elimine la validación ETag en la solicitud de fragmento de GET.
* SITES-31387: error de JavaScript &quot;ns.ui.alert no es una función&quot; al volver a habilitar la herencia de componentes fantasma.
* SITES-31455: API REST de fragmentos de contenido: corrija la discrepancia ETag entre los puntos de conexión para el mismo modelo de fragmento de contenido.
* SITES-31459: API REST de fragmentos de contenido: la Live Copy de CF no se puede editar cuando hay un campo de referencia de contenido.
* SITES-31467: js-errors de contexthub.authoring-hook.js en el editor de páginas.
* SITES-31594: API REST de fragmentos de contenido: error `extractMetadataSchemaFieldLabel`.
* SITES-31621: Edge Delivery con el editor universal: elimine la fila vacía de las hojas de cálculo que son Live Copies.
* SITES-31676: La creación o eliminación de componentes deja un espacio en blanco en la parte inferior de la página.
* SITES-31822: falta la etiqueta de casilla de verificación ClassicUI y HTML codificado.
* SITES-31857: la creación de CF falla en carpetas con comillas simples.
* SITES-31888: La eliminación de fragmentos de contenido no se puede propagar a la vista previa.
* SITES-31922: API REST de fragmentos de contenido: el extremo referencedBy no devuelve referencias de página.
* SITES-31987: no mostrar direcciones URL de vista previa para fragmentos de contenido al publicarlos en Vista previa.
* SITES-32095: la actualización automática falla al eliminar el detector de eventos después de la creación en Live Copy.
* SITES-32237: Edge Delivery con editor universal: corrija la representación de componentes de texto vacíos o mal formados.

### Problemas conocidos {#known-issues-21331}

Ninguna.

### Características y API obsoletas {#deprecated-21331}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-21331}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 21 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-21331}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
