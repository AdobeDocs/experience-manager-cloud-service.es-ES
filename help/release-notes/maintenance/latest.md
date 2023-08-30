---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 22ed74b307b9eb4c6c2f72ac2a34e2ab6d30a85c
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 45%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 13239 {#release-13239}

A continuación se resumen las mejoras continuas para la 13239 de la versión de mantenimiento, que se publicó el 29 de agosto de 2023. Esta versión de mantenimiento sustituye a las 13206 de la versión.

La activación de funciones 2023.9.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-13239}

- GRANITE-46784: Agregar opción para deshabilitar BearerAuthenticationHandler
- GRANITE-36205: Actualice la versión interna de la versión de Oak a la más reciente
- GRANITE-47059: Eliminar paquete SSL de Granite Jetty
- ASSETS-26713: vínculo externo de la interfaz de usuario táctil al nuevo panel de la interfaz de usuario de la experiencia. Integración con el shell unificado y actualización con la interfaz táctil optimizada
- SKYOPS-63302: actualizar com.adobe.granite:com.adobe.granite.auth.saml a la versión 1.0.54
- GRANITE-46634: actualizar al cliente de eventos 1.4.0
- GRANITE-46788: Actualizar bibliotecas de Apache Commons
- GRANITE-29211: Actualización de las herramientas a Sling Feature Model 2.0
- GRANITE-46705: Actualización a Apache Felix Http Jetty 4.1.14
- GRANITE-46631: actualizar la versión de Jackrabbit a 2.20.11
- SKYOPS-61895: Actualización a Jackrabbit Filevault 3.7.0

### Problemas corregidos {#fixed-issues-13239}

- SKYOPS-63290: Se ha corregido la evolución incorrecta de los contenedores
- SKYOPS-54607: El cálculo de la carga del servidor de Ratelimiter no es correcto para la solicitud que ha fallado
- ASSETS-27648: ContentModelIT no puede leer archivos de exclusión de otros paquetes
- GRANITE-43744: Sling Authenticator no funciona correctamente si hay una configuración incorrecta con el requisito de autenticación y la ruta de vanidad
- AEM GRANITE-46419: Problema de integración de con Auth0 Idp
- AEM GRANITE-46292: La configuración de Okta SAML no funciona después de la actualización de la nube de

### Problemas conocidos {#known-issues-13239}

Ninguna.

### Tecnologías integradas {#embedded-tech-13239}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,54-T20230817132355-3800a65 | [API Oak 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.2 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
