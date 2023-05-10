---
title: Notas de la versión 2023.1.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
description: Notas de la versión 2023.1.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
source-git-commit: e0f3f876ce8bc4245f7118f8ae7553907bc0567e
workflow-type: ht
source-wordcount: '978'
ht-degree: 100%

---


# Notas de la versión 2023.1.0 para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión de funciones de la versión 2023.1.0 de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2021, 2022, etc.
>
>Eche un vistazo a la [Hoja de ruta de versiones de Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html?lang=es) para obtener más información acerca de las próximas activaciones de funcionalidades para [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de la versión 2023.1.0 de funciones de [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] es el 9 de febrero de 2023. La próxima versión con funcionalidades (2023.2.0) está planificada para el 12 de abril de 2023.

## Vídeo de la versión {#release-video}

Eche un vistazo al vídeo Información general sobre la versión de enero de 2023 para ver un resumen de las funciones añadidas en la versión 2023.1.0:

>[!VIDEO](https://video.tv.adobe.com/v/3413479/?quality=12)

## [!DNL Experience Manager Sites] as a [!DNL Cloud Service] {#sites}

### Nuevas funciones en el canal de prelanzamiento de [!DNL Sites] {#prerelease-features-sites}

* La API de envío de contenido de GraphQL de AEM ahora es compatible con la [Paginación](/help/headless/graphql-api/content-fragments.md#paging) y [Ordenación](/help/headless/graphql-api/content-fragments.md#sorting) de GraphQL, para que la recuperación y el procesamiento de grandes conjuntos de contenido sean más eficientes. La paginación de GraphQL permite mejorar el tiempo de respuesta a las consultas devolviendo resultados en subconjuntos en lugar de todos a la vez. La ordenación de GraphQL permite colocar los conjuntos de contenido en el orden deseado, lo que facilita a una aplicación del cliente el procesamiento del contenido.  El tiempo de respuesta a la consulta mejora aún más con el filtrado híbrido en el motor de GraphQL de AEM. Ahora, el contenido se lee desde JCR en conjuntos más pequeños que se corresponden con los filtros de consulta.

## [!DNL Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Nuevas funciones de [!DNL Assets] {#assets-features}

* Los informes de activos ahora permiten a los administradores [generar informes de descarga de activos](/help/assets/asset-reports.md) desde la implementación de Experience Manager Assets as a Cloud Service. Estos datos permiten a los administradores obtener perspectivas de métricas de éxito clave para medir la adopción de activos en su empresa y por parte de los clientes.

   ![Representación del PDF para otros formatos](/help/release-notes/assets/choose_report.png)

* Experience Manager Assets ahora [admite el token SAS](/help/assets/add-assets.md#asset-bulk-ingestor) además de la clave de acceso para la autenticación al conectarse a la fuente de datos de almacenamiento de Azure Blob para la ingesta de activos mediante la herramienta de importación masiva.

* Se ha mejorado la administración de las imágenes CMYK en Asset Compute, lo que le permite generar recortes inteligentes y etiquetas inteligentes para imágenes CMYK.

### Nuevas funciones en el canal de prelanzamiento de [!DNL Assets] {#prerelease-features-assets}

* Experience Manager Assets ahora admite [ingesta a gran escala de activos de Google Cloud Platform](/help/assets/add-assets.md#asset-bulk-ingestor) mediante la herramienta de importación masiva.

## [!DNL Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

### Nuevas funciones disponibles en [!DNL Forms] {#new-features-available-in-channel}

* **[Pasos del flujo de trabajo para generar documentos PDF no interactivos y salida imprimible](/help/forms/aem-forms-workflow-step-reference.md)**: automatice la creación de documentos PDF no interactivos y la salida imprimible para sus procesos empresariales con pasos de flujo de trabajo de AEM, lo que optimiza el proceso de generación de documentos y ahorra tiempo.
* **[Utilice las notas al pie para proporcionar citas o información adicional en formularios adaptables](/help/forms/footnotes-richtextsupport.md)**: utilice notas al pie en un formulario adaptable para mostrar la información sobre cómo completar o utilizar un formulario. También puede aprovecharlas para proporcionar información entre paréntesis, permisos de copyright y otra información útil.

### Nuevas funciones en el canal de prelanzamiento de [!DNL Forms] {#prerelease-features-forms}

* **[Uso de los componentes principales de captura de datos para crear formularios adaptables](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es)**: [use el editor de formularios adaptables](/help/forms/creating-adaptive-form-core-components.md) para crear formularios basados en componentes de captura de datos estandarizados (componentes principales). Estos componentes proporcionan funcionalidades de personalización, un tiempo de desarrollo reducido y costes de mantenimiento más bajos para sus experiencias de inscripción digital.
* **[Compatibilidad de canalización front-end para aplicar estilo a componentes principales basados en formularios adaptables](/help/forms/using-themes-in-core-components.md)**: utilice temáticas fácilmente personalizables de BEM para formularios adaptables basados en componentes principales implementándolas con la canalización de implementación de front-end y mejore la apariencia de sus formularios.
* **[Generar documento de registro para el componente principal basado en formularios adaptables](/help/forms/generate-document-of-record-core-components.md)**: cree un registro para el formulario adaptable basado en componentes principales al enviarlo para su archivo a largo plazo, en formato impreso o en formato de documento.

![https://www.aemcomponents.dev/](/help/forms/assets/sample-core-components-based-adaptive-form.png)

* **[Enviar formularios adaptables a Microsoft SharePoint y Microsoft OneDrive](/help/forms/configuring-submit-actions.md)**: optimice el envío de datos con la capacidad de enviar directamente datos de formularios adaptables a Microsoft SharePoint y a Microsoft OneDrive. Puede enviar datos basados en esquemas y sin esquemas. Estas acciones de envío se añaden a las ya disponibles.
* **[Creación eficiente de formularios con la funcionalidad Guardar un formulario adaptable como plantilla](/help/forms/template-editor.md#save-an-adaptive-form-as-template-saving-adaptive-form-as-template)**: optimice el proceso de creación de formularios guardando un formulario adaptable como plantilla y reutilizando las plantillas para el siguiente.
* **[Conexión de AEM Forms a bases de datos compatibles con JDBC](/help/forms/configure-data-sources.md#configure-relational-database-configure-relational-database)**: conecte fácilmente el modelo de datos de AEM Forms a bases de datos compatibles con JDBC, lo que le permite leer y escribir datos sin problemas.
* **[Integrar con puntos de conexión REST mediante la API abierta 3.0](/help/forms/configure-data-sources.md#configure-restful-services-open-api-specification-version-20-configure-restful-services-swagger-version30)**: conecte los modelos de datos de formulario de AEM Forms as a Cloud Service a puntos de conexión REST compatibles con la especificación de API abierta versión 3.0, lo que le permite enviar y recibir datos con facilidad.
* **[Compartir un formulario adaptable para su revisión](/help/forms/create-reviews-forms.md)**: utilice el mecanismo de revisión de formularios adaptables para permitir que uno o más revisores revisen el formulario.

## [!DNL Experience Manager as a Cloud Service] Foundation {#foundation}

### Novedades {#what-is-new-foundation}

* [Entornos de desarrollo rápido](/help/implementing/developing/introduction/rapid-development-environments.md): los RDE permiten a los desarrolladores solucionar rápidamente problemas e implementar nuevas funciones en AEM as a Cloud Service.

   Los entornos de desarrollo rápido son un nuevo tipo de entorno de nube diseñado como una forma veloz, coherente y extensible de validar que el código que funciona localmente también funciona como se espera en la nube. Con las herramientas de la línea de comandos, “sincronice” rápidamente los paquetes de contenido, los paquetes, los archivos de contenido, la configuración OSGI o la configuración de Dispatcher con el RDE. Vea esto en acción en el siguiente vídeo:

   >[!VIDEO](https://video.tv.adobe.com/v/3413508/?quality=12&learn=on)

   Después de validar correctamente el código en el RDE, se recomienda implementarlo en un entorno de desarrollo en la nube para ejercitar las puertas de calidad de Cloud Manager, antes de implementarlo a través de la canalización de producción en entornos de fase y producción.

   Cada programa incluye un RDE y, opcionalmente, se pueden obtener licencias de más.

   >[!NOTE]
   >
   >Los RDE se implementarán gradualmente en las próximas semanas; puede enviar un correo electrónico a aemcs-rde-support@adobe.com para pasar al principio de la cola.

* [Compatibilidad ampliada para tokens de acceso a API del lado del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md): Ahora puede generar varias credenciales, lo que resulta útil en escenarios donde las API tienen características diferentes. Ahora también es posible revocar las credenciales de forma de autoservicio.

## Notas de la versión de mantenimiento {#maintenance}

Puede encontrar las últimas notas de la versión de mantenimiento [aquí](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Puede encontrar una lista completa de las versiones mensuales de Cloud Manager [aquí.](/help/implementing/cloud-manager/release-notes/current.md)

## Herramientas de migración {#migration-tools}

Puede encontrar una lista completa de las versiones de las herramientas de migración [aquí](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
