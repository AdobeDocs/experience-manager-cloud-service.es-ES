---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: fa2da21ef6424bce0830d503eba650e1c1bf3dc2
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 18%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 17964 {#release-17964}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 17964, que se publicó el jueves, 25 de septiembre de 2024. La versión de mantenimiento anterior era 17689. La 17882 de la versión se ha convertido en privada debido a un problema.

La activación de funcionalidades 2024.10.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-17964}

* ASSETS - 37750: [Prioridad 4] [Compatibilidad de GraphQL] con URL de DM scene7: recortes inteligentes de imagen.
* CQ - 4354583: [AEMaaCS] Enviar eventos de proceso de traducción a través de la canalización de Adobe.
* CQ - 4357642: actualizar credenciales de MSFT en el conector OOTB.
* CQ - 4358217: deserialice el cuerpo de la solicitud desde la entidad de solicitud.
* CQ - 4358342: registrar RequestProcessors solo en un método HTTP.
* FORMS - 10781: mejore el editor de reglas para crear reglas para el elemento siguiente/anterior de un panel.
* FORMS - 14595: [Faltan valores de característica sin explorador] en el documento de registro cuando se usan datos rellenados previamente para calcular el documento de registro para la representación sin explorador.
* FORMS - 15619: Kit de traducción actualizado de AEM Forms.
* FORMS - 16113: [Adobe Sign]No se puede actualizar el estado del acuerdo por un usuario diferente.
* FORMS - 16155: [Editor de reglas] Implementar función asincrónica.
* GRANITE - 53872: Añadir nuevas eVars envolventes para el ID del cliente IMS.
* SITES - 23738: Versión Componentes principales 2.27.0.
* SITES: 16610: Fragmentos de contenido: obtener el punto de conexión de detalles del inicio.
* SITES - 16614: Fragmentos de contenido: Punto final de Rebase Launch.
* SITES - 16615: Fragmentos de contenido: Promocionar extremo de Launch.
* SITES: 24215: Fragmentos de contenido: Implementar Obtener extremo de fuentes de Launch.
* SITES - 20336: Fragmentos de contenido: mejore la validación al eliminar un modelo de fragmento de contenido.
* SITES - 21090: Fragmentos de contenido: agregar compatibilidad con valores mínimos y máximos fraccionarios para campos numéricos
* SITES - 21658: Fragmentos de contenido: actualice para utilizar referencias UUID.
* SITES - 23054: Fragmentos de contenido: Copiar modelos de fragmentos de contenido.
* SITES: 23264: Fragmentos de contenido: cree un esquema estático de un modelo.
* SITES: 23265: fragmentos de contenido: exponen el esquema estático de un modelo a través del punto final de la GET del esquema de la interfaz de usuario.
* SITES - 23266: Fragmentos de contenido: capacidad para agregar restricciones a los modelos de fragmentos de contenido.
* SITES - 23778: Fragmentos de contenido: Los modelos de fragmentos de contenido de búsqueda deben permitir la búsqueda de modelos que nunca se hayan publicado.
* SITES - 23335: Fragmentos de contenido: Agregue compatibilidad para referencias de recursos externos.
* SITES - 24626: Fragmentos de contenido: RTC: Permisos para la migración UUID: 2.
* SITIOS - 24786: Fragmentos de contenido: mejoras para el extremo `referencesTree`.
* SITES - 24833: Fragmentos de contenido: elimina la validación de la entrada del HTML con una lista de etiquetas de HTML permitidas.
* SITES: 23380: GraphQL: utilice la API adecuada para leer los metadatos de los recursos.
* SITES - 22864: [Editor universal de Edge Delivery AEM] con nueva integración de estructura de contenido de la nueva versión H2 2024 (en inglés).
* SITES - 23584: Las pruebas de componentes de base fallan en Java 17.
* SITES - 23662: Evento: el usuario que almacena en déclencheur una solicitud de publicación no se puede extraer de las instrucciones de registro JCR en los registros del servidor.
* SITES - 23301: Añada compatibilidad para iniciar un nuevo flujo de trabajo para crear estructuras de carpetas al crear traducciones de fragmentos de contenido.
* SITES - 23336: Fragmentos de contenido: Agregar compatibilidad con referencias de recursos externos
* SITES: 24091: división del paquete de contenido de MSM: principal.
* SITES - 24114: isSourceRenderCondition: Reduzca el mensaje de registro de errores a DEBUG.
* SITES - 24166: mitigación de recursos remotos para el editor de IU táctil.
* SITES - 24409: registre todos los procesadores de solicitudes en un único método HTTP.
* SITES - 25008: Mejore el tratamiento de los problemas de PersistenceExceptions y permisos.
* SITIOS - 24821: [Xwalk] Haga que aem.page / aem.live sea el predeterminado.

