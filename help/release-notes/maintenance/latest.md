---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9323464610b804ff407f5eedf404ab2cca93a8da
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 50%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 17689 {#release-17689}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 17689, que se publicó el miércoles, 10 de septiembre de 2024. La versión de mantenimiento anterior fue la 17569.

La activación de funcionalidades 2024.9.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-17689}

* ASSETS-41404: Cambios para admitir mejoras de DRM.
* ASSETS-41621: Trabajo de copia asincrónica de recursos actualizado.
* ASSETS-32166: Trabajo de movimiento asincrónico de recursos actualizado.
* ASSETS-41429: Compatibilidad con ajustes preestablecidos de imagen en DM OpenAPI.
* ASSETS-38968: Mejore la representación de las referencias de fragmentos de contenido.
* ASSETS-41787, ASSETS-41183: Mejoras para el marco de trabajo de operaciones en lote de Assets.
* GRANITE-52917: Optimizaciones para mejorar los tiempos de instalación del paquete de copia de contenido.
* SCRNS-3980: Detecta la pantalla gris en reproductores que tienen subsecuencias sin recursos programados.

### Problemas solucionados {#fixed-issues-17689}

* ASSETS-40875: NPE falso registrado por AssetDeleteHandler.
* ASSETS-42422: evite activar un trabajo asincrónico en un solo movimiento de recurso.
* ASSETS-41234: Unified Shell: la navegación global podría no funcionar si se abre cuando se abre la barra de búsqueda.
* ASSETS-42256: Unified Shell: etiqueta/distintivo que indica que el entorno solo funciona de forma intermitente.
* ASSETS-41271: Impida la republicación innecesaria de Assets durante las operaciones de movimiento.
* ASSETS-38894: limitar reintentos procesando watchdog.
* ASSETS-40815: utilice la representación del PDF de vista previa para mostrar el archivo PPT en la interfaz de usuario de Link Share
* ASSETS-37123: No se puede cargar la previsualización de recursos en el cuadro de diálogo Compartir vínculos.
* CQ-4358156: actualizar los backlinks de la etiqueta que se está eliminando.
* SCRNS-4495: el botón Pegar corregido no funciona correctamente para diferentes grupos de usuarios.
* SCRNS-4512: elimine componentes relacionados con el dispositivo de las pantallas de AEMaaCS.
* SCRNS-4466: en el panel del canal, ocultar: ver manifiesto, generar contenido sin conexión, actualizar caché de manifiesto, mostrar panel.
* SCRNS-4513: Agregar encabezados de columna para la página de resultados de búsqueda en la vista de lista.

### Problemas conocidos {#known-issues-17689}

* FORMS-14340: Error al crear una instancia de FormsAndDocumentOmniSearchHandler y CloudStorageSubmitActionInserter. Son instrucciones de registro inofensivas.
* FORMS-15818: entrada de descriptor de componente &quot;OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml&quot; no se encontró en los registros del servidor. Son instrucciones de registro inofensivas.
* SITES-23662: el usuario que almacena en déclencheur una publicación no se puede extraer de las sentencias de registro JCR en los registros del servidor. Se trata de una función en desarrollo que podría provocar errores intermitentes e inofensivos &quot;No se puede encontrar un ID de usuario válido en el lote de eventos OSGI&quot; en el registro.

### Aviso de cambio {#change-notice-17689}

* A partir de septiembre de 2024, AEM as a Cloud Service deshabilitará la serialización de los solucionadores de recursos a través del marco de trabajo Exportador de modelos Sling. Consulte la [documentación](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obtener más información.

### Características y API obsoletas {#deprecated-17689}

Tenga en cuenta que estamos en proceso de actualizar `com.day.cq.wcm.api` y con la versión actual, hemos marcado como `@Deprecated` algunos de sus métodos y clases. Estos se eliminarán en futuras versiones, por lo que considere la posibilidad de cambiar a las alternativas sugeridas si utiliza alguna de ellas.

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-17689}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 4 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-17689}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.68.0 | [API Oak 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.26.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
