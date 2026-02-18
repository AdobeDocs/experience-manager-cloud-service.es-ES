---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a58225edb8ca49db9743db6c9c5b08c786fa0144
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 27%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 24464 {#release-24464}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 24464, que se publicó el miércoles, 17 de febrero de 2026. La versión de mantenimiento anterior fue la 24288.

La activación de funciones 2026.2.0 proporciona el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-24464}

* AEMARCH-264: Agregar compatibilidad para validar solicitudes condicionales basadas en RequestEntity.
* AEMARCH-269: Exponer las API de validación de JavaEE para implementaciones de OpenAPI.
* AEMARCH-276: proporcionar compatibilidad con i18n a través de RequestEntity.
* ASSETS-10995: establezca un límite en la cantidad de recursos en el zip de descarga.
* ASSETS-50788: Actualice la API de búsqueda para utilizar la API de GET de metadatos del recurso.
* ASSETS-50946: asigne el cuerpo de la solicitud mediante la API de GET de metadatos a los metadatos JCR.
* ASSETS-55866: evite enviar una nueva solicitud para el mismo recurso hasta que se complete el procesamiento anterior.
* ASSETS-60300: proporcione una API para recuperar el contexto y el resultado asincrónicos del trabajo.
* ASSETS-60574: Añada compatibilidad con la última versión del paquete de API de Sling.
* ASSETS-61049: Continuar con el desarrollo del paquete del administrador de metadatos.
* ASSETS-61692: realice una búsqueda semántica de forma predeterminada en Buscar en la API abierta.
* ASSETS-61696: ruta BAM y contenedor MFE en la vista de recursos.
* ASSETS-61854: enviar la solución GenStudio en el mensaje de activación/desactivación.
* ASSETS-61973: Cree una API en AEM para administrar las peticiones de datos.
* ASSETS-62182: controlador de eventos de Asset Compute para la representación de manifiesto c2pa.
* ASSETS-62311: Problemas de regresión de búsqueda.
* ASSETS-62413: Agregue compatibilidad para el campo customModifier en cada capa del JSON.
* ASSETS-62432: Combinar carpetas para eliminar API PR.
* ASSETS-62540: aumente la versión optimizada para dispositivos táctiles en el inicio rápido.
* ASSETS-62622: Controlar el modo de búsqueda en MatchQuery.
* ASSETS-62671: Corregir el operador MatchQuery startsWith.
* ASSETS-62780: Agregar opción de característica para la API de carpeta.
* ASSETS-62988: oculta la representación de manifiesto c2pa para que no se muestre en la pestaña representaciones.
* ASSETS-63336: La sincronización de plantillas de AEM a DM solo debe producirse para metadatos con espacio de nombres DAM.
* ASSETS-63375: ponga las API abiertas experimentales de carga de recursos detrás de la alternancia de funciones.
* ASSETS-63453: Asegúrese de que todos los usuarios puedan leer la configuración de omnisearch.
* GRANITE-63744: permite conectar trabajos asincrónicos a trabajos de sling.
* GRANITE-64567: deshabilitar automáticamente la búsqueda semántica para búsquedas de SKU.
* GUIDES-41187: Añada encabezados para el uso de las guías.
* SITES-30452: API de contenido con ASO: sugerencias de título y descripción.
* SITES-33116: Corrija la validación de la ruta.
* SITES-34234: Editor de páginas: conservar el estado del árbol de contenido.

### Problemas solucionados {#fixed-issues-24464}

* ASSETS-43198: los correos electrónicos de notificación de caducidad de los recursos no respetan la preferencia de idioma del usuario.
* ASSETS-51840: mejoras en el procesamiento de recursos.
* ASSETS-52061: No se puede volver atrás después de seleccionar la búsqueda guardada.
* ASSETS-53155: mejoras en el contenido de los recursos.
* ASSETS-53745: El flujo de descarga de Dynamic Media requiere anular la selección del recurso original antes de elegir el ajuste preestablecido web.
* ASSETS-54260: correcciones de contenido de recursos.
* ASSETS-54787: mejoras en el contenido de los recursos.
* ASSETS-57391: actualizaciones de contenido de recursos.
* ASSETS-59213: cq-dynamicmedia-core depende de la biblioteca obsoleta de commons-lang.
* ASSETS-59214: cq-scene7-imaging depende de la biblioteca obsoleta de commons-lang.
* ASSETS-59546: cq-remotedam-client-core depende de la biblioteca obsoleta de commons-lang.
* ASSETS-59703: cq-dam-core depende de la biblioteca obsoleta de commons-lang.
* ASSETS-59705: cq-dam-handler depende de la biblioteca obsoleta de commons-lang.
* ASSETS-59707: cq-dam-indesign depende de la biblioteca obsoleta de commons-lang.
* ASSETS-59709: cq-scene7-core depende de la biblioteca obsoleta de commons-lang.
* ASSETS-59929: el CSV de la exportación de metadatos se interrumpe cuando el campo tiene un carácter de nueva línea.
* ASSETS-60241: El trabajo de movimiento asincrónico falla al cambiar el nombre de la carpeta.
* ASSETS-61134: elimine las etiquetas comparisonVersion de los archivos pom.
* ASSETS-61309: La operación de mover o copiar fragmentos de contenido ya no actualiza las referencias internas.
* ASSETS-61730: La redirección al acceso binario directo debe respetar la codificación de los recursos.
* ASSETS-62358: el CSV del informe de Assets muestra valores dañados en la ruta de contenido.
* ASSETS-62610: botón de licencia de Adobe Stock deshabilitado en la interfaz de usuario de Assets.
* ASSETS-62613: NPE en `downloadasset`/`saveas`.
* ASSETS-62656: el indicador de Búsqueda por IA Omnisearch se muestra incorrectamente para las búsquedas que no son de Assets.
* GRANITE-55387: Corregir la palabra entre comillas elimina toda la palabra.
* GRANITE-61240: RCE a través de XSS almacenado en lazycontainer.js.
* GRANITE-64101: Los índices OOTB convertidos a ES volvieron a Lucene al reiniciar.
* SITES-24530: el destinatario táctil de los botones de cerrar/quitar en el modo de búsqueda no es lo suficientemente grande.
* SITES-31425: mensaje de error no localizado en el flujo de trabajo de inicio.

### Problemas conocidos {#known-issues-24464}

Ninguna.

### Características y API obsoletas {#deprecated-24464}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-24464}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 14 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-24464}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.90.0 | [API de Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.30.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

