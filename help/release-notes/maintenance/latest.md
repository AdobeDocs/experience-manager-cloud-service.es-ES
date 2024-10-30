---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9278ec9bb5bccd7b40cd65a120f296faba454b9c
workflow-type: ht
source-wordcount: '569'
ht-degree: 100%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 18311 {#18311}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 18311, que se publicó el 22 de octubre de 2024. La versión de mantenimiento anterior fue la 18175.

La activación de funcionalidades 2024.10.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-18311}

* ASSETS-41820: mejoras en la indexación para la vigilancia de procesamiento.
* ASSETS-43720: mejoras funcionales en la vigilancia de procesamiento.
* ASSETS-42554: mejoras de rendimiento para carpetas grandes.
* SKYOPS-77603: gestión de redireccionamientos por parte de usuarios de empresas.

### Problemas solucionados {#fixed-issues-18311}

* ASSETS-37534: cambios en la búsqueda para no exponer la propiedad utilizada para el destinatario de aprobación.
* ASSETS-38322: quitar configuración del proveedor de criterios de publicación Quitar función de evento de publicación.
* ASSETS-40482: problema de accesibilidad en el botón de reproducción/pausa y silencio/reactivación de sonido en el reproductor de vídeo de Scene7.
* ASSETS-40593: la página de error se produce después de hacer clic en el botón “Propiedades” en Recursos > Archivos.
* ASSETS-40598: la sincronización recorta cuando el recurso no sincronizado se mueve a una carpeta con sincronización habilitada.
* ASSETS-40743: problemas al activar el cuadro de diálogo Reemplazar recurso cuando existen ciertos caracteres en el nombre del archivo.
* ASSETS-40825: las facetas de búsqueda de recursos desaparecen después de editar el formulario de búsqueda.
* ASSETS-41007: la eliminación en AEM deja, en ocasiones, recursos huérfanos en la entrega.
* ASSETS-41172: el nombre no admite caracteres especiales de plantillas de Dynamic Media.
* ASSETS-41896: los recursos mencionados en la propiedad cq:discarded de la carpeta NO deben publicarse en Brand Portal.
* ASSETS-42067: plantillas Dynamic Media: la descarga genera un error.
* ASSETS-42070: plantillas de Dynamic Media: los usuarios no administradores deben tener acceso de creación/edición de plantillas.
* ASSETS-42344: se ha conectado la sincronización de recursos desconectada: reconexión y consejos para el cliente.
* ASSETS-42620: problema con la opción de previsualización de las versiones de los recursos: muestra una previsualización en blanco cuando abrimos el recurso.
* ASSETS-42701: problema de recorte y entrega de imágenes optimizadas para la web.
* ASSETS-42966: la barricada asíncrona puede desbloquearse por error si varios trabajos comparten la misma ruta.
* ASSETS-43072: plantillas de Dynamic Media: la plantilla hace referencia a saltos de búsqueda en una referencia no válida.
* ASSETS-43212: problemas de internacionalización en el editor de esquemas de metadatos.
* ASSETS-43202: correcciones en la selección de anotaciones para imprimir desde la cronología.
* ASSETS-43502: el nombre de ajuste preestablecido de imagen existente en AEM CS no se muestra en la página de edición.
* ASSETS-43538: el trabajo de copiar recursos asincrónicos utiliza una propiedad incorrecta para la ruta de origen.
* ASSETS-43798: compruebe primero la ruta de destino antes de copiar los recursos.
* ASSETS-43945: aumenta el retraso de reintentos a 20 minutos para la cola de trabajos de recursos asincrónicos.
* ASSETS-44025: el trabajo de eliminación asíncrona de recursos falla cuando se seleccionan recursos individuales.
* SITES-26128: excepción de conversión de clase en CreateLiveCopyStep.
* SCRNS-4551: [SG Pools] El canal de Screens que contiene el componente de vídeo muestra “Error general de página” en la vista previa del explorador y el reproductor

### Problemas conocidos {#known-issues-18311}

* FORMS-15818: no se ha encontrado la entrada del descriptor de componente `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` en los registros del servidor. Son sentencias del registro inofensivas.

### Características y API obsoletas {#deprecated-18311}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-18311}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 3 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-18311}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.70.0 | [API Oak 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.27.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
