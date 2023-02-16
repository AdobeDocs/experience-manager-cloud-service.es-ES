---
title: Notas de la versión actuales de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión actuales de  [!DNL Adobe Experience Manager]  as a Cloud Service.
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
mini-toc-levels: 1
source-git-commit: 0c7ed29e53d9315ad45102eef5d4e1f66ab4b4ae
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 23%

---


# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de las funciones de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2021, 2022, etc.
>
>Eche un vistazo a la [Hoja de ruta de las versiones del Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información sobre las próximas activaciones de funciones de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] como [!DNL Cloud Service] la versión de la función actual (2023.1.0) es 9 de febrero de 2023. La próxima versión de la función (2023.2.0) está planificada para el 16 de marzo de 2023.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de enero de 2023 para ver un resumen de las funciones añadidas en la versión 2023.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones en el canal de prelanzamiento de [!DNL Sites] {#prerelease-features-sites}

* La API de envío de contenido de AEM GraphQL ahora es compatible con GraphQL [Paginación](/help/headless/graphql-api/content-fragments.md#paging) y [Ordenar](/help/headless/graphql-api/content-fragments.md#sorting), para que la recuperación y el procesamiento de grandes conjuntos de contenido sean más eficientes. La paginación de GraphQL permite mejorar el tiempo de respuesta de la consulta devolviendo resultados en subconjuntos en lugar de todos a la vez. La ordenación de GraphQL permite colocar conjuntos de contenido en el orden deseado, lo que facilita que una aplicación cliente procese el contenido.  El tiempo de respuesta de consulta se mejora aún más con el filtrado híbrido en el motor de GraphQL AEM. El contenido ahora se lee desde JCR en conjuntos más pequeños que se corresponden con filtros de consulta.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Los informes de recursos ahora incluyen la capacidad de los administradores de [generar informes de descarga de recursos](/help/assets/asset-reports.md) de la implementación as a Cloud Service de Experience Manager Assets. Estos datos permiten a los administradores obtener perspectivas a partir de métricas de éxito clave para medir la adopción de activos en su empresa y por parte de los clientes.

   ![Representación del PDF para otros formatos](/help/release-notes/assets/choose_report.png)

* Experience Manager Assets ahora [admite el token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) además de la clave de acceso para la autenticación al conectarse a la fuente de datos de almacenamiento de Azure Blob para la ingesta de activos mediante la herramienta de importación masiva.

* Se ha mejorado la administración de imágenes CMYK en el Asset compute, lo que permite generar Recorte inteligente y etiquetas inteligentes para imágenes CMYK.

### Nuevas funciones en el canal de prelanzamiento de [!DNL Assets] {#prerelease-features-assets}

* Experience Manager Assets ahora es compatible [ingesta a gran escala de recursos desde Google Cloud Platform](/help/assets/add-assets.md#asset-bulk-ingestor) uso de la herramienta Importación masiva .

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en [!DNL Forms] {#new-features-available-in-channel}

* **[Pasos del flujo de trabajo para generar documentos de PDF no interactivos y resultados imprimibles](/help/forms/aem-forms-workflow-step-reference.md)**: Automatice la creación de documentos de PDF no interactivos y resultados imprimibles para sus procesos empresariales con AEM pasos del flujo de trabajo, optimizando el proceso de generación de documentos y ahorrando tiempo.
* **[Utilice las notas a pie de página para proporcionar citas o información adicional en Forms adaptable](/help/forms/footnotes-richtextsupport.md)**: Utilice las notas al pie en un formulario adaptable para mostrar la información sobre cómo rellenar o utilizar un formulario. También puede utilizarla para proporcionar información entre paréntesis, permisos de copyright y otra información útil.

### Nuevas funciones en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **[Utilice componentes principales de captura de datos para crear Forms adaptable](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en)**: [Uso del editor de Forms adaptable](/help/forms/creating-adaptive-form-core-components.md) para crear formularios basados en componentes de captura de datos estandarizados (componentes principales). Estos componentes proporcionan capacidades de personalización, tiempo de desarrollo reducido y menores costes de mantenimiento para sus experiencias de inscripción digital.
* **[Compatibilidad con la canalización de front-end para el diseño de Forms adaptable basado en componentes principales](/help/forms/using-themes-in-core-components.md)**: Utilice temas fácilmente personalizables basados en BEM para Forms adaptable basado en componentes principales al implementarlos con la canalización de implementación de front-end para mejorar el aspecto de sus formularios.
* **[Generar documento de registro para Forms adaptable basado en componentes principales](/help/forms/generate-document-of-record-core-components.md)**: Cree un registro para el formulario adaptable basado en componentes principales en el envío para su archivo a largo plazo, impreso o en formato de documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Envío de Forms adaptable a Microsoft SharePoint y Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: Optimice el envío de datos con la capacidad de enviar directamente datos de Formulario adaptable a Microsoft SharePoint y Microsoft OneDrive. Puede enviar datos basados en esquemas y sin esquema. Estas acciones de envío se suman a las acciones de envío ya disponibles.
* **[Creación eficaz de formularios con la función Guardar un formulario adaptable como plantilla](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: Optimice el proceso de creación de formularios guardando un formulario adaptable como plantilla y reutilizando las plantillas para su siguiente formulario adaptable.
* **[Conectar AEM Forms a bases de datos compatibles con JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: Conecte fácilmente su modelo de datos de AEM Forms a bases de datos compatibles con JDBC, lo que le permite leer y escribir datos sin problemas.
* **[Integración con puntos de conexión REST mediante la API abierta 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: Conecte los modelos de datos de formulario as a Cloud Service de AEM Forms a los extremos de REST compatibles con la especificación de API abierta versión 3.0, que le permite enviar y recibir datos con facilidad.
* **[Compartir un formulario adaptable para su revisión](/help/forms/create-reviews-forms.md)**: Utilice el mecanismo de revisión de Forms adaptable para permitir que uno o más revisores revisen el formulario.


## Complemento CIF {#cloud-services-cif}

### Novedades {#what-is-new-cif}

* Los autores pueden enriquecer dinámicamente listas de productos con Fragmentos de experiencias (por ejemplo: colocar banner entre listas de productos).
* El componente de lista ahora admite páginas de productos o categorías asociados para mostrar dinámicamente páginas relacionadas.
* Se ha añadido compatibilidad con los componentes de Peregrine 12.5.
* Se ha añadido compatibilidad con la carga de precios del lado del cliente en teaser y carrusel de productos.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* [Entornos de desarrollo rápido](/help/implementing/developing/introduction/rapid-development-environments.md) - Los RDE permiten a los desarrolladores solucionar problemas rápidamente e implementar nuevas funciones en AEM as a Cloud Service.

   Los entornos de desarrollo rápido son un nuevo tipo de entorno de nube que sirve como una forma rápida, coherente y extensible de validar ese código que funciona localmente también funciona como se espera en la nube. Mediante las herramientas de la línea de comandos, &quot;sincronice&quot; rápidamente paquetes de contenido, paquetes, archivos de contenido, configuración OSGI o configuración de Dispatcher con el RDE. Vea esto en acción en el siguiente vídeo:

   >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

   Después de validar correctamente el código en RDE, se recomienda implementar en un entorno de desarrollo de nube para ejercer las puertas de calidad de Cloud Manager antes de implementar mediante canalización de producción en entornos de ensayo y producción.

   Cada programa incluye un RDE y, opcionalmente, se pueden obtener más licencias.

   >[!NOTE]
   >
   >Los RDE se pondrán en marcha gradualmente en las próximas semanas; puede enviar un correo electrónico a aemcs-rde-support@adobe.com para saltar al principio de la línea.

* [Compatibilidad ampliada con tokens de acceso a API del lado del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md) : Ahora puede generar varias credenciales, lo que resulta útil en escenarios en los que las API tienen características diferentes. Ahora también es posible revocar las credenciales de forma autoservicio.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [here](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí.](/help/implementing/cloud-manager/release-notes/current.md)

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
