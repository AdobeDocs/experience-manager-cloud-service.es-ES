---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9d081b468e42306c56238bee6117d92c6afd48d4
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 25%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 23122 {#23122}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 23122, que se publicó el jueves, 29 de octubre de 2025. La versión de mantenimiento anterior fue la 22943.

La activación de funcionalidades 2025.11.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-23122}

* FORMS-21594: Habilitar el bloqueo del contenido y el diseño de las plantillas de comunicaciones interactivas para los autores de contenido.
* FORMS-20385: admite la edición XDP en el editor de comunicaciones interactivas.
* FORMS-10883: Compatibilidad con JSON con etiquetas de área de nombres XHTML en la generación de DoR para garantizar la representación precisa de los datos de texto enriquecido enviados mediante API.
* FORMS-21751: Funciones de lienzo: desbordamiento de texto, interfaz de usuario para salto de página.
* FORMS-22049: editor de comunicaciones interactivas, migración a Spectrum 2.
* FORMS-22050: Compatibilidad con la numeración dinámica de páginas en el Editor de comunicaciones interactivas.
* FORMS-21606: las SPI de procesamiento de OSGi públicas para comunicaciones interactivas.
* FORMS-21613: Informes de transacciones y registro de rendimiento para procesar SPI de comunicaciones interactivas.
* SITES-35092: fragmentos de contenido: nuevo procedimiento de mezcla y actualización para la búsqueda semántica.
* SITES-32319: Entrega OpenAPI: referencias de página de asistencia.
* SITES-20123: GraphQL: admite elementos de superíndice en la respuesta JSON.
* SITES-34744: nueva propiedad &quot;card&quot; en la respuesta del fragmento de contenido que contiene datos que se pueden utilizar para representar una miniatura.
* SITES-34571: permite que los campos de enumeración estén vacíos.
* SITES-34812: Se ha agregado la capacidad de recuperar un fragmento de contenido sin sus referencias, utilizando el parámetro &quot;referencias&quot; con el valor &quot;ninguno&quot;.
* SITES-35176: La extracción de un fragmento de contenido mediante la IU táctil ahora impide que otros usuarios editen el fragmento de contenido en el nuevo editor.
* SITES-30371: compatibilidad añadida para campos de referencia basados en uuid.
* SITES-19309: recupere un máximo de 150 referencias al abrir el asistente para mover páginas.
* SITES-32515: Edge Delivery con editor universal: agregue compatibilidad con varios campos y campos múltiples compuestos (acceso anticipado).
* SITES-33784: Edge Delivery con editor universal: agregue compatibilidad con ld-json en los metadatos de página.
* SITES-34832: Edge Delivery con editor universal: añada la ruta pública de una página a la respuesta del servlet de información de página.
* SITES-25893: Edge Delivery con editor universal: añada compatibilidad para crear y resaltar la representación de texto en bloques.
* SITES-26158: Edge Delivery con editor universal: agregue compatibilidad con el marcado de tablas en bloques y columnas (acceso anticipado).
* SITES-27949: Edge Delivery con editor universal: convierta la asignación de rutas en opcional.

### Problemas solucionados {#fixed-issues-23122}

* CQ-4361144: se ha corregido la omisión de fragmentos de contenido de los trabajos de traducción.
* CQ-4355446: se ha corregido la cadena no localizada en el proyecto de traducción que se produce en el cuadro de diálogo Cancelar trabajo de traducción.
* SITES-34555: GraphQL - QueryValidationError después de las implementaciones.
* SITES-35077: Fragmentos de contenido: la cancelación de la publicación falla en los fragmentos con paréntesis debido a una codificación URL incorrecta.
* SITES-35374: Fragmentos de contenido: el fragmento de contenido editado desaparece después de volver a la navegación.
* SITES-36130: NPE en `EditorRestrictionsStatusImpl`.
* SITES-35810: NullPointerException en Lanzamientos bloquea la cola publishEdgeDeliverySubscriber.
* SITES-34368: AEM CIF genera 12 alias de GraphQL; supera el límite de 10 de Magento 2.4.6-P12.
* SITES-36193: correcciones del conector CCS.
* SITES-35169: Se ha resuelto un problema que causaba una paginación incorrecta cuando la búsqueda devolvía recursos de fragmento no válidos.
* SITES-34574: se ha corregido un problema en el que, en algunos casos, la API de búsqueda de fragmentos de contenido no devolvía el cursor.
* SITES-35520: se ha corregido un problema que provocaba ClassCastException o tiempos de espera al intentar publicar contenido.
* SITES-35210: se ha corregido una excepción NullPointerException que se producía al intentar publicar un fragmento roto con un filtro de referencias vacío.
* SITES-35933: se ha corregido un error que provocaba que los flujos de trabajo de &quot;Solicitud de activación&quot; vacíos se activaran después de que se publicara el fragmento de contenido.
* SITES-35925: se ha corregido un error relacionado con el parche de modelos de fragmentos de contenido que eliminaba las propiedades &quot;traducible&quot; y &quot;showThumbnail&quot; del modelo.
* SITES-35409: se ha corregido un error que impedía volver a publicar los fragmentos ajustados al mover una página.
* SITES-15757: se ha corregido un error que impedía volver a publicar páginas ajustadas al mover una página.
* SITES-34638: se ha corregido un error por el que las propiedades de las páginas principales no se incluían al crear nuevas versiones.
* SITES-35071: La exportación de CSV devuelve resultados sin filtrar cuando Omnisearch utiliza una frase citada.
* SITES-32182: Edge Delivery con el editor universal . Corrija los problemas de codificación con las direcciones URL que contienen parámetros de solicitud ya codificados.
* SITES-34324: Edge Delivery con editor universal: corrija la renderización de vínculos con un tel: protocol.
* SITES-35333: Edge Delivery con editor universal: corrija la selección de representación de recursos para imágenes en los metadatos de la página.
* SITES-35549: Edge Delivery con editor universal: corrección de entidades html con codificación doble en los metadatos de la página.

### Problemas conocidos {#known-issues-23122}

Ninguna.

### Características y API obsoletas {#deprecated-23122}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-23122}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 18 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-23122}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.86.0 | [API de Oak 1.86.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html?lang=es) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.30.2 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
