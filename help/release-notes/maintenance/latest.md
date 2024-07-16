---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 573de431328650778b3ef0979a24190477382310
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 47%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 17098 {#release-17098}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 17098, que se publicó el miércoles, 16 de julio de 2024. La versión de mantenimiento anterior fue la 16971.

La activación de funciones 2024.7.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-17098}

- SKYOPS-79817: Habilitar la tarea del analizador de funciones de Sling para las asignaciones de usuarios de servicio

### Problemas solucionados {#fixed-issues-17098}

- ASSETS-39665: la sincronización de recortes inteligentes no funciona después de migrar de 6.5 a AEM CS
- FORMS-14993: la API de Forms devuelve 500 para el material colateral que funcionaba anteriormente
- GRANITE-52120: CRXDE devuelve 500 al mostrar datos de control de acceso
- GRANITE-52573: Solicitudes que devuelven 400 cuando se utiliza // en direcciones URL reescritas
- GRANITE-52746: Todos los tipos de nodo no cargados en el cuadro de diálogo Crear nodo
- GRANITE-52777: Manejo de 404s roto cuando se ajusta la solicitud
- GRANITE-52871: Asegúrese de que publish-worker se sincronice con golden-publish y se complete antes de la compactación
- SKYOPS-79173: El replicador no se replica en varios agentes que coinciden con un AgentIdFilter determinado
- SKYOPS-80075: Problemas con los valores predeterminados en los nombres de los recursos que causan el bloqueo de las colas de publicación (Mac)
- SKYOPS-81032: Filtre los registros generados por las solicitudes para obtener registros al utilizar el registro mejorado

### Problemas conocidos {#known-issues-17098}

Ninguno

### Aviso de cambio {#change-notice-17098}

- A partir de septiembre de 2024, AEM as a Cloud Service deshabilitará la serialización de los solucionadores de recursos a través del marco de trabajo Exportador de modelos Sling. Consulte la [documentación](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obtener más información.

### Características y API obsoletas {#deprecated-17098}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Tecnologías integradas {#embedded-tech-17098}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.66.0 | [API Oak 1.66.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.66.0/index.html) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.25.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
