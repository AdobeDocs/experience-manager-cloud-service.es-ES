---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 6493c48797c09fa4598c2c0ff86c9cc1fafa758c
workflow-type: tm+mt
source-wordcount: '1448'
ht-degree: 15%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 20783 {#20783}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 20783, que se publicó el miércoles, 13 de mayo de 2025. La versión de mantenimiento anterior fue la 20626.

La activación de funcionalidades 2025.5.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-20783}

* FORMS-19125: El editor del formulario adaptable del componente principal se ha mejorado para admitir la asignación automática de los fragmentos de formulario adaptable disponibles cuando se suelta una sección correspondiente del árbol de fuentes de datos en el lienzo del formulario. Esto lleva una función de productividad clave del editor de bases a los componentes principales.
* FORMS-17107: AEM Forms ahora ofrece análisis de funciones personalizadas mejorados en el lado del cliente. Esto incluye compatibilidad con funciones modernas de JavaScript (ECMAScript ES10+), como el encadenamiento opcional, e introduce la capacidad de utilizar importaciones estáticas en scripts de función personalizados. Esto permite a los desarrolladores organizar mejor el código, utilizar los módulos ESM y eliminar las limitaciones anteriores con funciones personalizadas en Forms adaptable basadas en componentes principales y Edge Delivery Services, especialmente para los usuarios que anteriormente necesitaban soluciones alternativas para estas funciones.
* SITES-27775: búsqueda de referencia optimizada durante la publicación.
* SITES-30885: procesamiento JSON optimizado en consultas persistentes.
* SITES-25433: Edge Delivery con editor universal: admite la representación de páginas completas al comparar versiones antiguas.
* SITES-27792: Edge Delivery con el editor universal: agregue una plantilla específica para las configuraciones del servicio Edge Delivery
* SITES-19754: Edge Delivery con editor universal: mensaje de error convincente cuando se interrumpe la configuración.
* SITES-30328: Edge Delivery con editor universal: vista previa desde el soporte de Sidekick.
* SITES-23499: Edge Delivery con editor universal: permite que se utilicen varios campos para las opciones de bloque.
* SITES-29987: agregue la capacidad para establecer `previewUrlPattern` al crear modelos de fragmento de contenido.
* SITES-29874: Agregue compatibilidad para las referencias de LongTextField en la API de fragmento de contenido.
* SITES-29601: agregue validación para los fragmentos de contenido a los que se hace referencia mediante campos de texto largo.
* SITES-24623: haga que las etiquetas ET devueltas por la API de fragmentos de GET y SEARCH se puedan utilizar para el parche.
* SITES-28557: permitir el parámetro de dirección URL `references` en el fragmento de contenido de PATCH.
* SITES-5358: [OpenAPI] Copiar fragmentos de contenido con elementos secundarios.
* SITES-29614: extremo del flujo de trabajo de GET.
* SITES-29615: Enumerar el extremo de API de solicitudes por lotes.
* SITES-25130: actualizar componentes principales a 2.28.0
* SITES-10575: &quot;MSM Blueprint Bloomfilter Loader&quot; intenta cargar >100 000 filas.
* SITES-26711: los vínculos de los campos de texto RTE no se actualizan para que apunten a la Live Copy en el despliegue de MSM.
* SITES-25976: Los vínculos dentro de los fragmentos de experiencias no se adaptan después del despliegue de MSM.

### Problemas solucionados {#fixed-issues-20783}

