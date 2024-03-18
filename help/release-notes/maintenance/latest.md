---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: b0198fee3fb8c2f02f50819bea5757e5b8373ac1
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 87%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 15262 {#release-15262}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 15262, que se publicó el jueves, 06 de marzo de 2024. La versión de mantenimiento anterior era 14697.

La activación de funcionalidades 2024.3.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-15262}

* ASSETS-30632: se ha añadido una columna de estado de publicación de Brand Portal independiente en la vista de lista.
* ASSETS-30934: compatibilidad añadida para las propiedades `Iptc4xmpCore:AltTextAccessibility` y `Iptc4xmpCore:ExtDescrAccessibility` en el Editor de metadatos de recursos.
* ASSETS-31297: mejora las comprobaciones para evitar la eliminación de recursos copiados de medios dinámicos.
* ASSETS-33246: definición de índice de versión `damAssetLucene-10`.
* ASSETS-33590: Añade compatibilidad con representaciones web para vídeos en perfiles de procesamiento.
* GRANITE-36205: actualiza la versión de Oak a 1.60-T20240131102219-0cde853.
* SITES-19326: actualiza los vínculos de la interfaz de usuario de recursos para abrir FC en el nuevo editor de FC.
* GUIDES-12945: sugerencias inteligentes con tecnología de IA para añadir referencias de contenido al crear contenido
* GUIDES-12706: función de historial de versiones modificada en el editor web
* GUIDES-14948: experiencia del usuario mejorada en el panel de traducción
* GUIDES-8782: se ha mejorado la lógica de búsqueda en el cuadro de diálogo Insertar elemento
* GUIDES-14681: posibilidad de publicar varios ajustes preestablecidos de salida con líneas de base dinámicas
* Para obtener una lista completa de las mejoras en las guías de la, consulta: [Novedades de AEM Guides](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/whats-new-2024-2-0.html?lang=es#release-info)

### Problemas corregidos {#fixed-issues-15262}

* ASSETS-15977: elimina los eventos de búsqueda obsoletos de la versión 1 y el productor de canalizaciones.
* ASSETS-18088: actualiza las dependencias de la biblioteca de batik a 1.17.
* ASSETS-21965: el flujo de trabajo de reescritura de metadatos solo debe iniciarse si se producen cambios en los metadatos de recursos.
* ASSETS-26368: los trabajos programados de importación masiva no se eliminan si la configuración del trabajo no existe.
* ASSETS-26549: los recursos o nodos con &quot;jcr:lastModifiedBy&quot;: &quot;workflow-process-service&quot; se muestran como &quot;usuario externo&quot; en la vista de lista.
* ASSETS-26842: actualiza el texto &quot;Firefly&quot; para que se lea &quot;App Builder&quot; en el perfil de procesamiento.
* ASSETS-28708: respuesta muy lenta para algunas solicitudes de token de IMS.
* ASSETS-28767: estado de publicación incoherente en los recursos si la carpeta contiene un número grande de recursos publicados.
* ASSETS-29011: el recorte inteligente es visible para los usuarios de solo lectura.
* ASSETS-29348: AssetMoveEventHandler puede consumir demasiada memoria.
* ASSETS-29738: la restricción de carga de recursos falla con NullPointerException para archivos woff.
* ASSETS-30068: importación masiva de Assets Essentials para incluir el estado COMPLETED_WITH_ERROR para &quot;trabajo completado, pero con error&quot;.
* ASSETS-30261: imsUserId incorrecto enviado a la canalización para eventos de recursos.
* ASSETS-30538: falta la opción Ver página después de mover un archivo PDF.
* ASSETS-30626: error al crear la solicitud de envío notificada para los recursos con assetId vacío.
* ASSETS-30756: la acción del Asistente para mover recursos falla cuando el nombre de la carpeta termina en &quot;html&quot;.
* ASSETS-30810: vacía las etiquetas antes de procesar la configuración heredada de YouTube.
* ASSETS-31015: no se pueden cargar recursos con la extensión de nombre de archivo .msg.
* ASSETS-31038: las tareas y los eventos recibidos por el servicio de notificación no se procesan.
* ASSETS-31097: deshabilita la copia asíncrona para el contenido WCM para evitar advertencias de consultas de transversales.
* ASSETS-31256: los recursos o nodos con &quot;jcr:lastModifiedBy&quot;: &quot;workflow-process-service&quot; se muestran como &quot;usuario externo&quot; en la vista de lista.
* ASSETS-31260: el campo desplegable del formulario de metadatos de recursos no funciona correctamente cuando el JSON desplegable tiene una lista grande.
* ASSETS-31280: haz que los recursos se descarguen en una estructura plana cuando se añadan a una colección.
* ASSETS-31301: la API de uso no puede crear correctamente una instancia de `dynamicmedia_sly.js`.
* ASSETS-31330: ko_KR: cadenas no localizadas en subtítulos y pistas de audio.
* ASSETS-31405: el procesamiento de InDesign Server falla en los diseños de InDesign grandes.
* ASSETS-31570: Unified Shell: los botones &quot;Guardar y cerrar&quot; y &quot;Cancelar&quot; de los detalles del recurso deben presionarse más de una vez para que funcionen.
* ASSETS-31673: error de importación masiva para archivos Dropbox grandes.
* ASSETS-32108: AEM Assets no guarda el tamaño de tarjeta definido por el usuario en la configuración de vista.
* ASSETS-32230: actualiza la versión de tiempo de ejecución mínima del paquete com.adobe.aem.repoapi.
* ASSETS-32544: el trabajo de exportación de metadatos falla intermitentemente.
* ASSETS-32679: almacena en caché problemas con vistas previas de recursos (PDF).
* ASSETS-32754: las tareas no se pueden asignar a usuarios que no hayan iniciado sesión anteriormente.
* ASSETS-32755: configura el tema del trabajo com/adobe/cq/dam/assetmove para utilizar una cola ordenada.
* ASSETS-32899: la búsqueda dentro de colecciones es extremadamente lenta.
* ASSETS-33098: las facetas de búsqueda de AEM Assets &quot;Predicado de etiquetas&quot; no funcionan según lo esperado.
* ASSETS-33454: la actividad Revisar tarea y los comentarios no aparecen en la cronología.
* ASSETS-34088: La vista previa del PDF no funciona en AEM Assets.
* ASSETS-34155: Dynamic Media: actualizados Visores AEM / 2024.1.0.
* ASSETS-34684: administra varios valores dc:title en el árbol de contenido.
* ASSETS-34789: corrige los problemas de normalización en la comprobación de conflictos de nombres de archivo.
* AEM DXML-13276: Guías de AEM: integra índices en GraniteContent y elimínalos de la biblioteca.
* GRANITE-47995: las operaciones de eliminación pueden fallar debido a conflictos con la propiedad &quot;cq:isDelivered&quot;.
* GRANITE-48079: habilita las solicitudes de POST para la validación de tokens en línea de OAuth.
* GRANITE-48143: actualiza org.apache.sling.resourcemerger to 1.4.4 .
* GRANITE-49031: actualiza a Jackson 2.16.1.
* SCRNS-3961: Screens - Canal de secuencia: la animación Jquery utilizada en la transición Fade conduce a una pantalla en negro.
* SITES-15868: mejora del rendimiento para listar fragmentos.
* SITES-16079: `/fragments/{id}/references` ha comenzado a devolver duplicados.
* SITES-16118: si se aplica un parche a un fragmento y falta un campo de fragmento en el modelo, se genera una excepción.
* SITES-16121: la recuperación de un campo de fecha de modelo genera una excepción.
* SITES-16207: la operación POST /adobe/sites/cf/models devuelve dos códigos de estado OK diferentes.
* SITES-17361: vuelve a incrustar Jsoup en el paquete sin encabezado de sitios.
* SITES-17768: GraphQL para la salida de URL de medios dinámicos para activos referenciados en fragmentos de contenido.
* SKYOPS-66622: la implementación del autor bloquea el bucle después de ejecutar una canalización habilitada para buildTransform.
* SKYOPS-69977: el servlet de imagen adaptable no carga la imagen después de la última actualización.
* GUIDES-15045: la revisión ortográfica en el editor no permite la selección de sugerencias.
* GUIDES-14968: el botón de navegación global no funciona y el panel no se puede cargar.
* GUIDES-14943: en la publicación de PDF nativos, los atributos personalizados dentro de ajustes preestablecidos de condición no funcionan para la publicación de PDF nativos.
* GUIDES-15085: en la publicación de PDF nativos, las referencias clave no se resuelven para la versión de diciembre de 2023 de Adobe Experience Manager Guides.
* GUIDES-13486: los archivos **Filtro de línea base** no funcionan con Nombre de archivo en el Editor web.
* Para obtener una lista completa de los problemas corregidos en AEM Guides, consulta: [ Problemas corregidos de AEM Guides](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/fixed-issues-2024-2-0.html?lang=es#release-info)

### Problemas conocidos {#known-issues-15262}

* ASSETS-35923: `UnsupportedClassVersionError` en el paso Generar de canalización de CM después de actualizar `aem-sdk-api` versión a `2024.2.15262.20240224T002940Z-231200`. **Requiere la acción del cliente para establecer la versión de CM Java en 11**, consulte [Entorno de compilación / Configuración de la versión del JDK de Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=en#alternate-maven-jdk-version)
* ASSETS-35860: conversión de huso horario incorrecta en la vista de columna de AEM Assets.
* SCRNS-4171: Pantallas de Windows se queda en blanco y deja de funcionar al actualizar a 15262 y publicar un canal.
* GRANITE-50774: GraniteContent debe utilizar un orden determinista de los valores de propiedad al inicio.

### Aviso de cambio {#change-notice-15262}

**Acciones necesarias**

#### Establecer la versión de CM Java en 11 {#set-java-version-11}

La nueva versión de aem-sdk-api contiene clases compiladas con un destino Java 11, que no es compatible con la versión 1.8 JDK predeterminada del entorno de compilación de Cloud Manager. Esta actualización requiere que Maven se ejecute con JDK 11.

Se recomienda a los clientes que agreguen un `.cloudmanager/java-version` a la raíz de su repositorio de Git con el contenido: `11`. [Entorno de compilación / Configuración de la versión del JDK de Maven](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/build-environment-details.html?lang=en#alternate-maven-jdk-version)

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

### Tecnologías integradas {#embedded-tech-15262}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html?lang=es) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.4 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
