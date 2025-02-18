---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 1d6a54f87d55179c11c7ccc7766eeeb475674f05
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 49%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 19567 {#19567}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 19567, que se publicó el miércoles, 18 de febrero de 2025. La versión de mantenimiento anterior fue la 19352.

La activación de funcionalidades 2025.2.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-19567}

* GRANITE-56650: La distribución de contenido solo debe indicar la cola bloqueada después de unos pocos reintentos
* SKYOPS-89616: permite crear hasta 40 cuentas técnicas en Adobe Developer Console

### Problemas solucionados {#fixed-issues-19567}

* CNTBF-232: paquete profundo nt:nodos de archivo para incluir el elemento secundario jcr:content obligatorio
* CQ-4358930: Problema de rendimiento durante la carga de propiedades de página con muchos campos múltiples
* GRANITE-55960: Problema de rendimiento con el campo Coral Select en AEM as Cloud Service
* GRANITE-56197: El nuevo paso del flujo de trabajo TreeActivation no agrupa recursos en una estructura de carpetas plana grande

#### Guías de AEM {#guides}

* GUIDES-23526: Al actualizar las condiciones desde el perfil de carpeta, todos los grupos de condiciones se pierden y las condiciones se acoplan.
* GUIDES-22574: Si un vínculo externo contiene un UUID, se inicia el procesamiento posterior y convierte el vínculo externo en un vínculo UUID, lo que rompe el vínculo en el editor y también en los sitios de publicación.
* GUIDES-24983: al copiar una imagen de cualquier producto externo (por ejemplo, MS PowerPoint) y pegarla en Guides, la funcionalidad para cargar el recurso sobre la marcha para utilizarlo en los saltos de archivo.
* GUIDES-21772: Error en la generación nativa de PDF para el contenido con **atributo de fragmento** establecido en **para el contenido**.
* GUIDES-23964: al elegir **Editar propiedades**, el cuadro de diálogo de línea de base no muestra los criterios guardados anteriormente para la línea de base dinámica.
* GUIDES-19067: Al duplicar cualquier perfil de carpeta, su lista de usuarios administradores también se copia del perfil de carpeta original

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-19567}

Ninguna.

### Características y API obsoletas {#deprecated-19567}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-19567}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 21 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-19567}

| Tecnología | Versión | Vínculo |
|---|--------------|-------------------------------------------------------------------------------------------------------------------|
| AEM Oak | 1.76.0 | [API Oak 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.27.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
