---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: a8651a44300772b5c9706a5fd85e7fefef72e47d
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 12%

---

# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 14227 {#release-14227}

A continuación se resumen las mejoras continuas para la 14227 de la versión de mantenimiento, que se publicó el 9 de noviembre de 2023. Esta versión de mantenimiento es una actualización de la versión de mantenimiento 14029 anterior. La 14227 de la versión de mantenimiento sustituye a la 14157 para corregir un problema.

La activación de funciones 2023.11.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información.

### Mejoras {#enhancements-14227}

* ASSETS-29631: Assets Cloud: Utilice dam:roles para una entrega/búsqueda segura.
* CQ-4354515: Translations: Opción para suprimir la traducción de recursos a los que se hace referencia.
* FORMS-9993: Defina los pasos para mover los componentes principales de Forms a Skyline.
* FORMS-10570: Incorporar API de EC a API: primer enrutador.
* GRANITE-48143: actualizar Sling ResourceMerger a 1.4.4.
* SITES-14874: Eventing: expanda el árbol CFM para que los eventos de modelo incluyan cambios en los metadatos.
* SITES-2719: Fragmentos de contenido: Compatibilidad de etiquetado para variaciones de fragmentos de contenido (reactivada).
* SITES-3619: Fragmentos de contenido: etiquetas de variación CF de GraphQL salida en JSON y filtrado por etiqueta de variación (reactivada).
* SITES-13750: Fragmentos de contenido: elimina las etiquetas de un modelo de fragmento de contenido.
* SITES-13920: Fragmentos de contenido: Compatibilidad con la configuración minItems para varios campos (versión previa).
* SITES-14080: Fragmentos de contenido: Eliminar la etiqueta de una variación de fragmento de contenido.
* SITES-14770: Fragmentos de contenido: la variación del fragmento debe incluir la propiedad fieldTags.
* SITES-15356: Fragmentos de contenido: Devolver la etiqueta como encabezado de respuesta cuando se crea un recurso.
* SITES-15357: Fragmentos de contenido: permitir la publicación de fragmentos sin sus referencias.
* SITES-15938: Fragmentos de contenido: faltan metadatos de referencia de contenido.
* SITES-16078: Fragmentos de contenido: rellene la propiedad de resultado de validación de la variación cuando se recupere un fragmento.
* SITES-16545: Fragmentos de contenido: agregue un punto final para recuperar las referencias de la variación de un fragmento de contenido.
* SITES-16853: Fragmentos de contenido: Eliminar /adobe/sites/cf/fragments/{fragmentId}/variation/{name}Extremo /tags.

### Problemas corregidos {#fixed-issues-14227}

