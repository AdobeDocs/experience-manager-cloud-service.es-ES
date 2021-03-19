---
title: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
description: Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service.
translation-type: tm+mt
source-git-commit: 93ae24247ae36f44e659211f1e7ab2f0888e4ad6
workflow-type: tm+mt
source-wordcount: '1793'
ht-degree: 3%

---


# Notas de la versión actuales de [!DNL Adobe Experience Manager] como Cloud Service {#release-notes}

La siguiente sección describe las notas de la versión generales de la versión actual (más reciente) de [!DNL Experience Manager] como Cloud Service.

>[!NOTE]
>Desde aquí puede navegar hasta las notas de versiones de versiones anteriores; por ejemplo, para los de 2020, 2021 y así sucesivamente.

>[!NOTE]
>
>Consulte [Actualizaciones de documentación recientes](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) para obtener más información sobre las actualizaciones de documentación no relacionadas directamente con una versión.

## Fecha de la versión {#release-date}

La fecha de versión de [!DNL Adobe Experience Manager] como Cloud Service 2021.2.0 es el 25 de febrero de 2021.
La siguiente versión (2021.3.0) será el 25 de marzo de 2021.

## [!DNL Adobe Experience Manager Sites] como Cloud Service  {#sites}

* **[El componente](/help/implementing/developing/hybrid/remote-page.md)** RemotePage: Se ha agregado compatibilidad con la visualización y edición de SPA externos dentro de AEM.

* **[Edición de un SPA externo dentro de AEM](/help/implementing/developing/hybrid/editing-external-spa.md)**: Se ha agregado la capacidad de cargar una aplicación independiente de una sola página en una instancia de AEM, agregar secciones de contenido editables y habilitar la creación.

<!--
### Progressive Web Apps (PWAs) {#pwa}

* [A Progressive Web App (PWA) version of a site](/help/sites-cloud/authoring/features/enable-pwa.md)  can now be enabled at the project level via simple configuration.
-->

## [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service] {#assets}

## Novedades de [!DNL Assets] {#what-is-new-assets}

* [!DNL Experience Manager Assets] as a  [!DNL Cloud Service] tiene derecho a tener una  [!DNL Brand Portal] instancia preconfigurada. El usuario [!DNL Cloud Manager] puede activar [!DNL Brand Portal] en [!DNL Experience Manager Assets] como [!DNL Cloud Service]. Consulte [activar Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=en).

