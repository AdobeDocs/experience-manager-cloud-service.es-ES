---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: e58e1355b923e1da447e3dbcfd0a81086aee3e66
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 23%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 24288 {#24288}

A continuación se resumen las mejoras continuas para la versión de mantenimiento 24288, que se publicó el jueves, 04 de febrero de 2026. La versión de mantenimiento anterior fue la 23963.

La activación de funciones 2026.2.0 proporciona el conjunto completo de funciones para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

>[!NOTE]
>
>La 24222 de la versión se ha convertido en privada.

### Mejoras {#enhancements-24288}

* CNTBF-604: Crear nuevo paquete de flujo de retorno de contenido.
* CQ-4361592: Agregue compatibilidad con TypeHint para la creación y actualización de proyectos.
* CQ-4362198: Últimas traducciones de paquetes de AEM y Granite.
* GRANITE-36205: Actualice la versión interna de Oak a la más reciente.
* GRANITE-59211: OPTEL: Se ha agregado compatibilidad con nonce y configuración de autoservicio.
* GRANITE-62166: actualice el paquete de migración para reutilizar los estados de migración de la herramienta de migración.
* GRANITE-62598: elimina la propiedad redundante excluir del filtro del paquete de contenido.
* GRANITE-62684: Hacer que el tiempo de espera del socket de cliente sea configurable a través de skyline-ops.
* GRANITE-62702: Reemplace el descubrimiento de sling con una implementación independiente para la migración en línea.
* GRANITE-62763: Actualice la lista de excepciones de obsolescencia de Guava en función de ASSETS rotativo.
* GRANITE-62771: Error en las compilaciones de Quickstart cuando se introducen nuevas dependencias de Commons-Lang obsoletas.
* GRANITE-62987: Actualice la consola web de Felix a la versión 5.0.18.
* GRANITE-63339: mejore el mecanismo de concesión para el blob de estado de migración de Azure.
* GRANITE-63343: Añada compatibilidad con la última versión del paquete de API de Sling en workflow.core.
* GRANITE-63799: Bump OIDC Authentication Bundle version.
* GRANITE-63821: Actualice Quickstart a la corrección de la versión de filevault JCRVLT-831/JCRVLT-839.
* GRANITE-63827: Actualice Quickstart a la última versión pública de Oak (1.90.0).
* GRANITE-63888: Actualice Quickstart a Jackrabbit 2.22.3.
* GRANITE-64030: agregue palabras clave y patrones a la lista de permitidos de Validador del lenguaje de expresión.
* GRANITE-64050: permite que las carpetas de configuración ocultas oculten la funcionalidad de productos externos.
* SITES-30452: API de contenido con ASO - Sugerencias de título y descripción.
* SITES-38099: actualice `testing-model.txt` para utilizar una versión superior de las comprobaciones de coherencia.
* SKYOPS-43616: Migre las credenciales de Jenkins a Vault en repositorios de Dispatcher.
* SKYOPS-108584: herramienta Bump FACT de 0.6.0 a 0.6.10.
* SKYOPS-115691: Actualice el paquete de filtros CORS para agregar el encabezado Vary Origin en las solicitudes de verificación previa.
* SKYOPS-123094: Actualice los componentes HTTP de Apache en Quickstart.
* SKYOPS-123236: incluye `rep:cugPolicy` en el paquete de replicación.
* SKYOPS-123240: Actualice las dependencias CRXDE en Quickstart.
* SKYOPS-123247: Actualice el paquete Sling XSS en Quickstart.
* SKYOPS-123250: Actualice el paquete de seguridad de Sling en Quickstart.
* SKYOPS-123327: Requiere Java 21 para AEM-CS SDK.
* SKYOPS-125574: Actualice los paquetes de herramientas de CA netcentric en Quickstart.
* SKYOPS-126150: Mejorar el comando superior para volcados de hilos script generador.

### Problemas solucionados {#fixed-issues-24288}

* FORMS-23687: corrige el error de validación de SSV cuando la regla contiene se utiliza sin valor predeterminado.
* GRANITE-48472: Error de localización al cambiar la contraseña en la pestaña Editar configuración de usuario.
* GRANITE-50286: corrija el problema de diseño en la columna de estado del modal de Administración de usuarios.
* GRANITE-52301: Localizar No se pueden confirmar los cambios en la cadena de sesión en los grupos de seguridad.
* GRANITE-52920: Error de localización al crear un usuario en Seguridad Crear nuevo usuario.
* GRANITE-54654: Localice la cadena en el cuadro de diálogo Comprobación de configuraciones de Adobe IMS de seguridad.
* GRANITE-56371: corrija el formato de datos incorrecto en el almacén de confianza de seguridad.
* GRANITE-62717: Actualice el almacén de claves criptográficas para la administración de contraseñas de JSafe con caracteres no ASCII.
* GRANITE-62789: Actualice messaging-client para que no admita el modo de reintentos en la distribución de contenido.
* GRANITE-62824: Se corrigió `NullPointerException` al acceder a la pestaña Grupos en el Editor de usuarios.
* GRANITE-63080: hacer compatible la importación de `org.slf4j.spi` con `slf4j 2.x`.
* GRANITE-63210: Actualice el núcleo de distribución para corregir la invalidación de Dispatcher al inicio de la publicación.
* GRANITE-63293: Corrija el campo de ruta obligatorio que pierde el asterisco requerido después de la primera creación.
* GRANITE-63360: Corrija la información incorrecta que se muestra cuando se seleccionan varias rutas.
* SITES-36242: Reduzca la regex de ejecución de GraphQL para corregir la omisión del filtro de Dispatcher.
* SITES-40122: corrección de la integración de Edge Delivery con el servicio Ims de distribución de contenido.
* SKYOPS-84379: Utilice la última herramienta FACT para la selección de funciones adecuada por RDEs.
* SKYOPS-121216: Revertir la actualización a las bibliotecas de Jackson 2.20.0.

#### Guías de AEM {#guides-24288}

* GUIDES-38198 : Al actualizar una ecuación de MathML en línea mediante la opción Editar MathML del menú contextual, el valor actualizado no se refleja hasta que se actualiza la página.
* GUIDES-38276: No se pueden quitar las etiquetas de Versión del panel Historial de versiones en la IU de Assets.
* GUIDES-36641: Al generar la salida de AEM Sites, los títulos de los mapas que contienen palabras clave y títulos de temas con el elemento `<ph>` no se incluyen en la salida publicada.
* GUIDES-37837: Al intentar guardar un tema o asignación, la operación puede fallar intermitentemente con un error de No se pudo guardar el archivo, especialmente durante las tareas intensivas de procesamiento de recursos o los flujos de trabajo de traducción que se ejecutan en segundo plano.
* GUIDES-27774: el informe Lista rota incluye incorrectamente vínculos externos, `keyrefs` válidos y palabras clave que se han resuelto correctamente en el ámbito del mapa actual.

>[!NOTE]
>
> Hay un cambio importante en AEM Guides que se debe tener en cuenta: [Se mejoró el manejo de los archivos de solo lectura](https://experienceleague.adobe.com/en/docs/experience-manager-guides/using/release-info/release-notes/cloud-release-notes/2026-releases/2601-release/whats-new-2026-01-0#improved-handling-for-read-only-files).

Para obtener más información sobre las funciones nuevas y mejoradas y los problemas corregidos en la versión, consulte la [hoja de ruta de la versión de Experience Manager Guides](https://experienceleague.adobe.com/es/docs/experience-manager-guides/using/release-info/aem-guides-releases-roadmap).

### Problemas conocidos {#known-issues-24288}

* SITES-40408: el extremo de GraphQL devuelve 404 debido a las reglas de reescritura personalizadas del Dispatcher.

### Características y API obsoletas {#deprecated-24288}

* AEMSRE-2896: Corrija la administración de la configuración personalizada de logmanager.
* GRANITE-62802: quita la dependencia `commons-lang` obsoleta de `granite.auth.saml`.
* GRANITE-62805: quita la dependencia `commons-lang` obsoleta de `granite.httpcache.core`.
* GRANITE-62864: quita la dependencia `commons-lang` obsoleta de `granite.jobs.async`.
* GRANITE-62865: quita la dependencia `commons-lang` obsoleta de `granite.replication.core`.
* GRANITE-62868: quita la dependencia `commons-lang` obsoleta de `granite.rest.api`.
* GRANITE-62895: quita la dependencia `commons-lang` obsoleta de `translation.connector.msft.core`.
* GRANITE-63069: obsoleto `com.adobe.granite.httpcache.core`.
* GRANITE-63179: quita la dependencia `commons-lang` obsoleta de `cq-workflow-impl`.
* GRANITE-63180: quitar la exportación de `commons.lang` obsoleta del paquete `cq-mailer`.
* SKYOPS-123329: cancele la compatibilidad con Java 11 para las implementaciones de AEM Ethos y actualice `commons-lang3`.
* SKYOPS-124983: quitar `nashorn.args` obsoletos de los scripts de inicio de AEM.

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

### Correcciones de seguridad {#security-24288}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 10 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-24288}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.90.0 | [API de Oak 1.90.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.90.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.28-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Apache HTTP Server | 2.4.65 | [Apache Httpd 2.4.65](https://apache.googlesource.com/httpd/+/refs/tags/2.4.65/CHANGES) |
| Componentes principales de AEM | 2.30.2 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
| Node.js | 14 (valor predeterminado) | [Versiones de Node.js compatibles](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/developing/developing-with-front-end-pipelines#node-versions) |