* Se han corregido varios problemas de accesibilidad
* ASSETS-31015: no se pueden cargar archivos en Assets con extensiones de archivo desconocidas.
* ASSETS-24739: deshabilitar el punto final de acción personalizada Frame.io en la publicación.
* CMGR-49845: Reflujo de contenido: Problema con la identificación de la ruta raíz correcta para un punto de comprobación determinado.
* CMGR-49709: Reflujo de contenido: actualice el filtro de propiedades para ignorar propiedades adicionales.
* CQ-4354503: la configuración de Adobe IMS se elimina aleatoriamente.
* CQ-4354414: ConfigurationReplicationEventHandler crea muchas acciones de vaciado individuales.
* CQ-4354401: Traducciones: el recurso creado por Proyectos debe guardarse antes de iniciar el procesamiento de recursos.
* CQ-4354430: Traducciones: Se ha producido un error al añadir recursos que no forman parte de una estructura de carpetas de idioma a un proyecto de traducción.
* CQ-4354412: Traducciones: al eliminar el contenido del trabajo de traducción, no se elimina todo el contenido referenciado.
* CQ-4354636: Translations: La creación de una copia de idioma en el nivel raíz del idioma no ajusta las rutas en la página.
* CQ-4354700: Workflows: La pantalla de carga útil del flujo de trabajo no se carga.
* CQ-4354834: Workflows: no se puede añadir un comentario en la tarea de bandeja de entrada del flujo de trabajo.
* FORMS-11302: El título del componente editado en RTE se muestra incorrectamente en el Editor de formularios adaptables > Editor de reglas.
* GRANITE-45706: La importación de i18n falla si el valor clave tiene (&quot;Äú)) FLORES.
* SITES-14156: Eventos: Los eventos de publicación no siempre se envían.
* SITES-14520: GraphQL: mal rendimiento con consultas de graphql paginadas debido a FT_SITES-2719.
* SITES-16444: GraphQL: DataFetchingException para campos del mismo nombre que no aparecen en la consulta de GraphQL.
* SITES-16225: GraphQL: Los tipos de contenido de los campos RTE de modelo y fragmento devueltos por la API de Java no son correctos.
* SITES-15373: Fragmentos de contenido: /adobe/sites/cf/fragments/{fragmentId}/variation/{name}El extremo /tags no utiliza las convenciones de nomenclatura de recursos correctas.
* SITES-15709: Fragmentos de contenido: Crear problema de extremo de modelo al crear un campo booleano.
* SITES-15727: Fragmentos de contenido: el campo de tipo &quot;Etiqueta&quot; solo se puede añadir una vez en el editor de modelos.
* SITES-15782: Fragmentos de contenido: falta una propiedad única del modelo de campo del tipo Lista desglosada.
* SITES-15786: Fragmentos de contenido: El fragmento de contenido no se puede crear en una carpeta que contenga &quot;.
* SITES-15790: Fragmentos de contenido: Actualizar encabezado de ubicación para la creación de versiones.
* SITES-15923: Fragmentos de contenido: El administrador de CF no muestra todas las carpetas.
* SITES-15987: Fragmentos de contenido: obteniendo 500 al crear una variante.
* SITES-16067: Fragmentos de contenido: No se puede modificar el tipo MIME del campo de fragmento de texto largo.
* SITES-16074: Fragmentos de contenido: Etiquete campos que no sean de cadena[] no se puede recuperar de JCR.
* SITES-16079: Fragmentos de contenido: /fragments/{id}/references ha comenzado a devolver duplicados.
* SITES-16118: Fragmentos de contenido: si se aplica un parche a un fragmento y falta un campo de fragmento en el modelo, se genera una excepción.
* SITES-16119: Fragmentos de contenido: si los metadatos del fragmento contienen campos no reconocidos, se genera una excepción.
* SITES-16121: Fragmentos de contenido: la recuperación de un campo de fecha de modelo genera una excepción.
* SITES-16123: Fragmentos de contenido: Si un recurso no es un fragmento de contenido, el extremo de obtener fragmentos genera una excepción.
* SITES-16208: Fragmentos de contenido: ContentFragmentModelIdentifier expone una propiedad de título engañosa.
* SITES-16707: Fragmentos de contenido: Los tipos de datos de los modelos de fragmentos de contenido no se leen correctamente.
* SITES-16818: Fragmentos de contenido: realice la eliminación solo cuando haya etiquetas.
* SITES-16207: Fragmentos de contenido: La operación POST /adobe/sites/cf/models devuelve dos códigos de estado OK diferentes.
* SITES-15616: Fragmentos de contenido: El extremo de publicación no publica a veces todas las referencias de un fragmento de contenido.
* SITES-16027: Fragmentos de contenido: falta información de referencia de variación en la respuesta del fragmento.
* SITES-16243: Fragmentos de contenido: Buscar y reemplazar no funciona con campos que tienen Procesar como: Múltiple.
* SITES-16250: Fragmentos de contenido: Al aplicar parches a un CF, a veces se devuelve un encabezado de etiqueta incorrecto.
* SITES-16686: Fragmentos de contenido: las referencias no fragmentos de fragmentos de contenido se serializan cuando la referencia principal está en la profundidad máxima.
* SITES-12880: Fast-Track: solución de localización para Sites > Configuración de Analytics.
* SITES-16103: Fragmentos de experiencias: Las opciones de Target no se muestran en Cloud Service debido a un error de la consola.
* SITES-16001: MSM: capacidad para excluir componentes de varios campos de la configuración de despliegue al crear Live Copy.
* SITES-16559: MSM: Las configuraciones de despliegue se eliminan durante el proceso de despliegue de los fragmentos de experiencias.
* SITES-16797: MSM: se ha corregido la reactivación de la herencia para un campo CF en el Editor.
* SITES-16273: Editor de páginas: error de copia y pegado dentro de páginas de aem sites desde el portapapeles.
* SITES-16126: Administrador de sitios: el rendimiento de la creación es lento para los usuarios que no son administradores después de SITES-10288.
* FORMS-10534: Se produce un error en el editor de reglas al seleccionar la opción de operando booleano.
* FORMS-10248: en un formulario adaptable, cuando el valor de los datos es de tipo booleano, las reglas no establecen correctamente los valores de los botones de opción o los componentes de casilla de verificación.
* FORMS-11361: El componente desplegable toma como valor predeterminado automáticamente la selección de la primera opción de la lista.
* FORMS-11413: un error relacionado con el servicio de relleno previo del portal de Forms se activa mediante Forms adaptable, incluso cuando el servicio no está en uso.
* FORMS-11433: Cuando se incluye un componente que no es de formulario en un formulario adaptable, el proceso de envío no se completa.
* FORMS-11206: Cuando un usuario intenta programar un flujo de trabajo de publicación para un formulario adaptable, no funciona como se espera.
* FORMS-11546: Lighthouse ha detectado una etiqueta ARIA que falta para los paneles repetidos en un formulario adaptable, lo que afecta a la accesibilidad.
* FORMS-11095: el atributo ARIA se define incorrectamente para los campos de número de teléfono, dirección de correo electrónico y número, lo que provoca problemas de accesibilidad.

### Problemas conocidos {#known-issues-14227}

Ninguna.

### Tecnologías integradas {#embedded-tech-14227}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM OAK | 1,56-T20230927085643-189caed | [API Oak 1.56.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.56.0/index.html) |
| API AEM SLING | Versión 2.27.2 | [API de Apache Sling 2.27.2 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | Versión 1.4.20-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | Versión 2.23.4 | [Componentes principales de WCM de AEM](https://github.com/adobe/aem-core-wcm-components) |
