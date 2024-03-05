---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 77a4b445d9117959ed8855aef445c02529178800
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 13%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 15262 {#release-15262}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 15262, que se publicó el miércoles, 05 de marzo de 2024. La versión de mantenimiento anterior era 14697.

La activación de funcionalidades 2024.3.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-15262}

* ASSETS-30632: se ha agregado una columna de estado de publicación de Brand Portal independiente en la vista de lista.
* ASSETS-30934: compatibilidad añadida para `Iptc4xmpCore:AltTextAccessibility` y `Iptc4xmpCore:ExtDescrAccessibility` propiedades en el Editor de metadatos del recurso.
* ASSETS-31297: mejore las comprobaciones para evitar la eliminación de recursos copiados de medios dinámicos.
* ASSETS-33246: liberar definición de índice `damAssetLucene-10`.
* ASSETS-33590: Añade compatibilidad con representaciones web para vídeos en perfiles de procesamiento.
* GRANITE-36205: Actualice la versión de Oak a 1.60-T20240131102219-0cde853.
* SITES-19326: actualice los vínculos de la interfaz de usuario de Assets para abrir el FQ en el nuevo editor de FQ.
* GUIDES-12945: Sugerencias inteligentes con tecnología de IA para agregar referencias de contenido al crear contenido
* GUIDES-12706: función de historial de versiones modificada en el editor web.
* GUIDES-14948: experiencia del usuario mejorada en el panel de traducción
* GUIDES-8782: Se ha mejorado la lógica de búsqueda en el cuadro de diálogo Insertar elemento
* GUIDES-14681: capacidad de publicar varios ajustes preestablecidos de salida con líneas de base dinámicas
* AEM Para obtener una lista completa de las mejoras en las guías de la, consulte: [AEM Novedades de las guías de la aplicación de la](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/whats-new-2024-2-0.html?lang=en#release-info)

### Problemas corregidos {#fixed-issues-15262}

* ASSETS-15977: elimine los eventos de búsqueda obsoletos de la versión 1 y el productor de canalizaciones.
* ASSETS-18088: actualizar las dependencias de la biblioteca de batik a 1.17.
* ASSETS-21965: el flujo de trabajo de reescritura de metadatos solo debe iniciarse si se producen cambios en los metadatos del recurso.
* ASSETS-26368: Los trabajos programados de importación masiva no se eliminan si la configuración del trabajo no existe.
* ASSETS-26549: los recursos o nodos con &quot;jcr:lastModifiedBy&quot;: &quot;workflow-process-service&quot; se muestran como &quot;usuario externo&quot; en la vista de lista.
* ASSETS-26842: Actualice el texto &quot;Firefly&quot; para que diga &quot;App Builder&quot; en el perfil de procesamiento.
* ASSETS-28708: Respuesta muy lenta para algunas solicitudes de token de IMS.
* ASSETS-28767: estado de publicación incoherente en los recursos si la carpeta contiene un número grande. de recursos publicados.
* ASSETS-29011: El recorte inteligente es visible para los usuarios de solo lectura.
* ASSETS-29348: AssetMoveEventHandler puede consumir demasiada memoria.
* ASSETS-29738: La restricción de carga de recursos falla con NullPointerException para archivos woff.
* ASSETS-30068: Importación masiva de Assets Essentials para incluir el estado COMPLETED_WITH_ERROR para &quot;trabajo completado, pero con error&quot;.
* ASSETS-30261: imsUserId incorrecto enviado a la canalización para eventos de recursos.
* ASSETS-30538: Falta la opción Ver página después de mover un archivo del PDF.
* ASSETS-30626: Error al crear la solicitud de envío notificada para los recursos con assetId vacío.
* ASSETS-30756: la acción del Asistente para mover recursos falla cuando el nombre de la carpeta termina en &quot;html&quot;.
* ASSETS-30810: Vacíe las etiquetas antes de procesar la configuración heredada de YouTube.
* ASSETS-31015: No se pueden cargar recursos con la extensión de nombre de archivo .msg.
* ASSETS-31038: Las tareas y los eventos recibidos por el servicio de notificación no se procesan.
* ASSETS-31097: deshabilite la copia asíncrona para el contenido WCM para evitar advertencias de consultas de recorrido.
* ASSETS-31256: los recursos o nodos con &quot;jcr:lastModifiedBy&quot;: &quot;workflow-process-service&quot; se muestran como &quot;usuario externo&quot; en la vista de lista.
* ASSETS-31260: El campo desplegable del formulario de metadatos del recurso no funciona correctamente cuando el JSON desplegable tiene una lista grande.
* ASSETS-31280: haga que los recursos se descarguen en una estructura aplanada cuando se agreguen a una colección.
* ASSETS-31301: `dynamicmedia_sly.js` La API de uso no puede crear correctamente una instancia de.
* ASSETS-31330: ko_KR: Cadenas no localizadas en Subtítulos y Pistas de audio.
* ASSETS-31405: el procesamiento del servidor de InDesign falla en los diseños de InDesign grandes.
* ASSETS-31570: Unified Shell: los botones &quot;Guardar y cerrar&quot; y &quot;Cancelar&quot; de los detalles del recurso deben presionarse más de una vez para que funcionen.
* ASSETS-31673: error de importación masiva para archivos de Dropbox grandes.
* ASSETS-32108: AEM Assets no guarda el tamaño de tarjeta definido por el usuario en la configuración de vista.
* ASSETS-32230: actualizar la versión de tiempo de ejecución mínima del paquete com.adobe.aem.repoapi.
* ASSETS-32544: el trabajo de exportación de metadatos falla intermitentemente.
* ASSETS-32679: Almacenar en caché problemas con vistas previas de recursos (PDF).
* ASSETS-32754: las tareas no se pueden asignar a usuarios que no hayan iniciado sesión anteriormente.
* ASSETS-32755: configure el tema del trabajo com/adobe/cq/dam/assetmove para utilizar una cola ordenada.
* ASSETS-32899: La búsqueda dentro de colecciones es extremadamente lenta.
* ASSETS-33098: Las facetas de búsqueda de AEM Assets &quot;Predicado de etiquetas&quot; no funcionan según lo esperado.
* ASSETS-33454: la actividad Revisar tarea y los comentarios no aparecen en la cronología.
* ASSETS-34088: La vista previa del PDF no funciona en AEM Assets.
* ASSETS-34155: Dynamic Media AEM: actualización de la versión para visores de la aplicación de la versión 2024.1.0.
* ASSETS-34684: administra varios valores dc:title en el árbol de contenido.
* ASSETS-34789: corrija los problemas de normalización en la comprobación de conflictos de nombres de archivo.
* AEM DXML-13276: Guías de: integre índices en GraniteContent y elimínelos de la biblioteca.
* GRANITE-47995: Las operaciones de eliminación pueden fallar debido a conflictos con la propiedad &quot;cq:isDelivered&quot;.
* GRANITE-48079: habilita las solicitudes de POST para la validación de tokens en línea de OAuth.
* GRANITE-48143: actualice org.apache.sling.resourcemerger a 1.4.4 .
* GRANITE-49031: Actualización a Jackson 2.16.1.
* SCRNS-3961: Screens - Sequence channel: la animación Jquery utilizada en la transición Fade conduce a una pantalla en negro.
* SITES-15868: mejora del rendimiento para enumerar fragmentos.
* SITES-16079: `/fragments/{id}/references` ha comenzado a devolver duplicados.
* SITES-16118: Si se aplica un parche a un fragmento y falta un campo de fragmento en el modelo, se genera una excepción.
* SITES-16121: la recuperación de un campo de fecha de modelo genera una excepción.
* SITES-16207: La operación POST /adobe/sites/cf/models devuelve dos códigos de estado OK diferentes.
* SITES-17361: vuelva a incrustar Jsoup en el paquete sin encabezado de sitios.
* SITES-17768: GraphQL para generar la URL de Dynamic Media de salida para los recursos a los que se hace referencia en los fragmentos de contenido.
* SKYOPS-66622: La implementación del autor bloquea el bucle después de ejecutar una canalización habilitada para buildTransform.
* SKYOPS-69977: El servlet de imagen adaptable no carga la imagen después de la última actualización.
* GUIDES-15045: La revisión ortográfica en el editor no permite la selección de sugerencias.
* GUIDES-14968: el botón de navegación global no funciona y el panel no se puede cargar.
* GUIDES-14943: en la publicación de PDF nativos, los atributos personalizados dentro de ajustes preestablecidos de condición no funcionan para la publicación de PDF nativos.
* GUIDES-15085: en la publicación de PDF nativos, las referencias clave no se resuelven para la versión de diciembre de 2023 de las guías de Adobe Experience Manager.
* GUIDES-13486: **Filtro de línea base** Los archivos no funcionan con Nombre de archivo en el Editor web.
* AEM Para obtener una lista completa de los problemas corregidos en las Guías de, consulte: [AEM Problemas corregidos de Guías de](https://experienceleague.adobe.com/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2024-releases/2402-release/fixed-issues-2024-2-0.html?lang=en#release-info)

### Problemas conocidos {#known-issues-15262}

Ninguna.

### Aviso de cambio {#change-notice-15262}

**Acción necesaria**

Los próximos cambios requerirán la biblioteca [aem-cloud-testing-customers](https://github.com/adobe/aem-testing-clients) se utiliza en las pruebas funcionales personalizadas para actualizarse al menos a la versión **1.2.1**

Asegúrese de que la dependencia de en `it.tests/pom.xml` se ha actualizado.

```xml
<dependency>
   <groupId>com.adobe.cq</groupId>
   <artifactId>aem-cloud-testing-clients</artifactId>
   <version>1.2.1</version>
</dependency>
```

Este cambio será necesario después del 6 de abril de 2024.

Si no se actualiza la biblioteca de dependencias, se producirán errores de canalización en el paso &quot;Pruebas funcionales personalizadas&quot;.

### Tecnologías integradas {#embedded-tech-15262}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1.60-T20240131102219-0cde853 | [API Oak 1.60.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.60.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.4 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
