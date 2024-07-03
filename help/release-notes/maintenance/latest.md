---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 9303ecadea38d83bd71ed0d440067bae5c419940
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 20%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 16971 {#release-16971}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 16971, que se publicó el jueves, 03 de julio de 2024. La versión de mantenimiento anterior fue la 16799.

La activación de funcionalidades 2024.7.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-16971}

* AEM SITES-22948: elimina las referencias de comercio en el contenido base para el CSS de la.
* SITES-22141: [Fragmentos de contenido] SegmentNotFoundException de CFM ModelChangeRepositoryImpl después de OnRC.
* SITES-21893: problema con el recorte de imágenes en la instancia de autor.
* SITES-21788: [Fragmentos de contenido] Mostrar NOTA en el editor de modelos CF y CF cuando uiSchema está habilitado para el modelo.
* SITES-21688: El despliegue de MSM no actualiza la ruta del fragmento de experiencia (XF) en las páginas de Live Copy.
* SITES-21659: devuelve el nombre completo del usuario que crea, modifica o replica un recurso de modelo.
* SITES-21609: extremo de OpenAPI para migrar fragmentos de contenido de un modelo a otro.
* SITES-21598: [Abrir API] Crear CFM: error de devolución si la ruta de configuración dada no existe.
* SITES-21491: [Abrir API] El punto final del PATCH de FQ debe respetar las relaciones activas en el nivel de campo.
* SITES-21434: [Abrir API] El punto final de la GET CF debe respetar las relaciones activas en el campo.
* SITES-21415: Editor de CF: admite referencias de UUID.
* SITES-21326: [Abrir API] Proporcionar información sobre la presencia de referencias para un fragmento de contenido.
* SITES-21310: [Abrir API] Añadir ID de fragmento de contenido en la respuesta de la API de traducciones.
* SITES-20859: CF Abrir API: devuelve referencias al recuperar un fragmento por ruta.
* SITES-20687: [Abrir API] Punto final para la recuperación del estado de procesamiento por lotes.
* SITES-20657: [Abrir API] Proporcionar la opción a match palabra completa al reemplazar una cadena mediante `FindAndReplace` punto final.
* SITES-20587: [Abrir API] Crear `COPY` punto final para fragmentos de contenido.
* SITES-20584: [Abrir API] Optimizar la recuperación de referencias.
* SITES-20308: [Abrir API] Habilite el procesamiento por lotes en API.
* SITES-19976: [Abrir API] Esquema de interfaz de usuario genérico para campos condicionales.
* SITES-19556: [Fragmentos de contenido] Actualice uiSchema si existe cuando se edita el modelo.
* SITES-18056: [Abrir API] Al publicar un fragmento de contenido en Vista previa, incluya referencias.
* SITES-16898: [Esquema] Extremo OpenAPI para migrar fragmentos de contenido de un modelo a otro.
* SITES-16609: Extremo de lista de inicios.
* SITES-16606: Crear extremo de Launch.
* SITES-21617: [Xwalk] Hacer que las propiedades y los metadatos de la página sean editables en UE.
* SITES-19614: [Xwalk] Paginación del editor de hojas de cálculo y desplazamiento infinito.
* SITES-22163: [Xwalk] Se ha mejorado la compatibilidad con el contenido servido desde el nivel de publicación para Edge Delivery Sites.
* SITES-22109: [Xwalk] Se ha mejorado el manejo del marcado de texto enriquecido después del procesamiento.
* SITES-22035: [Xwalk] Se ha mejorado el manejo de MSM y los lanzamientos.
* SITES-21839: [Xwalk] Se ha mejorado la asignación de rutas y el saneamiento del contenido que no sirve Edge Delivery.

### Problemas solucionados {#fixed-issues-16971}

* CQ-4356898: [Traducción] Error outOfMemory para CF, que contiene un número inusualmente alto de vínculos.
* CQ-4357055: [Traducción] La traducción automática no funciona con la API de REST.
* CQ-4353931: [Traducción] Añada jcr:uuid en la página de origen de la traducción/xf/asset cuando falte.
* CQ-4357591: [Traducción] Modifique el flujo de trabajo &quot;Asociar JCR:UUID&quot; para que funcione para Pages/XF.
* FORMS-14844: Forms adaptable permite el envío de formularios a pesar de la verificación reCAPTCHA fallida.
* FORMS-14984: Forms con CAPTCHA omite la validación si &quot;submitMetaData&quot; no está presente en los datos enviados.
* FORMS-14477: Las opciones &quot;Después de&quot; e &quot;Antes de&quot; del editor de reglas no funcionan correctamente en la validación del selector de fechas.
* FORMS-14019: La funcionalidad &quot;Invocar servicio&quot; del editor de reglas no funciona en el editor universal.
* FORMS-14336: cuando no se selecciona ningún campo de formulario, el editor debe abrirse enfocado en todo el elemento del formulario.
* FORMS-15061: El círculo de carga persiste indefinidamente al utilizar la opción de invocación del servicio en el editor de reglas.
* SITES-22457: promocionar un lanzamiento que no es profundo no actualiza el contenido de origen.
* SITES-22748: [Fragmentos de contenido] Mejore la administración de errores para el trabajo de actualización de fragmentos de contenido
* SITES-22349: [Fragmentos de contenido] ContentType para elementos cf vacíos de varias líneas no se puede cambiar.
* SITES-22343: [Fragmentos de contenido] La &quot;enumeración&quot; de tipo semántico está dañada.
* SITES-22194: después de configurar la redirección, model.json ya no funciona.
* SITES-21953: [Abrir API] Etag cambia según el orden de validationStatus.
* SITES-21894: [Abrir API] Mejore la validación de rutas principales al crear archivos CF.
* SITES-21887: [Abrir API] ETag no válido devuelto por el extremo de variaciones del POST.
* SITES-21657: [Abrir API] Mejore la validación en la propiedad de ruta de búsqueda CF.
* SITES-21949: El cursor no válido de la API de búsqueda devuelve 500.
* SITES-20927: Las API de búsqueda devuelven un 500 cuando falta la consulta.
* SITES-20544: [Abrir API] Cambie la generación de nombres de paquetes de publicación para evitar conflictos con oak.
* SITES-19710: CVE-2022-47937: elimine todos los usos de org.apache.sling.commons.json del Editor de páginas.
* SITES-11992: [Accesibilidad] Falta un nombre accesible en el botón del selector de muestras de anotación.
* SITES-10979: [Accesibilidad] La etiqueta no es persistente.
* SITES-10962: [Accesibilidad] Botón: el botón no tiene una función.
* SITES-10905: [Accesibilidad] El estado del componente activo carece de una relación de contraste de 3 a 1.
* SITES-2974:  [Accesibilidad] - Desplazamiento horizontal a 320 píxeles de ancho.
* AEM SITES-22026: no se pueden mover fragmentos de experiencias entre carpetas en el modo de trabajo de la
* SITES-22106: problema de funcionalidad del cambio de idioma en el nuevo editor de fragmentos de contenido
* SITES-21980: manejo incoherente de los tipos de referencia basados en UUID.
* SITES-7257: NPE en ThumbnailServlet.

### Problemas conocidos {#known-issues-16971}

Ninguna.

### Aviso de cambio {#change-notice-16971}

* A partir de septiembre de 2024, AEM as a Cloud Service deshabilitará la serialización de los solucionadores de recursos a través del marco de trabajo Exportador de modelos Sling. Consulte la [documentación](/help/implementing/developing/hybrid/disallow-the-serialization-of-resourceresolvers-via-sling-model-exporter.md) para obtener más información.

### Características y API obsoletas {#deprecated-16971}

Para saber qué es lo que está en desuso o se ha eliminado en AEM as a Cloud Service, consulte [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Tecnologías integradas {#embedded-tech-16971}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.64.0 | [API Oak 1.64.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.64.0/index.html) |
| API AEM SLING | 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.22-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.25.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
