---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: ee3e1bedddddff0aa41665359a91a0de48fd19c8
workflow-type: ht
source-wordcount: '1411'
ht-degree: 100%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 17964 {#release-17964}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 17964, que se publicó el 25 de septiembre de 2024. La versión de mantenimiento anterior fue la 17689. La versión 17882 ahora es privada debido a un problema.

La activación de funcionalidades 2024.10.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-17964}

* ASSETS - 37750: [prioridad 4] [GraphQL] Compatibilidad para URL de DM scene7: recortes inteligentes de imagen.
* CQ - 4354583: [AEMaaCS]: enviar eventos del proceso de traducción a través de la canalización de Adobe.
* CQ - 4357642: actualizar credenciales de MSFT en el conector OOTB.
* CQ - 4358217: deserializar cuerpo de solicitud desde la entidad de solicitud.
* CQ - 4358342: registrar RequestProcessors solo en un método HTTP.
* FORMS - 10781: mejorar el editor de reglas para crear reglas para el elemento siguiente/anterior de un panel.
* FORMS - 14595: [Función sin explorador] faltan valores en el documento de registro cuando se usan datos rellenados previamente para calcular el documento de registro para el procesamiento sin explorador.
* FORMS - 15619: kit de traducción actualizado de AEM Forms.
* FORMS - 16113: [Adobe Sign]no se puede actualizar el estado del acuerdo por un usuario diferente.
* FORMS - 16155: [Editor de reglas] implementar la función asincrónica.
* GRANITE - 53872: añadir nuevas variables de entorno para el ID de cliente de IMS.
* SITES - 23738: componentes principales de la versión 2.27.0.
* SITES - 16610: fragmentos de contenido: obtener punto final de detalles de inicio.
* SITES - 16614: fragmentos de contenido: volver a basar punto final de inicio.
* SITES - 16615: fragmentos de contenido: promocionar punto final de inicio.
* SITES - 24215: fragmentos de contenido: implementar Obtener punto final de orígenes de inicio.
* SITES - 20336: fragmentos de contenido: mejorar la validación al eliminar un modelo de fragmento de contenido.
* SITES - 21090: fragmentos de contenido: añadir compatibilidad con valores mínimos y máximos fraccionarios para campos numéricos
* SITES - 21658: fragmentos de contenido: actualizar para utilizar referencias de UUID.
* SITES - 23054: fragmentos de contenido: copiar modelos de fragmentos de contenido.
* SITES - 23264: fragmentos de contenido: crear un esquema estático de un modelo.
* SITES - 23265: fragmentos de contenido: exponer el esquema estático de un modelo a través del punto final de la GET del esquema de la interfaz de usuario.
* SITES - 23266: fragmentos de contenido: posibilidad de añadir restricciones a los modelos de fragmentos de contenido.
* SITES - 23778: fragmentos de contenido: los modelos de fragmentos de contenido de búsqueda deben permitir la búsqueda de modelos que nunca se hayan publicado.
* SITES - 23335: fragmentos de contenido: añadir compatibilidad para referencias de recursos externos.
* SITES - 24626: fragmentos de contenido: RTC: permisos para la migración de UUID: 2.
* SITIOS - 24786: fragmentos de contenido: mejoras para el punto final `referencesTree`.
* SITES - 24833: fragmentos de contenido: eliminar la validación de la entrada del HTML con una lista de etiquetas HTML permitidas.
* SITES - 23380: GraphQL: utilizar la API adecuada para leer los metadatos de los recursos.
* SITES - 22864: [Edge Delivery AEM] Editor universal con nueva integración de estructura de contenido de AEM H2 2024.
* SITES - 23583: las pruebas de componentes de base fallan en Java 17.
* SITES - 23662: Eventos: el usuario que activa una solicitud de publicación no se puede extraer de las sentencias del registro JCR en los registros del servidor.
* SITES - 23301: añadir compatibilidad para iniciar un nuevo flujo de trabajo para crear estructuras de carpetas al crear traducciones de fragmentos de contenido.
* SITES - 23336: Fragmentos de contenido: añadir compatibilidad con referencias de recursos externos
* SITES - 24091: división del paquete de contenido de MSM: maestro.
* SITES - 24114: isSourceRenderCondition: reducir el mensaje de registro de errores a DEBUG.
* SITES - 24166: mitigación de recursos remotos para el editor de IU táctil.
* SITES - 24409: registrar todos los procesadores de solicitudes en un único método HTTP.
* SITES - 25008: mejorar el tratamiento de los problemas de PersistenceExceptions y de permisos.
* SITES - 24821: hacer que aem.page / aem.live sea el predeterminado.