### Problemas solucionados {#fixed-issues-17964}

* CQ - 4356887: Incoherencia en el estado del proyecto de traducción para Akamai Technologies Inc.
* CQ - 4357878: El marco de trabajo de traducción no establece el estado de error tras la traducción del error del proveedor
* CQ - 4358028: error al crear el proyecto si se carga la miniatura.
* CQ - 4358290: La configuración de Target NO funciona en la página publicada.
* FORMS: 13173: Desalineación de la lista desplegable en el campo Formulario adaptable > Editor de reglas > Colocar objeto.
* FORMS - 13873: AFv2: (&quot;-&quot;) en el nombre del componente resultan en errores de reglas.
* FORMS - 14340: Error en la creación de instancias de FormsAndDocumentOmniSearchHandler y CloudStorageSubmitActionInserter.
* FORMS - 15363: Nombre mostrado en el editor de reglas.
* FORMS: 15381: mejora de la interfaz de usuario del mensaje Ámbito de autorización.
* FORMS AEM - 15595: Problema de salto de línea del texto de consentimiento del componente de TnC del formulario de.
* FORMS - 15623: AEMaaCS Forms: Alternativas para actualizar varias tablas en Dynamics con un POST.
* FORMS - 15682: AEM Forms - No se puede enlazar el documento de registro a Dynamics FDM.
* FORMS - 15799: La página de firma de Adobe Sign GovCloud no se representa en el iframe.
* FORMS - 15835: problema de reescritura de URL del formulario posterior al envío.
* FORMS - 16091: Consumo del archivo Binary.java reestructurado.
* FORMS - 16096: El usuario de Forms no tiene acceso al cuadro de diálogo de extremo de restauración.
* FORMS: 16139: Agregar el registro necesario para el DoR en el formulario de componentes principales.
* FORMS - 6935: el estado del componente activo carece de una relación de contraste de 3 a 1.
* FORMS - 7018: El elemento vacío recibe el enfoque.
* GRANITE - 53028: NPE en ExternalProcessPollingHandler.
* GRANITE - 53907: No se puede identificar al usuario de servicio como superusuario de flujo de trabajo.
* SITES - 24405: Fragmentos de contenido: La información ampliada de las enumeraciones debe ser más flexible
* SITES - 23024: Fragmentos de contenido: La enumeración no devuelve bloqueado: true en fragmentos de GET.
* SITES - 23269: Fragmentos de contenido: la creación de fragmentos de contenido permite configurar campos bloqueados.
* SITES - 23337: Fragmentos de contenido: El extremo por lotes con `body` falla con la excepción de conversión.
* SITIOS - 23474: Fragmentos de contenido: la paginación debe excluir los recursos rotos en los fragmentos de contenido de búsqueda.
* SITIOS - 23615: Fragmentos de contenido: La información de creación de la copia de fragmentos de contenido no se actualiza
* SITES - 23668: Fragmentos de contenido: el parche de Live Copy con varios campos falla con 400
* SITES - 23695: Fragmentos de contenido: La descripción de la pestaña no está disponible en UiSchema
* SITES - 23704: Fragmentos de contenido: no se admiten enumeraciones de varios valores en _extendedInfo
* SITES - 23781: Fragmentos de contenido: no se permiten valores duplicados en los campos de enumeración
* SITES - 24150: Fragmentos de contenido: Versión del fragmento de contenido Faltan datos de creación sobre la creación
* SITES - 24230: Fragmentos de contenido: corregir el filtrado después del estado de replicación `modified` en Buscar modelos de fragmentos de contenido
* SITES - 24233: Fragmentos de contenido: filtrar por `publishedBy` puede incluir recursos sin publicar en los modelos de fragmentos de contenido de búsqueda
* SITES: 24355: Fragmentos de contenido: la relación activa no se respeta para los fragmentos de contenido creados en carpetas
* SITES - 24816: Fragmentos de contenido: El orden de los mensajes ValidationStatus es incoherente.
* SITIOS - 23896: Eventos: hay más eventos junto con un evento Página desplazada
* SITIOS - 23899: Evento: los eventos de página se retrasan o no se generan
* SITES - 23961: Evento: la creación de modelos de fragmentos de contenido con referencias falla cuando la carpeta de configuración está presente
* SITIOS - 23963: Evento: los eventos eliminados de la página a veces no llegan
* SITES - 23443: GraphQL: El cursor de GraphQL consulta un comportamiento incoherente.
* SITES - 10994: El orden de enfoque del teclado no es lógico.
* AEM SITIOS - 16357: El botón de configuración se trunca en la pestaña Configurar Analytics del menú Sitios.
* SITIOS - 19836: el componente Fantasma del contenedor se muestra en las instancias de publicación y vista previa.
* SITIOS - 22348: La página de información general de Live Copy no se carga si su contenido supera las 100 Live Copies para un proyecto.
* SITES - 22960: solucionador de recursos sin cerrar en ContentFragmentModelOmniSearchHandler.
* SITES - 23284: codificación de URL que provoca el cuadro de diálogo del explorador de rutas en blanco.
* SITIOS - 23505: los componentes muestran direcciones URL incorrectas cuando la página se mueve a otra ubicación.
* SITIOS - 23574: no se puede obtener una vista previa o comparar con las versiones actuales para muchas páginas
* SITES - 23585: Problema con la restauración de la herencia para los componentes que tienen un nodo cq:responsive
* AEM SITES - 23650: Discrepancia en el recuento de vínculos entrantes en el entorno de autor de la publicación de la página de
* SITES - 23659: Regresión del servlet de idioma de contenido provocada por la alternancia FT_* SITES - 9757
* SITES - 23759: Los Assets añadidos en el fragmento de experiencia no se publican con los lanzamientos
* AEM SITES - 24025: 302 Redirecciones en el encabezado de ubicación de devolución de la ubicación de retorno usando DNS interno en lugar de DNS público
* AEM SITES - 24036: investigación necesaria para la detección de caracteres persistentes RTE en formato ASCII de la
* SITES - 24317: La configuración proxy no funciona con la autenticación básica
* SITIOS - 24918: [Xwalk] corrige 504 errores que se devuelven ocasionalmente al usar una salida de IP dedicada.

### Problemas conocidos {#known-issues-17964}

* FORMS - 15818: No se encontró la entrada de descriptor de componente `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` en los registros del servidor. Son sentencias del registro inofensivas.

### Características y API obsoletas {#deprecated-17964}

Tenga en cuenta que estamos en proceso de actualizar `com.day.cq.wcm.api` y con la versión actual, hemos marcado como `@Deprecated` algunos de sus métodos y clases. Estos se eliminarán en futuras versiones, por lo que considere la posibilidad de cambiar a las alternativas sugeridas si utiliza alguna de ellas.

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-17964}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 16 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-17964}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.68.0 | [API Oak 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.27.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
