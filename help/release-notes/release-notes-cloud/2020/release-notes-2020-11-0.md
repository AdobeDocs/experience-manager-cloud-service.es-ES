---
title: Notas de la versión 2020.11.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2020.11.0."
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
source-git-commit: bc4da79735ffa99f8c66240bfbfd7fcd69d8bc13
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 11%

---

# Notas de la versión [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de [!DNL Experience Manager] as a Cloud Service.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] El as a Cloud Service 2020.11.0 es el 2 de diciembre de 2020.
La siguiente versión (2020.12.0) será el 17 de diciembre de 2020

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* **[Ejecuta Administración de jerarquía](/help/sites-cloud/authoring/launches/managing-pages.md) &amp; [Deformación de tiempo futura](/help/sites-cloud/authoring/launches/preview.md)**: La nueva interfaz de usuario para agregar o eliminar páginas dentro de un lanzamiento, y al explorar el sitio con Deformación de tiempo, se muestra el estado futuro de los lanzamientos.

* **[Ampliación de modelos y editor de fragmentos de contenido](/help/assets/content-fragments/content-fragments-models.md)**: En la interfaz de usuario de Assets se muestran y se pueden buscar nuevas opciones para la validación de entradas en varios tipos de datos, el tipo de datos de enumeración mejorado con nuevas visualizaciones de formulario y el nombre del modelo de fragmento de contenido.

