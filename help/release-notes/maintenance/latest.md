---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8a798e1f1b7234f91682b6e5ef7072e024df022
workflow-type: ht
source-wordcount: '693'
ht-degree: 100%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 18751 {#18751}

A continuación se resumen las mejoras continuas de la versión de mantenimiento 18751, que se publicó el jueves, 11 de diciembre de 2024. La versión de mantenimiento anterior fue la 18598.

La activación de funcionalidades 2025.1.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-18751}

* SKYOPS-88509: compatibilidad con Java 21 para el SDK de AEM.

### Problemas solucionados {#fixed-issues-18751}

* ASSETS-42802: el botón Atrás de MFE no siempre funciona y muestra cuadros de diálogo adicionales.
* ASSETS-44148: el evento NODE_MOVED corregido en AEM puede provocar NPE.
* ASSETS-44418: el entorno Correct corregido no está configurado en skyline.
* ASSETS-44821: se ha corregido el filtro de evento de actualización para incluir datos codificados con URL para los eventos de carga.
* CNTBF-298: la copia de contenido corregido falla con conflictos de UUID.
* CNTBF-331: [content-copy-bundle] versión 2.0.14.
* FORMS-16572: eliminar errores de prueba del flujo de trabajo para la compilación de SDK de java 21.
* GRANITE-36205: actualización automatizada para la versión interna de Oak en QS.
* GRANITE-53704: volver a evaluar Sling Discovery en el servicio de repositorio.
* GRANITE-54300: actualización Oak a la última versión pública (1.70.0).
* GRANITE-54416: actualizar Filevault a la versión 3.8.2.
* GRANITE-54462: configurar SubscriberAgents para que utilice hc.tags de &quot;systemready&quot;.
* GRANITE-54542: actualizar la dependencia de commons-io a 2.17.0.
* GRANITE-54658: añadir delayFactor y configuraciones OSGi de tamaño por lotes para fullGC en QS.
* GRANITE-54696: amplia gama de importaciones para la API de Jackrabbit.
* AEM GRANITE-54803: deshabilitar ClusterAtExchange en AEM cuando imsauth esté activo.
* GRANITE-55095: actualización Oak a la última versión pública (1.72.0).
* GUIDES-20006: el estado del documento marcado como Listo vuelve al Borrador antes de guardar una nueva versión, lo que provoca que el estado Listo no persista en ninguna versión del documento.
* GUIDES-21840: en la salida del PDF nativo, faltan títulos de capítulo en la TDC, lo que conduce a una jerarquía incorrecta.
* GUIDES-19558: editar y luego guardar una línea de base en una configuración en la nube agota el tiempo de espera después de 1 minuto si la línea de base tiene un gran número de temas o mapas.
* GUIDES-19733: la traducción de mapas mediante la línea de base se vuelve lenta y, finalmente, no puede cargar la lista de todos los temas asociados y los archivos de mapas.
* SITES-26798: la promoción automática de lanzamiento no actualiza el estado de la promoción (fecha de promoción).
* SITES-27137: eliminar la dependencia de métricas de Sling Commons del núcleo de MSM.
* SKYOPS-75446: el AEM corregido a veces devuelve un valor 404 o páginas a las que les falta contenido.
* SKYOPS-76366: no hay métricas de Jetty Threadpool en el lanzamiento de la versión 15977 y posteriores.
* SKYOPS-82371: java.io.IOException: classFile.delete() ha dado error.
* SKYOPS-83369: las implementaciones de AEM no se inician si la ejecución del trabajo de transformación no genera paquetes.
* SKYOPS-83910: se han encontrado problemas de accesos simultáneos en SKYOPS-82371.
* SKYOPS-84821: establecer la configuración sling.includes.checkcontenttype del servlet principal de Sling en true.
* SKYOPS-85798: el trabajo de transformación corregido genera definiciones de índice vacías.
* SKYOPS-86251: actualizar al núcleo de AEM Analyser 1.5.6 y habilitar el analizador de importación de paquetes de productos en el trabajo de transformación.
* SKYOPS-86710: eliminar los errores de prueba de Minify para la compilación del SDK de java 21.
* SKYOPS-86745: actualizar a Sling ResourceResolver 1.122.
* SKYOPS-89616: se ha corregido No se puede crear una cuenta técnica en Adobe Developer Console.
* SKYOPS-89691: se ha corregido un ID de artefacto incorrecto utilizado para las advertencias de ASM.
* SKYOPS-89699: faltan advertencias para las versiones antiguas de Groovy incrustadas en el sabor &quot;orbinson&quot; de Groovy Console.
* SKYOPS-88664: registrar y proteger contra un caso cuando el archivo de mapa descargado tiene una línea que supera el límite de 1024.
* SKYOPS-89734: lanzamiento de la imagen de Dispatcher 2.0.235.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en Experience Manager Guides, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-18751}

Ninguna.

### Características y API obsoletas {#deprecated-18751}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-18751}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 3 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-18751}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.72.0 | [API Oak 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html?lang=es) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.27.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
