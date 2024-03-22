---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: dbdc63db9a9ac954ce6359d3643231d6e195fd53
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 92%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 15575 {#release-15575}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 15575, que se publicó el miércoles, 19 de marzo de 2024. La versión de mantenimiento anterior era 15262.

La activación de funcionalidades 2024.3.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-15575}

Ninguna.

### Problemas corregidos {#fixed-issues-15575}

* ASSETS-36358: no se puede procesar el informe de carga.
* GRANITE-50774: GraniteContent debe utilizar un orden determinista de los valores de propiedad en el momento de la inicialización.

### Problemas conocidos {#known-issues-15575}

Ninguna.

### Aviso de cambio {#change-notice-15575}

**Acción necesaria**

#### Establecer la versión de CM Java en 11 {#set-java-version-11}

La nueva versión de aem-sdk-api contiene clases compiladas con un destino Java 11, que no es compatible con la versión 1.8 JDK predeterminada del entorno de compilación de Cloud Manager. Esta actualización requiere que Maven se ejecute con JDK 11.

Se recomienda a los clientes que añadan un archivo `.cloudmanager/java-version` a la raíz de su repositorio de Git con el contenido: `11`. Consulte [Entorno de compilación / Configuración de la versión del JDK de Maven](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#alternate-maven-jdk-version).

#### Actualizar aem-cloud-testing-customers a 1.2.1 {#update-aem-cloud-testing-clients}

Los próximos cambios requerirán que se actualice la biblioteca [aem-cloud-testing-customers](https://github.com/adobe/aem-testing-clients) en las pruebas funcionales personalizadas para actualizarse al menos a la versión **1.2.1**

Asegúrate de que la dependencia en `it.tests/pom.xml` se ha actualizado.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

Este cambio debe realizarse antes del 6 de abril de 2024.

Si no se actualiza la biblioteca de dependencias, se producirán errores de canalización en el paso &quot;Pruebas funcionales personalizadas&quot;.

### Tecnologías integradas {#embedded-tech-15575}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html?lang=es) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.4 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
