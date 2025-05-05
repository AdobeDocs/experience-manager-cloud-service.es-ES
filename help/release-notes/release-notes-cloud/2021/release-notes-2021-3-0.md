---
title: Notas de la versión 2021.3.0 de la versión de  [!DNL Adobe Experience Manager]  as a Cloud Service.
description: "[!DNL Adobe Experience Manager] notas de la versión as a Cloud Service para 2021.3.0."
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1271'
ht-degree: 35%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>Desde aquí puede navegar hasta las notas de versiones anteriores; por ejemplo, las de 2020, 2021, etc.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de lanzamiento {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] as a Cloud Service 2021.3.0 es el 25 de marzo de 2021.
La de la siguiente versión (2021.4.0) será el 29 de abril de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* [Ahora se puede habilitar una versión de aplicación web progresiva (PWA) de un sitio](/help/sites-cloud/authoring/sites-console/enable-pwa.md) en el nivel de proyecto mediante una configuración simple.
* Extensiones del modelo de fragmentos de contenido: ahora es posible definir tipos de datos de texto multilínea como listas de varios campos.
* Mejoras en la experiencia de usuario del editor de fragmentos de contenido: los fragmentos secundarios anidados ahora se muestran en la ruta de exploración y se mejora la vista de las acciones de publicar, guardar, y guardar y salir

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novedades de [!DNL Assets] {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] amplía la funcionalidad de Assets conectado para admitir el uso de imágenes de [!DNL Dynamic Media] en los componentes principales admitidos. Consulte [usar Assets conectado](/help/assets/use-assets-across-connected-assets-instances.md).
* Los administradores de Experience Manager pueden programar las ingestas masivas de recursos en una fecha u hora específicas. Además, los administradores pueden programar ingestas recurrentes en función de la fecha y la hora. Consulte [ingesta masiva de recursos](/help/assets/add-assets.md#asset-bulk-ingestor).

### Correcciones de errores en [!DNL Assets] {#bug-fixes-assets}

* La página de copyright no se muestra al intentar descargar varios recursos administrados por derechos. (CQ-4314403)
* Al elegir editar un archivo INDD, la resolución cambia inesperadamente. (CQ-4317376)
* Solo la última página de la plantilla de InDesign está allí en la representación del PDF. (CQ-4317305)
* El selector de etiquetas tarda mucho en abrirse cuando forma parte de un esquema de metadatos complejo. (CQ-4316426)
* Al cargar un recurso con el mismo nombre de archivo que uno existente, no aparece el cuadro de diálogo de conflicto de nombres para solicitar al usuario que cree una versión. (CQ-4315424)
* Las propiedades de metadatos de carpeta se pueden definir y guardar en el menú emergente de la página Propiedades de una carpeta. Mientras la selección se guarda en el repositorio, no se muestra cuando se abren de nuevo las Propiedades de metadatos de carpeta. (CQ-4314429)
* Assets con nombres de archivo que contienen espacios o caracteres especiales se cargan mediante el explorador. (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] as a [!DNL Cloud Service] {#forms}

AEM Forms ha ayudado a muchas organizaciones a ofrecer buenas experiencias de incorporación y registro a lo largo de los años. Estas experiencias han ayudado a las organizaciones a convertir posibles clientes en ventas, a procesar los datos capturados de los clientes, a ofrecer experiencias adaptables basadas en el perfil de audiencia y a mucho más. Ahora, AEM Forms está disponible como servicio en la nube.

Puede usar [AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html?lang=es) para crear formularios digitales, conectar formularios a fuentes de datos existentes, integrar formularios con Adobe Sign para agregar firmas electrónicas a formularios y generar documentos de registro (DoR) para archivar formularios enviados como archivos de PDF. El servicio también puede convertir los PDF forms existentes en formularios digitales. Además de las funciones estándar de AEM Forms, el servicio ofrece varias funciones nativas de la nube, como escalado automático, tiempo de inactividad cero para las actualizaciones y un entorno de desarrollo nativo en la nube.

Póngase en contacto con el representante de su Adobe para ver una demostración o regístrese para usar el servicio.

## as a Cloud Service de Adobe Experience Manager Commerce {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Compatibilidad con Adobe Commerce 2.4.2

* Ahora, el componente de detalles del producto se puede utilizar y configurar en cualquier página de contenido

* CIF CIF Lanzamiento del sitio de referencia de Venia el 25 de marzo de 2021, que incluye la versión más reciente de componentes principales (v1.9.0) de la versión de Venia. CIF Consulte [Sitio de referencia de Venia en el que se hace referencia a Venia](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25) para obtener más información.

* CIF Lanzamiento de los componentes principales de la versión 1.9.0 de. CIF Consulte [Componentes principales](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0) para obtener más información.


## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.3.0.

## Fecha de lanzamiento {#release-date-cm-march}

La fecha de lanzamiento de Cloud Manager en AEM as a Cloud Service 2021.3.0 es el 11 de marzo de 2021.
La próxima versión está planificada para el viernes, 08 de abril de 2021.

### Novedades {#what-is-new-march}

* Los clientes con entornos con configuraciones de nombre de dominio personalizado preexistentes para [Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn), [certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) y [nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) ven un mensaje sobre las configuraciones existentes anteriormente y pueden servirse automáticamente a través de la interfaz de usuario.

* Los usuarios con los permisos necesarios ahora pueden editar un programa, lo que les permite hacer lo siguiente en forma de autoservicio:

   * Agregar la solución Sites a un programa existente con Assets o a la inversa.
   * Eliminar Sites o Assets de un programa existente que incluya ambos.
   * Agregar el derecho a una solución no utilizada a un programa existente o como un nuevo programa.

* AEM Ahora se mostrará la etiqueta **Actualización de push de** para las pantallas *Ejecución de canalización* y *Actividad*.

* Si un entorno está en hibernación pero también hay una actualización de AEM disponible, el estado **Hibernado** tendrá prioridad sobre **Actualización disponible**.

* Los usuarios ahora pueden ver sus roles de Cloud Manager al seleccionar la opción “Ver roles de Cloud Manager” después de navegar hasta el icono del perfil de usuario (parte superior derecha) de Unified Shell.

* La etiqueta **Solicitud de aprobación** se ha vuelto a etiquetar como **Aprobación de producción** para una mayor claridad.

* La etiqueta **Versión** se ha vuelto a etiquetar como **Etiqueta de Git** en la pantalla de ejecución de la canalización de producción.

* Las etiquetas que definen el comportamiento cuando métricas importantes no alcanzan el umbral definido se han vuelto a etiquetar para reflejar su verdadero comportamiento: **Cancelar inmediatamente** y **Aprobar inmediatamente**.

* Las listas de desaprobación de clases y métodos se han actualizado en función de la versión `2021.3.4997.20210303T022849Z-210225` del SDK de AEM Cloud Service.

* La canalización de producción de Cloud Manager ahora incluye la capacidad [Pruebas de IU personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing).

### Correcciones de errores {#bug-fixes-cm-march}

* En algunos casos, las versiones de paquetes se omitían durante actualización push de AEM.

* Algunos problemas de calidad no se veían correctamente cuando los paquetes estaban incrustados en otros paquetes.

* En situaciones oscuras, el nombre predeterminado del programa generado al abrir el cuadro de diálogo Agregar programa podía ser un duplicado de un nombre de programa existente.

* En ocasiones, si el usuario sale de la página de ejecución de la canalización inmediatamente después de iniciar una canalización, aparecía un mensaje de error que indicaba que la acción había fallado, aunque la ejecución realmente se iniciaba.

* El paso de generación se reiniciaba innecesariamente cuando las generaciones de clientes generaban paquetes no válidos.

* En ocasiones, el usuario podía ver el estado “activo” verde junto a una lista de IP permitidas incluso cuando esa configuración no se implementaba.

* Todas las canalizaciones de producción existentes se habilitan automáticamente con el paso Auditoría de experiencias.

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.3.4 es el 19 de marzo de 2021.

### Correcciones de errores {#bug-fixes-ctt}

* CTT omitía contenido de carpetas con el mismo nombre pero con un guion en el nombre. Esto se ha corregido.

### Fecha de lanzamiento {#release-date-ctt-march}

La fecha de versión de la herramienta de transferencia de contenido v1.3.0 es el 4 de marzo de 2021.

### Novedades de la herramienta de transferencia de contenido {#what-is-new-ctt-march}

* Ahora, CTT se instala en `/apps` en lugar de `/libs`. Es posible que los marcadores del explorador en determinadas páginas ya no sean válidos.
* Cuando se instala CTT, el usuario debe desplazarse a un nivel adicional para llegar a la página de transferencia de contenido. Consulte [Uso de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html?lang=es) para obtener más información.

### Correcciones de errores {#bug-fixes-ctt-march}

* Al migrar contenido desde una ruta específica, CTT extraía recursos no relacionados. Esto se ha corregido.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de lanzamiento del Analizador de prácticas recomendadas v2.1.8 es el 22 de marzo de 2021.

### Novedades del Analizador de prácticas recomendadas {#what-is-new-bpa}

* Capacidad para filtrar los resultados de ACS Commons desde el informe BPA en la interfaz de usuario y desde el informe exportado como archivo CSV.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades de las herramientas de refactorización de código {#what-is-new-crt}

* Nuevas funciones y mejoras para el Modernizador de repositorios. Consulte [Recurso de GitHub: Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para obtener la versión más reciente.
   * Normalice las configuraciones de OSGi (excepto las configuraciones de RepoInit) al formato .cfg.json preferido.
   * Cambie el nombre de las carpetas de configuración de OSGi al formato especificado.
   * Genere el proyecto ui.apps.structure.
   * Cree el módulo de análisis.

* Nuevas funciones y mejoras para Dispatcher Converter. Ver [recurso de GitHub: Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * Creación de archivos independientes para diferentes inclusiones en lugar de en la alineación del contenido.
   * Capacidad para gestionar tanto la ruta de carpeta de vhosts como la ruta a los archivos vhost.
   * Generación de archivos de granja con grandes configuraciones de cliente en el rango de 600 y más.
