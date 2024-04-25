---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: b7e7bc7546b836667fff9db0ea5419e751f492cb
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 78%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 15977 {#release-15977}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 15977, que se publicó el 19 de abril de 2024. La versión de mantenimiento anterior fue la 15939.

La activación de funcionalidades 2024.4.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-15977}

* GRANITE-51335: optimizar la comprobación de estado de AEM para aumentar la estabilidad de la instancia.

### Problemas corregidos {#fixed-issues-15977}

* CQ-4357226: corregir la regresión en la compatibilidad de las configuraciones de IMS con las credenciales de OAuth.
* GRANITE-51335: actualizar Ratelimit a 5.0.4 Corregidos los registros de comprobación de estado de Felix.

### Problemas conocidos {#known-issues-15977}

* **(Solo para AEM Forms)** AEM Después de instalar la versión de mantenimiento de Cloud Foundation 15977, los campos de formulario adaptable se representan en un orden incorrecto durante la creación del formulario y para los formularios publicados. Si utiliza AEM Forms, para evitar inconvenientes, se recomienda no actualizar a la versión 15977 hasta que el problema se resuelva en la próxima versión de mantenimiento.


### Funciones y API obsoletas {#deprecated-15977}

* [Credenciales JWT de Adobe Developer Console en desuso](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Eche un vistazo a [Funciones y API en desuso y eliminadas](/help/release-notes/deprecated-removed-features.md) para saber qué se ha desaprobado o eliminado en AEM as a Cloud Service.

### Tecnologías integradas {#embedded-tech-15977}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1.62.0 | [API Oak 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html?lang=es) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.24.6 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
