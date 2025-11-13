---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 5474d0c4295cf8eb576cc416589727c67ffafac7
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 20%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 23320 {#23320}

A continuación se resumen las mejoras continuas de la versión de mantenimiento 23320, que se publicó el jueves, 12 de noviembre de 2025. La versión de mantenimiento anterior fue la 22943.

La activación de funcionalidades 2025.11.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

>[!NOTE]
>
>La 23122 de la versión se hizo privada el 3 de noviembre.

### Mejoras {#enhancements-23320}

* AEM CQ-4361363: últimas traducciones de AEM y Granite.
* FORMS-21594: Habilitar el bloqueo del contenido y el diseño de las plantillas de comunicaciones interactivas para los autores de contenido.
* FORMS-20385: admite la edición XDP en el editor de comunicaciones interactivas.
* FORMS-10883: Compatibilidad con JSON con etiquetas de área de nombres XHTML en la generación de DoR para garantizar la representación precisa de los datos de texto enriquecido enviados mediante API.
* FORMS-21751: Funciones de lienzo: desbordamiento de texto, interfaz de usuario para salto de página.
* FORMS-22049: editor de comunicaciones interactivas, migración a Spectrum 2.
* FORMS-22050: Compatibilidad con la numeración dinámica de páginas en el Editor de comunicaciones interactivas.
* FORMS-21606: las SPI de procesamiento de OSGi públicas para comunicaciones interactivas.
* FORMS-21613: Informes de transacciones y registro de rendimiento para procesar SPI de comunicaciones interactivas.
* GRANITE-62394: tiempo de joda actualizado a 2.12.7.
* GRANITE-36205: actualice la versión de Oak a 1.88.0.
* GRANITE-62020: mejore la directiva de reintentos en `RepositoryServiceHttpClient`.
* GRANITE-62169: actualice commons-lang a 3.19.0.
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
* SITES-35811: utilice un nuevo índice en las consultas de fragmentos de contenido.
* SKYOPS-120857: Actualice filevault a 4.1.4.
* SKYOPS-118390: actualizar el recurso JCR a 3.3.6.
* SKYOPS-121082: actualizar versiones de `org.apache.sling.discovery.standalone`, `org.apache.sling.jcr.packageinit` y `org.apache.sling.commons.fsclassloader` paquetes sling.

### Problemas solucionados {#fixed-issues-23320}

* ASSETS-58926: Corregir la función de miniaturas de cambio de vídeo en DM.
* ASSETS-58623: corrija npe en omnisearch cuando existe la configuración de.
* CQ-4361144: se ha corregido la omisión de fragmentos de contenido de los trabajos de traducción.
* CQ-4355446: se ha corregido la cadena no localizada en el proyecto de traducción que se produce en el cuadro de diálogo Cancelar trabajo de traducción.
* CQ-4360747: corrija un problema en el que los trabajos de traducción repetibles crean cargas útiles e déclencheur vacíos con demasiada frecuencia.
* GRANITE-61318: corrija un problema en el que el asistente para la creación de páginas solo resalta los campos obligatorios en la pestaña básica.
* GRANITE-60514: corrija un problema en el que se detenían las publicaciones programadas durante la ejecución de la canalización de pila completa.
* GRANITE-61019: Corrija el problema con GC en la primera ejecución después del reinicio de AEM.
* GRANITE-60456: Corrija el problema cuando el administrador abre cualquier página de propiedades del usuario.
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

#### Guías de AEM {#guides-23320}

* GUIDES-33597: Si se agrega un elemento `prop` vacío sin atributos ni valores a un archivo DITAVAL, no se pueden agregar `prop` elementos adicionales.
* GUIDES-33693: cuando se vuelve a cargar una imagen editada a través de la interfaz de usuario de Experience Manager Guides, la representación original de la imagen se actualiza, pero el contenido DITA asociado sigue mostrando la versión anterior de la imagen.
* GUIDES-35607: Registros de errores que se generan al cargar un recurso a través de la interfaz de usuario de Assets o al crear un nuevo archivo desde la interfaz del editor; utilice incorrectamente el término `predecessor` en lugar de `successor` en el mensaje de registro.
* GUIDES-37649: al publicar un mapa DITA con línea de base en AEM Sites (con asignación de componentes heredados), los elementos de mapa con el atributo `processing-role = resource-only` también se publican.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).


### Problemas conocidos {#known-issues-23320}

* FORMS-22633: es posible que los envíos de formularios produzcan errores cuando se utilice código personalizado que dependa de las API de GuideBridge (`getData` o `getDataXML`). Si tiene este problema, póngase en contacto con el Soporte técnico de Adobe para obtener ayuda.

### Características y API obsoletas {#deprecated-23320}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-23320}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 31 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-23320}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.88.0 | [API de Oak 1.88.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.88/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.30.2 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
