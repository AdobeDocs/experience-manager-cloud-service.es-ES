---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 7bc6d9a947a5ce7c56481eaec8a2f186caf36c64
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 41%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 18099 {#release-18099}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 18099, que se publicó el jueves, 09 de octubre de 2024. La versión de mantenimiento anterior fue la 17964.

La activación de funcionalidades 2024.10.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-18099}

* ASSETS AEM-38322: Habilitando el evento de solicitud http para la.
* ASSETS-41448: actualice el paquete auth.ims para admitir asignaciones de FI a grupos.
* ASSETS-41684: agregue configuraciones OSGI OOB para definir la asignación de FI a grupo para Assets, Foundation, Sites y Forms.
* ASSETS-43015: Actualización al último paquete auth.ims.
* CQ-4356633: añada caracteres adicionales en la información sobre herramientas &quot;Solo contenido&quot;.
* AEM GRANITE-50948: Integre el servicio de repositorio en la compatibilidad con el servicio de repositorio de la.
* GRANITE-52454: añadiendo el asistente de soporte 0.1.2.
* GRANITE-52454: Actualización del soporte Helper GRANITE-52454 actualización del soporte Helper para utilizar la última versión para AEMaaCS.
* GRANITE-53287: Actualizando la versión de prueba de integración de privilegios de seguridad.
* GRANITE-53485: Autenticación principal del servicio de soporte para el almacenamiento del blob de Azure de replicación.
* GRANITE-53514: Treeactivation actualizada a la versión 1.0.26.
* GRANITE-53870: Cree un mecanismo interno para omitir la comprobación de la versión máxima de JVM para el inicio rápido.
* GRANITE-53914: Corrija los errores de prueba de la plataforma con Java 17 Versión de módulo actualizada.
* GRANITE-53966: utilice un grupo de hilos independiente para la distribución de contenido.
* GRANITE-54006: actualice Jackson a 2.17.2.
* GRANITE-54038: añada el cliente IMS de Creative Cloud AEM Enterprise a la lista de permitidos de cliente IMS de la empresa de la empresa de la empresa de la que se ha realizado el.
* GRANITE-54054: Variable de entorno para com.adobe.granite.repository.impl.SystemUserValidation warnOnly.
* GRANITE-54266: Falta el servicio de sugesor de búsqueda en el SDK de producción.
* GRANITE-54274: aceptar el cliente IMS del Firefly.
* GRANITE-54300: actualizar Oak a la última versión pública (1.70.0).
* GUIDES-19069: agregue guidesPeerLinkIndex para el complemento de guías de aem.
* SITES-23584: corrija la prueba con errores para el componente Foundation en Java 17.
* SKYOPS-69768: Los modelos Sling no deserializan ResourceResolvers.
* SKYOPS-76378: Mejore la seguridad de los subprocesos del registro/anulación de registro del paquete de recursos en i18n.
* SKYOPS-79285: Actualice Sling XSS a 2.4.2.
* SKYOPS-82383: Exponga el resultado &quot;helm-values&quot; convert-merge-analyze en el descriptor de ejecución del comando.
* SKYOPS-84810: omitir la ejecución &quot;40-initialize-publish.sh&quot; al inicio para RDE.
* SKYOPS-84951: Corrija el código de generación de suma de comprobación de contenido mutable.
* SKYOPS-85335: Actualice org.apache.sling.jcr.repoinit a 1.1.52.
* SKYOPS-85336: Actualice Sling Commons Threads a 3.3.0.
* SKYOPS-86329: actualización de versiones de módulos de prueba de plataforma para admitir el sdk de java 21.

### Problemas solucionados {#fixed-issues-18099}

* CNTBF-298: elimina jcr:uuid de los paquetes exportados por CC.
* SKYOPS-83910: solucione los problemas de concurrencia que se encuentran en SKYOPS-82371.
* GRANITE-52876: Actualización a com.adobe.granite.ui.content 0.8.1448.
* GRANITE-53088: Regresión introducida por la corrección de SITES-11992.
* GUIDES-14445: La generación del PDF nativo falla con un error relacionado con la obtención de dependencias para Node.js.
* GUIDES-16961: el título de `<conref>` no se resuelve en los paneles Línea de base y Traducción del Editor Web.
* GUIDES-17283: al seleccionar la opción **Usar metadatos agregados en topicmeta**, las propiedades de metadatos no se propagan en las propiedades de documento de la salida del PDF nativo.
* GUIDES-17793: El PDF al que se hace referencia no se activa desde el **tablero de Publish en masa** durante la activación en lote del contenido publicado.

Para obtener más información sobre las características y los problemas nuevos y mejorados de las guías corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-18099}

* FORMS-15818: No se encontró la entrada de descriptor de componente `OSGI-INF/com.adobe.aemfd.docmanager.impl.*.xml` en los registros del servidor. Son sentencias del registro inofensivas.

### Características y API obsoletas {#deprecated-18099}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

A continuación se muestra un resumen de las funciones que han quedado recientemente en desuso o de las que están en proceso de finalización de soporte.

#### API de uso de JavaScript {#javascript-use-api}

[La API de uso de JavaScript](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) está en desuso oficialmente debido a los desafíos que los usuarios tienen al depurar y mantener el código que aprovecha la API, así como las limitaciones de rendimiento en comparación con la alternativa de Java.

Debería hacer la transición a [la API para uso de Java](https://experienceleague.adobe.com/es/docs/experience-manager-htl/content/java-use-api), que ofrece un mejor rendimiento, una depuración más sencilla y una mayor compatibilidad a largo plazo.

#### com.day.cq.wcm.api {#com-day-cq-wcm-api}

Tenga en cuenta que Adobe está en proceso de actualizar `com.day.cq.wcm.api`. Algunos de sus métodos y clases se han marcado como `@Deprecated` en la versión actual. Se eliminarán en futuras versiones. Considere la posibilidad de cambiar a las alternativas sugeridas.

#### org.apache.jackrabbit.oak.plugins.blob {#org.apache.jackrabbit.oak.plugins.blob}

* GRANITE-54165: obsoleto org.apache.jackrabbit.oak.plugins.blob en la API pública.

### Correcciones de seguridad {#security-18099}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 2 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-18099}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.70.0 | [API Oak 1.70.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.70.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.27.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
