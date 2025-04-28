---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: c5152543550b5f81bf0b79741f288b0c16648584
workflow-type: ht
source-wordcount: '452'
ht-degree: 100%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 20476 {#20476}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 20476, que se publicó el miércoles, 15 de abril de 2025. La versión de mantenimiento anterior fue la 20133.

La activación de funcionalidades 2025.4.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-20476}

* CNTBF-411: añadir la posibilidad de eliminar el trabajo sling en caso de que JCR lo elimine.
* CQ-4359813: kit de traducción de AEM: 20 de marzo.
* CQ-4359811: kit de traducción de Granite: 20 de marzo.
* GRANITE-57863: actualizar Filevault a la versión 3.8.4.
* GRANITE-56154: configurar reintentos exponenciales en oak-segment-azure.
* GRANITE-55999: mejora del rendimiento de UserPropertiesService.
* GRANITE-55781: evitar la reconfiguración redundante de la pertenencia de los usuarios.
* GRANITE-53956: actualizar Azure SDK V8 a V12 para oak-segment-azure.
* GRANITE-50654: en la pestaña de permisos principales, quitar la carga &quot;todos&quot; de forma predeterminada en el front-end.
* SKYOPS-103444: actualizar a Sling ResourceResolver 1.12.6.
* SKYOPS-101147: actualización de la impl. de caconfig.
* SKYOPS-97124: añadir advertencias del analizador para las versiones obsoletas del paquete SPIFly.
* SKYOPS-95826: actualizar las versiones de Java en tiempo de ejecución a 11.0.26 y 21.0.6.
* SKYOPS-53671: utilizar artefactos instalados por el cliente de modelos de funciones en reinicios de AEM (RDE).

### Problemas solucionados {#fixed-issues-20476}

* ASSETS-49027: [Regresión] AemRequestEventFilter interrumpe las solicitudes POST a la consola web de OSGI.
* ASSETS-44956: no se puede seleccionar ninguna representación de Dynamic Media. Las etiquetas de script deben cargarse en el componente de nivel superior.
* CNTBF-410: puntero nulo CheckJob getId en el paquete ContentCopy.
* CNTBF-341: índice de exportación de ContentCopy fuera de los límites.
* CQ-4355411: la información sobre herramientas permanece en la pantalla del cuadro de diálogo &quot;Preferencias de usuario&quot;.
* GRANITE-57265: los valores de la selección desplegable no se seleccionan.
* GRANITE-57067: faltan directivas eficaces en la interfaz de usuario.
* SITES-30727: es posible que se produzca un error al arrastrar y soltar subcomponentes dentro del editor de AEM.
* SKYOPS-90607: los trabajos de Sling se ejecutan en una implementación inactiva/contenido mutable.
* SKYOPS-95722: eliminar el tamaño `MaxPermSize` de las etiquetas de inicio rápido en AEM-SDK.
* SKYOPS-103569: determinadas imágenes no se pueden cargar con Java 21: `javax.imageio.IIOException: Cannot create Sun JPEGImageReader backend`.

### Problemas conocidos {#known-issues-20476}

Ninguna.

### Características y API obsoletas {#deprecated-20476}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-20476}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 5 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-20476}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.78.0 | [API Oak 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html?lang=es) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.28.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
