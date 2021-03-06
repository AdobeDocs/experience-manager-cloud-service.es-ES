---
title: Notas de la versión 2021.3.0 de la versión  [!DNL Adobe Experience Manager] as a Cloud Service.
description: '"[!DNL Adobe Experience Manager] Notas de la versión as a Cloud Service para 2021.3.0."'
exl-id: 0c07364c-ba25-4081-8e35-3c1c84ed556f
source-git-commit: 71647239fc5e740faa25524a01a8ef21ed2d7a3b
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 10%

---

# Notas de la versión actuales de [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

En la siguiente sección se describen las notas de la versión generales de la versión actual (la más reciente) de [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>Desde aquí puede navegar hasta las notas de versiones de versiones anteriores; por ejemplo, para los de 2020, 2021 y así sucesivamente.

>[!NOTE]
>
>Consulte [Actualizaciones recientes de la documentación](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html?lang=es) para obtener más información sobre las actualizaciones de la documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de lanzamiento de [!DNL Adobe Experience Manager] El as a Cloud Service 2021.3.0 es el 25 de marzo de 2021.
La siguiente versión (2021.4.0) se publicará el 29 de abril de 2021.

## [!DNL Adobe Experience Manager Sites] as a Cloud Service {#sites}

* [Versión progresiva de la aplicación web (PWA) de un sitio](/help/sites-cloud/authoring/features/enable-pwa.md) ahora se puede habilitar en el nivel de proyecto mediante una configuración sencilla.
* Extensiones del modelo de fragmento de contenido : ahora es posible definir tipos de datos de texto multilínea como listas de varios campos.
* Mejoras en la experiencia de usuario del editor de fragmentos de contenido: los fragmentos secundarios anidados ahora se muestran en la ruta de exploración y se mejora la vista de las acciones de publicación, guardado y guardado&amp;salida

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

### Novedades de [!DNL Assets] {#what-is-new-assets}

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  

Indicators for expired, approved, and rejected statuses now available for assets in Column view.

Ability to select a root path. select if a minimum number of tags is required. 

Add a Boolean or radio widget type to metadata schema setup. -->

* [!DNL Experience Manager] amplía la funcionalidad Recursos conectados para admitir el uso de [!DNL Dynamic Media] imágenes en los componentes principales admitidos. Consulte [usar recursos conectados](/help/assets/use-assets-across-connected-assets-instances.md).
* Los administradores de Experience Manager pueden programar las ingestas masivas de recursos en una fecha u hora específicas. Además, los administradores pueden programar ingestas recurrentes en función de la fecha y la hora. Consulte [ingesta masiva de recursos](/help/assets/add-assets.md#asset-bulk-ingestor).

### Correcciones de errores en [!DNL Assets] {#bug-fixes-assets}

* La página de copyright no se muestra al intentar descargar varios recursos administrados por derechos. (CQ-4314403)
* Al elegir editar un archivo INDD, la resolución cambia inesperadamente. (CQ-4317376)
* Solo la última página de la plantilla de InDesign está allí en la representación del PDF. (CQ-4317305)
* El selector de etiquetas tarda mucho en abrirse cuando forma parte de un esquema de metadatos complejo. (CQ-4316426)
* Al cargar un recurso con el mismo nombre de archivo que uno existente, no se muestra el cuadro de diálogo de conflicto de nombres para pedir al usuario que cree una versión. (CQ-4315424)
* Las propiedades de metadatos de carpeta se pueden establecer y guardar desde el menú emergente de la página Propiedades de una carpeta. Mientras la selección se guarda en el repositorio, no se muestra cuando se vuelven a abrir las Propiedades de metadatos de carpeta . (CQ-4314429)
* Los recursos con nombres de archivo que contienen espacios o caracteres especiales se cargan mediante el explorador. (CQ-4318381)

## [!DNL Adobe Experience Manager Forms] como [!DNL Cloud Service] {#forms}

AEM Forms ha ayudado a muchas organizaciones a ofrecer buenas experiencias de incorporación e inscripción a lo largo de los años. Estas experiencias han ayudado a las organizaciones a convertir posibles clientes en ventas, a procesar los datos capturados de los clientes, a ofrecer experiencias adaptables basadas en el perfil de audiencia y mucho más. Ahora, AEM Forms está disponible como servicio en la nube.

Puede usar [AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-forms-cloud-service/forms/home.html) para crear formularios digitales, conecte formularios a orígenes de datos existentes, integre formularios con Adobe Sign para agregar firmas electrónicas a formularios, genere un documento de registro (DoR) para archivar formularios enviados como archivos PDF. El servicio también puede convertir los PDF forms existentes en formularios digitales. Además de las funciones estándar de AEM Forms, el servicio ofrece varias funciones nativas de la nube, como el escalado automático, el tiempo de inactividad cero para las actualizaciones y el entorno de desarrollo nativo de la nube. Lectura [esta publicación de blog](https://blog.adobe.com/en/publish/2021/03/11/experience-manager-forms-as-a-cloud-service.html) para obtener más información sobre las funciones y características de AEM Forms as a Cloud Service.

Póngase en contacto con el representante de su Adobe para realizar una demostración o registrarse en el servicio.

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Compatibilidad con Adobe Commerce 2.4.2

* Ahora, el componente de detalle del producto se puede utilizar y configurar en cualquier página de contenido

* Sitio de referencia de Venia del CIF publicado - 2021.03.25 que incluye la última versión v1.9.0 de los componentes principales del CIF. Consulte [Sitio de referencia de Venia del CIF](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.03.25) para obtener más información.

* Componentes principales del CIF v1.9.0. Consulte [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.9.0) para obtener más información.


## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión para Cloud Manager en AEM as a Cloud Service 2021.3.0.

## Fecha de la versión {#release-date-cm-march}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.3.0 es el 11 de marzo de 2021.
La próxima versión está planificada para el 08 de abril de 2021.

### Novedades {#what-is-new-march}

* Clientes con entornos con configuraciones de nombre de dominio personalizado preexistentes para [LISTAS DE PERMITIDOS IP](/help/implementing/cloud-manager/ip-allow-lists/managing-ip-allow-lists.md#pre-existing-cdn), [Certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md#pre-existing-cdn) y [Nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) Verá un mensaje sobre las configuraciones existentes anteriormente y podrá autoabastecerse a través de la interfaz de usuario.

* Los usuarios con los permisos necesarios ahora pueden editar un programa, lo que les permite hacer lo siguiente de forma autoservicio:

   * Agregar la solución Sitios a un programa existente con Assets o viceversa.
   * Elimine Sitios o Recursos de un programa existente con Sitios y Recursos.
   * Agregue el derecho a una solución no utilizada a un programa existente o como un nuevo programa.

* **Actualización de AEM** la etiqueta ahora se muestra para ambos *Ejecución de canalización* y *Actividad* pantallas.

* Si un entorno está en hibernación pero también hay una actualización de AEM disponible, la variable **Hibernado** el estado tendrá prioridad sobre **Actualización disponible**.

* Los usuarios ahora pueden ver sus funciones de Cloud Manager seleccionando la opción &quot;Ver funciones de Cloud Manager&quot; después de navegar al icono de perfil de usuario (parte superior derecha) del shell unificado.

* La etiqueta **Solicitud de aprobación** se ha vuelto a etiquetar como **Aprobación de producción** para una buena claridad.

* La variable **Versión** se ha vuelto a etiquetar como **Etiqueta de Git** en la pantalla de ejecución de la canalización de producción.

* Las etiquetas que definen el comportamiento cuando métricas importantes no alcanzan el umbral definido se han vuelto a etiquetar para reflejar su verdadero comportamiento: **Cancelar inmediatamente** y **Aprobar inmediatamente**.

* Las listas de desaprobación de clases y métodos se han actualizado en función de la versión `2021.3.4997.20210303T022849Z-210225` del SDK de AEM Cloud Service.

* La canalización de producción de Cloud Manager ahora incluye [Pruebas de IU personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) capacidad.

### Corrección de errores {#bug-fixes-cm-march}

* En algunos casos, las versiones de paquetes se omitían durante AEM actualización push.

* Algunos problemas de calidad no se descubrieron correctamente cuando los paquetes estaban incrustados en otros paquetes.

* En situaciones oscuras, el nombre predeterminado del programa generado al abrir el cuadro de diálogo Agregar programa podría ser un duplicado de un nombre de programa existente.

* En ocasiones, si el usuario sale de la página de ejecución de la canalización inmediatamente después de iniciar una canalización, aparece un mensaje de error que indica que la acción ha fallado, aunque la ejecución realmente se inicia.

* El paso de compilación se reinició innecesariamente cuando las compilaciones de clientes generaron paquetes no válidos.

* En ocasiones, el usuario puede ver un estado &quot;activo&quot; verde junto a una Lista de permitidos IP incluso cuando esa configuración no se implementó.

* Todas las canalizaciones de producción existentes se habilitarán automáticamente con el paso Auditoría de experiencias .

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.3.4 es el 19 de marzo de 2021.

### Corrección de errores {#bug-fixes-ctt}

* CTT omitía contenido de carpetas con el mismo nombre pero con un guión en el nombre. Esto se ha solucionado.

### Fecha de la versión {#release-date-ctt-march}

La fecha de versión de la herramienta de transferencia de contenido v1.3.0 es el 4 de marzo de 2021.

### Novedades de la herramienta de transferencia de contenido {#what-is-new-ctt-march}

* CTT ahora se instala en `/apps` en lugar de `/libs` Es posible que los marcadores del explorador para ciertas páginas ya no sean válidos.
* Cuando se instala CTT, el usuario tendrá que navegar un nivel adicional para llegar a la página de transferencia de contenido. Consulte [Uso de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html) para obtener más información.

### Corrección de errores {#bug-fixes-ctt-march}

* Al migrar contenido desde una ruta específica, CTT obtenía recursos no relacionados. Esto se ha solucionado

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.8 es el 22 de marzo de 2021.

### Novedades de Best Practices Analyzer {#what-is-new-bpa}

* Posibilidad de filtrar los resultados de ACS Commons desde el informe BPA en la interfaz de usuario, así como desde el informe exportado como archivo CSV.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades de las herramientas de refactorización de código {#what-is-new-crt}

* Nuevas funciones y mejoras para el Modernizador de repositorios. Consulte [Recurso de GitHub: Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para la versión más reciente.
   * Normalice las configuraciones de OSGi (excepto las configuraciones de RepoInit) con el formato preferido .cfg.json .
   * Cambie el nombre de las carpetas de configuración de OSGi al formato especificado.
   * Genere el proyecto ui.apps.structure .
   * Cree el módulo de análisis.

* Nuevas funciones y mejoras para Dispatcher Converter. Consulte [Recurso de GitHub: Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * Creación de archivos independientes para diferentes inclusiones en lugar de alinear el contenido.
   * Capacidad para gestionar la ruta de carpeta de vhosts y la ruta a los archivos vhost.
   * Generación de archivos de granja con grandes configuraciones de cliente en un rango de 600 o más.
