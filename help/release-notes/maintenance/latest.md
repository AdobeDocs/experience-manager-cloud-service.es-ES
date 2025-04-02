---
title: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
description: Notas de la versión actuales sobre el mantenimiento de [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
feature: Release Information
role: Admin
source-git-commit: 96084c84c45af54b1f152e22b8331f85dc6b583f
workflow-type: tm+mt
source-wordcount: '1501'
ht-degree: 21%

---


# Notas de la versión de mantenimiento {#maintenance-release-notes}

En la siguiente sección se describen las notas de la versión técnicas actuales sobre el mantenimiento de Experience Manager as a Cloud Service.

## Versión 20133 {#20133}

A continuación, se resumen las mejoras continuas para la versión de mantenimiento 20133, que se publicó el miércoles, 01 de abril de 2025. La versión de mantenimiento anterior fue la 19823.

La activación de funcionalidades 2025.4.0 proporciona el conjunto completo de funcionalidades para esta versión de mantenimiento. Consulte la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/es/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) para obtener más información.

### Mejoras {#enhancements-20133}

* ASSETS-47850: Restrinja la adición de configuraciones de Scene7 si AEM CS está habilitado para ES.
* CQ-4359547: eliminación completa de Guava del repositorio de Git.
* FORMS-17551: se ha agregado compatibilidad con el documento de registro (DoR) para integraciones de listas de SharePoint.
* FORMS-18432: se ha implementado la configuración de relleno previo del lado del cliente específica del formulario (basada en regex) para habilitar la funcionalidad de relleno previo selectivo sin cambios en el nivel OSGI.
* FORMS-18513: se ha implementado compatibilidad con la transformación del árbol de datos en AEP Connector para mejorar la funcionalidad del asistente y las capacidades de administración de datos.
* FORMS-19068: se ha agregado compatibilidad con las acciones de envío del conector de AEP en las API de Forms Manager para mejorar las capacidades de integración de datos de formulario.
* GRANITE-57717: Actualice el paquete de cliente en AEM.
* SITES-10469: AdapterFactory siempre debe devolver la misma instancia de PageManager.
* SITES-25130: Versión Componentes principales 2.28.0.
* SITES-25433: admite el procesamiento de páginas completas al comparar versiones antiguas.
* SITES-25923: LinkInfoStorageImpl puede bloquearse cuando ya no se almacenan direcciones URL.
* SITES-26208: la eliminación de un fragmento de contenido mediante un flujo de trabajo ahora permite actualizar los recursos de referencia al eliminar el fragmento recién eliminado.
* SITES-26500: agregando la opción para mover fragmentos de contenido a través del flujo de trabajo - `move-fragments`.
* SITES-26711: Déclencheur de despliegue: los vínculos no se actualizan.
* SITES-27583: los fragmentos de experiencias pierden el historial de versiones después de moverse.
* SITES-27618: La búsqueda de referencias de un fragmento en páginas no devuelve todos los resultados.
* SITES-27781: se ha implementado la validación a nivel de modelo para las referencias de fragmento de contenido, lo que permite validar los fragmentos a los que se hace referencia con respecto a sus restricciones de modelo y la etiqueta requerida.
* SITES-27784: Actualice la generación de consultas SQL para utilizar la función PATH en lugar de `jcr:path`.
* SITES-28040: Adobe Target ExperienceFragmentsReplicationListener está dañado.
* SITES-28051: obtenga los permisos del usuario actual en un fragmento de contenido: GET /cf/fragments/{fragmentId}/permissions.
* SITES-28190: configuración para la prueba de integración de vista previa.
* SITES-28227: al agregar recursos como referencias a un fragmento, validamos que el recurso existe.
* SITES-28248: alternar eventos de sitios basados en la configuración OSGI.
* SITES-28255: falta el nombre completo en las 3 propiedades de auditoría: creadas, modificadas y publicadas.
* SITES-28390: PageImpl: Optimize hasContent().
* SITES-28404: la eliminación de páginas en el autor debe cancelar la publicación del servicio de vista previa.
* SITES-28446: se han agregado dos nuevos campos que no eran visibles en la respuesta: el marcador de posición de NumberModelField y los modelos permitidos de LongTextModelField.
* SITES-28536: crear el extremo `RENAME` para los fragmentos de contenido.
* SITES-28537: agregando la opción para cambiar el nombre de los fragmentos de contenido mediante el flujo de trabajo - `rename-fragments`.
* SITES-28538: las referencias deben volver a publicarse para mantener un contenido válido en Autor y Publicación.
* SITES-28549: cree `/cf/domains` para devolver el ID de dominio en función del nivel de AEM.
* SITES-29026: se ha agregado un parámetro opcional que especifica la configuración regional del fragmento de contenido, utilizando un idioma y un código de país.
* SITES-29031: se ha mejorado la lógica para los fragmentos de PATCH, lo que proporciona un mejor rendimiento.
* SITES-29169: los recursos con estado PUBLICADO se volverán a publicar si hacen referencia a un recurso que se movió, cambió de nombre o eliminó.
* SITES-29376: alternar Añadir código para validar la eliminación de recursos publicados.
* SITES-29417: actualice `/libs/cq/Page/proxy.jsp` para reenviar la solicitud al nodo jcr:content en lugar de incluir.
* SITES-2947: Cree/modifique la visualización kibana para comparar el rasp de publicación.
* SITES-29733: mayor rendimiento de la búsqueda de modelos por etiquetas de fragmentos de contenido.
* SITES-8316: Políticas de contenido: Almacene en caché ContentPolicyManager.
* SITES-24906: Edge Delivery con editor universal: admite hojas de cálculo creadas por el autor sin una asignación (acceso anticipado).
* SITES-24907: Edge Delivery con editor universal: admite la publicación de Assets en varios sitios para casos de uso de MSM (acceso anticipado).
* SITES-27956: Edge Delivery con editor universal: mejore el rendimiento de la publicación (acceso anticipado).
* SITES-27956: Edge Delivery con editor universal: mejore la gestión de errores para publicar en Edge Delivery Services (acceso anticipado).