* Las empresas ahora pueden crear recursos mediante [!DNL Brand Portal]. La función de abastecimiento de recursos aprovecha [!DNL Brand Portal] para ayudar a los clientes a interactuar con los usuarios de la agencia para obtener recursos para nuevas campañas de marketing, sesiones fotográficas y proyectos. Consulte [abastecimiento de recursos en [!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html).

* El informe de uso [!DNL Brand Portal] ahora muestra solamente los usuarios activos. Los usuarios inactivos no se muestran ahora. Los usuarios activos son aquellos cuya cuenta se asigna a un perfil de producto en [!DNL Admin Console]. Consulte [[!DNL Brand Portal] informes](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/admin-tools/brand-portal-reports.html).

* En [!DNL Brand Portal], se introduce una nueva configuración de descarga que permite crear carpetas independientes para cada recurso al descargar carpetas, colecciones, etc. Consulte [configuración de descarga](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/download/brand-portal-download-assets.html).

<!-- TBD: refine this list of features and enh. for Feb release.

Customers using the Connected Assets feature can now easily view and track assets used on remote Sites instances. This affords customers a complete view of being used across all Sites powered pages, allowing for better tracking, management, and brand consistency.  -->

## Correcciones de errores en [!DNL Assets] {#bug-fixes-assets}

* Cuando se crea una nueva versión de un recurso existente después de resolver el conflicto de nombres, los metadatos del recurso original se sobrescriben. (CQ-4313594)
* Cuando se imprime un recurso con texto de anotación largo, el texto de la anotación se recorta aunque haya espacio disponible. (CQ-4314101)
* Cuando se seleccionan varios recursos para actualizar las propiedades, a veces se produce un error o se actualizan las propiedades de un recurso no seleccionado. (CQ-4316532)
* Al intentar abrir [!UICONTROL Carril de búsqueda de administración de Assets], la página permanece en blanco y al hacer clic en [!UICONTROL Editar] > [!UICONTROL Configuración] se genera un error. (CQ-4315079)

## Adobe Experience Manager Commerce as a Cloud Service {#cloud-services-commerce}

### Novedades {#what-is-new-commerce}

* Administración de experiencia del producto: Enriquezca las páginas del catálogo de productos individualmente con fragmentos de experiencias.

* Se han ampliado las propiedades de la consola de producto para mostrar los recursos vinculados y los fragmentos de experiencia, incluida la acción para navegar rápidamente al contenido asociado.

* Sitio de referencia de Venia del CIF publicado - 2021.02.24 que incluye la versión más reciente de los componentes principales del CIF v1.8.0. Consulte [Sitio de referencia de Venia del CIF](https://github.com/adobe/aem-cif-guides-venia/releases/tag/venia-2021.02.24) para obtener más información.

* Componentes principales de CIF v1.8.0. Consulte [Componentes principales de CIF](https://github.com/adobe/aem-core-cif-components/releases/tag/core-cif-components-reactor-1.8.0) para obtener más información.

## Cloud Manager {#cloud-manager}

Esta sección describe las notas de la versión de Cloud Manager en AEM as a Cloud Service 2021.3.0.

## Fecha de la versión {#release-date-cm-march}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.3.0 es el 11 de marzo de 2021.
La próxima versión está planificada para el 08 de abril de 2021.


### Novedades {#what-is-new-march}

* Los clientes con entornos con configuraciones de nombre de dominio personalizado preexistentes para [Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md#pre-existing-cdn), [certificados SSL](/help/implementing/cloud-manager/managing-ssl-certifications/check-status-ssl-certificate.md#pre-existing-cdn) y [nombres de dominio personalizados](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#pre-existing-cdn) verán un mensaje sobre las configuraciones existentes anteriormente y podrán autoabastecerse mediante la interfaz de usuario.

* Los usuarios con los permisos necesarios ahora pueden editar un programa, lo que les permite hacer lo siguiente de forma autoservicio:

   * Agregar la solución Sitios a un programa existente con Assets o viceversa.
   * Elimine Sitios o Recursos de un programa existente con Sitios y Recursos.
   * Agregue el derecho a una solución no utilizada a un programa existente o como un nuevo programa.

* **AEM** actualización push ahora se mostrará para las pantallas  *Ejecución de la* canalización y  ** Actividad.

* Si un entorno está en hibernación pero también hay una actualización AEM disponible, el estado **Hibernated** tendrá prioridad sobre **Update available**.

* Los usuarios ahora pueden ver sus funciones de Cloud Manager seleccionando la opción &quot;Ver funciones de Cloud Manager&quot; después de navegar al icono de perfil de usuario (parte superior derecha) del shell unificado.

* La etiqueta **Application for Approval** se ha vuelto a etiquetar como **Production Approval** para una buena claridad.

* La etiqueta **Version** se ha vuelto a etiquetar como **Git Tag** en la pantalla de ejecución de la canalización de producción.

* Las etiquetas que definen el comportamiento cuando métricas importantes no alcanzan el umbral definido se han vuelto a etiquetar para reflejar su verdadero comportamiento: **Cancelar inmediatamente** y **Aprobar inmediatamente**.

* Las listas de deprecación de clases y métodos se han actualizado en función de la versión `2021.3.4997.20210303T022849Z-210225` del SDK del Cloud Service de AEM.

* La canalización de producción de Cloud Manager ahora incluirá la capacidad [Pruebas de IU personalizadas](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing).

### Corrección de errores {#bug-fixes-cm-march}

* En algunos casos, las versiones de paquetes se omitían durante AEM actualización push.

* Algunos problemas de calidad no se descubrieron correctamente cuando los paquetes estaban incrustados en otros paquetes.

* En situaciones oscuras, el nombre predeterminado del programa generado al abrir el cuadro de diálogo Agregar programa podría ser un duplicado de un nombre de programa existente.

* En ocasiones, si el usuario sale de la página de ejecución de la canalización inmediatamente después de iniciar una canalización, aparece un mensaje de error que indica que la acción ha fallado, aunque la ejecución realmente se inicia.

* El paso de compilación se reinició innecesariamente cuando las compilaciones de clientes generaron paquetes no válidos.

* En ocasiones, el usuario puede ver un estado &quot;activo&quot; verde junto a una Lista de permitidos IP incluso cuando esa configuración no se implementó.

* Todas las canalizaciones de producción existentes se habilitarán automáticamente con el paso Auditoría de experiencias .


### Fecha de la versión {#release-date-cm}

La fecha de versión de Cloud Manager en AEM as a Cloud Service 2021.2.0 es el 11 de febrero de 2021.

### Novedades {#what-is-new-cloud-manager}


* Los clientes de Assets ahora podrán elegir cuándo y dónde implementar su instancia de Brand Portal de forma independiente a través de la interfaz de usuario de Cloud Manager. Para un programa normal (que no sea de espacio aislado) con la solución Assets, Brand Portal se puede aprovisionar en el entorno de producción. El aprovisionamiento solo se puede realizar una vez en el entorno de producción.

* El tipo de archivo del proyecto AEM utilizado en la creación de proyectos y entornos limitados se ha actualizado a la versión 25.

* La lista de API obsoletas identificadas durante la digitalización del código se ha refinado para incluir clases y métodos adicionales que ya no se utilizan en las últimas versiones del SDK de Cloud Service.

* El perfil de SonarQube para Cloud Manager se ha actualizado para eliminar la regla Sonar squid:S2142. Esto ya no entrará en conflicto con las comprobaciones de Interrupción de subprocesos.

* La interfaz de usuario de Cloud Manager informará al usuario que no pueda añadir o actualizar temporalmente el nombre de dominio porque el entorno asociado tiene una canalización en ejecución conectada a él o está en espera del paso de aprobación.

* Las propiedades configuradas en los archivos `pom.xml` del cliente con el prefijo sonar ahora se eliminarán dinámicamente para evitar errores de análisis de calidad y compilación.

* La interfaz de usuario de Cloud Manager informará al usuario que no pueda seleccionar temporalmente un certificado SSL si lo está utilizando un nombre de dominio que se esté implementando actualmente.

* Se han agregado reglas de calidad de código adicionales para cubrir los problemas de compatibilidad con el Cloud Service.

### Corrección de errores {#bug-fixes-cloud-manager}

* La coincidencia del certificado SSL con un nombre de dominio ya no distingue entre mayúsculas y minúsculas.

* La interfaz de usuario de Cloud Manager informará a un usuario si las claves privadas del certificado no cumplen el límite de 2048 bits con un mensaje de error apropiado.

* La interfaz de usuario de Cloud Manager informará al usuario que no pueda seleccionar temporalmente un certificado SSL si lo está utilizando un nombre de dominio que se esté implementando actualmente.

* En algunos casos, un problema interno puede provocar que la eliminación del entorno se bloquee.

* Algunos errores de canalización se notificaron incorrectamente como errores de canalización.

## Herramienta de transferencia de contenido {#content-transfer-tool}

### Fecha de la versión {#release-date-ctt}

La fecha de versión de la herramienta de transferencia de contenido v1.3.4 es el 19 de marzo de 2021.

### Corrección de errores {#bug-fixes-ctt}

* CTT omitía contenido de carpetas con el mismo nombre pero con un guión en el nombre. Esto se ha solucionado.


### Fecha de la versión {#release-date-ctt-march}

La fecha de versión de la herramienta de transferencia de contenido v1.3.0 es el 4 de marzo de 2021.

### Novedades de la herramienta de transferencia de contenido {#what-is-new-ctt-march}

* CTT ahora se instala en `/apps` en lugar de `/libs` Los marcadores del explorador en ciertas páginas pueden no ser válidos.
* Cuando se instala CTT, el usuario tendrá que navegar un nivel adicional para llegar a la página de transferencia de contenido. Consulte [Uso de la herramienta de transferencia de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-content-transfer-tool.html) para obtener más información.

### Corrección de errores {#bug-fixes-ctt-march}

* Al migrar contenido desde una ruta específica, CTT obtenía recursos no relacionados. Esto se ha solucionado


### Fecha de la versión {#release-date-ctt-feb}

La fecha de versión de la herramienta de transferencia de contenido v1.2.4 es el 10 de febrero de 2021.

### Corrección de errores {#bug-fixes-ctt-feb}

* Al asignar varios usuarios, los ID de IMS de algunos usuarios se asignaban incorrectamente. Esto se ha solucionado.

### Fecha de la versión {#release-date-ctt-feb01}

La fecha de versión de la herramienta de transferencia de contenido v1.2.2 es el 1 de febrero de 2021.

### Novedades de la herramienta de transferencia de contenido {#what-is-new-ctt}

* Nueva capacidad e interfaz de usuario agregada a la herramienta de transferencia de contenido: herramienta de asignación de usuarios. Esta función asigna automáticamente los usuarios y grupos existentes a sus ID de sistema de Identity Management de Adobe como parte de la actividad de migración de contenido.
Consulte [Uso de la herramienta de asignación de usuarios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/content-transfer-tool/using-user-mapping-tool.html) para obtener más información.
* La herramienta de transferencia de contenido ahora migra todos los grupos y usuarios a los que se hace referencia en el conjunto de migración, incluidos los niños.
* Los usuarios pueden seleccionar determinadas rutas en `/etc` al crear conjuntos de migración.

## Analizador de prácticas recomendadas {#best-practices-analyzer}

### Fecha de la versión {#release-date-bpa}

La fecha de versión de Best Practices Analyzer v2.1.2 es el 18 de febrero de 2021.

### Novedades de Best Practices Analyzer {#what-is-new-bpa}

* Capacidad para detectar el uso de la implementación de AEM Forms y AEM Forms e indicar las áreas que son relevantes para migrar a AEM Forms como Cloud Service.
* Capacidad para detectar y crear informes sobre el uso y el recuento de componentes y plantillas personalizados.
* Capacidad para detectar el tipo de almacén de nodos y almacén de datos utilizado.
* Capacidad para detectar el uso de Dynamic Media.
* Capacidad para detectar la versión de Java utilizada.

## Herramientas de refactorización de código {#code-refactoring-tools}

### Novedades de las herramientas de refactorización de código {#what-is-new-crt}

* Se ha lanzado una nueva versión del complemento AIO-CLI. La última versión de este complemento incluye varias funciones nuevas y correcciones de errores para el Modernizador de repositorio y Dispatcher Converter.    Consulte [Experiencia unificada](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/unified-experience.html?lang=en#benefits) para obtener más información sobre este complemento.

* Nuevas funciones y mejoras para el Modernizador de repositorios. Consulte [Recurso de GitHub: Modernizador de repositorio](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/repository-modernizer) para la versión más reciente.
   * Normalice las configuraciones de OSGi (excepto las configuraciones de RepoInit) con el formato preferido .cfg.json .
   * Cambie el nombre de las carpetas de configuración de OSGi al formato especificado.
   * Genere el proyecto ui.apps.structure .
   * Cree el módulo de análisis.

* Nuevas funciones y mejoras para Dispatcher Converter. Consulte [Recurso de GitHub: Dispatcher Converter](https://github.com/adobe/aem-cloud-service-source-migration/tree/master/packages/dispatcher-converter)
   * Creación de archivos independientes para diferentes inclusiones en lugar de alinear el contenido.
   * Capacidad para gestionar la ruta de carpeta de vhosts y la ruta a los archivos vhost.
   * Generación de archivos de granja con grandes configuraciones de cliente en un rango de 600 o más.

## [!DNL Adobe Experience Manager] como Cloud Service Foundation  {#aem-as-a-cloud-service-foundation}

### Problemas conocidos {#known-issues-foundation}

**Algunas compilaciones pueden fallar debido a un problema con el complemento de Build Analyzer**

En algunos casos, una compilación de proyecto puede fallar durante la ejecución del `aemanalyser-maven-plugin` con el siguiente mensaje de error:

```
[ERROR] repoinit: Parsing error in repoinit from extension : Encountered "" at line 15, column 37.
 
Was expecting one of:
 
     
 
[ERROR] Analyser detected errors on feature
```

**Solución alternativa**

Para solucionar este problema, seleccione la última versión de `aemanalyser-maven-plugin` en el archivo principal `pom.xml`:

```xml
<aemanalyser.version>0.9.2</aemanalyser.version>
```

