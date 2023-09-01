---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 370d5742065d659f32ec1ff4d4b0fc0a153f71c2
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 40%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 13323 {#release-13323}

A continuación se resumen las mejoras continuas para la 13323 de la versión de mantenimiento, que se publicó el 1 de septiembre de 2023. Esta versión de mantenimiento sustituye a las 13239 de la versión.

La activación de funciones 2023.9.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-13323}

- GRANITE-46784: Agregue la opción para deshabilitar BearerAuthenticationHandler.
- GRANITE-36205: Actualice la versión interna de la versión de Oak a la más reciente.
- ASSETS-26713: vínculo externo de la interfaz de usuario táctil al nuevo panel de la interfaz de usuario de la experiencia. Integración de shell unificado y UI táctil optimizada actualizada.
- SKYOPS-63302: actualizar com.adobe.granite:com.adobe.granite.auth.saml a la versión 1.0.54.
- GRANITE-46634: actualizar al cliente de eventos 1.4.0.
- GRANITE-46788: Actualizar bibliotecas a Apache Commons IO 2.13.0, Commons Lang 3.13.0, Commons Code 1.16.0 y Commons Compress 1.23.0.
- GRANITE-46705: Actualización a Apache Felix Http Jetty 4.1.14.
- GRANITE-46631: Actualice la versión de Jackrabbit a 2.20.11.
- SKYOPS-61895: Actualización a Jackrabbit Filevault 3.7.0.

### Problemas corregidos {#fixed-issues-13323}

- ASSETS-28461: el visualizador de nube de documentos no funciona para los PDF, corregido desde 13239.
- SKYOPS-63290: Se ha corregido una evolución incorrecta de los contenedores.
- SKYOPS-54607: El cálculo de la carga del servidor de Ratelimiter no es correcto para las solicitudes con errores.
- ASSETS-27648: ContentModelIT no puede leer archivos de exclusión de otros paquetes.
- GRANITE-43744: Sling Authenticator no funciona correctamente si hay una configuración incorrecta con el requisito de autenticación y la ruta de vanidad.
- AEM GRANITE-46419: Problema de integración de con Auth0 Idp.
- AEM GRANITE-46292: La configuración de Okta SAML no funciona después de actualizar el servicio de nube de.
- GRANITE-47059: Eliminar el paquete SSL Granite Jetty.

### Problemas conocidos {#known-issues-13323}

- SITES-15622: GraphQL: problema con consultas persistentes con número y parámetros booleanos.
- SITES-15654: GraphQL: problemas con uniones y propiedades del mismo nombre.

### Tecnologías integradas {#embedded-tech-13323}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,54-T20230817132355-3800a65 | [API Oak 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.2 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
