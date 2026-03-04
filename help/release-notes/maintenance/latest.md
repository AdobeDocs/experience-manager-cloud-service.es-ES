---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 4b05f571904384521b79dbaf0fa5f4a3a75fef2b
workflow-type: tm+mt
source-wordcount: '1561'
ht-degree: 13%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 24678 {#release-24678}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 24678, publicada el jueves, 04 de marzo de 2026. La versión de mantenimiento anterior fue la 24464.

La activación de funcionalidades 2026.3.0 proporcionará el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-24678}

* FORMS-18927: se ha agregado compatibilidad con tipos MIME personalizados y extensiones de archivo en el componente Archivo adjunto de AEM Forms, lo que permite a los usuarios adjuntar una variedad más amplia de tipos de documentos.
* FORMS-18211, FORMS-22936: Los usuarios experimentaron un problema de accesibilidad en el cual las casillas de verificación no se agrupaban correctamente dentro de un elemento `<fieldset>`, con la etiqueta de grupo no anidada en un elemento `<legend>` como primer elemento secundario. Esto afectaba a los usuarios con discapacidades que dependían de los lectores de pantalla para la navegación. Los componentes principales basados en Forms adaptable ahora han introducido la compatibilidad con conjuntos de campos y leyendas para proporcionar una mejor compatibilidad de accesibilidad.
Se ha agregado la opción Conjunto de campos en el panel que permite a los usuarios organizar y agrupar los campos relacionados de forma más eficaz en sus formularios.
* FORMS-23880: se ha agregado compatibilidad con el editor de temáticas en los componentes principales. Esta mejora permite a los usuarios personalizar y administrar los temas de forma más eficaz dentro de los componentes principales, lo que mejora su flexibilidad de diseño y flujo de trabajo.
* FORMS-21772: se ha agregado compatibilidad con versiones a la IU de administración de Forms. Esta mejora permite a los usuarios crear y recuperar versiones para componentes principales basados en y en componentes básicos como Forms adaptable, fragmentos de formulario, temas y Assets binario, lo que mejora la administración de recursos y el control de versiones.
* FORMS-23094: se ha agregado análisis del lado del cliente para Forms adaptable basado en componentes de base, lo que permite a los clientes empresariales migrar sus formularios a la nube. Esta mejora admite funciones de EcmaScript en las reglas del editor de código, que anteriormente no eran compatibles, lo que facilita un proceso de migración más fluido.
* FORMS-23853: se ha agregado compatibilidad para anular reCAPTCHA en el componente sling. Esta mejora permite a los usuarios personalizar la configuración de reCAPTCHA, lo que mejora la flexibilidad y seguridad para los clientes empresariales.
* SITES-34936: Edge Delivery con editor universal: agregue fragmentos de contenido de filtrado por modelo para la publicación.
* SITES-36203: Edge Delivery con editor universal: agregue el código de alternancia para habilitar la compatibilidad con varios campos y campos múltiples compuestos.
* SITES-37037: Edge Delivery con editor universal: mejore la importación de hojas de cálculo para detectar el delimitador automáticamente.
* SITES-37804: Edge Delivery con editor universal: Agregue compatibilidad para la creación de grupos de usuarios cerrados (acceso anticipado).
* SITES-38990: Edge Delivery con editor universal: agregue compatibilidad para exclusiones en asignaciones de rutas.
* SITES-39171: Edge Delivery con editor universal: agregar compatibilidad con `cq:tags` en bloques y elementos de bloque.
* SITES-40042: Edge Delivery con el editor universal: convierta el servicio de configuración en el predeterminado para los nuevos sitios.
* SITES-37649: GraphQL: admite el filtrado de campos de texto multilínea en el nivel JCR.
* SITES-37843: GraphQL: El filtrado para campos multivalor (colecciones) no es compatible con el nivel JCR.
* SITES-37540: Replace y replaceAll operaciones para valores de campo CF (buscar y reemplazar para un nombre de campo determinado).
* SITES-37741: agregue la propiedad &quot;tarjeta&quot; en obtener respuesta de variación de fragmento (vista de tarjeta en la IU del administrador).
* SITES-37754: Publicar carpeta mediante API: validación de árbol bajo demanda cuando `validateReferences` está establecido en verdadero.
* SITES-37756: muestra la información de estado de protección y desprotección de un fragmento de contenido.
* SITES-37805: Actualización del esquema: los fragmentos MODIFICADOS no se pueden mover ni cambiar de nombre (documentación).
* SITES-37847: rendimiento mejorado para la consulta del proveedor de referencia de contenido prestado SQL-2 (recuperación de contenido prestado).
* SITES-39255: actualice la implementación de OpenAPI a los cambios recientes de la API de Java para el campo compuesto.
* SITES-37096: elimina la lentitud de la consola Lanzamientos cuando hay nodos huérfanos.
* SITES-38117: Encuentre una forma de consultar lanzamientos secundarios sin afectar al rendimiento.
* SITES-38317: agregue el usuario que inició el flujo de trabajo a los metadatos (usuario real en lugar de genérico cuando lo ejecuta el usuario del servicio).
* SITES-39203: muestra el usuario que inició el flujo de trabajo (en lugar del usuario genérico cuando lo ejecuta el usuario de servicio).
* SITES-13083: Localice las cadenas de error en el cuadro de diálogo Sitios > Creación de Live Copy.
* SITES-13389: localice la cadena &quot;Versión creada de... antes de promocionar el lanzamiento&quot; en Sites > Cronología.
* SITES-16176: localice cadenas en el cuadro de diálogo de configuración del componente Editor de páginas > Imagen v3.
* SITES-35702: cadena &quot;Live Copy actualizada con herencia limitada&quot; sin localizar en la pestaña &quot;Información general de Live Copy&quot;.
* SITES-35748: etiqueta de casilla de verificación &quot;Habilitar selección de variante de producto&quot; no localizada en el Editor del modelo de fragmentos de contenido.
* SITES-35750: marcador de posición &quot;SKU de producto&quot; sin localizar separado por `#` carácter&quot; en el campo de entrada en &quot;Editor del modelo de fragmentos de contenido&quot;.
* SITES-37113: cuadro de diálogo &quot;Cancelar herencia&quot; no localizado en la pestaña &quot;Configuraciones de CIF&quot;.
* SITES-25240: corrección de accesibilidad para el call to action modal de teaser.
* SITES-25531: corrección de accesibilidad para el contraste de color en el modo de búsqueda.
* SITES-37115: Iconos truncados en la tienda de demostración de Vienia.

### Problemas solucionados {#fixed-issues-24678}

* CQ-4361552: se ha corregido el diccionario JSON de i18n que retenía el Unicode escapado de HTML en las traducciones importadas.
* CQ-4361634: los fragmentos de experiencia fijos no se pueden seleccionar o no se agregan al proyecto de traducción.
* CQ-4362072: Se ha corregido el flujo de trabajo de traducción de AEMaaCS - DE > El paso ES no puede agregar una página al proyecto de traducción.
* FORMS-23741: Los usuarios experimentaron problemas en los que los pasos de carga de InvokeDDX y Asset no se ejecutaban en cascada, lo que requería dos ejecuciones de flujo de trabajo independientes. Esto afectó al entorno de producción al utilizar AEM as a Cloud Service con el complemento Sites and Forms.
* FORMS-23877: Los usuarios experimentaron problemas con las funciones personalizadas que no se cargaban en tiempo de ejecución al crear formularios directamente en las páginas de Sites mediante una versión anterior de los componentes principales.
* FORMS-24038: Los usuarios experimentaban problemas con el botón de navegación cuando se añadían más pestañas dinámicamente.
* FORMS-23721: se ha corregido un problema por el que los patrones de validación configurados para las entradas de texto en el cuadro de diálogo de edición no persistían. Anteriormente, el valor del patrón se guardaba, pero no se conservaba ni se mostraba en la interfaz de usuario, lo que resultaba en confusión para los autores de formularios.
* FORMS-23456: Los usuarios experimentaban anuncios erróneos de lectores de pantalla en dispositivos móviles para filas de encabezado ocultas en una tabla al utilizar el componente Tabla en Forms adaptable. Se anunció un encabezado de tabla oculto fuera de contexto, lo que causó confusión a los usuarios que dependen de iOS VoiceOver y Android TalkBack.
* FORMS-23454: Los usuarios experimentaron problemas con el selector de fechas para componentes principales basados en Forms adaptable. Al introducir fechas no válidas, el sistema corregiría automáticamente para cerrar las posibles fechas.
* FORMS-23117: Los usuarios experimentaron que Captcha no se traducía correctamente en componentes de base basados en Forms adaptable.
* FORMS-22634: Los usuarios experimentaron un problema por el que los archivos adjuntos del correo electrónico no se incluían cuando las opciones &quot;Incluir datos adjuntos&quot; y &quot;Usar plantilla de HTML&quot; se utilizaban juntas.
* FORMS-23288: Los usuarios han experimentado problemas con el Forms adaptable incrustado en los modelos Asset Share Commons. El formulario no se pudo cargar correctamente cuando la dirección URL contenía `.html` en la ruta intermedia.
* FORMS-19198: Los usuarios experimentaron errores 404 al incrustar formularios mediante reglas de Dispatcher. Se han producido errores en direcciones URL como /etc.clientlibs/toggles.json, rum library y analyticsparserconfigparser.json, debido a que el reescritor de URL no puede reescribir estas direcciones URL.
* SITES-33799: Edge Delivery con editor universal: corrija la representación de vídeo optimizada no publicada.
* SITES-35082: Edge Delivery con el editor universal: elimina los párrafos vacíos, los saltos de línea iniciales y finales de los textos enriquecidos.
* SITES-35524: Edge Delivery con editor universal: corrija los errores de publicación de las rutas que contienen caracteres especiales no ASCII.
* SITES-38647: Edge Delivery con el editor universal: corrija los cuellos de botella de rendimiento en entornos con muchos sitios.
* SITES-40521: Edge Delivery con el editor universal: corrija los nombres de clase duplicados para bloques y elementos de bloque.
* SITES-37887: GraphQL: Las búsquedas de UUID para conjuntos de resultados más grandes pueden causar un aumento de los tiempos de respuesta.
* SITES-38412: no se pueden aplicar parches a los fragmentos en Launch cuando existen campos/slug únicos (la restricción única ahora excluye los CF en lanzamientos).
* SITES-38606: Error de validación al añadir una variación a CF con UUID de referencia de fragmento (hidrate los CF a los que hace referencia uuid en variaciones).
* SITES-39489: la interfaz de usuario de Assets muestra fragmentos de carpetas cq:discarded (los archivos CF eliminados de forma suave se han eliminado de las respuestas de la API de administración).
* SITES-39517: GET CF con un campo compuesto que contiene una enumeración falla con el error 500.
* SITES-40072: los campos compuestos con pestañas devuelven valores de marcador de posición vacíos.
* SITES-39575: al guardar Live Copy, se elimina `cq:rolloutConfigs`: se ha perdido la configuración de despliegue.
* SITES-39694: Despliegues de producción fallidos con NPE.
* SITES-39761: NavigationItem.getLink() devuelve nulo en el componente de navegación de CIF v2.
* SITES-40519: el despliegue de MSM falla con NullPointerException cuando el recurso de destino de Live Copy es nulo.
* SITES-17531: cadena codificada &quot;Vista previa de recorte inteligente&quot; en Editor de páginas > Imagen > Recorte inteligente.
* SITES-31575: la información del objeto no es totalmente visible en Editor de páginas > Componente de carrusel > Propiedades.
* SITES-34215: el componente JS autocompletado genera un error de validación inmediato en el campo de ruta requerido en la pestaña del cuadro de diálogo.
* SITES-35218: Algunos componentes principales de AEM no representan correctamente la etiqueta alt vacía.
* SITES-37114: Información sobre la herramienta &quot;Habilitar compatibilidad con UID de catálogo&quot; truncada en la pestaña &quot;Configuraciones de CIF&quot;.
* SITES-36138: consulta sin índice detectado (incidente).
* SITES-37682: anulación de tipo de contenido en `/libs/cq/Page/Page.css.jsp` y `/libs/cq/Page/Page.js.jsp.`
* SITES-38709: El RTE de texto de la IU clásica muestra el HTML sin procesar después de la actualización a 6.5.24.
* SITES-39630: Las actualizaciones de fragmentos de contenido anidadas no se reflejan en las ofertas de Target exportadas.
* SITES-39696: el tiempo de activación/desactivación para programar la activación/desactivación no funciona.
* SITES-39824: La exportación de fragmentos de experiencias a Adobe Target devuelve 500 (NPE).
* SITES-40253: 500 errores intermitentes en `/bin/cif/invalidate-cache` - Conflictos de Oak en `/var/cif/cacheinvalidation`.
* SITES-40341: corrija imágenes en línea base64 en la etiqueta de estilos en `HtmlToJsonConvertorImpl`.

### Problemas conocidos {#known-issues-24678}

Ninguna.

### Características y API obsoletas {#deprecated-24678}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-24678}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 15 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-24678}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.90.0 | [API de Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.30.4 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

