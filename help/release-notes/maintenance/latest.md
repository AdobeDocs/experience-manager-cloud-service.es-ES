---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 0dab7428d8ae5ec4c11a88ff310fad649a365868
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 22%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 13665 {#release-13665}

A continuación se resumen las mejoras continuas para la 13665 de la versión de mantenimiento, que se publicó el 27 de septiembre de 2023. Esta versión de mantenimiento sustituye a las 13420 de la versión.

La activación de funciones 2023.10.0 proporciona el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-13665}

* Varias mejoras en las API de fragmentos de contenido.
* ASSETS-26713: Panel de recursos: nuevo panel de IU de Experience ahora accesible desde la interfaz de usuario táctil.
* SITES-11206: Fragmentos de contenido: API de búsqueda para fragmentos de contenido.
* SITES-11262: Fragmentos de contenido: Botón para cambiar al nuevo Editor de fragmentos de contenido.
* SITES-15447: Componentes principales: versión 2.23.4.

### Problemas corregidos {#fixed-issues-13665}

* Varias actualizaciones relacionadas con la traducción.
* CQ-4354428: Workflows: no se puede completar una tarea en la bandeja de entrada.
* SITES-9733: Fragmentos de contenido: las referencias de recurso en el panel de referencia de fragmentos de contenido muestran referencias 0 (cero).
* SITES-14561: Fragmentos de contenido: corregido y mejorado HTML a la conversión de Marcado.
* SITES-14882: Fragmentos de contenido: una vez que editamos un fragmento de contenido y cerramos la pestaña sin hacer clic en el botón Guardar o Cerrar, los valores se almacenan.
* SITES-15167: Fragmentos de contenido: Al aplicar parches a una variación con una carga útil no válida, se devuelven 400 pero 500.
* SITES-15514: Fragmentos de contenido: Salida de Markdown mal formada para la tabla dentro de RTE.
* SITES-15661: Fragmentos de contenido: no utilice restricciones únicas y reordene elementos en campos de referencias en la API de fragmentos.
* SITES-15730: Screens: La funcionalidad de vista previa de canal de Screens no funciona en el panel.
* SITES-15995: Fragmentos de contenido: Los tipos MIME de los campos de texto largo de modelo y fragmento están codificados.
* SITES-16074: Fragmentos de contenido: Etiquete campos que no sean de cadena[] no se puede recuperar de JCR.
* SITES-16084: Fragmentos de contenido: Falta el navegador de destino en CFHomeCardModelImpl.
* SITES-14773: Fragmentos de experiencia: La referencia de vínculo no se actualiza dentro del fragmento de experiencia.
* SITES-14899: Fragmentos de experiencias: Varias ofertas creadas para variaciones de XF en Target.
* SITES-8590: GraphQL: Problemas de codificación con variables en consultas persistentes.
* SITES-9224: GraphQL: La excepción &quot;Writer ya se ha cerrado&quot; en GraphQLServlet.
* SITES-14800: GraphQL: excepción en consultas de GraphQL persistentes con variables.
* SITES-15586: GraphQL: Problema con el filtrado de consultas persistentes con valores nulos.
* SITES-15622: GraphQL: Problema con consultas persistentes con números y parámetros booleanos.
* SITES-15654: GraphQL: Problema con uniones y propiedades con el mismo nombre.
* SITES-15267: Lanzamientos: la promoción no recoge las páginas de lanzamiento modificadas antes de modificar la configuración de lanzamiento.
* SITES-15406: Lanzamientos: No se puede añadir una página de lanzamiento.
* SITES-15427: Lanzamientos: comportamiento incoherente del ámbito &quot;Promocionar página actual y páginas secundarias&quot;.
* SITES-15429: Lanzamientos: las páginas de creación se eliminaron al promocionar lanzamientos.
* SITES-15462: Lanzamientos: el proceso de promoción automática publica páginas fuera del ámbito de la promoción.
* SITES-15815: Lanzamientos: la página eliminada del lanzamiento hace que este no se promocione correctamente.
* SITES-15223: Editor de páginas: no se pueden cambiar los componentes en el emulador de tamaño de tableta.
* SITES-15463: Plantillas de página: Las plantillas no se pueden publicar.

### Problemas conocidos {#known-issues-13665}

Ninguno

### Tecnologías integradas {#embedded-tech-13665}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1,54-T20230817132355-3800a65 | [API Oak 1.54.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.54.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.4 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