### Problemas solucionados {#fixed-issues-20133}

* CQ-4358378: Gestión de errores de licencia en la ejecución de traducción.
* CQ-4359263: no se muestra ningún mensaje en el cuadro de diálogo cuando se completa el trabajo.
* CQ-4359386: No se puede agregar el diccionario i18n al proyecto de traducción en AEMaaCS.
* FORMS-18068: Problemas de procesamiento de texto en negrita en el documento de registro (DoR) para grupos de botones de opción y casillas de verificación que utilizan campos de texto enriquecido.
* FORMS-18189: se ha modificado la administración de funciones personalizadas para evitar el registro de errores en bibliotecas de cliente vacías y mejorar la visualización de errores en la IU.
* FORMS-18213: se ha implementado la funcionalidad para ocultar/excluir campos deshabilitados del documento de registro (DoR) para mejorar la claridad del documento y la experiencia del usuario.
* FORMS-18271: el editor de temáticas de Forms muestra mensajes de error no localizados, lo que afecta a la experiencia del usuario en la configuración del formulario y la personalización de temáticas.
* FORMS-18304: los documentos de PDF/A-1b que pasan la validación en Acrobat y LiveCycle ES4 se marcan incorrectamente como no compatibles en AEM 6.5 Forms debido a errores de color dependientes del dispositivo.
* FORMS-18325: Se ha añadido la configuración de nube de Adobe Experience Platform (AEP) para mejorar la integración de datos de formulario y las capacidades de procesamiento.
* FORMS-18360: administración mejorada del ámbito de la lista de SharePoint para equipos y sitios en Forms Document Management para mejorar la organización de los datos y el control de acceso.
* FORMS-18375: los formularios basados en componentes de base seleccionan incorrectamente las configuraciones de recaptcha de la carpeta `conf/global` cuando no se selecciona ningún contenedor de configuración específico.
* FORMS-18426: La funcionalidad de búsqueda de listas de SharePoint falla cuando los nombres de lista contienen caracteres especiales (por ejemplo, &quot;-&quot;), lo que afecta a la integración de formularios con listas de SharePoint.
* FORMS-19028: La funcionalidad de relleno previo del lado del cliente interrumpe la administración de eventos del formulario, lo que evita que los eventos Value commit y DOMContentLoaded se activen correctamente al cargar el formulario.
* FORMS-6950: se han agregado los roles y atributos ARIA necesarios a los componentes de vista de árbol del navegador del sistema de archivos para mejorar la accesibilidad del lector de pantalla y cumplir con el estándar WCAG 4.1.2 Nombre, función, valor (nivel A).
* FORMS-7016: El orden de enfoque del teclado en el Editor de formularios no sigue la navegación lógica.
* SITES-1960: rendimiento mejorado de la operación de previsualización JSON del Editor de fragmentos de contenido.
* SITES-24308: la barra de desplazamiento horizontal aparece cuando se cambia el tamaño del contenido al 400 %.
* SITES-24493: el elemento interactivo no tiene la función requerida.
* SITES-24669: El divisor de la ventana del carril de referencias no es accesible mediante el teclado.
* SITES-26881: error de accesibilidad de AEMaaCS: la función incorrecta se proporciona para el icono &quot;Tres puntos&quot; que está junto al campo de entrada de comentarios.
* SITES-26956: seguimiento en SITES-24920 No se puede mover la página en el entorno de producción.
* SITES-27707: la lista de recursos del Buscador de contenido falla debido a problemas con los nombres de recursos (regresión de 6.5 SP22).
* SITES-27757: Edge Delivery con editor universal: reescriba los iconos según la semántica de hélice-html-canalización.
* SITES-27780: Aparece una etiqueta &lt;br> inesperada en RTE con el texto sin formato DefaultPasteMode en SP22.
* SITES-27958: El verificador de vínculos genera errores &quot;Esta sesión se ha cerrado&quot;.
* SITES-28149: ExperienceFragmentLinkRewriterProvider personalizado no se activa durante la exportación de XF a Target.
* SITES-28449: Error en la interfaz de usuario del widget del flujo de trabajo - Incluir elementos secundarios que no muestran todas las páginas secundarias en AEM.
* SITES-28456: falta la notificación en la interfaz de usuario en caso de guardar una consulta persistente incorrecta en el Explorador de GraphiQL (seguimiento: SITES-28313).
* SITES-28464: actualice la consulta de fragmento para utilizar fechas con formato con milisegundos.
* SITES-28486: la edición in situ en el nuevo Editor de fragmentos de contenido no redirige al editor antiguo.
* SITES-28570: la GraphQL de los fragmentos de contenido gestiona correctamente los metadatos de los recursos que faltan.
* SITES-28580: El buscador de recursos de imagen clásico se ha roto tras la actualización a SP22.
* SITES-28600: Lanzamientos: contenido duplicado.
* SITES-28668: No se puede promocionar el lanzamiento con LaunchPromotionParameters.
* SITES-28820: prefijo de inicio añadido dos veces dentro de la nueva variación creada al volver a basar.
* SITES-28877: el servicio de URL de la UE lanza una excepción cuando el extremo del externalizador local no está definido.
* SITES-28956: La operación de eliminación de etiquetas muestra una advertencia, si los fragmentos de contenido hacen referencia a la etiqueta.
* SITES-29208: las referencias y las variaciones se devuelven correctamente en situaciones en que un campo de referencia contiene una ruta no válida.
* SITES-29363: el botón Restablecer Live Copy no funciona para la jerarquía de contenido de Live Copy anidada.
* SITES-29369: Problema de evento de Assets en AIO | Activar Incorrectamente Eventos Publicados/No Publicados De La Página.
* SITES-29972: las acciones Eliminar y Cambiar nombre a veces producen comentarios de flujo de trabajo no verdaderos.

