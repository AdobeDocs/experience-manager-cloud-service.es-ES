---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 82be9b2b328343e827b90bd8266d93127757f477
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 40%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 17569 {#release-17569}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 17569, que se publicó el miércoles, 27 de agosto de 2024. La versión de mantenimiento anterior fue la 17465.

La activación de funcionalidades 2024.9.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-17569}

* CQ-4353778: Eventos de proceso de traducción.
* CQ-4354583: envía eventos de proceso de traducción a través de la canalización de Adobe.
* CQ-4356479: permitir que solo el código de Adobe utilice el contexto de servlet /adobe.
* CQ-4358133: optimice el uso de Jenkins worker.
* CQ-4358226: La funcionalidad de palabra clave Save Translation no funciona para un formato de cadena determinado.
* AEM CQ-4358270: Kit de traducción de la: 8 de agosto.
* CQ-4358310: agregue oak-compat-query-spi-1.2 a quickstart.
* GRANITE-36205: Actualización automatizada para la versión interna de Oak en QS.
* GRANITE-49833: Compatibilidad por lotes para el remitente y el proxy de eventos.
* GRANITE-52053: Eliminar usos de Commons Collections 3: Platform otros.
* GRANITE-52492: Recuperación asíncrona elástica en caso de restauración PIT.
* GRANITE-53086: Actualice la versión del complemento jacoco a 0.8.12 en AEMaaCS.
* GRANITE-53099: Actualización a Apache Felix Http Jetty 5.1.24.
* GRANITE-53125: Agregar clasificación a CloudEvent.
* GRANITE-53328: Actualice Filevault a 3.8.0-T20240726111512-3cc11d50 que contenga mejoras en el registro de la colocación.
* AEM GRANITE-53340: 660: Versiones y ramificaciones adecuadas para 660 CQ/Platform.
* GRANITE-53341: No advertir sobre el uso de ACS Commons 6.
* GRANITE-53453: actualice commons-lang a 3.15.0.
* GRANITE-53473: Configuración de Sling no obsoleta.
* GRANITE-53478: Actualice Filevault a la versión 3.8.0.
* GRANITE-53505: Actualice QS a commons-collections-3.2.2-adobe-2.
* GRANITE-53528: Actualización de la versión de los artefactos de la plataforma .
* GRANITE-53547: Proporciona una API alternativa que evita el uso de Apache Commons Lang 2.
* GRANITE-53575: utilice BSAFE 6.2.5 en CS.
* GRANITE-53608: Actualice Oak a la última versión pública (1.68.0).
* SITES-23583: Las pruebas de Sites Evergreen fallan en Java 17.
* SKYOPS-79535: Actualización a la versión 2.0 del script rum.
* SKYOPS-79816: Habilitar la tarea del analizador de funciones Sling para asignaciones de usuarios de servicio en la herramienta FACT.
* AEM SKYOPS-81179: crea pruebas para la alternancia de paquetes.
* SKYOPS-81866: Informe de advertencias para paquetes que se sabe que son incompatibles con Java 21.
* SKYOPS-82660: actualizar la API de Sling a 2.27.6.
* SKYOPS-82961: Actualización a Sling ResourceResolver 1.12.0-T20240723153354-a0270a0.
* AEM SKYOPS-83356: cree un tablero global para rastrear las versiones de JVM utilizadas en las implementaciones de la.
* SKYOPS-83436: El lanzamiento de Java Runtime 21 interrumpe la creación de formularios adaptables en AEM Forms.
* SKYOPS-84272: Registra la versión de java utilizada al iniciar aem launcher.

### Problemas solucionados {#fixed-issues-17569}

* CMGR-60225: error de ejecución de la canalización identificado en el cliente de AEM Sites AEM CS al validar la actualización a los 17486 de la versión de la versión de la.
* GRANITE-45919: Los países en los que se ha embargado a alguien aparecen en la lista de países/regiones de Editar configuración de usuario.
* GRANITE-51715: A veces, el selector no introduce la selección en el campo de texto.
* GRANITE-53290: Compruebe correctamente el protocolo al analizar la URL en la comprobación XSS.
* GRANITE-53576: Definición incorrecta de la clasificación de servicios en las configuraciones OSGi.
* SKYOPS-82129: Fuga de memoria en modelos Sling.

### Problemas conocidos {#known-issues-17569}

Ninguna.

### Aviso de cambio {#change-notice-17569}

* A partir de septiembre de 2024, AEM as a Cloud Service deshabilitará la serialización de los solucionadores de recursos a través del marco de trabajo Exportador de modelos Sling. Consulte la [documentación](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obtener más información.

### Características y API obsoletas {#deprecated-17569}

Tenga en cuenta que estamos en proceso de actualizar `com.day.cq.wcm.api` y con la versión actual, hemos marcado como `@Deprecated` algunos de sus métodos y clases. Estos se eliminarán en futuras versiones, por lo que considere la posibilidad de cambiar a las alternativas sugeridas si utiliza alguna de ellas.

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-17569}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 4 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-17569}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.68.0 | [API Oak 1.68.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.68.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.26.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
