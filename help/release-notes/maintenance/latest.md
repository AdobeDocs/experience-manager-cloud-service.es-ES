---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 80edd0255b38beee93b3f9c779ae0f364500b4a5
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 81%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 17465 {#release-17465}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 17465, que se publicó el jueves, 14 de agosto de 2024. La versión de mantenimiento anterior fue la 17258.

La activación de funcionalidades 2024.8.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-17465}

* FORMS-15436: Gestione correctamente las excepciones en el planificador de estados de Adobe Sign.
* FORMS-15362: Agregue la configuración para forms-foundation en aemds para habilitar el inicio de sesión.
* FORMS-15261: SPA no se procesa en el editor de Forms.
* FORMS-15138: Gestión de la compatibilidad con versiones anteriores de datos dobles debido a la actualización json de Sling Commons.
* FORMS-15113: Cambio de nombre de clave a sid desde visitorId para el seguimiento RUM.
* FORMS-15103: Los recursos adjuntos en un formulario no se publican en Edge Delivery.
* FORMS-15082: Esquema JSON para asignar a componentes de formulario adaptable personalizados.
* FORMS-15002: Registro de tipo de plantilla de fragmentos v1.
* FORMS-14845: Compatibilidad con xdpRef en el formulario de bases de componentes principales mediante Forms Manager.
* FORMS-14840: Errores del servicio de relleno previo de Forms.
* FORMS-14836: Mejorar la IU del administrador de formularios para enumerar las plantillas de fragmento AF1.
* FORMS-14834: Compatibilidad con plantillas para fragmentos en AF1.
* FORMS-14275: Anulación de página de agradecimiento y el mensaje de agradecimiento en el contenedor incrustado.
* FORMS-13623: Habilite la funcionalidad basada en el tiempo de guardado automático para la versión 2.
* FORMS-8651: cuadro de diálogo de advertencia sobre el cambio de la configuración del modelo de datos en la página de propiedades del formulario.
* SITES-23310: API de REST de fragmentos de contenido: evite las dependencias circulares en las referencias anidadas para fragmentos de contenido.
* SITES-23285: API de REST de fragmentos de contenido: cree un punto final para enumerar todos los idiomas disponibles.
* SITES-22857: API de REST de fragmentos de contenido: los campos de enumeración de la casilla de verificación no deben permitir que varias propiedades se establezcan como falso.
* SITES-22813: API de REST de fragmentos de contenido: defina las propiedades mín./máx. para los campos de enumeración.
* SITES-22031: API de REST de fragmentos de contenido: obtenga modelos de fragmentos de contenido permitidos para la carpeta de un fragmento.
* SITES-17640: API de REST de fragmentos de contenido: validación de la operación de publicación de fragmentos de contenido.
* SITES-22677: API de REST de fragmentos de contenido: recupera una lista plana de referencias descendientes.
* SITES-22207: modelo duplicado en la creación de fragmentos de contenido.
* SITES-23093 - Eventos: añada etiquetas a las cargas útiles para eventos de modelos de fragmentos de contenido.
* SITES-23092 - Eventos: añada etiquetas a las cargas útiles para eventos de fragmentos de contenido.
* SITES-22447: añada compatibilidad de herencia de propiedades del fragmento de experiencia a la pestaña Propiedades básicas.
* SITES-12209: mejore el rendimiento del Editor de políticas añadiendo cq:policy al índice.

### Problemas solucionados {#fixed-issues-17465}

