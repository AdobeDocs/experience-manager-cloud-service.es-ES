---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e1fa4b3bcb04ab3e834b34f507f1350fb536b513
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 52%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 21005 {#21005}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 21005, que se publicó el miércoles, 27 de mayo de 2025. La versión de mantenimiento anterior fue la 20626.

La activación de funcionalidades 2025.5.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-21005}

* GRANITE-58927: mejoras en la opción de búsqueda semántica.
* GRANITE-58800: Actualización de las colecciones Apache Commons a la versión 4.5.0.
* GRANITE-58866: Actualización de Oak a 1.80.0.
* SKYOPS-106509: Compatibilidad GSON mejorada mediante el acceso reflexivo en Java 21.
* SKYOPS-107761: Actualización de los modelos Sling de Jackson Exportador a 1.1.6.
* SKYOPS-107813: actualizar a Sling ResourceResolver 1.12.8.

### Problemas solucionados {#fixed-issues-21005}

* CNTBF-443: propiedad SearchSlingJob `EVENT_JOB_TOPIC` fija.
* GRANITE-57853: Se han corregido problemas de alineación desplegable en la IU de.
* GRANITE-58107: se corrigieron errores 404 en la publicación al deshabilitar la afinidad de pod basada en el usuario en el controlador OAuth.
* GRANITE-58276, SLING-12755: Se han corregido ciclos de dependencia OSGi que podían impedir que la fábrica del motor de scripts HTL se iniciara correctamente, lo que provocaba errores de procesamiento intermitentes en el lado del servidor.
* SKYOPS-105151: Se corrigió NPE al acceder a la lista de paquetes.
* SKYOPS-83910, SKYOPS-82371: se corrigieron problemas de concurrencia de compilación de JSP.

#### Guías de AEM {#guides}

* GUIDES-26919 : Al abrir un mapa DITA con el shell unificado habilitado, el editor se actualiza de forma intermitente.
* GUIDES-26282: Si no se cierran las conexiones de sesión JCR al actualizar o crear temas, se producen pérdidas de memoria y tiempo de inactividad del servicio.
* GUIDES-26434: La publicación nativa de PDF continúa indefinidamente, si el contenido DITA tiene un vínculo web sin tener el ámbito como `external`.
* GUIDES-26516: La publicación de PDF nativos y sitios de AEM se detiene y se pone en cola cuando hay errores en el contenido.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-21005}

Ninguna.

### Características y API obsoletas {#deprecated-21005}

* GRANITE-54164: se eliminó `org.apache.jackrabbit.oak.plugins.blob` de la API pública.
* GRANITE-54280: se eliminó `org.apache.jackrabbit.oak.cache` de la API pública.
* GRANITE-58332: `org.apache.jackrabbit.oak.plugins.memory` obsoleto en la API pública.
* La funcionalidad [Automatización de la instalación de Experience Cloud](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md) ha quedado obsoleta.

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-21005}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 5 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Aviso de cambio {#change-notice-21005}

* Esta versión incluye las siguientes versiones nuevas del índice de productos:
   * **damAssetLucene-12**

Las versiones personalizadas de las versiones de índice anteriores se combinarán automáticamente con la nueva versión del índice de productos. Aplique otras actualizaciones personalizadas a la versión combinada.

#### Actualizar aem-cloud-testing-customers {#update-aem-cloud-testing-clients-21005}

Los próximos cambios requerirán que la biblioteca [aem-cloud-testing-customers](https://github.com/adobe/aem-testing-clients) que se use en las pruebas funcionales personalizadas se actualice al menos a la versión **1.2.1** (Recomendado: última versión 1.2.9)

Asegúrate de que la dependencia en `it.tests/pom.xml` se ha actualizado.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.9</version>
</dependency>
```

Este cambio debe realizarse antes del 15 de junio de 2025.
Si no se actualiza la biblioteca de dependencias, se producirán errores de canalización en el paso &quot;Pruebas funcionales personalizadas&quot;.

### Tecnologías integradas {#embedded-tech-21005}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
