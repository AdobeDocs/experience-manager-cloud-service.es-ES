---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 0f16c31a5fea1fc538fbeabe6db182ad3a30560d
workflow-type: tm+mt
source-wordcount: '1619'
ht-degree: 13%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 21772 {#21772}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 21772, que se publicó el jueves, 06 de agosto de 2025. La versión de mantenimiento anterior fue la 21706.

La activación de funcionalidades 2025.8.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Nuevas funciones  {#new-features-21772}

* SITES-30049: se ha agregado un nuevo punto de conexión para recuperar las copias de idioma de un fragmento de contenido mediante su UUID.

### Mejoras {#enhancements-21772}

* CQ-4358722 : Problemas de localización resueltos causados por diferentes códigos de configuración regional entre Java 11 y Java 17.
* FORMS-19624: Habilitación de las comunicaciones interactivas (CI). Permite a las organizaciones ofrecer comunicaciones personalizadas bajo demanda, como extractos, facturas y correspondencia, combinando plantillas estructuradas con datos dinámicos. Con funciones como el diseño de plantillas basadas en la web, fragmentos de contenido reutilizables, variaciones basadas en reglas e integración de datos perfecta, la CI permite comunicaciones de clientes coherentes y escalables entre canales.
* FORMS-19587, FORMS-17107, FORMS-19591, FORMS-19582, FORMS-20129, FORMS-20002, FORMS-19593, FORMS-20655, FORMS-19583, FORMS-18024, FORMS-19581: Se han realizado las siguientes mejoras en el editor de reglas de Forms adaptable:
   * El método `validate` de la lista de funciones ahora puede validar paneles, campos y formularios.
   * Se ha mejorado el análisis de funciones personalizadas del lado del cliente para admitir funciones ES10+ e importaciones estáticas.
   * Se ha agregado el botón &quot;Descargar documento de registro (DoR)&quot; predeterminado (OOTB) en el editor de reglas.
   * Se ha agregado compatibilidad con variables dinámicas dentro de reglas.
   * Se ha habilitado la creación de reglas basadas en eventos personalizados.
   * Las reglas para paneles repetibles ahora se ejecutan en el contexto correcto, en lugar de solo en la última instancia del panel.
   * Ahora, las reglas se pueden activar en función de parámetros de consulta, parámetros de UTM y parámetros de explorador.
   * Se ha agregado compatibilidad con scripts de funciones personalizadas específicos de formularios en EDS (almacén de datos de Experience).
   * Se agregó compatibilidad para usar `EVENT_PAYLOAD` en la acción &quot;Navegar a&quot; dentro del controlador de éxito del editor de reglas.
   * Llamadas de función compatibles dentro de parámetros de entrada en el editor de reglas y reglas garantizadas que no se guardan si falta algún parámetro requerido en la llamada de función.
   * Se han resaltado las reglas rotas en la IU del editor de reglas.
* FORMS-18450: reCAPTCHA V2 (incluido el reCAPTCHA invisible) ahora es más fácil de configurar y utilizar en Forms adaptable. La configuración ahora se administra en un solo lugar, lo que facilita la activación de la protección contra correo no deseado en los formularios.
* FORMS-18385: se ha agregado compatibilidad con la generación de AFP a partir de XDP y datos en AEM Forms a través del servicio Output.
* FORMS-17789: se ha agregado un botón predeterminado en el editor de reglas para descargar el documento de registro (DoR).
* FORMS-20313, FORMS-2896: se ha agregado compatibilidad con la propiedad `dorExclude` para deshabilitar características específicas en los formularios principales basados en componentes.
* FORMS-20262: archivos adjuntos no válidos administrados (0 bytes) en el lado del cliente.
* FORMS-18347: se ha mejorado el registro del editor de Forms adaptable para los componentes proxy del contenedor de formularios que faltan.
* FORMS-16205: excluye los componentes deshabilitados del documento de registro (DoR) en los formularios basados en componentes principales.
* FORMS-10836: se ha cambiado la orientación de las propiedades de la página maestra en el documento de registro (DoR) para los idiomas de derecha a izquierda.
* SITES-33025: abre un nuevo editor CF a través de un ID en lugar de una ruta.
* SITES-32741: Déclencheur de la actualización de las referencias de página de fragmento de contenido de forma asíncrona.
* SITES-32087: GraphQL: Agregar compatibilidad con `_ignoreCase` en StringArray.
* SITES-12211: rendimiento mejorado en el editor de plantillas
* SITES-32861: Mejora del rendimiento para la creación de Live Copy mediante el procesamiento fragmentado.
* SITES-21383: Optimización del rendimiento para operaciones de eliminación del inicio de fragmentos de contenido.
* SITES-31165: Mejora del rendimiento al dividir las operaciones de despliegue en fragmentos manejables.
* SITES-21353: mejora del rendimiento de las consultas para inicios de fragmentos de contenido mediante la indexación de bases de datos.
* SITES-30495: Mejora para admitir referencias de fragmento basadas en UUID en los lanzamientos de fragmentos de contenido.
* SITES-32151: Mejora de la API que expone la funcionalidad de la propiedad del contenedor.
* SITES-26849: ajustar las referencias secundarias cuando se mueve o elimina una variación de fragmento de contenido.
* SITES-31846: agregue la opción para copiar/pegar el fragmento raíz y las referencias en la misma carpeta para la operación de copiar árbol.
* SITES-30241: ajusta las referencias ubicadas dentro de un campo de texto largo al mover, cambiar el nombre o eliminar un fragmento.
* SITES-32684: mejora del mecanismo para sincronizar los cambios de pestañas en el esquema de la interfaz de usuario.
* SITES-33308: agregue el mecanismo de reintento para sincronizar cambios en el esquema de la interfaz de usuario al editar modelos.
* SITES-32247: Falta la desalineación del cuadro de diálogo Personalization e IU en el componente &quot;Texto y Personalization&quot;.
* SITES-32261: Fragmento de experiencia i18n no aplicado al campo.
* SITES-32666: el predicado de plantilla contiene `\n`, lo que provoca que la búsqueda de HTML falle.
* SITES-32674: El selector de imágenes de campo de imagen destacado no funciona para el asistente de creación de páginas a pesar de `cq:showOnCreate`.
* SITES-32014: Edge Delivery con editor universal: agregue la configuración automática de las políticas CORS para localhost, aem.page y aem.live
* SITES-26532: Edge Delivery con editor universal: agregue compatibilidad con URL localizadas (acceso anticipado).
* SITES-30887: agregue los uuid de fragmento de contenido almacenados en los metadatos del flujo de trabajo.

### Problemas solucionados {#fixed-issues-21772}

* CQ-4360190: se corrigió `UnsupportedOperationException` que se producía al intentar utilizar agregar un keySet que no admite la operación.
* CQ-4360421: se ha solucionado un problema con el cifrado de claves de suscripción de Microsoft Translator para mejorar la seguridad y la compatibilidad.
* FORMS-20980: se han corregido problemas de accesibilidad del teclado en el Selector de fechas con formato de visualización personalizado en Forms adaptable.
* FORMS-20498: Se ha agregado una comprobación de excepciones de puntero nulo en OdataResponse para evitar errores de tiempo de ejecución.
* FORMS-20947: se han solucionado varios problemas de accesibilidad, incluidas infracciones del lector de pantalla y problemas de truncamiento/superposición de texto.
* FORMS-21030, FORMS-20630: Se han resuelto problemas con campos desplegables configurados para varias selecciones en formularios adaptables. La PDF generada ahora incluye correctamente todos los valores seleccionados.
* FORMS-19579: se ha corregido un problema por el que la regla de servicio Invocar no se corregía automáticamente al volver a guardar.
* FORMS-20734: se ha corregido la duplicación de campos de firma en documentos de PDF generados por el servicio Output para plantillas de PDF de entrada basadas en XFAF.
* FORMS-20934: se ha corregido el menú desplegable Atributo de relleno automático de la interfaz de usuario de creación de AEM Forms para eliminar las entradas duplicadas e incluir todos los tokens de autocompletar estándar de HTML.
* FORMS-20700: se ha resuelto el parpadeo del texto de ayuda desplegable en la carga inicial en AEM Forms.
* FORMS-20307: se ha corregido el problema que causaba que los formularios incrustados en una página de sitio no se tradujeran con configuraciones regionales de 4 caracteres.
* FORMS-20493: se ha solucionado el problema que causaba que los formularios se actualizaran automáticamente cuando se recuperaban datos de, lo que causaba molestias al usuario.
* FORMS-18455: se ha mejorado el Editor de Forms adaptable para componentes principales para mostrar puntos para objetos de datos utilizados en el árbol de fuentes de datos.
* FORMS-19373: se evitaron errores de replicación en entornos de publicación que no tenían ningún agente de replicación configurado.
* FORMS-20042: se ha corregido la vista de propiedades dañada causada por la configuración del servlet de Apache Sling GET con la configuración de HTML habilitada.
* FORMS-20036, FORMS-19978: Se han corregido los problemas de conformidad y validación de PDF/A-1b.
* FORMS-19166: se ha movido pagedatasource.jsp al servlet para mejorar la claridad del seguimiento de la pila de errores y se han agregado más protecciones y registros.
* FORMS-16466: se han corregido problemas con los paneles repetibles que no se rellenaban correctamente en AEM Forms.
* FORMS-19629: se han solucionado problemas con el análisis del esquema JSON del cliente que proporcionaba resultados no válidos.
* LC-3923083: Error resuelto de &quot;objeto de ruta no etiquetado&quot; para elementos con borde en plantillas XDP.
* SITES-33177: Edge Delivery con editor universal: corrija los estilos de sección rotos cuando se almacenan como cadenas separadas por comas.
* SITES-33262: Edge Delivery con editor universal: corrige bloques sin nombre propiedad salto página procesamiento y publicación.
* SITES-33309: Edge Delivery con editor universal: corregir `IllegalArgumentException` al escribir en una hoja de cálculo con una barra diagonal en las columnas.
* SITES-33408: Edge Delivery con editor universal: corregir Las hojas de cálculo no aparecen como modificadas después de realizar cambios.
* SITES-31992: GraphQL: Corrija los errores esporádicos en el análisis del modelo durante el inicio de los paquetes.
* SITES-29967: GraphiQL: Los nombres de consulta largos se cortan.
* SITES-26266: Las referencias de contenido que no comienzan con `/` no se devuelven desde la respuesta de BE (API de Java).
* SITES-17874: GraphQL persisted queries: Corrija la codificación para el tipo de contenido application/graphql-response+json.
* SITES-24506: lectores de pantalla informados sobre los resultados de búsqueda.
* SITES-25268: mejoras en el lector de pantalla para anotaciones.
* SITES-32366: resultados de la revisión ortográfica ocultos detrás del cuadro de diálogo RTE.
* SITES-32829: mejoras del emulador MediaQuery para analizar los niveles de consulta de medios 3 y 4.
* SITES-32278: los campos de etiqueta se han corregido para utilizar correctamente la etiqueta de campo.
* SITES-25244: la barra horizontal ya no aparece en el modo de imagen.
* SITES-33395: se ha corregido la funcionalidad de botón de despliegue para la sincronización de Live Copy de fragmentos de contenido.
* SITES-33147: se ha corregido un problema de enlace de servicio que afectaba a la funcionalidad de la relación activa.
* SITES-33528: se ha corregido un problema de preservación de marca de hora durante la promoción de lanzamiento.
* SITES-33014: se corrigió una generación excesiva de registros de advertencia desde LaunchesAdapterFactory.
* SITES-32305: se ha corregido la funcionalidad de interrupción de herencia de Live Copy después de cambios de diseño.
* SITES-32268: deshabilitar la codificación de URL para la búsqueda de fragmentos de contenido.
* SITES-32772: la propiedad bloqueada en los campos de la variación siempre era falsa al habilitar las mejoras de SITES-31455 relacionadas con la unificación del valor de etiqueta.
* SITES-32696: se ha corregido un problema que se producía cuando un campo de Live Copy de fragmento de contenido con herencia dañada no se podía editar más.
* SITES-31712: Consultas lentas desde Omni-search en prod Author.
* SITES-33039: Los eventos de página no se activan correctamente.
* SITES-31192: los fragmentos de experiencia pierden el historial de versiones después de moverse.
* SITES-33529: Error al vincular las plantillas de campaña de ACS con páginas de AEM.
* SITES-33678: Agregar alternancia para SITES-33529.
* SITES-33468: AEMaaCS no puede conectarse a ACS.

### Funcionalidad modificada {#altered-functionality-21772}

* SITES-26344: unifique la validación de `fragmentId`/`modelId` entre extremos; estos identificadores ahora se validan y se devuelve un código de estado 400 si no son válidos.
* SITES-29598: Validar referencias de fragmento de contenido agregadas en campos de referencia de fragmento al actualizar un modelo de fragmento de contenido.

### Problemas conocidos {#known-issues-21772}

* SITES-31791: Fragmentos de contenido GraphQL: error de consulta con &quot;Se ha superado el recuento máximo de campos&quot;. Consulte [Artículo de la base de conocimiento](https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27231).

### Características y API obsoletas {#deprecated-21772}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-21772}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 35 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.


### Tecnologías integradas {#embedded-tech-21772}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.80.0 | [API Oak 1.80.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.80/index.html?lang=es) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.63 | [Apache Httpd 2.4.63](https://github.com/apache/httpd/blob/2.4.63/CHANGES) |
| Componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |

