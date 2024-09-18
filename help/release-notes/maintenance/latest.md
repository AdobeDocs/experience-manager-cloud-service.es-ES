---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9323464610b804ff407f5eedf404ab2cca93a8da
workflow-type: ht
source-wordcount: '572'
ht-degree: 100%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 17689 {#release-17689}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 17689, que se publicó el 10 de septiembre de 2024. La versión de mantenimiento anterior fue la 17569.

La activación de funcionalidades 2024.9.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-17689}

* ASSETS-41404: cambios para admitir mejoras de DRM.
* ASSETS-41621: se ha actualizado el trabajo de copia asíncrono de recursos.
* ASSETS-32166: se ha actualizado el trabajo de movimiento asíncrono de recursos.
* ASSETS-41429: compatibilidad con ajustes preestablecidos de imagen en DM OpenAPI.
* ASSETS-38968: mejorar la representación de las referencias de fragmentos de contenido.
* ASSETS-41787, ASSETS-41183: mejoras para el marco de trabajo de operaciones en lote de Assets.
* GRANITE-52917: optimizaciones para mejorar los tiempos de instalación del paquete de copia de contenido.
* SCRNS-3980: detectar la pantalla gris en reproductores que tienen subsecuencias sin recursos programados.

### Problemas solucionados {#fixed-issues-17689}

* ASSETS-40875: NPE falso registrado por AssetDeleteHandler.
* ASSETS-42422: evitar activar un trabajo asíncrono para un solo movimiento de recurso.
* ASSETS-41234: Shell unificado: la navegación global podría no funcionar si se abre cuando la barra de búsqueda está abierta.
* ASSETS-42256: Shell unificado: etiqueta/insignia que indica que el entorno solo funciona de forma intermitente.
* ASSETS-41271: impedir tener que volver a publicar innecesariamente los recursos durante las operaciones de movimiento.
* ASSETS-38894: limitar los reintentos mediante guardián de procesamiento.
* ASSETS-40815: utilizar la representación de vista previa de PDF para mostrar el archivo PPT en la interfaz de usuario de vínculo compartido.
* ASSETS-37123: no se puede cargar la vista previa de recursos en el cuadro de diálogo Vínculo compartido.
* CQ-4358156: actualizar los vínculos Atrás de la etiqueta que se está eliminando.
* SCRNS-4495: se ha corregido el botón Pegar que no funcionaba correctamente para diferentes grupos de usuarios.
* SCRNS-4512: quitar componentes relacionados con el dispositivo de las pantallas de AEMaaCS.
* SCRNS-4466: en el panel de control de canal, ocultar: ver manifiesto, generar contenido sin conexión, actualizar manifiesto de caché, mostrar panel.
* SCRNS-4513: añadir encabezados de columna para la página de resultados de búsqueda en la vista de lista.

### Problemas conocidos {#known-issues-17689}

* FORMS-14340: error al crear una instancia de FormsAndDocumentOmniSearchHandler y CloudStorageSubmitActionInserter. Son sentencias del registro inofensivas.
* FORMS-15818: la entrada del descriptor de componente “OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml” no se ha encontrado en los registros del servidor. Son sentencias del registro inofensivas.
* SITES-23662: el usuario que activa una publicación no se puede extraer de las sentencias del registro JCR en los registros del servidor. Se trata de una función en desarrollo que podría provocar errores intermitentes e inofensivos de tipo “No se puede encontrar un ID de usuario válido en el lote de eventos OSGI” en el registro.

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
