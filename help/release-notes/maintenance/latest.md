---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 8ee3da55024c0f5246f6c194bc07172b4b71823a
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 53%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 22758 {#22758}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 22758, que se publicó el jueves, 01 de octubre de 2025. La versión de mantenimiento anterior fue la 22450.

La activación de funcionalidades 2025.10.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-22758}

* ASSETS-56227: cambie el nombre del modificador adobe-countdown-timer.
* CNTBF-493: Bump content-backflow bundle version to 2.0.28.
* CQ-4361110: traducciones de Granite.
* CQ-4361112: Últimas traducciones de AEM.
* GRANITE-56026: Mejore los permisos y las respuestas del código de estado de la API.
* GRANITE-61015: se agregó el paquete `org.apache.commons.io.channels` a la lista pública exportada.
* GRANITE-61167: El registro Felix se ha actualizado a la última especificación OSGI.
* GRANITE-61167: Actualice las dependencias felix.
* GRANITE-61169: Mejore la comprobación de cadenas protegidas.
* GRANITE-61622: Actualizar dependencias de Sling.
* GRANITE-61663: Agregue `com.adobe.granite.repository.indexdefs-1.0.2` al inicio rápido.
* GRANITE-61811: Agregue `com.adobe.granite.repository-2.0.0` al inicio rápido.
* SITES-32014: escucha eventos externos para actualizar los registros de servicios.
* SITES-34277: corrección del error de bloqueo en los flujos de trabajo de traducción para páginas.
* SKYOPS-108706: La versión actualizada cambia el paquete a la última versión (almacenamiento en caché de etiquetas).
* SKYOPS-114210: actualizando a la última versión del paquete aem.pss.service.
* SKYOPS-116171: actualizar a Sling ResourceResolver 1.12.12.
* SKYOPS-119811: Lanzamiento de Dispatcher-publish 2.0.258.

### Problemas solucionados {#fixed-issues-22758}

* GRANITE-61875: corrija los déclencheur para la &quot;evaluación de expresiones no válidas&quot;: los autores no pueden guardar los fragmentos de contenido y los recursos no se pueden descargar.
* SITES-22059: Corrija el error de JS en los componentes del visualizador de PDF. Cadena sin localizar &quot;Vista previa de archivos no disponible&quot; en el sitio de componentes principales > Visor de PDF.
* GRANITE-59704: corrija htmllibmanager.debug que provoca que el modo de edición falle.
* GRANITE-61042: Integre FELIX-6796 (corrección de ServiceTracker NPE) en el paquete de la consola web de AEM Felix.
* GRANITE-61165: Workspace.copy() está iniciando RepositoryException.
* GRANITE-61875: Actualice ui.commons a 5.10.50.

### Problemas conocidos {#known-issues-22758}

Ninguna.

### Características y API obsoletas {#deprecated-22758}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-22758}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 13 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-22758}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.86.0 | [API de Oak 1.86.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.30.1 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
