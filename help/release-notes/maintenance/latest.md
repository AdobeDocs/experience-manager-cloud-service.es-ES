---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 636183e0597bed24b3e437ed53a35c9e64ac0504
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 21%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 19352 {#19352}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 19352, que se publicó el jueves, 05 de febrero de 2025. La versión de mantenimiento anterior fue la 19149.

La activación de funcionalidades 2025.2.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-19352}

* FORMS-13998: Añadir el componente Acordeón.
* FORMS-17913: Agregar variante de tarjeta para el grupo de radio.
* FORMS-17333: Habilitación de plantillas de correo electrónico de HTML AEM en el envío de formularios de.
* FORMS-17702: habilite los PDF generados en las API de sincronización de salida para que se carguen en Azure Blob Storage.
* SITES-28282: Edge Delivery con editor universal: proporcione la ruta base, el nombre del sitio y la organización como información de página para cualquier página.
* SITES-27055: Edge Delivery con el editor universal: admite parámetros de consulta en el servlet proxy inverso.
* SITES-26796: Edge Delivery con editor universal: admite columnas personalizadas para la hoja de cálculo de taxonomía.
* SITES-26087: Edge Delivery con editor universal: admite la exportación de CSV para hojas de cálculo.
* SITES-26265: Edge Delivery con el editor universal: muestra la cuenta de TA para integrarla con Edge Delivery en la interfaz de usuario de configuración.
* SITES-20372: Edge Delivery con editor universal: habilite casos de uso básicos de MSM para hojas de cálculo.
* SITES-26681: Edge Delivery con editor universal: admite el parámetro ?sheet= para las hojas de cálculo de taxonomía en el autor.
* SITES-26479: [Esquema] Modelo de fragmento de contenido Punto final de estado de publicación programada.
* SITES-25944: [Información general de Livecopy] agrega el estado &quot;Live Copy actualizado con herencia limitada&quot;.
* SITES-28713: [V2] Agregue compatibilidad con datos estructurados al raspador de contenido.
* SITES-27896: CommentsTab se abre automáticamente al recibir una notificación.
* SITES-26720: no se debe permitir al usuario seleccionar una colección completa del selector de recursos.
* SITES-27875: permite mover de forma predeterminada cualquier elemento editable dentro de un contenedor.
* SITES-28340: complemento del servicio de editor universal de Dark Alley.
* SITES-26098: Posibilidad de evitar la publicación de páginas referenciadas al publicar un fragmento de contenido.
* SITES-27789: compatibilidad del atributo de datos data-aue-component en el DOM.
* SITES-25997: mejora las variaciones para admitir la fecha de modificación.
* SITES-28023: salida de GraphQL para referencias de recursos remotos (repositorio + ID de recurso).
* SITES-26058: Punto final del estado de publicación programada del modelo de fragmento de contenido.
* SITES-25108: migración de modelos para referencias de UUID.
* SITES-26630: punto final del estado de publicación programada del fragmento de contenido para varios fragmentos de contenido.
* SITES-23432: mejore la capacidad de eliminación de referencias.
* SITES-25797: Compatibilidad con referencias de recursos externos: GraphQL.
* SITES-17514: elimine la mejora del extremo para cancelar la publicación del fragmento de contenido.
* SITES-14633: Validar el modelo de fragmento de contenido para crear cargas útiles antes de instalar: ejecución en seco.

### Problemas solucionados {#fixed-issues-19352}

* CQ-4356756: no traduzca la compatibilidad con recursos relacionados.
* CQ-4358206: El Planificador de traducción repetida no funciona para proyectos de traducción.
* CQ-4358126: no se puede seleccionar la subcarpeta de configuración en el servicio de nube de traducción.
* FORMS-18098, FORMS-17954: El Forms adaptable no se puede cargar en el modo Internet Explorer del explorador Microsoft Edge.
* FORMS-17162: la publicación de un recurso lleva a la ejecución de consultas OOTB que degradan el rendimiento de la publicación.
* SITES-28415: Edge Delivery con editor universal: botón Corregir propiedades abiertas para hojas de cálculo.
* SITES-26669: Edge Delivery con el editor universal: corrija los problemas al cargar archivos CSV codificados en UTF-8 con una BOM como hoja de cálculo.
* SITES-26543: Edge Delivery con el editor universal: corrija bloques vacíos sin un modelo que procese el marcado incorrecto.
* SITES-26857: Edge Delivery con editor universal: corrija que el token de autenticación del sitio sea visible en la interfaz de usuario para configuraciones basadas en archivos.
* SITES-26662: Edge Delivery con editor universal: solucione problemas con metadatos masivos que distinguen entre mayúsculas y minúsculas.
* SITES-28133: Publish para &quot;Previsualizar&quot; está haciendo que el contenido esté disponible en producción.
* SITES-27187: la activación programada de la página/recurso, incluidas las referencias (experimental), no se pueden publicar referencias.
* SITES-27264: 2 pruebas de Selenium relacionadas con la creación de LiveCopy y los fragmentos de contenido fallan de forma consistente en la página maestra.
* SITES-26559: Anclar la consulta de modelos de fragmento de contenido al índice cqPageLucene.
* SITES-24469: el elemento interactivo no es accesible mediante el teclado.
* Los botones SITES-24518: Nombre y Modelo de la tabla Referencia principal no son accesibles mediante el teclado.
* SITES-27937: las restricciones de UISchema se establecen en null después de actualizar el modelo.
* SITES-27852: falta el esquema UIS del modelo en Categorizaciones.
* SITES-27904: falta el esquema de metadatos en los modelos de fragmento de contenido de lista/búsqueda para una proyección completa.
* SITES-26827: La lista de fragmentos termina en un bucle infinito.
* SITES-27678: [Rendimiento] Impide la captura innecesaria de _referencias.
* SITES-27589: error de actualización de UUID para modelos de fragmento de contenido con varios campos de referencia de contenido/fragmento.
* SITES-26679: cancelar la publicación de los modelos de fragmentos de contenido solo debe validar las referencias publicadas.
* SITES-26666: referencesTree y referencias que devuelven puntos de conexión con resultados diferentes.
* GET SITES-26499: Orden incorrecto del valor del campo de etiqueta en los fragmentos y el PATCH aleatorizan el orden.
* SITES-26585: corrija un error de descripción pequeña en el esquema.
* SITES-26647: la validación de referencia de Eliminar extremo y UnpublishFragments puede fallar para usuarios no administradores.
* SITES-26458: [Modelo de fragmento de contenido de búsqueda] Corrija el filtrado por estado de replicación.
* SITES-23513: [Editor del modelo de fragmento de contenido] La validación falla para la propiedad &quot;Referencia de fragmento&quot; - &quot;Modelo de fragmento de contenido permitido&quot;.
* SITES-26575: la cancelación de la publicación de un fragmento de la vista previa debe actualizar el previewStatus.
* SITES-26571: las referencias de página no se pueden guardar cuando FT_SITES-12435 está habilitado.
* SITES-26660: la comparación de versiones de fragmentos de contenido puede romperse cuando el @ContentType es del tipo &quot;cadena&quot;.
* SITES-26626: falta customErrorMessage en los campos numéricos y booleanos.
* SITES-26268: Se ha devuelto un código de estado incorrecto si una referencia no es válida al crear un fragmento.

### Problemas conocidos {#known-issues-19352}

Ninguna.

### Características y API obsoletas {#deprecated-19352}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-19352}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 36 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-19352}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.72.0 | [API Oak 1.72.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.72.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.24-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.27.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
