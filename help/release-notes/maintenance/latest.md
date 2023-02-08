---
title: Últimas notas de la versión de mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Últimas notas de la versión de mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: 76da86d31e2780c2d22419cb8a338cf37963fad8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 5%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las rutas de versiones técnicas para la última versión de mantenimiento de Experience Manager as a Cloud Service.

## Versión 10912 {#release-10912}

A continuación se resumen las mejoras continuas de la versión de mantenimiento 10912, que se publicó el 3 de febrero de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento anterior 9850.

La activación de funciones para esta versión de mantenimiento le proporcionará el conjunto completo de funciones. Consulte la [notas de la versión actual](/help/release-notes/release-notes-cloud/release-notes-current.md) para obtener más información.

### Problemas conocidos {#known-issues}

No actualice si está utilizando CORS. Hemos identificado un problema que afecta a la parte de envío de contenido de GraphQL en esta versión. Un cambio en la configuración predeterminada AEM Dispatcher en torno a cómo se almacenan en caché las consultas persistentes de GraphQL puede interrumpir la entrega de contenido de GraphQL de las consultas persistentes para los clientes que utilizan una configuración CORS.

### Tecnologías integradas {#embedded-tech}

| Tecnología | Versión | Vínculo |
|---|---|---|
| Componentes principales AEM WCM | Versión 2.21.2 | [GitHub](https://github.com/adobe/aem-core-wcm-components) |
