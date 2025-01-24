---
title: Notas de la versión para Cloud Manager 2025.1.0 en Adobe Experience Manager as a Cloud Service
description: Obtenga información acerca del lanzamiento de Cloud Manager 2025.1.0 en AEM as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 9850a52626c2bd80f7528931d23691dff1dd3eb2
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 10%

---

# Notas de la versión para Cloud Manager 2025.1.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3389843928 -->

Obtenga información sobre el lanzamiento de Cloud Manager 2025.1.0 en AEM (Adobe Experience Manager) as a Cloud Service.

>[!NOTE]
>
>Consulte las [notas de la versión actuales de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.1.0 en AEM as a Cloud Service es el miércoles, 22 de enero de 2025.

La próxima versión planificada es el viernes, 13 de febrero de 2025.


## Novedades {#what-is-new}

* **Reglas de calidad del código - Actualización del servidor de SonarQube:** El paso de calidad del código de Cloud Manager empezará a utilizar SonarQube Server 9.9 con la versión 2025.2.0 de Cloud Manager, programada para el jueves 13 de febrero de 2025.

  Para prepararse, las reglas actualizadas de SonarQube ya están disponibles en [Reglas de calidad de código](/help/implementing/cloud-manager/code-quality-testing.md#understanding-code-quality-rules).

  Puede &quot;comprobar antes&quot; las nuevas reglas configurando la siguiente variable de texto de canalización:

  `CM_BUILD_IMAGE_OVERRIDE` = `self-service-build:sonar-99-upgrade-java17or21`

  Además, establezca la siguiente variable para asegurarse de que el paso de calidad del código se ejecuta para la misma confirmación (normalmente se omite para el mismo `commitId`):

  `CM_DISABLE_BUILD_REUSE` = `true`

![Página de configuración de variables](/help/implementing/cloud-manager/release-notes/assets/variables-config.png)

>[!NOTE]
>
>Adobe recomienda crear una nueva canalización de calidad de código de CI/CD, configurada en la misma rama que la canalización de producción principal. Establezca las variables apropiadas *antes* de la versión del 13 de febrero de 2025 para validar que las nuevas reglas aplicadas no introduzcan bloqueadores.

* **Compatibilidad con Java 17 y Java 21 Build:** Los clientes ahora pueden compilar con Java 17 o Java 21, obteniendo acceso a mejoras de rendimiento y nuevas características del lenguaje. Para ver los pasos de configuración, incluida la actualización del proyecto Maven y las versiones de la biblioteca, consulte [Entorno de compilación](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md). Cuando la versión de compilación se establece en Java 17 o Java 21, el tiempo de ejecución implementado es Java 21.

   * **Habilitación de características**
      * Esta función se habilitará para todos los clientes el jueves 13 de febrero de 2025, coincidiendo con el despliegue predeterminado de la nueva versión de SonarQube.
      * Los clientes pueden habilitarlo *inmediatamente* estableciendo las dos configuraciones de variables descritas anteriormente para actualizar la versión de SonarQube 9.9.

   * **Implementación de tiempo de ejecución de Java 21**
      * El tiempo de ejecución de Java 21 se implementa al crear con Java 17 o Java 21.
      * El despliegue gradual en todos los entornos de Cloud Manager comienza en febrero para los entornos de pruebas y desarrollo y se extiende a los entornos de producción en abril.
      * Los clientes que usen Java 11 y deseen adoptar el tiempo de ejecución de Java 21 *antes* pueden ponerse en contacto con el Adobe en [aemcs-java-adopter@adobe.com](mailto:aemcs-java-adopter@adobe.com).

* Se cambió el nombre de **&quot;Configuraciones de CDN&quot; a &quot;Asignaciones de dominio&quot;:** Como parte de las mejoras en la interfaz de usuario en AEM Cloud Manager, ahora se cambia el nombre de la etiqueta &quot;Configuraciones de CDN&quot; a &quot;Asignaciones de dominio&quot;. Este cambio mejora la alineación de la terminología con la funcionalidad. <!-- CMGR-64738 -->

  Se cambió el nombre de ![ &quot;Configuraciones de CDN&quot; a &quot;Asignaciones de dominio&quot; en la interfaz de usuario](/help/implementing/cloud-manager/release-notes/assets/domain-mappings.png)

* **Aprovisionar un sitio Edge Delivery con un solo clic:** Cloud Manager ahora permite a los usuarios con los permisos y licencias apropiados crear un sitio de Edge Delivery Services de ejemplo con un solo clic. Este proceso optimizado ofrece las siguientes funcionalidades automatizadas:

   * **Integración de GitHub**: crea automáticamente un repositorio de GitHub dentro de una organización existente, preconfigurado con una plantilla de plantillas para Edge Delivery Services.
   * AEM AEM **Instalación de la aplicación de sincronización de código de**: instala la aplicación de sincronización de código de la aplicación en el repositorio, lo que garantiza una sincronización e implementación sin problemas.
   * **Configuración de Collaboration de contenido**: vincula una carpeta designada de Google Drive para el almacenamiento de contenido, lo que proporciona un entorno de colaboración para la administración de contenido.
   * **Publicación de contenido**: Los usuarios ahora pueden publicar contenido para sitios aprovisionados directamente desde la interfaz de usuario de Cloud Manager, lo que simplifica los flujos de trabajo y mejora la eficacia.
   * **Collaboration mejorado**: la plataforma permite a los usuarios agregar varios colaboradores a la carpeta de almacenamiento de contenido de Google Drive, lo que facilita el trabajo en equipo y las contribuciones de contenido.

  Estas mejoras tienen como objetivo mejorar la automatización, simplificar los procesos de configuración y mejorar la colaboración entre los usuarios de Edge Delivery Services. <!-- CMGR-59362 -->

  ![Aprovisionamiento de un sitio de Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

  ![Aprovisionar cuadro de diálogo del sitio de Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)

* **Compatibilidad mejorada con los sitios de Edge Delivery Services:** Cloud Manager ahora admite la incorporación de los sitios de Edge Delivery Services más recientes. Esta actualización incluye una refactorización completa de la red de distribución de contenido (CDN) y de la pila de envíos, lo que mejora la solidez y la capacidad de mantenimiento.

* **Actualización anticipada del programa del usuario que lo adoptó - Soporte de validación de PR para Bitbucket y GitLab:** Cloud Manager ahora admite la validación de solicitudes de extracción (PR) tanto para la nube como para las versiones autohospedadas de Bitbucket y GitLab. Esta función permite a los clientes probar los cambios de código en relación con los umbrales de calidad del código de Adobe antes de combinar una PR. Al garantizar una mayor calidad del código antes de la combinación, esta mejora mejora mejora significativamente la tasa de éxito de los cambios de código en las canalizaciones de producción, lo que reduce el tiempo de salida al mercado y optimiza los flujos de trabajo de desarrollo.

* **Opciones de filtrado avanzadas para canalizaciones:** Cloud Manager ahora cuenta con opciones de filtrado avanzadas en la página Canalizaciones, lo que le permite acceder rápidamente a los datos relevantes y mejorar la eficacia de la implementación. Algunas de las características clave son las siguientes:

   * **Filtrado de criterios múltiples:** Refine los resultados de búsqueda con filtros como el nombre de la canalización, el entorno y el código de implementación.
   * **Búsqueda optimizada de canalizaciones:** Localice fácilmente canalizaciones específicas para una navegación más rápida y una administración mejorada del flujo de trabajo.

  En conjunto, estas mejoras hacen que la administración y la implementación de canalizaciones sean más eficientes y fáciles de usar.

  ![Función de filtros de canalización](/help/implementing/cloud-manager/release-notes/assets/pipeline-filters.png)

* **Configuración de CDN de autoservicio para el servicio Edge Delivery:** Los nuevos usuarios que adoptan el servicio Edge Delivery ahora pueden configurar su CDN de forma independiente a través de Cloud Manager. Esta actualización amplía la compatibilidad de `.hlx.page/live` con el nuevo `.aem.page/live`, lo que proporciona mayor flexibilidad y una configuración optimizada para los usuarios.


<!-- ## Early adoption program {#early-adoption}

Be a part of Cloud Manager's early adoption program and have a chance to test upcoming features. -->

<!-- ## Bug fixes -->




<!-- ## Known issues {#known-issues} -->