### Problemas conocidos {#known-issues-20133}

Ninguna.

### Características y API obsoletas {#deprecated-20133}

Las funciones y API obsoletas y eliminadas de AEM as a Cloud Service se detallan en el documento [Funciones y API obsoletas y eliminadas](/help/release-notes/deprecated-removed-features.md).

#### Cambios en la sincronización de grupos de usuarios y perfiles de producto {#changes-user-groups}

Cuando se utiliza Adobe Admin Console para la administración de permisos, NO SE DEBEN utilizar los siguientes grupos porque ya no se sincronizarán más con AEM:
* Grupos de AEM que terminan con _GROUP_NAME_SUFFIX.
* Perfiles de producto de otros entornos, programas o productos.

Para obtener más información, compruebe [Cambios en la sincronización de grupos de usuarios y perfil de producto](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/security/changes-in-user-group-and-product-profile-synchronization).

#### Desuso del editor de SPA {#deprecate-spa-editor}

El [Editor de SPA](/help/implementing/developing/hybrid/introduction.md) ha quedado obsoleto para nuevos proyectos a partir de la versión 2025.4.0. El editor de SPA sigue siendo compatible con los proyectos existentes, pero no debe utilizarse en nuevos proyectos.

Los editores preferidos para administrar contenido sin encabezado son:

* [El Editor universal](/help/edge/wysiwyg-authoring/authoring.md) para la edición visual.
* [El editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-managing.md) para la edición de contenido sin encabezado basada en formularios.

Puede encontrar más información sobre esta desaprobación en el documento [Desaprobación del editor de SPA.](/help/implementing/developing/hybrid/spa-editor-deprecation.md)

### Correcciones de seguridad {#security-20133}

AEM as a Cloud Service se dedica a optimizar la seguridad y el rendimiento de su plataforma. Esta versión de mantenimiento aborda 34 vulnerabilidades identificadas, reforzando nuestro compromiso con una sólida protección del sistema.

### Tecnologías integradas {#embedded-tech-20133}

| Tecnología | Versión | Vínculo |
|---|---|---|
| AEM Oak | 1.76.0 | [API Oak 1.76.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.76.0/index.html) |
| API AEM SLING | 2.27.6 | [API de Apache Sling 2.27.6 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.26-1.4.0 | [Especificación de idioma de la plantilla HTML](https://github.com/adobe/htl-spec) |
| Los componentes principales de AEM | 2.28.0 | [Componentes principales de WCM AEM](https://github.com/adobe/aem-core-wcm-components) |