* ASSETS-50994: Tráfico entrante bloqueado en AemRequestEventFilter.
* CQ-4358591: faltan proyectos para algunos idiomas cuando se crean copias de idioma desde el panel de referencia de sitios con la opción &quot;Crear proyectos de traducción&quot;.
* CQ-4359108: el formato XLIFF 2.0 está fallando mientras se utiliza la importación/exportación de traducción humana.
* CQ-4358722: la localización no funciona para códigos ISO heredados debido a que hay diferentes códigos de configuración regional en Java 11 y Java 17.
* FORMS-19808: Al guardar un formulario grande que incluye fragmentos habilitados con carga diferida, el usuario no puede extraer los borradores.
* FORMS-19887: Un campo desplegable de un formulario XFA, establecido inicialmente como acceso de solo lectura, no cambia a un estado abierto/editable cuando el formulario se procesa en HTML5. El campo permanece como de solo lectura y evita la interacción del usuario, a diferencia del procesamiento en PDF, donde funciona según lo esperado.
* FORMS-19651: en el Editor de reglas, una regla no funciona correctamente cuando se utiliza un clic en un botón en una condición binaria y el mismo botón también se utiliza en la instrucción &quot;then&quot; de esa regla.
* FORMS-19628: en el documento de registro (DoR) generado automáticamente para Forms adaptable basado en componentes principales, al excluir el título de un panel anidado del DoR también se oculta incorrectamente el título del panel raíz si este tiene habilitada la opción &quot;Permitir texto enriquecido para el título&quot;.
* FORMS-18977: A los PDF generados por el servicio de documento de registro (DoR) les falta el título del documento. Esto puede conllevar un incumplimiento de los estándares de accesibilidad de PDF/UA y WCAG 2.1, ya que el título del documento es un atributo requerido para los PDF accesibles.
* FORMS-18526: Cuando una regla que contiene varios campos en sus condiciones se copia de un campo a otro, una referencia de campo fijo dentro de estas condiciones retiene incorrectamente su referencia al campo de origen original en lugar de actualizar al nuevo campo donde se copia la regla.
* FORMS-19047: Después de modificar y volver a publicar un formulario adaptable en AEM Forms (específicamente 6.5.22.0), es posible que falten traducciones para determinados elementos de formulario, especialmente cuadros de texto.
* FORMS-19234: La función de cronología para archivos PDF en AEM Forms, que permite a los usuarios ver detalles sobre la creación y el control de versiones de un PDF, deja de funcionar después de que se cargue cualquier PDF en la sección &quot;Forms y documentos&quot;.
* FORMS-18196: la API HTTP de sincronización `generatePrintedOutput` (o `generatePdfOutput`) devuelve incorrectamente un código de respuesta 200 (correcto) en lugar del código de error 400 (solicitud incorrecta) esperado cuando los datos de campo opcionales requeridos por la plantilla XDP se dejan vacíos en la solicitud.
* FORMS-19336: En el editor de formularios adaptables del componente principal (editor AF2), la funcionalidad de búsqueda dentro del árbol de Source de datos no funciona correctamente o como se espera, lo que impide que los usuarios encuentren fácilmente elementos de datos específicos.
* FORMS-17707: El conector AEP (Adobe Experience Platform) no funciona correctamente cuando se configura para conectarse a entornos &quot;stage&quot; de la plataforma AEP.
* FORMS-18526: al copiar una regla que tiene condiciones basadas en varios campos, un campo al que se hace referencia dentro de las condiciones o acciones de la regla (que no es el campo principal que activa la regla) no se actualiza para hacer referencia correctamente al nuevo campo al que se copia la regla. En su lugar, sigue haciendo referencia al campo de origen original desde el que se copió la regla.
* FORMS-18474: regla diseñada para establecer el enfoque en un panel o componente específico cuando cambia el valor de un campo en particular (por ejemplo, el campo &quot;A&quot;) se activa incorrectamente por un cambio en cualquier campo del formulario. Por ejemplo, si se modifica el campo &quot;B&quot;, el enfoque sigue establecido en el panel designado, aunque la regla solo se haya configurado para cambios en el campo &quot;A&quot;.
* GRANITE-58276: los ciclos de dependencia OSGi impiden que la fábrica del motor de scripts HTL funcione correctamente.
* OAK-11673: aumento de Oak-segment-azure v12 CPU causado por refreshLease.
* SITES-30752: no utilice encabezados `If-modified-since`/`last-modified` al generar una respuesta de consulta persistente.
* SITES-30353: GraphQL DataFetchingExceptions para el campo &quot;src&quot; en fragmentos de contenido de AEM.
* SITES-30333: lea los metadatos de los recursos de jcr para evitar problemas de análisis de xmp.
* SITES-30140: problema de doble ventana al crear la referencia de fragmento de contenido.
* SITES-29748: corrija las condiciones de procesamiento para mostrar las acciones Administrar publicación/Publicación rápida dentro del editor CF.
* SITES-15452: los elementos CF únicos no deben comprobarse con sus copias en el lanzamiento.
* SITES-30386: Edge Delivery con editor universal: el uso duplicado de cors.js hace que el uso duplicado de secciones al añadir contenido.
* SITES-29745: se ha corregido un problema poco frecuente por el que las variaciones de referencias no se hidrataban.
* SITES-30585: no se puede establecer &#39;previewUrlPattern&#39; al crear modelos con referencias.
* SITES-30327: la publicación de fragmentos de contenido sin permisos crea flujos de trabajo independientes para cada recurso de carga útil.
* SITES-29528: ETag no se puede usar para almacenar en caché en la instancia de publicación.
* SITES-30583: la herramienta Buscar y reemplazar cambia todos los caracteres a minúsculas.
* SITES-31157: el parche falla debido a una ETag incoherente.
* SITES-31327: [OpenAPI] Obtener solicitud de fragmento de contenido en instancia de autor puede responder con 304.
* SITES-29691: NullPointerException cuando se intenta mover la página.
* SITES-30728: OnTime/OffTime no se publica/cancela la publicación como se espera cuando se configura en las propiedades del recurso.
* SITES-29789: cambio en el vínculo del componente en las páginas raíz copiadas en AEM.
* SITES-29191: no se pueden añadir más de 20 SKU al componente de lista de productos.
* SITES-30372: el recorte inteligente no funciona en el componente principal Imagen (V2) de AEM.
* SITES-28693: El componente Teaser procesa el HTML dañado cuando el título está vacío.
* SITES-28668: no se puede promocionar el lanzamiento con LaunchPromotionParameters.
* SITES-31005: mejore la interfaz de usuario del trabajo de despliegue para mostrar al cliente el progreso.
* SITES-31020: mejora la interfaz de usuario del trabajo de creación de Live Copy para mostrar al cliente el progreso.
* SITES-29816: Error &quot;Recurso no encontrado&quot; al crear la Live Copy del fragmento de experiencia.
* SITES-29363: el botón Restablecer Live Copy no funciona para la jerarquía de contenido de Live Copy anidada.
* SKYOPS-106509: Agregue indicadores de complementos adicionales para admitir el acceso reflexivo GSON en Java 21.

### Problemas conocidos {#known-issues-20783}

Ninguna.

### Características y API obsoletas {#deprecated-20783}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-20783}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 19 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-20783}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.78.1-T20250429061757 | [API Oak 1.78.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.78.0/index.html?lang=es) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.29.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
