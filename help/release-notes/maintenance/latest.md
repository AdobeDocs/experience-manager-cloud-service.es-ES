---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: f12e60cdfce24dd2f6c1400157180d16b1b98653
workflow-type: tm+mt
source-wordcount: '998'
ht-degree: 20%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 17393 {#release-17393}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 17393, que se publicó el miércoles, 13 de agosto de 2024. La versión de mantenimiento anterior fue la 17258.

La activación de funcionalidades 2024.8.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-17393}

* FORMS-15436: gestione correctamente las excepciones en el programador de Adobe Sign Status.
* FORMS-15362: agregue la configuración para forms-foundation en aemds para habilitar el inicio de sesión.
* FORMS SPA-15261: La no se procesa en el editor de Forms.
* FORMS-15138: Gestión de la compatibilidad con versiones anteriores de datos dobles debido a la actualización json de sling commons.
* FORMS-15113: cambiando el nombre de clave a sid desde visitorId para el seguimiento RUM.
* FORMS-15103: Los Assets adjuntos en un formulario no se publican en la entrega de Edge.
* FORMS-15082: esquema JSON para asignar a componentes de formulario adaptable personalizados.
* FORMS-15002: registro de tipo de plantilla de fragmentos v1.
* FORMS-14845: compatibilidad con xdpRef en el formulario de bases de componentes principales mediante Forms Manager.
* FORMS-14840: errores del servicio de relleno previo de Forms.
* FORMS-14836: mejore la interfaz de usuario del administrador de formularios para ver las plantillas de fragmento AF1.
* FORMS-14834: compatibilidad con plantillas para fragmentos en AF1.
* FORMS-14275: anulando la página de agradecimiento y el mensaje de agradecimiento en el contenedor incrustado.
* FORMS-13623: habilite la funcionalidad basada en el tiempo de guardado automático para la versión 2.
* FORMS-8651: cuadro de diálogo de advertencia sobre el cambio de la configuración del modelo de datos en la página de propiedades del formulario.
* SITES-23310: API REST de fragmentos de contenido: Impedir dependencias circulares en referencias anidadas para fragmentos de contenido.
* SITES-23285: API de REST de fragmentos de contenido: cree un extremo para enumerar todos los idiomas disponibles.
* SITES-22857: API de REST de fragmentos de contenido: los campos de enumeración de la casilla de verificación no deben permitir que varias propiedades se establezcan en false.
* SITES-22813: API de REST de fragmentos de contenido: defina las propiedades mín./máx. para los campos de enumeración.
* SITES-22031: API de REST de fragmentos de contenido: obtenga modelos de fragmentos de contenido permitidos para la carpeta de un fragmento.
* SITES-17640: API de REST de fragmentos de contenido: validación de la operación de Publish de fragmentos de contenido.
* SITES-22677: API de REST de fragmentos de contenido: recupera una lista plana de referencias descendientes
* SITES-22207: modelo duplicado en la creación de fragmentos de contenido.
* SITES-23093 - Eventos: añadir etiquetas a las cargas útiles para eventos de modelos de fragmentos de contenido.
* SITES-23092 - Eventos: añadir etiquetas a las cargas útiles para eventos de fragmentos de contenido.
* SITES-22447: agregue compatibilidad de herencia de propiedades del fragmento de experiencia a la pestaña Propiedades básicas.
* SITES-12209: mejore el rendimiento del Editor de directivas agregando cq:policy al índice.

### Problemas solucionados {#fixed-issues-17393}