* CQ-4358028: error al crear el proyecto si se carga la miniatura.
* CQ-4357891: problema de secuencia del XLIFF exportado.
* CQ-4357059: el trabajo de traducción tarda horas en completarse, lo que provoca un tiempo de espera 503 en AEMaaCS.
* FORMS-15320: el envío de correo electrónico no funciona en el formulario basado en componentes principales.
* FORMS-15272: AEM Forms: el grupo de casillas de verificación solo envía 1 valor.
* FORMS-15269: hay problemas relacionados con el producto después de la versión 16461 de mantenimiento.
* FORMS-15174: problema JsonSchemaParser isValid.
* FORMS-15095: el cuadro de texto multilínea se puede extender más allá de los paneles contenedores en AEM Forms.
* FORMS-15057: la lista de SharePoint de FDM emite un error de envío de archivo adjunto > 999.
* FORMS-15011: el editor principal está causando un error de consola al abrir un formulario en el editor.
* FORMS-14809: la carpeta SDK no se crea automáticamente dentro del directorio temporal compartido.
* FORMS-14327: API del servicio de Forms: Extraer datos: proporciona un código de respuesta 500 cuando se proporciona un PDF no interactivo en la entrada.
* FORMS-7475: la ordenación no funciona en la página de creación de formularios adaptables.
* FORMS-3309: si se seleccionan varias opciones al enviar un formulario, en el DoR generado solo se muestra una opción.
* SITES-23646: el punto final de los modelos GraphQL falla en los modelos creados con OpenAPI si los campos contienen valores únicos.
* SITES-23637: API de REST de fragmentos de contenido: OpenAPI no utiliza el tipo de valor correcto para las enumeraciones.
* SITES-23573: API de REST de fragmentos de contenido: uuid no respeta las relaciones activas en los fragmentos de contenido de GET.
* SITES-23535: API de REST de fragmentos de contenido: los campos múltiples de la lista desglosada del modelo de fragmento de contenido tienen valores vacíos.
* SITES-23534: API de REST de fragmentos de contenido: ClassCastException de validación de fragmentos de contenido.
* SITES-23524: adapte el punto final de los modelos BFF de GraphQL para admitir campos de enumeración de varios campos.
* SITES-23467: API de REST de fragmentos de contenido: los modelos de búsqueda fallan debido a un problema con el cursor.
* SITES-23327: ArrayIndexOutOfBoundsException en AuditLogTimelineEventProvider durante la descripción del procesamiento del evento de cronología.
* SITES-23277: API de REST de fragmentos de contenido: la comprobación de la relación activa de los campos de fragmento de contenido solo debe realizarse para Live Copies.
* SITES-23232: la validación personalizada no funciona en la nueva interfaz de usuario del editor de CF.
* SITES-23090: API de REST de fragmentos de contenido: no se puede actualizar el título de un fragmento de contenido bloqueado.
* SITES-22981: la promoción de un lanzamiento anidado que no es profundo no es una publicación.
* SITES-22870: PathAttributesHandler.processSrcAttr ArrayIndexOutOfBoundsException.
* SITES-22814: API de REST de fragmentos de contenido: los valores de los campos de fragmento en la enumeración de la casilla de verificación deben ordenarse mediante las claves definidas en el modelo.
* SITES-22716: problema con la lista de uso activo de los componentes de OOTB.
* SITES-22457: promocionar un lanzamiento que no es profundo no actualiza el contenido de origen.
* SITES-22449: no se pueden guardar los cambios en los fragmentos de contenido después de la actualización a AEM P20.
* SITES-22279: API de REST de fragmentos de contenido: al fragmento de contenido le falta el atributo único para los tipos de enumeración.
* SITES-22203: API de REST de fragmentos de contenido: alinee las API de administración para responder lo mismo en la misma situación.
* SITES-21973: API de REST de fragmentos de contenido: al modelo le falta el atributo único para los tipos de enumeración.
* SITES-20364: 302 redirecciones que no funcionan con el selector de URL.
* SITES-21198 - VersionPreviewServlet: la limpieza se ejecuta simultáneamente en todos los nodos del clúster, lo que provoca conflictos de combinación y bloquea las confirmaciones.

### Problemas conocidos {#known-issues-17465}

* ASSETS-40875: la clase AssetDeleteHandler escucha eventos de eliminación de recursos y realiza acciones específicas según el tipo de evento de eliminación (PRE_DELETE o POST_DELETE). En determinados casos, el tipo de evento POST_DELETE provoca una NullPointerException.
* FORMS-14340: Error al crear una instancia de FormsAndDocumentOmniSearchHandler y CloudStorageSubmitActionInserter. Son instrucciones de registro inofensivas.
* FORMS-15818: entrada de descriptor de componente &quot;OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml&#39; no se encontró en los registros del servidor. Son instrucciones de registro inofensivas.
* 
   * SITES-23662: el usuario que almacena en déclencheur una publicación no se puede extraer de las sentencias de registro JCR en los registros del servidor. Se trata de una función en desarrollo que podría provocar errores intermitentes e inofensivos &quot;No se puede encontrar un ID de usuario válido en el lote de eventos OSGI&quot; en el registro.

### Aviso de cambio {#change-notice-17465}

* A partir de septiembre de 2024, AEM as a Cloud Service deshabilitará la serialización de los solucionadores de recursos a través del marco de trabajo Exportador de modelos Sling. Consulte la [documentación](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obtener más información.

### Características y API obsoletas {#deprecated-17465}

Tenga en cuenta que estamos en proceso de actualizar `com.day.cq.wcm.api` y con la versión actual, hemos marcado como `@Deprecated` algunos de sus métodos y clases. Estas se eliminarán en futuras versiones, por lo que considere la posibilidad de cambiar a las alternativas sugeridas si utiliza alguna de ellas.

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-17465}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 7 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-17465}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.66.0 | [API Oak 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.25.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
