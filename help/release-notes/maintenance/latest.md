---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 26c42152bdebc069dd60cc4f5f070276eb1a1f46
workflow-type: tm+mt
source-wordcount: '1780'
ht-degree: 98%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 21331 {#21331}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 21331, que se publicó el 24 de junio de 2025. La versión de mantenimiento anterior fue la 21193.

La activación de funcionalidades 2025.7.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-21331}

* CQ-4356522: optimización `WorkflowResourceStatusProvider`.
* FORMS-16458: interfaz de usuario para elegir propiedades de fuente (tipo de letra).
* FORMS-17707: el conector de AEP no funciona para la fase de plataforma de AEP.
* FORMS-19125: compatibilidad con la asignación automática de fragmentos en el editor AF.
* FORMS-19336: búsqueda añadida en el árbol de fuente de datos en el editor AF.
* FORMS-19417: compatibilidad con botones de opción en la vista de jerarquía.
* FORMS-19603: compatibilidad con la página maestra y la página de diseño en el editor de reglas.
* SITES-5358: API REST de fragmentos de contenido: copie archivos CF con tareas secundarias.
* SITES-10575: &quot;MSM: Blueprint Bloomfilter Loader&quot; intenta cargar más de 100 000 filas.
* SITES-14542: al cambiar el nombre o mover una página de origen de Live Copy, se debe activar la publicación de la página de Live Copy con el cambio de nombre o la que se movió en caso de que se publicara anteriormente.
* SITES-19754: Edge Delivery con editor universal: añada un mensaje de error legible en lenguaje natural cuando la integración tenga problemas.
* SITES-23499: Edge Delivery con editor universal: añada compatibilidad con varios campos para utilizarlos en opciones de bloque.
* SITES-23518: Edge Delivery con editor universal: añada compatibilidad para entregas de activos específicos de Edge Delivery.
* SITES-24436: API REST de fragmentos de contenido: se ha introducido la caché local para acelerar la recuperación de referencias duplicadas.
* SITES-25155: API REST de fragmentos de contenido: elimine el parámetro de consulta &quot;enabledForFolder&quot; obsoleto en la lista de modelos.
* SITES-25913: API REST de fragmentos de contenido: validación de recursos con intervalo de tiempo antes de iniciar el flujo de trabajo de publicación.
* SITES-25976: los vínculos dentro de los fragmentos de experiencias no se adaptan después del despliegue de MSM.
* SITES-26271: API REST de fragmentos de contenido: cambie a BFS Traversal para el punto final de variación de GET.
* SITES-27486: editor universal: integración de AEM.
* SITES-27775: búsqueda de referencia optimizada durante la publicación (carga diferida de metadatos).
* SITES-27782: Edge Delivery con el editor universal: añada una implementación específica de editor-suscriptor para publicar contenido en Edge Delivery (acceso anticipado).
* SITES-27792: Edge Delivery con editor universal: añada la plantilla de configuración del servicio Edge Delivery.
* SITES-28557: API REST de fragmentos de contenido: permita el uso de ETags recuperados llamando a `/cf/fragments/{fragmentId}` con `references=direct` para aplicar parches a un fragmento de contenido.
* SITES-28683: permita que las búsquedas de MSM LiveRelationship omitan el estado avanzado.
* SITES-29601: API REST de fragmentos de contenido: validación para referencias de fragmentos de contenido de campos de texto largos.
* SITES-29614: API REST de fragmentos de contenido: recupere un flujo de trabajo mediante el punto final `/cf/workflows/{workflowInstanceId}`, donde workflowInstanceId es el ID devuelto por la solicitud de publicación.
* SITES-29615: API REST de fragmentos de contenido: enumere todas las solicitudes por lotes creadas mediante POST `/cf/batch` mediante `GET /cf/batch`.
* SITES-29874: API REST de fragmentos de contenido: las referencias de campos de texto largos de fragmentos de contenido ahora se recuperan e hidratan.
* SITES-29930: API REST de fragmentos de contenido: añada métricas para el flujo de trabajo de publicación de fragmento de contenido.
* SITES-29986: API REST de fragmentos de contenido: compatibilidad con la nomenclatura técnica del modelo CF.
* SITES-30088: API REST de fragmentos de contenido: publicar CF: omita la recuperación de referencias cuando filterReferencesByStatus está vacío.
* SITES-30126: API REST de fragmentos de contenido: mejora de rendimiento de publicación de CF: se ha sustituido la comprobación de si un recurso es un fragmento con una comprobación mínima.
* SITES-30328: Edge Delivery con editor universal: añada compatibilidad para la previsualización desde la barra de tareas.
* SITES-30445: API REST de fragmentos de contenido: esquema de la interfaz de usuario del modelo CF: añada una opción para controlar el estado inicial de comprimible.
* SITES-30604: API REST de fragmentos de contenido: admite la adopción de esquemas de metadatos de modelo en la nueva interfaz de usuario.
* SITES-30885: procesamiento JSON optimizado en consultas persistentes.
* SITES-30886: API REST de fragmentos de contenido: flujos de trabajo de GET para el punto final del fragmento de contenido en función de los uuid de fragmento almacenados en los metadatos del flujo de trabajo.
* SITES-31005: mejore la interfaz de usuario del trabajo de despliegue para mostrar el progreso.
* SITES-31020: mejore la interfaz de usuario del trabajo de creación de Live Copy para mostrar el progreso.
* SITES-31111: API REST de fragmentos de contenido: permita que la API de parches de variación acepte referencias de fragmentos de contenido dentro de lanzamientos de fragmentos de contenido.
* SITES-31343: API REST de fragmentos de contenido: añada filtrado y paginación por fecha a un punto final que enumere las solicitudes por lotes.
* SITES-31472: eliminar el lanzamiento puede hacer que el repositorio se detenga si el lanzamiento es masivo.
* SITES-31641: API REST de fragmentos de contenido: añada la propiedad a los campos de modelo para almacenar mapas dinámicos relacionados con las extensiones.
* SITES-31677: el espacio de trabajo personalizado admite la exportación de fragmentos de contenido de AEM a destino.
* SITES-31770: API REST de fragmentos de contenido: mejoras de rendimiento de PATCH.
* SITES-31782: API REST de fragmentos de contenido: añada una descripción para los recursos locales.
* SITES-32175: permita confirmaciones intermediarias tanto para la creación de Live Copy como para el despliegue de la página MSM.

### Problemas solucionados {#fixed-issues-21331}

* CQ-4359756: Reglas de traducción ahora incluye propiedades de filtro a nivel de componente.
* CQ-4359826: resuelve el estado incoherente en el panel de referencia de fragmentos de contenido.
* CQ-4359866: la clase LanguageUtils ahora admite la prueba unitaria sin añadir dependencia adicional.
* FORMS-13990: API de servicios de formularios: Generación de documentos : el campo de datos, cuando se deja vacío después de seleccionarse, da 200 cuando se espera 400.
* FORMS-14309: API de servicios de formularios : extraiga la rectificación del código de respuesta de datos.
* FORMS-18526: cuando se copia una regla con varios campos en condiciones, el campo fijo no cambia.
* FORMS-18977: el servicio DOR no pasa el título del documento.
* FORMS-19047: faltan traducciones después de publicar un formulario adaptable en los formularios de AEM en SP22.
* FORMS-19234: no se puede utilizar la función de cronología de los PDF en los formularios de AEM.
* FORMS-19628: en el DOR generado automáticamente, al excluir el título del panel anidado, también se oculta el título del panel raíz.
* FORMS-19651: corrige la regla cuando se hace clic en un botón que se usa en una condición binaria y también se utiliza el mismo botón en la declaración Then.
* FORMS-19808: FormsPortal: no se pueden extraer borradores cuando la carga diferida está habilitada.
* FORMS-19887: la propiedad de acceso no funciona en la vista previa de HTML5.
* SITES-15452: los elementos CF únicos no deben comprobarse con sus copias en el lanzamiento.
* SITES-24492: la lista de pestañas ARIA no tiene un nombre accesible.
* SITES-24623: API REST de fragmentos de contenido: corrija la discrepancia de ETag entre los extremos para el mismo CF.
* SITES-24668: la funcionalidad del carril de referencias se interrumpe cuando el zoom se incrementa al 400 %.
* SITES-24678: el lector de pantalla no anuncia el mensaje de estado del carril de referencias.
* SITES-24697: el lector de pantalla no anuncia el estado de carga del modelo de imagen.
* SITES-24708: la funcionalidad del carril de filtros se interrumpe cuando el zoom se incrementa al 400 %.
* SITES-25235: el lector de pantalla no anuncia el mensaje de carga de contenido del carril de filtro.
* SITES-25254: la barra de desplazamiento horizontal aparece en modo carrusel cuando el contenido se ve a 320 píxeles.
* SITES-25433: Edge Delivery con editor universal: corrija el renderizado de versiones de páginas para estructuras de sitios en varios idiomas.
* SITES-26064: API REST de fragmentos de contenido: corrija la devolución del código de estado al crear un fragmento y obtener un `AccessDeniedException` en el servidor.
* SITES-26890: al utilizar el teclado, el enfoque del teclado &quot;Encabezados de tabla&quot; del ámbito no está visible en la página Administrar publicación.
* SITES-29075: la información general de Live Copy no funciona para sitios web de gran volumen.
* SITES-29514: Edge Delivery con editor universal: haga que GitHub/URL del proyecto sea obligatorio al crear un nuevo sitio.
* SITES-29691: no se puede mover la página en un caso específico relacionado con lanzamientos.
* SITES-29745: API REST de fragmentos de contenido: implemente la hidratación de las variaciones de referencias en el recorrido de BFS.
* SITES-29748: corrija las condiciones de procesamiento para mostrar las acciones Administrar publicación/Publicación rápida dentro del editor CF.
* SITES-29789: problema con el cambio del vínculo del componente en las páginas raíz copiadas.
* SITES-29987: API REST de fragmentos de contenido: crear y editar modelo de fragmento de contenido no es compatible con `previewUrlPattern`.
* SITES-30140: problema de doble ventana al crear la referencia de fragmento de contenido.
* SITES-30327: API REST de fragmentos de contenido: la publicación de CF sin permisos crea flujos de trabajo independientes para cada recurso de carga útil.
* SITES-30333: lea los metadatos de los recursos de jcr para evitar problemas de análisis de XMP.
* SITES-30353: GraphQL DataFetchingExceptions para el campo &quot;src&quot; en fragmentos de contenido de AEM.
* SITES-30377: Edge Delivery con editor universal: corrija los nombres de la organización y del sitio.
* SITES-30386: Edge Delivery con editor universal: quite UE duplicado y heredado `cors.js`.
* SITES-30583: API REST de fragmentos de contenido: la herramienta Buscar y reemplazar cambia todos los caracteres a minúsculas.
* SITES-30585: API REST de fragmentos de contenido: `previewUrlPattern` no se estableció en la creación de CFM con referencias.
* SITES-30634: Imagen Texto alternativo y alineación de RTE no funcionan de forma coherente.
* SITES-30660: problema de conformidad de ADA con el componente personalizado de AEM.
* SITES-30695: Edge Delivery con editor universal: aumente la clasificación de la canalización de reescritura para no interferir con el código personalizado.
* SITES-30727: no se pueden arrastrar y soltar componentes en el editor de creación de producción.
* SITES-30752: no utilice encabezados `If-modified-since`/`last-modified` al generar una respuesta de consulta persistente.
* SITES-30871: DOM se actualiza después de activar el detector de postedición.
* SITES-30877: estado de despliegue de página secundaria incorrecto.
* SITES-30899: la opción de despliegue &quot;Más tarde&quot; permite continuar sin seleccionar ninguna fecha.
* SITES-30947: excepción de puntero nulo debido a que falta la propiedad &quot;behavior&quot; en el modelo durante el despliegue.
* SITES-31157: API REST de fragmentos de contenido: el parche falla en un caso específico.
* SITES-31162: API REST de fragmentos de contenido: corrija el problema de conversión del campo `DateTimeField` en `ModelFieldMapper`.
* SITES-31174: API REST de fragmentos de contenido: las etiquetas no se publicaron junto con la solicitud de publicación.
* SITES-31272: no se puede crear una copia de idioma de Assets mediante PageManager.copy.
* SITES-31327: API REST de fragmentos de contenido: elimine la validación ETag en la solicitud de fragmento de GET.
* SITES-31387: error de JavaScript &quot;ns.ui.alert no es una función&quot; al volver a habilitar la herencia de componentes fantasma.
* SITES-31454: API REST de fragmentos de contenido: relaje el motivo para que los campos de referencia de fragmento también acepten UUID.
* SITES-31455: API REST de fragmentos de contenido: corrija la discrepancia ETag entre los puntos de conexión para el mismo modelo de fragmento de contenido.
* SITES-31459: API REST de fragmentos de contenido: la Live Copy de CF no se puede editar cuando hay un campo de referencia de contenido.
* SITES-31467: js-errors de contexthub.authoring-hook.js en el editor de páginas.
* SITES-31487: API REST de fragmentos de contenido: permita que se llame al punto final de permisos para la carpeta raíz.
* SITES-31621: Edge Delivery con el editor universal: elimine la fila vacía de las hojas de cálculo que son copias en vivo.
* SITES-31676: la creación o eliminación de componentes deja un espacio en blanco en la parte inferior de la página.
* SITES-31822: falta la etiqueta de casilla de verificación ClassicUI y HTML codificado.
* SITES-31857: la creación de CF falla en carpetas con comillas simples.
* SITES-31888: la eliminación de fragmentos de contenido no se puede propagar a la vista previa.
* SITES-31922: API REST de fragmentos de contenido: el punto final referencedBy no devuelve referencias de página.
* SITES-31987: no muestre direcciones URL de vista previa para fragmentos de contenido al publicarlos en Vista previa.
* SITES-32095: la actualización automática falla en el detector de eventos afterchilddelete en Live Copy.
* SITES-32237: Edge Delivery con editor universal: corrija el renderizado de componentes de texto vacíos o mal formados.

### Problemas conocidos {#known-issues-21331}

* SITES-33177: los estilos de sección almacenados como cadenas separadas por comas se rompen.
* SITES-33262: los bloques sin propiedad de nombre producen un error en la representación y publicación de la página.

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