* CQ-4358028: error al crear el proyecto si se carga la miniatura.
* CQ-4357891: problema de secuencia del XLIFF exportado.
* CQ-4357059: el trabajo de traducción tarda horas en completarse, lo que provoca un tiempo de espera 503 en AEMaaCS.
* FORMS-15320: el envío de correo electrónico no funciona en el formulario basado en componentes principales.
* FORMS-15272 - AEM Forms - Grupo de casillas de verificación que solo envía 1 valor.
* FORMS-15269: se enfrentan a problemas relacionados con el producto después de la 16461 de la versión de mantenimiento.
* FORMS-15174: problema JsonSchemaParser isValid.
* FORMS-15095: El cuadro de texto multilínea se puede extender más allá de los paneles contenedores en AEM Forms.
* FORMS-15057: error de la lista de SharePoint de FDM que emite el archivo adjunto para el envío > 999.
* FORMS-15011: el editor principal está causando un error de consola al abrir un formulario en el editor.
* FORMS-14809: la carpeta SDK no se crea automáticamente dentro del directorio temporal compartido.
* FORMS-14327: API de servicio de Forms : extraer datos:- proporciona un código de respuesta 500 cuando se proporciona un pdf no interactivo en la entrada.
* FORMS-7475: la ordenación no funciona en la página de creación de formularios adaptables.
* FORMS-3309: si se seleccionan varias opciones al enviar un formulario, en un DoR generado solo se muestra una opción.
* SITES-23646: el extremo de modelos GraphQL falla en los modelos creados con OpenAPI si los campos contienen valores únicos.
* SITES-23637: API de REST de fragmentos de contenido: OpenAPI no utiliza el tipo de valor correcto para enumeraciones.
* SITES-23573: API de REST de fragmentos de contenido: uuid no respeta las relaciones activas en los fragmentos de contenido de GET.
* SITES-23535: API de REST de fragmentos de contenido: los campos múltiples de la enumeración del modelo de fragmentos de contenido tienen valores vacíos.
* SITES-23534: API de REST de fragmentos de contenido: ClassCastException de validación de fragmentos de contenido.
* SITES-23524: adapte el punto de conexión de los modelos BFF de GraphQL para admitir campos de enumeración de varios campos.
* SITES-23467: API de REST de fragmentos de contenido: los modelos de búsqueda fallan debido a un problema con el cursor.
* SITES-23327: ArrayIndexOutOfBoundsException en AuditLogTimelineEventProvider durante la descripción del procesamiento del evento de la cronología.
* SITES-23277: API de REST de fragmentos de contenido: la comprobación de la relación activa de los campos de fragmentos de contenido solo debe realizarse para las Live Copies.
* SITES-23232: la validación personalizada no funciona en la nueva interfaz de usuario del editor de CF.
* SITES-23090: API de REST de fragmentos de contenido: no se puede actualizar el título de un fragmento de contenido bloqueado.
* SITES-22981: la promoción de un lanzamiento anidado que no es profundo no es una publicación.
* SITES-22870: PathAttributesHandler.processSrcAttr ArrayIndexOutOfBoundsException.
* SITES-22814: API de REST de fragmentos de contenido: casilla de verificación Los valores de los campos de fragmento de enumeración deben ordenarse mediante las claves definidas en el modelo.
* SITES-22716: problema con la lista de uso activo de los componentes de OOTB.
* SITES-22457: promocionar un lanzamiento que no es profundo no actualiza el contenido de origen.
* AEM SITES-22449: no se pueden guardar los cambios en los fragmentos de contenido después de la actualización a la versión P20 de la.
* SITES-22279: API de REST de fragmentos de contenido: a los fragmentos de contenido les falta el atributo único para los tipos de enumeración.
* SITES-22203: API de REST de fragmentos de contenido: alinee las API de administración para responder lo mismo en la misma situación.
* SITES-21973: API de REST de fragmentos de contenido: al modelo le falta el atributo único para los tipos de enumeración.
* SITES-20364 - 302 Redirecciones que no funcionan con el selector de URL.
* SITES-21198 - VersionPreviewServlet: la limpieza se ejecuta simultáneamente en todos los nodos del clúster, lo que provoca conflictos de combinación y bloquea las confirmaciones
* GRANITE-53094: los objetos de uso de JS basados en el repositorio no se pueden encontrar al utilizar rutas relativas.

### Problemas conocidos {#known-issues-17393}

Ninguna.

### Aviso de cambio {#change-notice-17393}

* A partir de septiembre de 2024, AEM as a Cloud Service deshabilitará la serialización de los solucionadores de recursos a través del marco de trabajo Exportador de modelos Sling. Consulte la [documentación](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obtener más información.

### Características y API obsoletas {#deprecated-17393}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Tecnologías integradas {#embedded-tech-17393}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.66.0 | [API Oak 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html?lang=es) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.25.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
