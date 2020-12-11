---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
translation-type: tm+mt
source-git-commit: d115f5ce463257af54ae0ff48749df455b863dfd
workflow-type: tm+mt
source-wordcount: '1194'
ht-degree: 3%

---


# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

La siguiente sección describe las Notas de revisión generales para [!DNL Experience Manager] como Cloud Service.

## Fecha de la versión {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] como Cloud Service 2020.11.0 es el 2 de diciembre de 2020.
La siguiente versión (2020.12.0) será el 17 de diciembre de 2020

## [!DNL Adobe Experience Manager Sites] como Cloud Service  {#sites}

### Novedades en [!DNL Sites] {#what-is-new-sites}

* **[Inicia la administración](/help/sites-cloud/authoring/launches/managing-pages.md)  de jerarquía y la  [futura deformación](/help/sites-cloud/authoring/launches/preview.md)** de tiempo: La nueva interfaz de usuario para agregar o quitar páginas en un inicio y la exploración del sitio con Deformación de tiempo muestra el estado futuro de los inicios.

* **[Editor](/help/assets/content-fragments/content-fragments-models.md)** y modelos de fragmento de contenido ampliado: En la interfaz de usuario de Recursos se muestran y pueden buscarse nuevas opciones para la validación de entradas en varios tipos de datos, un tipo de datos de Lista desglosada mejorado con nuevas visualizaciones de formularios y el nombre del modelo de fragmento de contenido.

* **Ordene las páginas de Live Copy disponibles para la implementación**: Nueva opción para ordenar las páginas de Live Copy disponibles para la implementación con las propiedades  [!UICONTROL Nombre], Fecha [!UICONTROL  de ]última modificación y  [!UICONTROL Última ] fecha de lanzamiento. La [!UICONTROL última fecha de implementación] de una página es una nueva propiedad introducida.

## [!DNL Adobe Experience Manager Assets] como Cloud Service  {#assets}

### Novedades en [!DNL Assets] y [!DNL Dynamic Media] {#what-is-new-assets}

