---
title: Notas de la versión de mantenimiento actual de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión de mantenimiento actual de [!DNL Adobe Experience Manager] as a Cloud Service.
source-git-commit: 4aa4954f214545dcd768fdf955f1fc2f776da939
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 34%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnica de la versión de mantenimiento actual de Experience Manager as a Cloud Service.

## Versión 11835 {#release-11835}

A continuación se resumen las mejoras continuas de la versión de mantenimiento 11835, que se publicó el 19 de abril de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento 11382 anterior.

La activación de funcionalidades para esta versión de mantenimiento le proporcionará el conjunto completo de funcionalidades. Consulte las [notas de la versión actual](/help/release-notes/release-notes-cloud/release-notes-current.md) para obtener información detallada.

### Problemas corregidos {#fixed-issues-11835}

- SITES-12573 - Las consultas de GraphQL que utilizan variables dentro de un filtro fallarán si no se especifica una variable. No actualice a esta versión si utiliza GraphQL con AEM as a Cloud Service.
- SKYOPS-51970 - Regresión identificada de la versión FACT utilizada en el paso buildImage, que conduce a una asignación de usuario no coincidente.
- GRANITE-44542 : Se han notificado problemas para clientes que no especificaron un tipo de nodo de paquete (al proporcionar un .content.xml con jcr:primaryType) para carpetas incluidas en el filtro de paquetes. Esto hacía que estas carpetas se trataran como nt:folder, lo que causaba problemas en varios casos.
- SKYOPS-56928 - La regresión HTTP de Apache puede provocar errores 404. Si experimenta estos problemas, por motivos de seguridad, se recomienda volver a la versión anterior y evitar que la canalización se ejecute durante ese período de tiempo.

### Tecnologías integradas {#embedded-tech-11835}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,44-T20221206170501-6d59064 | [API Oak 1.44.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| API AEM SLING | Versión 2.27.0 | [API de Apache Sling 2.27.0](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.21.2 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
