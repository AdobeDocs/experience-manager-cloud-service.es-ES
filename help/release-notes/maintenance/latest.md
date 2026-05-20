---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c8303f6792f36e9d1942cf398909cbf0b3f3f90f
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 30%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## 26125 de versión {#release-26125}

A continuación se resumen las mejoras continuas para la 26125 de la versión de mantenimiento, que se publicó el 20 de mayo de 2026. La versión de mantenimiento anterior era 25892.

La activación de funciones 2026.5.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-26125}

* ASSETS-56957: Se ha agregado compatibilidad con la carga de subtítulos y pistas de audio múltiples para vídeos en Dynamic Media con OpenAPI.
* ASSETS-58563: se ha agregado la integración de Adobe Commerce a los AEM Assets.
* ASSETS-65603: se ha mejorado el rendimiento de la lista de carpetas en la IU táctil al permitir la configuración de un recuento de recursos reducido.
* ASSETS-66032: se ha agregado compatibilidad avanzada con proxy de red a la importación masiva de Assets para entornos con almacenamiento en la nube restringido por IP.
* CQ-4363346: se ha mejorado la interfaz de usuario de las directrices de traducción para que sea compatible con la descarga de directrices de ejemplo, la carga de archivos de directrices en los formatos JSON, PDF y DOCX y la eliminación de directrices existentes.
* GRANITE-67514: aisló un paquete de biblioteca de almacenamiento en caché interno para evitar errores en los trabajos de transformación y conflictos con los paquetes implementados por el cliente.
* SITES-42076: Experimental: Se han agregado operaciones masivas de búsqueda y reemplazo para páginas como primitivas de MCP en la API de contenido.
* SITES-42835: Experimental: Ahora se puede acceder a las páginas de AEM Forms creadas fuera de la API de contenido a través de la API de contenido de AEM Sites sin necesidad de realizar cambios de esquema o migración.
* SITES-44265: se ha agregado un identificador de página replicada estable a la API de contenido que sigue siendo válido después de mover la página, lo que evita errores de referencia obsoleta 404.

### Problemas solucionados {#fixed-issues-26125}

* ASSETS-36208: los perfiles de imagen fijos no aparecen en las propiedades de la carpeta cuando Dynamic Media está deshabilitado.
* ASSETS-63240: se han corregido las operaciones de relación de selección múltiple en bloque en el modo Anexar, lo que dejaba a los usuarios en una página en blanco en lugar de volver a la consola de Assets.
* ASSETS-65076: se ha corregido un valor de protocolo incorrecto que se pasaba a la API de externalizador, lo que provocaba errores al utilizar los generadores de solicitudes de Sling.
* ASSETS-66102: se corrigieron los eventos de publicación de recursos de Adobe I/O Runtime que informaban de un valor `repo:version` incorrecto, lo que provocaba errores en las integraciones descendentes.
* ASSETS-66226: los activos fijos no se eliminan del nivel de entrega tras su eliminación cuando su estado de aprobación se almacena con valores de mayúsculas y minúsculas mixtos.
* ASSETS-66669: se ha corregido el error del botón Inicio de la página de resultados de búsqueda que no navegaba a la pantalla Inicio de la IU táctil cuando Unified Shell estaba habilitado.
* ASSETS-66683: se ha corregido un bucle de aprobación en Dynamic Media con OpenAPI activado por errores de carga, que creaban trabajos pendientes e interrumpían los flujos de trabajo de aprobación de recursos.
* ASSETS-67113: se corrigió la importación masiva que ignora los recursos de SVG al filtrar por tipo MIME `image/svg+xml`.
* CQ-4363466: se han corregido errores de resolución de rutas de configuración de nube que afectaban a los conectores de traducción de terceros que utilizan la resolución de configuración personalizada.
* CQ-4363355: se corrigieron solicitudes de traducción en el conector de traducción GenAI que se enrutaban a un extremo regional incorrecto debido a una URL estática codificada.
* SITES-44186: se ha corregido la inyección de metaetiquetas en la gestión de eventos del Editor de páginas de salto de autor para algunos clientes.

### Problemas conocidos {#known-issues-26125}

Ninguna.

### Características y API obsoletas {#deprecated-26125}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-26125}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 19 vulnerabilidades, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-26125}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 2.0.0 | [API de Oak 2.0.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.0.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.30.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
