---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 1dd2eae9201c86d2cdac78ff99634eff8ca57a05
workflow-type: ht
source-wordcount: '272'
ht-degree: 100%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 15860 {#release-15860}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 15860, que se publicó el 10 de abril de 2024. La versión de mantenimiento anterior fue la 15787.

La activación de funcionalidades 2024.3.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-15860}

Ninguna.

### Problemas corregidos {#fixed-issues-15860}

* Corrige la regresión para mostrar la consola Lanzamientos cuando un lanzamiento hace referencia a una página eliminada o movida.

### Problemas conocidos {#known-issues-15860}

Ninguna.

### Funciones y API obsoletas {#deprecated-15860}

* [Credenciales JWT de Adobe Developer Console en desuso](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Eche un vistazo a [Funciones y API en desuso y eliminadas](/help/release-notes/deprecated-removed-features.md) para saber qué se ha desaprobado o eliminado en AEM as a Cloud Service.

### Aviso de cambio {#change-notice-15860}

**Acción necesaria**

#### Establecer la versión de CM Java en 11 {#set-java-version-11}

La nueva versión de aem-sdk-api contiene clases compiladas con un destino Java 11, que no es compatible con la versión 1.8 JDK predeterminada del entorno de compilación de Cloud Manager. Esta actualización requiere que Maven se ejecute con JDK 11.

Se recomienda a los clientes que añadan un archivo `.cloudmanager/java-version` a la raíz de su repositorio de Git con el contenido: `11`. Consulte [Entorno de compilación / Configuración de la versión del JDK de Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).


### Tecnologías integradas {#embedded-tech-15860}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html?lang=es) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.24.4 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
