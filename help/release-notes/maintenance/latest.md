---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 3be366e5fa0a7625203a052426be6a2fd2412cf6
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 100%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 16145 {#release-16145}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 16145, que se publicó el 1 de mayo de 2024. La versión de mantenimiento anterior fue la 15977.

La activación de funciones 2024.5.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-16145}

* ASSETS-23489: mejoras en la información del repositorio.
* ASSETS-26926: mejoras en las encuestas de carga de Dynamic Media.
* ASSETS-30351: el cuadro de diálogo de descarga debe cargar los tamaños de representación de Dynamic Media de forma asíncrona.
* ASSETS-30379: mejorar la resolución de las licencias DRM en la descarga.
* AEM ASSETS-31058: mostrar las representaciones de recortes inteligentes en la IU de recursos de AEM y generar imágenes recortadas inteligentes cuando el usuario hace clic en estas representaciones.
* ASSETS-31218: añadir compatibilidad con smartCrop con nombre en la API de entrega de recursos.
* ASSETS-31979: añadir un indicador visual y deshabilitar las funciones de la IU durante las operaciones asíncronas de Assets.
* ASSETS-32735: mejoras en el evento actualizado de metadatos de recursos.
* ASSETS-34661: previsualización de API para DM y/o URL de envío de la publicación de AEMaaCS.
* XMP ASSETS-37259: mejoras en el análisis de XMP.
* ASSETS-37263: permitir la cancelación de los trabajos asincrónicos de recursos que fallen.
* CNTBF-114: mejoras en el reflujo de contenido.
* CNTBF-148: mejoras en el reflujo de contenido.
* AEM CQ-4356992: últimas traducciones de AEM y Granite.
* SITES-19326: actualiza los vínculos de la interfaz de usuario de recursos para abrir FC en el nuevo editor de FC.
* SITES-20686: GraphQL: exponer la URL de Dynamic Media a través de _dmS7Url (para recursos que no sean imágenes).
* SKYOPS-68091: actualizar a Java 11.0.20.

### Problemas corregidos {#fixed-issues-16145}

* ASSETS-32321: la resolución del flujo de trabajo posterior al procesamiento falla si en la carpeta predecesora falta el subnodo &quot;jcr:content&quot;.
* ASSETS-33856: el ajuste preestablecido de imagen JPEG carga el archivo como TXT.
* ASSETS-34096: corregir la vista de la IU táctil para el informe de descarga asíncrona.
* ASSETS-34493: error al cargar el cuadro de diálogo de descarga después de habilitar la alternancia de funciones de varias compañías.
* ASSETS-34824: la URL de copia aparece vacía para las carpetas con DM deshabilitado.
* ASSETS-35226: el flujo de trabajo posterior al procesamiento no se resuelve si se ha especificado en la raíz de DAM.
* ASSETS-35559: reducir el registro de errores de carga de lotes de DM a WARN.
* ASSETS-35860: conversión de huso horario incorrecta en la vista de columna de AEM Assets.
* ASSETS-35935: navegación de carpetas incorrecta después de cerrar la revisión de carga útil.
* ASSETS-35961: el botón Añadir recorte no funciona en el perfil de imagen.
* ASSETS-36227: deshabilitar el servicio FolderPreviewUpdaterImpl en la publicación.
* ASSETS-36943: omite las columnas alineadas cuando los elementos CF y otros elementos no CF están presentes en una carpeta en la vista de lista.
* ASSETS-36990: los trabajos de metadatos exportados fallan o se ralentizan con un gran número de propiedades.
* ASSETS-37113: el trabajo de reprocesamiento de recursos finaliza inmediatamente si la consulta solo devuelve resultados CF.
* AEM ASSETS-37260: la exportación de metadatos en AEM puede producir un CSV no válido.
* ASSETS-37261: PPTx y problema de anotación de PDF en AEM Assets.
* ASSETS-37282: posible solicitud lenta para abrir una carpeta grande.
* AEM ASSETS-37330: la importación masiva desde OneDrive crea una estructura de carpetas de recursos incorrecta.
* ASSETS-37609: quitar la búsqueda de conf de Scene7 heredada.
* ASSETS-38016: algunas actualizaciones de metadatos no se rastrean correctamente en los eventos.
* AEM CQ-4357161: la pantalla de carga útil de la bandeja de entrada de AEM devuelve 404.
* GRANITE-50041: Añadir representación no funciona cuando la resolución es superior a 1440 px de anchura cuando solo la opción &quot;Añadir representación&quot; está en la opción desplegable.
* GRANITE-50279: nombres de semanas desordenados en el componente Datepicker de Coral.
* SCRNS-3949: el tiempo de solicitud de captura del canal de Screens es demasiado largo.
* SCRNS-3981: [Canal de secuencia] se obtiene una pantalla en negro cuando la secuencia de eventos de carga/descarga de elementos se distorsiona.
* SCRNS-4180: [Canal de secuencia] la secuencia se detiene con una pantalla en blanco para los canales con vídeos de duración -1 al recuperarse de la miniatura de reserva.
* SCRNS-4245: [Canal de secuencia] duración limitada de la pantalla en blanco cuando se carga un vídeo y se cambia de la miniatura de reserva.
* SITES-16055: corregir los vínculos de Live Copy y origen de Live Copy en la página de propiedades correspondiente.
* SCRNS-4243: faltan botones en el proveedor de contenido para usuarios no administradores.

### Problemas conocidos {#known-issues-16145}

Ninguna.

### Funciones y API obsoletas {#deprecated-16145}

* [Credenciales de JWT de Adobe Developer Console en desuso](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* A partir del 1 de mayo de 2024, Adobe Dynamic Media deja de ofrecer asistencia para lo siguiente:

   * SSL (Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS (Transport Layer Security) 1.0 y 1.1
   * Los siguientes cifrados débiles en TLS 1.2:
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


Para saber qué es lo que está en desuso o se ha eliminado en AEM as a Cloud Service, consulte [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Tecnologías integradas {#embedded-tech-16145}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.62.0 | [API Oak 1.62.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html?lang=es) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.24.6 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
