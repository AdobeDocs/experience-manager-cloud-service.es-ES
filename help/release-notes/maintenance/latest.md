---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a876efeed0e078fa0f8f8718484bd3f069a71cb5
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 40%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## 26773 de versión {#release-26773}

A continuación se resumen las mejoras continuas para la 26773 de la versión de mantenimiento, que se publicó el 17 de junio de 2026. La versión de mantenimiento anterior era 26353.

La activación de funciones 2026.6.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

>[!NOTE]
>
>La 26635 de la versión se ha convertido en privada.

### Mejoras {#enhancements-26773}

* GRANITE-67251: Presentó `cqSiteSearch`, un nuevo índice predeterminado definido sobre el tipo de mezcla `cq:Searchable`. Esto permite un control preciso sobre qué contenido va al índice del sitio y proporciona búsquedas completas en sitios web de AEM, incluida la búsqueda semántica.
* GRANITE-68099: Se ha actualizado Apache Jackrabbit Oak incrustado a la última versión pública (2.2.0).
* SKYOPS-135241: introduzca el prefijo aem para filtros de granja inmutables a fin de evitar conflictos de nomenclatura con configuraciones definidas por el cliente.

### Problemas corregidos {#fixed-issues-26773}

Ninguna.

#### Guías de AEM {#guides-26773}

* GUIDES-46275: las dimensiones de imagen especificadas con unidades como `mm` no se representan correctamente, lo que hace que las imágenes se muestren en su tamaño original en lugar de las dimensiones especificadas.
* GUIDES-45800: copiar y pegar `<keywords>` dentro de `<topicmeta>` dentro de un `<keydef>` o `<topicref>` hace que las palabras clave se inserten dentro de etiquetas externas no deseadas.
* GUIDES-45409: Cuando un mapa contiene un(a) `topicref` externo que señala a un recurso no DITA (como `.html`), su vista previa no se muestra en la interfaz de usuario de Assets.
* GUIDES-45254: Al trabajar con archivos de `.plt` y `.css` en plantillas de PDF, la opción **Generate IDs** está disponible en el menú contextual que se muestra al hacer clic con el botón derecho, a pesar de que no es aplicable a estos tipos de archivo.
* GUIDES-45508: La aplicación de una línea de base a un mapa con muchos recursos retrasa la carga del informe de traducción para el idioma seleccionado, a veces conduce al tiempo de espera de la solicitud antes de que se procese el informe.
* GUIDES-45511: falta la información sobre herramientas del icono **Historial de versiones** en el panel izquierdo de la interfaz de usuario de revisión junto al nombre del tema.
* GUIDES-44942: Al añadir preguntas a una prueba utilizando la opción Insertar del banco de preguntas, las preguntas de respuesta corta no aparecen a pesar de tener un ID de pregunta válido.

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-26773}

Ninguna.

### Características y API obsoletas {#deprecated-26773}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-26773}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 10 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-26773}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 2.2.0 | [API de Oak 2.2.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.2.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.67 | [Apache Httpd 2.4.67](https://apache.googlesource.com/httpd/+/refs/tags/2.4.67/CHANGES) |
| Dispatcher | 2.0.274 |  |
| Componentes principales de AEM | 2.31.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
| Java 21 | 21.0.11 | [JDK 21.0.11](https://www.oracle.com/java/technologies/javase/21-0-11-relnotes.html) |
