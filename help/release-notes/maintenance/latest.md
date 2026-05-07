---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: d00af3aee8c2a42233bfc0f914a4e24abe921e08
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 30%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## 25892 de versión {#release-25892}

A continuación se resumen las mejoras continuas para la 25892 de la versión de mantenimiento, que se publicó el 7 de mayo de 2026. La versión de mantenimiento anterior era 25520.

La activación de funciones 2026.5.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

>[!NOTE]
>
>La 25821 de la versión se ha convertido en privada.

### Mejoras {#enhancements-25892}

* CQ-4362304: Crear directrices para front-end y actualizar la interfaz de usuario de configuración de LLM.
* GRANITE-39546: Actualice Apache Tika a 3.x.
* GRANITE-53957: Actualice Azure SDK V8 a V12 para oak-blob-azure.
* GRANITE-61245: Elimine todo el uso de commons-lang (reemplace por commons-lang3).
* GRANITE-64748: controlador de autenticación OIDC de Bump.
* GRANITE-64764: actualizar el texto de Apache Commons a 1.15.0.
* GRANITE-64963: Actualice Filevault a 4.2.0.
* GRANITE-66197: Agregue compatibilidad de correo electrónico de la API de Microsoft Graph para inquilinos de M365.
* GRANITE-66449: Actualización de los complementos de Maven para admitir la API de Java 17.
* GRANITE-66473: agregue la biblioteca de caché de cafeína a base-granite.
* GRANITE-66836: Actualice Quickstart a Oak 2.0.0.
* SKYOPS-129301: establezca el nivel de cumplimiento de Javadoc de las API jar en Java 17.
* SKYOPS-129351: Actualice reactive-streams y reactor-core para lograr la compatibilidad con MCP SDK.
* SKYOPS-131412: Actualice Apache Commons Exec a la versión más reciente.
* SKYOPS-131432: Actualice Felix SCR a 2.2.14.
* SKYOPS-131907: actualizar las regiones de la API de Sling a 1.1.10.
* SKYOPS-131938: Actualice GSON a la versión más reciente.
* SKYOPS-132173: Actualice el códec Apache Commons a la versión más reciente.
* SKYOPS-132182: Actualizar el paquete de inquilinos de Sling.
* SKYOPS-132267: actualizar la anotación `org.osgi.service.component`.
* SKYOPS-132272: Actualice el paquete del modelo de funciones de Sling.
* SKYOPS-132525: agregue el analizador de Quickstart para evitar nuevas eliminaciones de API.
* SKYOPS-134408: actualice `com.adobe.granite.asset.core` a 2.2.82.
* SKYOPS-137750: actualizar `com.adobe.granite.comments` a 1.0.40.
* SKYOPS-137759: actualizar `com.adobe.granite.jobs.async.ui.commons` a 3.2.4.
* SKYOPS-138356: actualizar `com.adobe.granite.oauth.server` a 1.1.36.
* SKYOPS-138739: Actualice SnakeYAML a 2.6.

### Problemas solucionados {#fixed-issues-25892}

* ASSETS-59546: elimine las dependencias de la biblioteca de idioma común obsoleta.
* ASSETS-64831: El recuento de intentos de procesamiento de restablecimiento de AssetProcessorProcess causa recursos atascados.
* ASSETS-66683: Bucle de aprobación causado por un error de uploadBlob.
* CNTBF-613: Se ha denegado la corrección del acceso (JCR-101) al registrar tipos de nodos.
* GRANITE-44537: La cadena en &quot;País/Región&quot; no está localizada en AEM.
* GRANITE-61760: Se ha corregido la activación fallida de AdminUserInitializer.
* GRANITE-64543: La respuesta de restricciones de permisos no sigue la estructura de la API.
* GRANITE-66692: El cargador de clases interno no distingue entre actualizaciones de paquetes.
* GRANITE-66732: utilice activadores en lugar de componentes de servicio para paquetes de inicio de nivel 1.
* GRANITE-66846: La API de permisos de AEM no muestra la restricción `rep:ntNames`.
* SITES-39267: restaura pagePath en las entradas de la cadena de relaciones.
* SITES-43715: la validación de permisos falla al leer el estado del recurso.

#### Guías de AEM {#guides-25892}

* GUIDES-45110: al seleccionar una imagen en el editor mediante el cuadro de diálogo **Seleccionar archivo**, solo se muestran los formatos de trama (como JPG, PNG y GIF). Los archivos vectoriales (como `.ai` y `.eps`) no se muestran y no se pueden seleccionar.
* GUIDES-41938: al crear un tema en una carpeta con espacios en su nombre, se crea incorrectamente una carpeta duplicada en la que los espacios se sustituyen por guiones y el tema se guarda allí en lugar de en la carpeta original.
* GUIDES-38377: cuando los cambios en un ajuste preestablecido de salida en un perfil de carpeta se aplican a asignaciones existentes, se restablece el **contexto de publicación** guardado para el ajuste preestablecido de AEM Sites.
* GUIDES-43547: Cuando se abren temas o mapas grandes, la instancia de autor deja de responder y, en algunos casos, es necesario reiniciar.
* GUIDES-32520: cuando se utiliza Retroceso en elementos, el Editor se desplaza hasta la parte superior del tema independientemente de la posición del cursor (Editor 2.0).

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-25892}

Ninguna.

### Características y API obsoletas {#deprecated-25892}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-25892}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 19 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-25892}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 2.0.0 | [API de Oak 2.0.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.0.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.30.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