### Problemas solucionados {#fixed-issues-17964}

* CQ - 4356887: incoherencia en el estado del proyecto de traducción para Akamai Technologies Inc.
* CQ - 4357878: el marco de trabajo de traducción no establece el estado de error tras la traducción del error del proveedor.
* CQ - 4358028: error al crear el proyecto si se carga la miniatura.
* CQ - 4358290: la configuración de destinatario NO funciona en la página publicada.
* FORMS - 13173: desalineación de la lista desplegable en el campo Formulario adaptable > Editor de reglas > Eliminar objeto.
* FORMS - 13873: AFv2: (&quot;-&quot;) en el nombre del componente produce errores de reglas.
* FORMS -14340: error al crear una instancia de FormsAndDocumentOmniSearchHandler y CloudStorageSubmitActionInserter.
* FORMS - 15363: nombre mostrado en el Editor de reglas.
* FORMS - 15381: mejora de la interfaz de usuario del mensaje de Ámbito de autorización.
* FORMS - 15595: problema de salto de línea del texto de consentimiento del componente TnC del Formulario de AEM.
* FORMS - 15623: AEMaaCS Forms: alternativas para actualizar varias tablas en Dynamics con un POST.
* FORMS - 15682: AEM Forms: no se puede enlazar el documento de registro a Dynamics FDM.
* FORMS - 15799: la página de firma de Adobe Sign GovCloud no se representa en iFrame.
* FORMS - 15835: problema de reescritura de URL del formulario posterior a envío.
* FORMS - 16091: consumo del archivo Binary.java reestructurado.
* FORMS - 16096: el usuario de formularios no tiene acceso al cuadro de diálogo de punto final REST.
* FORMS - 16139: añadir el registro necesario para DoR en el formulario de componentes principal.
* FORMS - 6935: el estado del componente activo carece de una relación de contraste de 3 a 1.
* FORMS - 7018: el elemento vacío recibe el enfoque.
* GRANITE - 53028: NPE en ExternalProcessPollingHandler.
* GRANITE - 53907: no se puede identificar al usuario de servicio como superusuario de flujo de trabajo.
* SITES - 24405: fragmentos de contenido: la información ampliada de las enumeraciones debe ser más flexible
* SITES - 23024: fragmentos de contenido: la enumeración no devuelve bloqueado: true en fragmentos GET.
* SITES - 23269: fragmentos de contenido: la creación de fragmentos de contenido permite configurar campos bloqueados.
* SITES - 23337: fragmentos de contenido: el punto final de lote con `body` falla con la excepción de proyección.
* SITES - 23474: fragmentos de contenido: la paginación debe excluir los recursos interrumpidos en los fragmentos de contenido de búsqueda.
* SITES - 23615: fragmentos de contenido: la información de creación de la copia de fragmentos de contenido no se actualiza
* SITES - 23668: fragmentos de contenido: el parche de Live Copy con varios campos falla con 400
* SITES - 23695: fragmentos de contenido: la descripción de la pestaña no está disponible en UiSchema
* SITES - 23704: fragmentos de contenido: no se admiten enumeraciones de varios valores en _extendedInfo
* SITES - 23781: fragmentos de contenido: no se permiten valores duplicados en campos de enumeración
* SITES - 24150: fragmentos de contenido: faltan datos de creación de la versión del fragmento de contenido sobre la creación
* SITES - 24230: fragmentos de contenido: solucionar el filtrado después del estado de replicación `modified` en modelos de fragmentos de contenido de búsqueda
* SITES - 24233: fragmentos de contenido: filtrar por `publishedBy` puede incluir recursos sin publicar en modelos de fragmentos de contenido de búsqueda
* SITES - 24355: fragmentos de contenido: la relación activa no se respeta para los fragmentos de contenido creados en carpetas
* SITES - 24816: fragmentos de contenido: el orden de los mensajes ValidationStatus es incoherente.
* SITES - 23896: eventos: hay más eventos junto con un evento Página movida
* SITES - 23899: eventos: los eventos de página se retrasan o no se generan en absoluto
* SITES - 23961: eventos: la creación de modelos de fragmentos de contenido con referencias falla cuando la carpeta de configuración está presente
* SITES - 23963: eventos: los eventos eliminados de la página a veces no llegan
* SITES - 23443: GraphQL: comportamiento incoherente de la consulta del cursor de GraphQL.
* SITES - 10994: el orden de enfoque del teclado no es lógico.
* SITES - 16357: el botón de configuración se trunca en la pestaña Análisis de configuración del menú de Sites.
* SITES - 19836: el componente fantasma del contenedor se muestra en las instancias de publicación y vista previa.
* SITES - 22348: la página de información general de Live Copy no se carga si su contenido supera las 100 Live Copies para un proyecto.
* SITES - 22960: solucionador de recursos sin cerrar en ContentFragmentModelOmniSearchHandler.
* SITES - 23284: la codificación de URL provoca que el cuadro de diálogo del explorador de rutas esté en blanco.
* SITES - 23505: los componentes muestran direcciones URL incorrectas cuando la página se mueve a otra ubicación.
* SITES - 23574: no se puede obtener una vista previa o comparar con las versiones actuales para muchas páginas
* SITES - 23585: problema con la restauración de la herencia para los componentes que tienen un nodo cq:responsive
* SITES - 23650: discrepancia en el recuento de vínculos entrantes en el entorno de autor de la publicación de la página en AEM
* SITES - 23659: regresión del servlet de idioma de contenido provocada por la alternancia FT_* SITES - 9757
* SITES - 23759: los recursos añadidos en el fragmento de experiencia no se publican con los lanzamientos
* SITES - 24025: 302 redirecciones en el encabezado de ubicación de devolución de AEM que utilizan DNS interno en lugar de DNS público
* SITES - 24036: investigación necesaria para caracteres persistentes de RTE de AEM en formato ASCII
* SITES - 24317: la configuración proxy no funciona con la autenticación básica
* SITES - 24918: corrige los errores 504 que se devuelven ocasionalmente al usar una salida de IP dedicada.

