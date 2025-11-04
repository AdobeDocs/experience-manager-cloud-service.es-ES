---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 89597ae0c54b1b2f42f597f556276700545ecd26
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 45%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

>[!NOTE]
>
>La 23122 de la versión se hizo privada el 3 de noviembre.

## Versión 22943 {#22943}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 22943, que se publicó el miércoles, 14 de octubre de 2025. La versión de mantenimiento anterior fue la 22758.

La activación de funciones 2025.10.0 proporciona el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-22943}

* ASSETS-57809: Actualización de la definición del índice para damAssetLucene-13.
* ASSETS-36521: Flujo de trabajo de recarga de DM mejorado para garantizar un procesamiento posterior coherente.
* ASSETS-56400: se ha añadido una nueva representación de OOTB Zoom PNG para los recursos con transparencia.
* ASSETS-55326: se habilitó la vista de configuración de carpeta de metadatos de IA mediante eventos HTTP.
* ASSETS-56905: admite la conexión a Indesign mediante proxy.
* ASSETS-48286: Agregue propiedades de CAI a Algolia para GenStudio.
* ASSETS-48653: aplique la marca de agua invisible en la fase de preprocesamiento.
* ASSETS-55874: Migrando ajustes preestablecidos de imagen de scene7 a DMWithOpenapi.
* SITES-30452: mejoras en la API de contenido para ASO en el extremo /content/definition.

### Problemas solucionados {#fixed-issues-22943}

* ASSETS-56301: se ha corregido la exportación selectiva de metadatos para incluir PredictedTags en el CSV.
* ASSETS-55543: Se ha refactorizado la lógica de procesamiento asincrónico en un paquete reutilizable.
* ASSETS-54789: se corrigió NPE en ACLPermissionsValidator cuando DM ACL está habilitado.
* ASSETS-55888: la representación de malware fija aparece en el panel Representaciones de la interfaz de usuario.
* GRANITE-62236: se ha corregido un problema de localización de palabras clave en las búsquedas guardadas de colecciones inteligentes.
* GRANITE-61875: se ha corregido un problema con la revisión &quot;evaluación de expresiones no válidas&quot; que impedía guardar fragmentos de contenido y descargas de recursos.
* SITES-24074: se ha corregido la navegación móvil oculta que recibe el enfoque durante la navegación mediante el teclado.
* SITES-33611: se ha corregido un problema con la información general de Live Copy para mercados de gran volumen.

#### Guías de AEM {#guides-22943}

* GUIDES-31421: cuando hay varios temas o mapas DITA abiertos y uno de los temas está cerrado, el botón **>** que muestra todas las pestañas abiertas se superpone con las pestañas abiertas restantes de la barra de pestañas.
* GUIDES-33229: Al generar PDF, las reglas de filtrado en un archivo DITAVAL se ignoran si algún nombre de propiedad contiene un punto.
* GUIDES-33720: al ampliar y reducir la pantalla de la interfaz de usuario de traducción, el botón Enviar para traducción se mueve bajo los puntos suspensivos y se activa incluso sin haber seleccionado ningún recurso.
* GUÍAS-33590: cuando un revisor completa una tarea de revisión o el iniciador actualiza la tarea de revisión sin introducir comentarios, el correo electrónico de notificación enviado muestra el comentario anterior más reciente.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Características y API obsoletas {#deprecated-22943}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-22943}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 14 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Aviso de cambio

* Esta versión incluye las siguientes versiones nuevas del índice de productos:
* **damAssetLucene-13**

### Tecnologías integradas {#embedded-tech-22943}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.86.0 | [API de Oak 1.86.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.86/index.html?lang=es) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.30.2 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
