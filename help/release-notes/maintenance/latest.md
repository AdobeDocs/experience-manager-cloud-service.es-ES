---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 09c52e32e6ffff2c69fb24f28e99a65477b434ec
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 15%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## 27083 de versión {#release-27083}

A continuación se resumen las mejoras continuas para la 27083 de la versión de mantenimiento, que se publicó el 15 de julio de 2026. La versión de mantenimiento anterior era 26908.

La activación de funciones 2026.7.0 proporcionará el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-27083}

* Capacidad de CQ-4354303:Added para eliminar la configuración de traducción.
* FORMS-23746: No coinciden los tipos de datos entre InvokeDDX y los pasos del flujo de trabajo de carga de recursos que impidieron su uso en secuencia.
* FORMS-24585: Conector de AEP con aprovisionamiento más sencillo.
* FORMS-25250: Se ha introducido el servicio ConvertPdf.
* FORMS-26044: análisis de virus/malware de archivos adjuntos agregados para cargas en formularios basados en AF1 y componentes principales.
* GRANITE-69298: Agregar `cqPageContent-5` y `graphqlConfig-3` índices.
* SITES-42563: Edge Delivery con el editor universal: mostrar los errores de publicación en el editor universal y el administrador de sitios (acceso anticipado).
* SITES-42792: marcador de posición &quot;Seleccionar ruta de Launch Source&quot; truncado en el panel de filtros en &quot;Herramientas&quot; > &quot;General&quot; > &quot;Lanzamientos&quot;.
* SITES-43178: AEM: El formato de hora localizado incluye AM/PM en Herramientas > Sitios > Lanzamientos.
* SITES-44344: API de contenido: trata las copias de MSM/idioma como parte del sitio principal.
* SITES-44598: presenta el botón Comprobación preliminar en la barra de encabezado del editor.
* SITES-44676: Los resultados de la búsqueda de fragmentos de contenido ahora incluyen el ID de esquema de metadatos para cada fragmento.
* SITES-44767: se ha agregado un esquema de metadatos predeterminado para los fragmentos de contenido.
* SITES-45651: se ha corregido el ejemplo del fragmento de contenido de OpenAPI en la especificación de la API.
* SITES-45664: se ha agregado un nuevo extremo GET `/cf/metadata/schemas` para recuperar propiedades de metadatos que se pueden filtrar.
* SITES-45725: API de contenido: agregue el filtro de correlación de solicitud para habilitar las alertas de SLO de recorrido de Oak.
* SITES-45817: Edge Delivery con el editor universal: compruebe las funciones y los permisos de entrega perimetral al publicar (acceso anticipado).
* SITES-45842: Edge Delivery con editor universal: conserva la instrumentación del editor universal para los casos de uso de solo lectura y de revisión/comentario.
* SITES-45848: Edge Delivery con el editor universal: valide `json-ld` antes de publicar.
* SITES-46768: Edge Delivery con editor universal: muestra los problemas de creación de sitios en el asistente de creación de sitios.

### Problemas solucionados {#fixed-issues-27083}