* **Ordenar las páginas de Live Copy disponibles para el despliegue**: Nueva opción para ordenar las páginas de Live Copy disponibles para el despliegue mediante la [!UICONTROL Nombre], [!UICONTROL Fecha de la última modificación]y [!UICONTROL Última fecha de lanzamiento] propiedades. La variable [!UICONTROL Última fecha de lanzamiento] para una página es una nueva propiedad introducida.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novedades de [!DNL Assets] y [!DNL Dynamic Media] {#what-is-new-assets}

* **ingesta masiva de recursos**: Proporcione a los clientes un servicio de ingesta escalable y nativo de la nube que aproveche [!DNL Experience Manager] Arquitectura as a Cloud Service que incluye microservicios de recursos. Los casos de uso clave incluyen la ingesta a escala con supervisión, creación de informes y programación, mientras que permiten la transferencia inicial de recursos a almacenes de datos en la nube mediante herramientas comunes de carga en la nube. Consulte [herramienta de ingesta masiva de recursos](/help/assets/add-assets.md#asset-bulk-ingestor).

   Esta herramienta es para administradores del sistema, consultores o socios de implementación. Esta función permite la ingesta a gran escala y se utiliza de forma ideal durante la ingesta inicial u ocasional ingesta a gran escala. Para trabajos de ingesta más pequeños, utilice la variable [[!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) o [cargar mediante la interfaz de usuario de Assets](/help/assets/add-assets.md#upload-assets).

   ![Configuración del importador masivo](/help/assets/assets/bulk-import-config-low-res.png)

* Los usuarios ahora pueden ordenar los recursos digitales en las vistas de tarjeta y columna.

   ![ordenar recursos](/help/assets/assets/asset-sort-options.png)

* Las siguientes mejoras se han realizado para mejorar la accesibilidad en [!DNL Experience Manager Assets] en esta versión. Para obtener más información, consulte [funciones de accesibilidad de [!DNL Assets]](/help/assets/accessibility.md).

   * Al navegar por la cronología con un teclado, la tecla Esc puede contraer la opción Mostrar todo sin perder el foco.
   * Al navegar mediante la tecla de tabulación del teclado, después de eliminar la última etiqueta de las etiquetas agregadas, el campo de etiqueta mantiene el foco.
   * [!DNL Experience Manager] los componentes ahora contienen información apropiada sobre el nombre, la función y el valor que deben utilizar los lectores de pantalla.
   * Después de eliminar el cuadro combinado Tipo/Tamaño, el cuadro combinado Vínculo, el cuadro combinado Idioma o el cuadro de edición de texto, el foco del teclado vuelve a los elementos de la interfaz de usuario siguientes o anteriores, o a un elemento de la interfaz de usuario más relevante.
   * Al pasar el puntero sobre las opciones, aparecen sugerencias como Seleccionar y Descargar. Es posible que los usuarios que utilizan un ampliador de pantalla no vean las miniaturas del archivo debido a estas sugerencias. Ahora, es posible conservar el enfoque, después de eliminar la opción mediante `Escape` clave.
   * Al seleccionar una celda de cuadrícula de la cuadrícula presente en la página, el foco se desplaza a la barra de acciones que aparece en la pantalla.
   * Los usuarios visuales pueden diferenciar entre texto normal y un vínculo, ya que se muestran pistas visuales (subrayado e icono de cheurón) para los vínculos a todas las soluciones de [!DNL Experience Manager] página principal.

* **Ajustes preestablecidos de conjuntos de lotes en Dynamic Media**: Ahora puede automatizar la creación y organización de varios recursos en un conjunto de imágenes o conjunto de giros en el momento de cargar archivos de recursos en una carpeta, ya sea de forma individual o mediante la ingesta masiva.

   Consulte [Acerca de los ajustes preestablecidos de conjuntos de lotes](/help/assets/dynamic-media/batch-set-presets-dm.md).

* Las siguientes mejoras de accesibilidad ya están disponibles en [!DNL Dynamic Media]:

   * Los lectores de pantalla (JAWS, Narrador) narran el nombre, la función y el estado de los elementos de menú en la opción de menú Tamaño incrustado .
   * Los usuarios pueden navegar por el cuadro de diálogo Vínculo de correo electrónico utilizando el `Tab` clave.
   * El flujo de trabajo para crear perfiles de codificación de vídeo es más sencillo de usar, dada la mejora del lector de pantalla.
   * Al navegar mediante `Tab` , el enfoque se desplaza a los elementos de interfaz de usuario correspondientes en el flujo de trabajo para crear un vídeo interactivo.
   * La página Publicar , la página Editar recurso , la página Editar recortes inteligentes y la página Editor de conjuntos de imágenes se han mejorado para cumplir con los estándares web. Los usuarios de tecnología de asistencia (AT) ahora pueden navegar fácilmente por estas páginas y realizar acciones como recortar imágenes.
   * Se han mejorado los visualizadores para que los usuarios puedan navegar mediante un teclado.
   * Los usuarios del teclado y del lector de pantalla pueden utilizar la funcionalidad de recorte.
   * Los usuarios del teclado pueden administrar mejor las zonas interactivas.

   Consulte [Accesibilidad en [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Sitio de referencia de Venia del CIF publicado - 2020.11.05 que incluye la última versión v1.5.0 de los componentes principales del CIF. Consulte [Sitio de referencia de Venia del CIF](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) para obtener más información.

* Componentes principales de CIF v1.5.0. Consulte [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) para obtener más información.

### Correcciones de errores {#bug-fixes-commerce}

* La configuración del cliente de GraphQL no se leyó correctamente cuando la configuración no se especificó directamente en la configuración de Sling CA, sino en una de las configuraciones principales. Esto se ha corregido.

## Cloud Manager {#cloud-manager}

### Fecha de la versión {#release-date-cm}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2020.11.0 es el 12 de noviembre de 2020.

### Novedades de [!DNL Cloud Manager] {#what-is-new-cm}

* Una nueva opción de menú **Inicio de sesión local** ahora está disponible para los usuarios desde las opciones de menú de entorno de la **Entornos** tarjeta y **Entornos** páginas de resumen.
Consulte [Administración de entornos](/help/implementing/cloud-manager/manage-environments.md#login-locally) para obtener más información.

* La variable **Más información** en Cloud Manager se ha actualizado con nuevas imágenes en la interfaz de usuario.

### Correcciones de errores {#bug-fixes-cloud-manager}

* La carga de dependencias realizada antes de la ejecución de la compilación requería la descarga de un complemento de Maven.
* El vínculo del pie de página de Cloud Manager para seleccionar un idioma ahora se desplaza a la ubicación correcta.
* A veces, durante la digitalización del código, el proceso SonarQube no se iniciaba. Esto se detectará automáticamente y se intentará reiniciar.
* Todas las canalizaciones de producción existentes se habilitarán automáticamente con el paso Auditoría de experiencias .

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Flujos de trabajo {#workflows}

* Se agregó compatibilidad para buscar instancias de flujo de trabajo en función del título del flujo de trabajo, el modelo de flujo de trabajo, el estado, el iniciador, la ruta de carga útil y la fecha de inicio. Consulte [Buscar instancias de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### Sincronización de datos de usuario del nivel de publicación {#user-sync}

* Los datos de usuario, incluidos los atributos de perfil y las suscripciones a grupos, se pueden mantener en el nivel de publicación. Obtenga más información sobre esta función en [Documentación de registro, inicio de sesión y perfil de usuario](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### Analizadores de creación de SDK {#analyzers}

El complemento Maven de AEM as a Cloud Service SDK Build Analyzer detecta problemas en un proyecto maven, incluidas las dependencias que faltan. Proporciona a los desarrolladores la oportunidad de descubrir problemas durante el desarrollo local, mucho antes de implementarlos en entornos de nube con Cloud Manager. Para obtener más información, consulte la documentación [here](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=es#developing) y [here](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

### Otros {#others-foundation}

Nuevo [Sintaxis &quot;httpd -t&quot;](/help/implementing/dispatcher/disp-overview.md#local-validation) compruebe si se ha ejecutado la configuración de apache y dispatcher durante la compilación de Cloud Manager, que también se puede ejecutar mediante AEM herramientas de Dispatcher del SDK as a Cloud Service.

## Herramienta de transferencia de contenido {#content-transfer-tool}

Siga esta sección para conocer las novedades y las actualizaciones de [Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html) Versión 1.1.12.

### Novedades {#what-is-new-ctt}

* Se ha mejorado la experiencia del usuario con los registros. Marcas de hora agregadas a los registros de extracción e ingesta. Mensaje añadido para indicar si los registros están vacíos.

### Correcciones de errores {#ctt-bug-fixes}

* La herramienta de transferencia de contenido omitía los archivos de contenido si el conjunto de migración contenía rutas con nombres de archivo parcialmente similares. Esto se ha corregido.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer es el 13 de noviembre de 2020.

### Novedades de [!DNL Best Practices Analyzer] {#what-is-new-bpa}

* Cloud Readiness Analyzer es ahora el Analizador de prácticas recomendadas (BPA). BPA proporciona una evaluación de prácticas recomendadas de su implementación de AEM actual y ayuda a evaluar la preparación para pasar de una instancia de AEM existente a AEM as a Cloud Service.

* Se ha añadido un nuevo detector para detectar el uso de `java.io.InputStream`, que puede causar problemas si se utiliza en AEM as a Cloud Service.

### Correcciones de errores {#bpa-bug-fixes}

* Error que causa los positivos relacionados con la variable *base de campo de texto* se ha corregido.
