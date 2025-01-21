---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: a091dd6b1b69d77f9eeb50065e8946af0133f4f9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 42%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 19149 {#19149}

A continuación se resumen las mejoras continuas de la versión de mantenimiento 19149, que se publicó el miércoles, 21 de enero de 2025. La versión de mantenimiento anterior fue la 18751.

La activación de funcionalidades 2025.1.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-19149}

* ASSETS-45286: mostrar el progreso granular del trabajo asincrónico de archivado de descarga.
* ASSETS-46296: Compatibilidad con plantillas de Dynamic Media en el Selector de recursos.
* ASSETS-44796: Activar eventos de Assets para trabajos de recursos asincrónicos de DAM.

### Problemas solucionados {#fixed-issues-19149}

* GRANITE-55074: Asegúrese de que los encabezados de respuesta CORS estén configurados en respuestas de error.
* ASSETS-43755: Mejoras de escalabilidad relacionadas con recursos en lote.
* ASSETS-45399: redirija a la consola de Assets después de crear una Live Copy de recursos.
* ASSETS-45462: Problemas de almacenamiento en caché del explorador con miniaturas de carpetas personalizadas.
* ASSETS-46398: Ocultar las acciones de descarga y reprocesamiento de plantillas DM.
* ASSETS-44484: Problemas al volver a guardar la configuración de Assets conectado.
* ASSETS-44122: El trabajo de copiar recursos asincrónicos no cambia el nombre de la carpeta de destino al copiar a la carpeta actual.
* ASSETS-44463: el botón Descargar CSV no está visible durante la exportación de metadatos correcta.
* ASSETS-45134: Mover el trabajo con el título de destino anula todos los títulos de carpeta.
* ASSETS-45137: entra en conflicto con las cargas masivas a través de la vista de Assets.
* ASSETS-45758: las relaciones de recursos obtienen una animación infinita de ocupado/carga después de agregar una relación.
* ASSETS AEM-44148: el evento NODE_MOVED en el caso de los archivos de registro puede causar un NPE espurio en los registros.
* ASSETS-28607: Error de JS al configurar la miniatura de vídeo personalizada.
* GRANITE-55781: Mejore la sincronización de grupos entre Adobe Developer Console AEM y los grupos de trabajo de los grupos de trabajo de los. Más detalles en [Cambios en la sincronización de grupos de usuarios y perfiles de productos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization).
* GRANITE-55754: Asegúrese de que los scripts de inicio de SDK admitan Java 21.
* GRANITE-54248: no se puede desplazar por todos los elementos de la carpeta de recursos grandes.
* SCRNS-4597: Mejoras en la vista de listas de resultados de búsqueda.


### Problemas conocidos {#known-issues-19149}

Ninguna.

### Características y API obsoletas {#deprecated-19149}

Cuando se utiliza Adobe Admin Console AEM para la administración de permisos, NO se DEBEN utilizar los siguientes grupos, ya que ya no se sincronizarán con los que se van a realizar las tareas de administración de permisos:
* AEM Grupos que terminan con _GROUP_NAME_SUFFIX.
* Perfiles de producto de otros entornos, programas o productos.

Para obtener más información, compruebe [Cambios en la sincronización de grupos de usuarios y perfiles de productos](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization).


Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-19149}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 4 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-19149}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.72.0 | [API Oak 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html?lang=es) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.27.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