* CQ-4364078: se ha corregido la reescritura de vínculos internos dentro de Fragmentos de experiencias por copia de idioma.
* CQ-4364077: se ha corregido un error en la creación de la copia de idioma debido a conflictos OakState0001.
* CQ-4363949: se ha corregido la adición incorrecta de fragmentos de experiencia a los que se hace referencia sin modificar en la traducción de solo actualización.
* CQ-4363942: interfaz de usuario de etiquetas: el menú desplegable &quot;Agregar idioma&quot; ahora muestra las configuraciones regionales no enumeradas que no eran visibles a pesar de persistir en JCR.
* CQ-4363527: se ha corregido el problema de interfaz de usuario del widget de copia de idioma para el método y proveedor agénticos.
* FORMS-25979: Se ha actualizado la biblioteca Underscore.js (1.13.6 → 1.13.8+) en el complemento AEM Forms.
* FORMS-18969: se ha corregido un problema por el que Temáticas de AEM Forms impedía a los usuarios actualizar la vista previa del formulario.
* FORMS-25184: se corrigieron los puntos del indicador de enlace de datos que faltaban en el panel lateral Fuentes de datos para los formularios basados en componentes principales (AF v2).
* FORMS-18721: se ha corregido un problema que impedía que los temas de AEM Forms actualizaran la biblioteca de cliente base.
* FORMS-19235: se ha corregido un error de la aplicación que podía exponer información confidencial en Forms Manager.
* FORMS-25369: se ha corregido un problema por el que la copia de una temática no transfería dependencias clientlib de los metadatos de la biblioteca de cliente base.
* FORMS-25372: se han corregido errores de relleno previo y problemas de combinación de JSON que afectaban al Forms adaptable incrustado.
* FORMS-24853: se ha corregido un problema de tabulación con el componente de firma manuscrita (componente de base) en el Forms adaptable.
* SITES-41928: la superposición de Contexthub y Unified Shell impide el acceso al menú de componentes en el editor.
* SITES-46579: API de contenido: Corregir el recorrido del repositorio en la consulta de copia de idioma de RelationshipService: definir la consulta de índice y reescritura.
* SITES-44192: Forms/API de contenido: La API de contenido devuelve 404 para los formularios EDS que utilizan `sling:configRef` en lugar de `cq:conf`.
* SITES-29367: GraphQL: Proteja ModelManager de las personalizaciones de índice `cqPageLucene` erróneas.
* SITES-46521: API de contenido: `jcr:path` en la consulta está causando un recorrido de la consulta.
* SITES-46784: GraphQL: los modelos del ModelManager deben deduplicarse.
* SITES-46304: API de contenido: la búsqueda de páginas de la API de contenido excluye silenciosamente a `/content/campaigns`.
* SITES-46769: GraphQL: La caché de datos por solicitud con modelos de fragmento de contenido grande lleva a excepciones de OM.
* SITES-46570: API de contenido: utilice el operando de rutas indexadas en la consulta de plantillas para la inserción de índice.
* SITES-24497: ahora se proporcionan etiquetas distintas para puntos de referencia repetidos, de modo que los técnicos de asistencia puedan diferenciarlos.
* SITES-24525: se ha corregido una función de encabezado incorrecta asignada a los botones modales . Los lectores de pantalla ahora los anuncian como botones.
* SITES-24703: El indicador de enfoque de los botones emergentes del cuadro de lista ahora está completamente visible y ya no se recorta.
* SITES-25217: el icono de información se ha ampliado para satisfacer el requisito mínimo de tamaño objetivo.
* SITES-25263: se ha corregido el valor aria-haspopup en el campo de fecha Deformación de tiempo para que los lectores de pantalla lo anuncien correctamente.
* SITES-25308: mayor contraste en los indicadores de enfoque del botón de la barra de herramientas demográfica para cumplir con los mínimos WCAG.
* SITES-25318: se ha mejorado el contraste del texto de los campos de entrada de la barra de herramientas Demografía.
* SITES-25364: las instrucciones de entrada ahora están vinculadas mediante programación a su casilla de verificación, por lo que el técnico de asistencia las anuncia juntas.
* SITES-25377: el carril lateral de Assets ya no vuelve a cargar su contenido cuando el campo de filtro recibe el enfoque.
* SITES-40752: se ha mejorado la navegación mediante el teclado a través de la lista de componentes del panel lateral.
* SITES-41121: Impedía que los lectores de pantalla anunciaran una etiqueta de grupo oculta junto al nombre del componente.
* SITES-43802: se ha eliminado una cadena &quot;false&quot; falsa que aparecía dentro del modal Insertar componente.
* SITES-46720: Las radios de Propiedades de página pierden la selección guardada después de la actualización de la versión 2026.05 o posterior (SDK ≥ 26353): los valores se borran en el lado del cliente.
* SITES-46680: no se puede crear el lanzamiento de CF debido a la asignación del servlet Sling en el código personalizado.
* SITES-46327: al crear un lanzamiento con la opción &quot;Heredar datos activos de la página de origen&quot; habilitada, el fragmento de experiencia de la página de origen no se hereda y algunos vínculos también se rompen.
* SITES-45969: páginas secundarias eliminadas en la promoción de lanzamiento al utilizar &quot;nueva plantilla&quot; + &quot;incluir subpáginas&quot;.
* SITES-45723: SITES-44245 correcciones de saltos Lanzamientos: empty-genericFrom guard suprime las reescrituras legítimas de referencia de lanzamiento.
* SITES-45689: Errores intermitentes de despliegue de MSM: &quot;Sin ruta de Source&quot; y AccessDeniedException.
* SITES-44918: código de idioma indonesio mostrado EN lugar de ID.
* SITES-41427: El despliegue de XF se realiza correctamente, pero falla silenciosamente cuando no existe ninguna Live Copy: solicitud de gestión adecuada o creación automática
* SITES-36149: duplicación de componentes en Launch después de la promoción con sincronización en directo.
* SITES-25970: se corta el cuadro de diálogo de despliegue de la IU de componentes.
* SITES-30707: se ha corregido una etiqueta &quot;General&quot; codificada en el Editor de fragmentos de contenido para admitir la localización.
* SITES-44228: se ha corregido un problema por el que, al eliminar un fragmento de contenido referenciado mediante uuid, los fragmentos de referencia no se ajustaban.
* SITES-45171: se ha corregido un problema por el que la solicitud de publicación podía almacenar en déclencheur incorrectamente un flujo de trabajo de solicitud de activación.
* SITES-46303: recuperación de la versión fija para evitar intentos innecesarios de migración de tarjetas.
* SITES-46713: se corrigieron errores en las operaciones de PATCH cuando el usuario carece de los permisos de eliminación necesarios para la migración de tarjetas.
* SITES-46590: se ha corregido una regresión por la que al volver a una versión anterior en la cronología no se actualizaba la miniatura de la tarjeta de recursos en la vista de administración de Assets.
* SITES-47292: Edge Delivery con editor universal: corrija la representación de etiquetas combinadas en los metadatos de la página.

### Problemas conocidos {#known-issues-27083}

Ninguna.

### Características y API obsoletas {#deprecated-27083}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-27083}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 18 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-27083}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 2.2.0 | [API de Oak 2.2.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/2.2.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.67 | [Apache Httpd 2.4.67](https://apache.googlesource.com/httpd/+/refs/tags/2.4.67/CHANGES) |
| Dispatcher | 2.0.274 |  |
| Componentes principales de AEM | 2.31.2 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
| Java 21 | 21.0.11 | [JDK 21.0.11](https://www.oracle.com/java/technologies/javase/21-0-11-relnotes.html) |
