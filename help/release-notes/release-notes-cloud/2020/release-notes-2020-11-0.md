---
title: Notas de la versión 2020.11.0 de la versión de [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2020.11.0."
exl-id: 8066c0fb-c2f5-4625-9448-b0c74ff4e192
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 18%

---

# Notas de la versión para [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de [!DNL Experience Manager] as a Cloud Service.

## Fecha de lanzamiento {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] as a Cloud Service 2020.11.0 es el 2 de diciembre de 2020.
La de la siguiente versión (2020.12.0) será el 17 de diciembre de 2020

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

### Novedades de [!DNL Sites] {#what-is-new-sites}

* **[Inicia Administración de jerarquía](/help/sites-cloud/authoring/launches/managing-pages.md) &amp; [Deformación de tiempo futura](/help/sites-cloud/authoring/launches/preview.md)**: nueva interfaz de usuario para añadir o quitar páginas dentro de un lanzamiento y al navegar por el sitio con Deformación de tiempo se muestra el estado futuro de los lanzamientos.

* **[Editor y modelos de fragmentos de contenido extendidos](/help/assets/content-fragments/content-fragments-models.md)**: nuevas opciones para la validación de entrada en varios tipos de datos, tipo de datos de enumeración mejorado con nuevas visualizaciones de formulario, y el nombre del modelo de fragmento de contenido se muestra y se puede buscar en la interfaz de usuario de Assets.

* **Ordenar las páginas de Live Copy disponibles para el despliegue**: nueva opción para ordenar las páginas de Live Copy disponibles para su despliegue mediante el [!UICONTROL Nombre], [!UICONTROL Fecha de la última modificación], y [!UICONTROL Última fecha de despliegue] propiedades. El [!UICONTROL Última fecha de despliegue] para una página es una nueva propiedad introducida.

## [!DNL Adobe Experience Manager Assets] as a Cloud Service {#assets}

### Novedades de la versión [!DNL Assets] y [!DNL Dynamic Media] {#what-is-new-assets}

* **Ingesta masiva de recursos**: proporcione a los clientes un servicio de ingesta escalable y nativo de la nube que utilice [!DNL Experience Manager] Arquitectura as a Cloud Service, incluidos los microservicios de recursos. Los casos de uso clave incluyen la ingesta a escala con monitorización, creación de informes y programación, a la vez que permiten la transferencia inicial de recursos a los almacenes de datos en la nube mediante herramientas comunes de carga en la nube. Consulte [herramienta ingestor masivo de recursos](/help/assets/add-assets.md#asset-bulk-ingestor).

  Esta herramienta es para usuarios administradores del sistema, consultores o socios de implementación. Esta función permite la ingesta a gran escala y se utiliza idealmente durante la ingesta inicial o la ingesta ocasional a gran escala. Para trabajos de ingesta más pequeños, utilice el [[!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html?lang=en) o [carga mediante la interfaz de usuario de Assets](/help/assets/add-assets.md#upload-assets).

  ![Configuración del importador en bloque](/help/assets/assets/bulk-import-config-low-res.png)

* Los usuarios ahora pueden ordenar los recursos digitales en las vistas de tarjetas y columnas.

  ![ordenar recursos](/help/assets/assets/asset-sort-options.png)

* Se han realizado las siguientes mejoras para la accesibilidad en [!DNL Experience Manager Assets] en esta versión. Para obtener más información, consulte [funciones de accesibilidad en [!DNL Assets]](/help/assets/accessibility.md).

   * Al navegar por la cronología con un teclado, la tecla Esc puede contraer la opción Mostrar todo sin perder el enfoque.
   * Al navegar con la tecla de tabulación del teclado, después de eliminar la última etiqueta de las etiquetas añadidas, el campo de etiqueta mantiene el enfoque.
   * [!DNL Experience Manager] Los componentes de ahora contienen información adecuada sobre el nombre, la función y el valor que deben utilizar los lectores de pantalla.
   * Después de eliminar el cuadro combinado Tipo/Tamaño, el cuadro combinado Vínculo, el cuadro combinado Idioma o el cuadro de edición Texto, el foco del teclado vuelve al siguiente o al anterior elemento de interfaz de usuario o a un elemento de interfaz de usuario más relevante.
   * Al pasar el puntero sobre las opciones, aparecen sugerencias como Seleccionar y Descargar. Los usuarios que utilizan un ampliador de pantalla pueden no ver las miniaturas del archivo debido a estas sugerencias. Ahora, es posible conservar el enfoque después de eliminar la opción utilizando `Escape` clave.
   * Al seleccionar una celda de cuadrícula de la cuadrícula presente en la página, el enfoque cambia a la barra de acciones que aparece en la pantalla.
   * Los usuarios visuales pueden diferenciar entre texto normal y un vínculo, ya que se muestran pistas visuales (subrayado y cheurón) para los vínculos a todas las soluciones en [!DNL Experience Manager] página principal.

* **Ajustes preestablecidos de conjunto de lotes en Dynamic Media**: Ahora puede automatizar la creación y organización de varios recursos en un conjunto de imágenes o conjuntos de giros en el momento de cargar archivos de recursos en una carpeta, ya sea de forma individual o mediante ingesta masiva.

  Consulte [Acerca de los ajustes preestablecidos del lote](/help/assets/dynamic-media/batch-set-presets-dm.md).

* Las siguientes mejoras de accesibilidad ya están disponibles en [!DNL Dynamic Media]:

   * Los lectores de pantalla (JAWS, Narrador) narran el nombre, la función y el estado de los elementos de menú en la opción de menú Tamaño incrustado.
   * Los usuarios pueden navegar por el cuadro de diálogo Vínculo de correo electrónico mediante la variable `Tab` clave.
   * El flujo de trabajo para crear perfiles de codificación de vídeo es más fácil de usar dada la mejora del lector de pantalla.
   * Al navegar mediante `Tab` , el enfoque se desplaza a los elementos de la interfaz de usuario adecuados en el flujo de trabajo para crear un vídeo interactivo.
   * La página Publicar, la página Editar recurso, la página Editar recortes inteligentes y la página Editor de conjuntos de imágenes se han mejorado para cumplir con los estándares web. Los usuarios de tecnología de asistencia (AT) ahora pueden navegar fácilmente por estas páginas y realizar acciones como recortar imágenes.
   * Se han mejorado los visores para permitir que los usuarios naveguen con un teclado.
   * Los usuarios del teclado y del lector de pantalla pueden utilizar la funcionalidad de recorte.
   * Los usuarios del teclado pueden administrar mejor los puntos interactivos.

  Consulte [Accesibilidad en [!DNL Dynamic Media]](/help/assets/dynamic-media/accessibility-dm.md).

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Lanzamiento del sitio de referencia de CIF Venia el 11 de noviembre de 2020, que incluye la versión más reciente de los componentes principales de CIF v1.5.0. Consulte [Sitio de referencia de CIF Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2020.10.27) para obtener más información.

* Componentes principales de CIF v1.5.0. Consulte [Componentes principales del CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.5.0) para obtener más información.

### Correcciones de errores {#bug-fixes-commerce}

* La configuración del cliente de GraphQL no se leyó correctamente cuando la configuración no se especifica directamente en la configuración de la CA de Sling, sino en una de las configuraciones principales. Esto se ha corregido.

## Cloud Manager {#cloud-manager}

### Fecha de lanzamiento {#release-date-cm}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2020.11.0 es el 12 de noviembre de 2020.

### Novedades de [!DNL Cloud Manager] {#what-is-new-cm}

* Una nueva opción de menú **Inicio de sesión local** ahora está disponible para los usuarios de en las opciones del menú de entorno de **Entornos** tarjeta y **Entornos** páginas de resumen.
Consulte [Administrar entornos](/help/implementing/cloud-manager/manage-environments.md#login-locally) para obtener más información.

* La pestaña **Más información** en Cloud Manager se ha actualizado con nuevas imágenes en la interfaz de usuario.

### Correcciones de errores {#bug-fixes-cloud-manager}

* La carga de dependencias realizada antes de la ejecución de la generación requería la descarga de un complemento de Maven.
* El vínculo del pie de página de Cloud Manager para seleccionar un lenguaje ahora le llevará hasta la ubicación correcta.
* A veces, durante la digitalización del código, el proceso SonarQube no se iniciaba. Ahora, esto se detectará automáticamente y se intentará reiniciar.
* Todas las canalizaciones de producción existentes se habilitan automáticamente con el paso Auditoría de experiencias.

## Adobe Experience Manager as a Cloud Service Foundation {#cloud-service-foundation}

### Flujos de trabajo {#workflows}

* Se agregó compatibilidad para buscar instancias de flujo de trabajo basadas en el Título de flujo de trabajo, Modelo de flujo de trabajo, Estado, Iniciador, Ruta de carga útil y Fecha de inicio. Consulte [Buscar instancias de flujo de trabajo](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites/administering/workflows-administering.html).

### Sincronización de datos de usuario del nivel de publicación {#user-sync}

* Los datos de usuario, incluidos los atributos de perfil y los miembros de grupo, se pueden mantener en el nivel de publicación. Obtenga más información acerca de esta función en [Documentación de registro, inicio de sesión y perfil de usuario](/help/sites-cloud/authoring/personalization/user-and-group-sync-for-publish-tier.md).

### Analizadores de creación de SDK {#analyzers}

El complemento Maven de AEM as a Cloud Service SDK Build Analyzer detecta problemas en un proyecto maven, incluidas las dependencias que faltan. Proporciona a los desarrolladores la oportunidad de descubrir problemas durante el desarrollo local, mucho antes de implementarlos en entornos de nube con Cloud Manager. Para obtener más información, consulte la documentación [aquí](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html?lang=es#developing) y [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/aem-as-a-cloud-service-sdk.html?lang=en#building-for-the-sdk).

### Otros {#others-foundation}

Nuevo [Sintaxis &quot;httpd -t&quot;](/help/implementing/dispatcher/disp-overview.md#local-validation) AEM compruebe la configuración de apache y dispatcher ejecutada durante la compilación de Cloud Manager, que también se puede ejecutar mediante las herramientas de Dispatcher del SDK as a Cloud Service.

## Herramienta de transferencia de contenido {#content-transfer-tool}

Siga esta sección para conocer las novedades y las actualizaciones de [Herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/overview-content-transfer-tool.html?lang?es) Versión v1.1.12.

### Novedades {#what-is-new-ctt}

* Se ha mejorado la experiencia del usuario con registros. Marcas de hora agregadas a los registros de extracción e ingesta. Se ha agregado un mensaje para indicar si los registros están vacíos.

### Correcciones de errores {#ctt-bug-fixes}

* La herramienta de transferencia de contenido omitía los archivos de contenido si el conjunto de migración contenía rutas con nombres de archivo parcialmente similares. Esto se ha corregido.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas es el 13 de noviembre de 2020.

### Novedades de [!DNL Best Practices Analyzer] {#what-is-new-bpa}

* Ahora, el Analizador de preparación para la nube es el Analizador de prácticas recomendadas (BPA). AEM AEM AEM BPA proporciona una evaluación de las prácticas recomendadas de su implementación actual de y ayuda a evaluar la preparación para pasar de una instancia de existente a una instancia de as a Cloud Service.

* Se ha añadido un nuevo detector para detectar el uso de `java.io.InputStream`AEM , que puede causar problemas si se utiliza en as a Cloud Service.

### Correcciones de errores {#bpa-bug-fixes}

* Error que causa los positivos relacionados con *textfield foundation* el componente se ha corregido.