### Problemas conocidos {#known-issues-17964}

* FORMS - 15818: no se ha encontrado la entrada del descriptor de componente `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` en los registros del servidor. Son sentencias del registro inofensivas.

### Características y API obsoletas {#deprecated-17964}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

A continuación se muestra un resumen de las funciones que han quedado recientemente en desuso o de las que están en proceso de finalización de soporte.

#### API de uso de JavaScript {#javascript-use-api}

[La API de uso de JavaScript](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) está en desuso oficialmente debido a los desafíos que los usuarios tienen al depurar y mantener el código que aprovecha la API, así como las limitaciones de rendimiento en comparación con la alternativa de Java.

Debería hacer la transición a [la API para uso de Java](https://experienceleague.adobe.com/es/docs/experience-manager-htl/content/java-use-api), que ofrece un mejor rendimiento, una depuración más sencilla y una mayor compatibilidad a largo plazo.

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

Tenga en cuenta que Adobe está en proceso de actualizar `com.day.cq.wcm.api`. Algunos de sus métodos y clases se han marcado como `@Deprecated` en la versión actual. Se eliminarán en futuras versiones. Considere la posibilidad de cambiar a las alternativas sugeridas.

### Correcciones de seguridad {#security-17964}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 16 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-17964}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.68.0 | [API Oak 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.27.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
