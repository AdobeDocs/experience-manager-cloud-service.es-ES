---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 57d818e3e89f17f829a6b51689f02e5f59614563
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 43%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 13420 {#release-13420}

A continuación se resumen las mejoras continuas para la 13420 de la versión de mantenimiento, que se publicó el 11 de septiembre de 2023. Esta versión de mantenimiento sustituye a las 13323 de la versión.

La activación de funciones 2023.9.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-13420}

- ASSETS-19544: la propiedad Última modificación de recursos por ahora se establece en el usuario que solicita el procesamiento.

### Problemas corregidos {#fixed-issues-13420}

- ASSETS-27628: se crea un nodo &quot;canales&quot; erróneo al personalizar el panel de búsqueda de recursos
- ASSETS-27539: coincidencia de expresiones regulares de restricciones de carga.
- ASSETS-26530: Unified Shell no devuelve a los usuarios a la página original.
- ASSETS-22719: los corchetes de los nombres de puntos de interrupción de recorte inteligente rompen la función de edición de recorte inteligente.
- ASSETS-27726: Google no debe indexar linkshare.html.
- ASSETS-27791: la validación del esquema de metadatos solo se produce para el primer campo.
- ASSETS-25544: se ha corregido el botón de invalidación de caché de CDN deshabilitado.
- ASSETS-26575: Se corrigió el truncamiento de nombres al crear conjuntos de imágenes.
- ASSETS-26705: se ha corregido el procesamiento innecesario en recursos de carpeta no DM y fragmentos de contenido.
- ASSETS-25740: los lectores de pantalla fijos no narran el nombre y la función de los controles Editar/Recortar en la página &quot;Editar recortes inteligentes&quot; mediante las teclas de flecha hacia abajo.
- CQ-4354266: no se pueden abrir los elementos de la bandeja de entrada.
- AEM CQ-4354347: Traducciones actualizadas de la.
- DISP-1009: User-Agent como encabezado no inicial recorta X-Forwarded-Host.
- Varias correcciones relacionadas con la accesibilidad y la seguridad.

### Problemas conocidos {#known-issues-13420}

Ninguna.

### Tecnologías integradas {#embedded-tech-13420}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,54-T20230817132355-3800a65 | [API Oak 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.2 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