* **Ingesta** masiva de recursos: Brinde a los clientes un servicio de ingestión escalable y nativo de la nube que aprovecha  [!DNL Experience Manager] como arquitectura Cloud Service, incluidos los microservicios de recursos. Entre los casos de uso clave se incluyen la ingestión a escala con supervisión, sistema de informes y programación, mientras que se permite la transferencia inicial de recursos a almacenes de datos en la nube mediante herramientas comunes de carga en la nube. Consulte [herramienta de ingestor masivo de recursos](/help/assets/add-assets.md#asset-bulk-ingestor).
Esta herramienta está destinada a administradores del sistema, consultores o asociados de implementación. Esta función permite la ingestión a gran escala y se utiliza de forma ideal durante la ingestión inicial o durante la ingestión ocasional de gran tamaño. Para trabajos de ingestión más pequeños, utilice la [[!DNL Experience Manager] carga de la aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) o [mediante la interfaz de usuario de Assets](/help/assets/add-assets.md#upload-assets).

   ![Configuración del importador a granel](/help/assets/assets/bulk-import-config-low-res.png)

* Ahora los usuarios pueden ordenar los recursos digitales en vistas de tarjetas y columnas.

   ![ordenar recursos](/help/assets/assets/asset-sort-options.png)

* En esta versión se han realizado las siguientes mejoras para la accesibilidad en [!DNL Experience Manager Assets]. Para obtener más información, consulte [características de accesibilidad en [!DNL Assets]](/help/assets/accessibility.md).

   * Al navegar por la línea de tiempo con un teclado, la tecla Esc puede contraer la opción Mostrar todo sin perder el enfoque.
   * Al navegar con la tecla de tabulación del teclado, después de quitar la última etiqueta de las etiquetas agregadas, el campo de etiqueta conserva el enfoque.
   * [!DNL Experience Manager] los componentes ahora contienen la información adecuada sobre el nombre, la función y el valor que utilizarán los lectores de pantalla.
   * Después de eliminar el cuadro combinado Tipo/Tamaño, el cuadro combinado Vínculo, el cuadro combinado Idioma o el cuadro de edición de texto, el enfoque del teclado vuelve a los elementos de la interfaz de usuario siguiente o anterior o a un elemento de la interfaz de usuario más relevante.
   * Al pasar el puntero sobre las opciones, aparecen sugerencias como Seleccionar y Descargar. Es posible que los usuarios que utilizan un ampliador de pantalla no vean las miniaturas de los archivos debido a estas sugerencias. Ahora, es posible conservar el enfoque, después de eliminar la opción con la tecla `Escape`.
   * Al seleccionar una celda de cuadrícula de la cuadrícula presente en la página, el enfoque se desplaza a la barra de acciones que aparece en la pantalla.
   * Los usuarios visuales pueden diferenciar entre texto normal y un vínculo, ya que se muestran pistas visuales (subrayado e icono de chevron) para los vínculos a todas las soluciones de la página de inicio [!DNL Experience Manager].

* **Valores preestablecidos de conjunto por lotes en Dynamic Media**: Ahora puede automatizar la creación y organización de varios recursos en un conjunto de imágenes o conjuntos de giros en el momento de cargar los archivos de recursos en una carpeta, ya sea de forma individual o mediante la ingestión masiva.

   Consulte [Acerca de los ajustes preestablecidos de conjunto por lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).

* Las siguientes mejoras de accesibilidad ya están disponibles en [!DNL Dynamic Media]:

   * Los lectores de pantalla (JAWS, Narrador) narran el nombre, la función y el estado de los elementos de menú en la opción de menú Tamaño incrustado.
   * Los usuarios pueden navegar por el cuadro de diálogo Vínculo de correo electrónico mediante la tecla `Tab`.
   * El flujo de trabajo para crear perfiles de codificación de vídeo es más sencillo de utilizar, dada la mejora del lector de pantalla.
   * Al navegar con la tecla `Tab`, el enfoque se desplaza a los elementos de interfaz de usuario correspondientes en el flujo de trabajo para crear un vídeo interactivo.
   * La página Publicar, la página Editar recurso, la página Editar recortes inteligentes y la página Editor de conjuntos de imágenes se han mejorado para cumplir con los estándares web. Los usuarios de tecnología de asistencia (AT) ahora pueden navegar fácilmente por estas páginas y realizar acciones como recortar imágenes.
   * Los visores se mejoran para permitir a los usuarios navegar con un teclado.
   * Los usuarios del teclado y del lector de pantalla pueden utilizar la función de recorte.
   * Los usuarios del teclado pueden administrar mejor las zonas interactivas.

   Consulte [Accesibilidad en [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Sitio de referencia CIF Venia publicado - 2020.11.05 que incluye la última versión v1.5.0 de los componentes principales de CIF. Consulte [CIF Venia Reference Site](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) para obtener más detalles.

* Componentes principales de CIF v1.5.0. Consulte [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) para obtener más detalles.

### Corrección de errores {#bug-fixes-commerce}

* La configuración del cliente GraphQL no se leyó correctamente cuando la configuración no se especificó directamente en la configuración de Sling CA, sino en una de las configuraciones principales. Esto se ha solucionado.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de Cloud Manager en AEM como Cloud Service 2020.12.0 es el 10 de diciembre de 2020.

### Novedades en [!DNL Cloud Manager] {#what-is-new-cm}

* Administración automática de [certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md) y [nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/introduction.md).

* Administración de autoservicio de [Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/introduction.md).

* La página de detalles **Entorno** actualizada ahora permite a los usuarios administrar nombres de dominio personalizados y Listas de permitidos IP en sus entornos.

### Corrección de errores {#bug-fixes-cloud-manager}

* Algunas ocurrencias de errores en la etapa de análisis de código sin proporcionar resultados resueltos.

* La tarjeta de entorno no mostraba de forma consistente el botón **Añadir**.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Flujos de trabajo {#workflows}

* Se agregó compatibilidad para buscar instancias de flujo de trabajo en función del título del flujo de trabajo, el modelo de flujo de trabajo, el estado, el iniciador, la ruta de carga útil y la fecha de Inicio. Consulte [Instancias de flujo de trabajo de búsqueda](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### Sincronización de datos de usuario de nivel de publicación {#user-sync}

* Los datos de usuario, incluidos los atributos de perfil y las pertenencias a grupos, pueden persistir en la capa de publicación. Obtenga más información sobre esta función en [documentación de registro, inicio de sesión y Perfil de usuario](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### SDK Build Analyzers {#analyzers}

El AEM como Cloud Service SDK Build Analyzer Maven Plugin detecta problemas en un proyecto determinado, incluyendo dependencias que faltan. Ofrece a los desarrolladores la oportunidad de descubrir problemas durante el desarrollo local, mucho antes de implementarlos en Cloud entornos con Cloud Manager. Para obtener más información, consulte la documentación [aquí](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=en#developing) y [aquí](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

### Otros {#others-foundation}

La nueva sintaxis [&quot;httpd -t&quot;](/help/implementing/dispatcher/disp-overview.md#local-validation) comprueba la existencia de una configuración de apache y dispatcher ejecutada durante la compilación de Cloud Manager, que también se puede ejecutar con AEM como herramientas de despachante del SDK de Cloud Service.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades en [!DNL Code Refactoring Tools] {#what-is-new-crt}

* Se ha lanzado la nueva versión del complemento AIO-CLI. La versión más reciente de este complemento incluye correcciones de errores para AEM Dispatcher Converter y el Modernizer de Repositorio y también admite una nueva utilidad: Convertidor de índices.
Consulte [Experiencia unificada](/help/move-to-cloud-service/unified-experience.md) para obtener más información sobre este complemento.

* [Index ](/help/move-to-cloud-service/refactoring-tools/index-converter.md) Converteres una utilidad que puede utilizarse para transformar las definiciones de índice OAK personalizadas de un cliente para AEM como definiciones de índice OAK compatibles con el Cloud Service.
Consulte [Convertidor de índices](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/index-converter) para obtener más detalles.

* Se agregó una nueva función al [Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) que crea un paquete independiente `ui.config` para contener todas las configuraciones de OSGi.

### Corrección de errores {#crt-bug-fixes}

* Se han realizado varias correcciones de errores en las herramientas AEM Dispatcher Converter y el Modernizador de repositorio.
Consulte [AEM Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter) y [Modernizer del repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer).