---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 36fefbf74a288d60a9529f0c7273dd6b0557177b
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 39%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 15939 {#release-15939}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 15939, que se publicó el jueves, 17 de abril de 2024. La versión de mantenimiento anterior fue la 15860.

La activación de funcionalidades 2024.4.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-15939}

* GRANITE-39892: Actualizar distribución para límite de tamaño de cola y listo para publicar.
* GRANITE-48777: actualización de QS a com.adobe.granite.security.user-0.4.84 terminada.
* GRANITE-49421: propiedades agregadas para la entidad de seguridad de servicio de segmentos.
* GRANITE-49855: escriba un analizador del modelo de funciones que falle en la compilación de Quickstart en caso de que se produzca un nuevo uso de commons.json.
* GRANITE-47995: permite cambiar la escritura de cq:isDelivered.
* GRANITE-36205: Actualice la versión interna de la versión de Oak a la más reciente.
* GRANITE-50156 Enlace la afinidad de AEM CS al ID de usuario de IMS para el editor universal.
* GRANITE-50556: actualice el paquete crosswalk a la versión 0.1.18.
* GRANITE-50728: actualice FileVault a 3.7.3-T20240308111857-81fa88f1.
* GRANITE-50957: actualice QS a com.adobe.granite.repository a 1.8.114.
* GRANITE-50158: agregue compatibilidad con el flujo de credenciales del servidor OAuth al servidor en el cargador YAML.
* GRANITE-51327: Actualice Oak a la última versión pública (1.62.0).
* SKYOPS-68091 Actualice las imágenes de tiempo de ejecución de Java 11 a la versión 3.0.0.
* SKYOPS-70421: actualizar el paquete org.apache.sling.servlet-helpers
* AEM SKYOPS-73483: permitir el inicio de sesión del token en la.

### Problemas corregidos {#fixed-issues-15939}

* GRANITE-46901: Añada métricas al cliente de mensajería.
* GRANITE-48793: actualice QS a com.adobe.granite.crx-explorer-1.1.28.
* GRANITE-48937: Omnisearch no funciona en la página aem/start.html.
* GRANITE-49638: Corrija la configuración de tipo de contenido incorrecta para la fábrica del transformador RUM.
* GRANITE-50141: IMSProviderImpl está enviando spam al registro.
* SITES-20949: Error de ComponentsIT.testEmbed después de que YouTube añadiera referrerpolicy=&quot;stricto-origin-when-cross-origin&quot;.
* SITES-21233: Actualización de componentes principales: corregir acordeón después de la actualización a 15860.
* SKYOPS-74819: Compatibilidad con versiones anteriores rotas para claves duplicadas en Apache Commons.
* SKYOPS-67087: La agregación de Clientlib no funciona en determinados casos.
* AEM CQ-4355415: Los vínculos de notificaciones de no funcionan en 6.5 SP18.

### Problemas conocidos {#known-issues-15939}

Ninguna.

### Funciones y API obsoletas {#deprecated-15939}

* [Credenciales JWT de Adobe Developer Console en desuso](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

Eche un vistazo a [Funciones y API en desuso y eliminadas](/help/release-notes/deprecated-removed-features.md) para saber qué se ha desaprobado o eliminado en AEM as a Cloud Service.

### Tecnologías integradas {#embedded-tech-15939}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1.62.0 | [API Oak 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.24.6 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
