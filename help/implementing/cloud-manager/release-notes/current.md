---
title: Notas de la versión 2025.10.0 de Cloud Manager
description: Obtenga información sobre la versión 2025.10.0 de Cloud Manager en Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 302248ade67683712bf1895fd8dfdd8853aae1ac
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 56%

---

# Notas de la versión 2025.10.0 de Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Obtenga información sobre la versión 2025.10.0 de Cloud Manager en AEM (Adobe Experience Manager) as a Cloud Service.

Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.10.0 en AEM as a Cloud Service fue el viernes, 02 de octubre de 2025.

La próxima versión está planificada para el viernes, 06 de noviembre de 2025.

## Novedades {#what-is-new}

* **Canalizaciones de implementación dedicadas solo de fase y de producción**

  Cloud Manager ahora ofrece canalizaciones de implementación dedicadas solo de fase y de producción, lo que proporciona una mayor flexibilidad para administrar implementaciones en entornos de ensayo y producción de forma independiente. Ver [Dividir canalizaciones solo de fase y solo de producción](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md).

* **Servicio de evaluación de estado en la nube de AEM**

  Adobe presenta el servicio de evaluación del estado de la nube de AEM, una herramienta de comprobación automatizada y no invasiva que mantiene su entorno de AEM as a Cloud Service optimizado, seguro y alineado con las prácticas recomendadas.

  Este servicio hace lo siguiente:

   * Analiza los entornos para detectar cuellos de botella, ineficiencias y riesgos potenciales de rendimiento.
   * Analiza las estructuras de contenido (modelos, Live Copies) y las configuraciones personalizadas.
   * Identifica dependencias obsoletas (AEM SDK, bibliotecas de terceros).
   * Indica problemas de calidad del código (anotaciones incorrectas, patrones ineficientes).
   * Proporciona instrucciones procesables a través de paneles como **Centro de acciones**.
   * Admite la optimización proactiva mediante la detección y corrección tempranas de problemas.

  Los equipos pueden monitorizar y mejorar continuamente sus entornos de AEM para obtener un rendimiento más fluido, una seguridad más sólida y una capacidad de mantenimiento a largo plazo.

  Consulte [Evaluación de estado para entornos de ensayo y producción](/help/implementing/cloud-manager/reports/report-health-assessment.md).

* **Compatibilidad con la canalización de configuración**

  Ahora se admiten las canalizaciones de configuración para los sitios creados con Edge Delivery Services, lo que amplía esta capacidad más allá de los entornos de Cloud Service. Puede usar **Canalizaciones de configuración** para administrar configuraciones como la configuración de CDN, incluidas las reglas de filtro de tráfico y los selectores de origen. Consulte [Configuraciones compatibles](/help/operations/config-pipeline.md#configurations).

  Las canalizaciones de configuración de Edge Delivery también admiten secretos a través de variables de canalización de Cloud Manager.

  Consulte [Agregar canalización de Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md).

* **Cuadro de diálogo de configuración de CDN y asignación de dominios optimizado**

  Cloud Manager ha simplificado el flujo de **Asignar dominio a CDN** para reducir la confusión y acelerar la configuración. El cuadro de diálogo ahora resalta **CDN administrado por Adobe** (con el distintivo &quot;Recomendado&quot;).

  ![Asignar dominio a CDN (cuadro de diálogo) con el botón de opción CDN administrado por Adobe seleccionado](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-adobe-managed-cdn.png).

  Consulte [Agregar una asignación de dominio](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).

  El cuadro de diálogo también presenta una lista de comprobación única y concisa para la tarjeta **Otro proveedor de CDN**, que se centra en el contenido de instrucciones con lo siguiente:

   * Apunte su origen de CDN a `publish-p<PROGRAM_ID>-e<ENV_ID>.adobeaemcloud.com`.
   * Establezca **Host/SNI** para reenviar el host original.
   * Agregue `X-AEM-Edge-Key` (después de implementar la clave en Cloud Manager).
   * Establezca `X-Forwarded-Host` en su dominio de cliente.
   * Borrar otros `X-Forwarded-*` encabezados antes de llegar a AEM.

  ![Cuadro de diálogo Asignar dominio a CDN con el botón de opción Otro proveedor de CDN seleccionado](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-dialog-box-other-cdn-provider.png)

  <!-- (no redundant `Origin` field or "Learn more" clutter) -->El pie de página adjunto proporciona dos vínculos útiles: configuraciones de muestra para CDN principales y un vínculo a la documentación completa. Un solo botón de confirmación (He configurado mi CDN) completa el flujo.

  Ver [CDN en AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN).

<!--
### Staging-Only and Production-Only Pipelines {#staging-production-only-pipelines}

Support for [staging-only and production-only pipelines](/help/implementing/cloud-manager/configuring-pipelines/stage-prod-only.md) has been introduced, enabling you to split full-stack production deployment pipelines into smaller, specialized deployments.

If you are interested in testing this new feature and sharing your feedback, send an email to  `Grp-cloudmanager_splitpipelines@adobe.com` from your email address associated with your Adobe ID. -->


## Programas Beta {#private-beta-program}

Participe en los programas Beta de Cloud Manager para obtener acceso exclusivo a las próximas funciones antes de su lanzamiento general.

Actualmente están disponibles las siguientes oportunidades:
<!--
### Support for Custom Author Domains in Cloud Service

AEM Cloud Service is going to soon support one custom domain per Author environment.-->

### Extensibilidad y personalización de Experience Hub {#exp-hub-extensibility}

[Experience Hub](/help/experience-hub.md) sirve como punto de entrada a AEM, personalizado para las necesidades de la organización. Informe a Adobe sobre las extensiones de la interfaz de usuario de AEM existentes para que puedan ayudarle a habilitarlas en Experience Hub con el mínimo esfuerzo.

![Diagrama del flujo de trabajo de personalización y extensibilidad de Experience Hub](/help/implementing/cloud-manager/release-notes/assets/experience-hub-extensibility-customization.png)

Incruste experiencias personalizadas en Experience Hub para ampliar y personalizar el tablero de su organización. Además de los widgets integrados de Adobe, agregue los suyos propios mediante el marco de trabajo [Extensibilidad de la interfaz de usuario](https://developer.adobe.com/uix/docs/). Cree aplicaciones de interfaz de usuario basadas en JavaScript y envíelas a sus usuarios para que cumplan con los requisitos y flujos de trabajo específicos de la empresa.

¿Te interesa la versión beta? Envíe un correo electrónico a [beta_exphubextensibility@adobe.com](mailto:beta_exphubextensibility@adobe.com) con su identificador de organización de Adobe y una breve descripción de la personalización que desea crear.

### Compilaciones más rápidas con almacenamiento en caché de módulos {#quick-build-cm-pipelines}

Un nuevo modelo de compilación compila solo los módulos modificados (en lugar de todo el repositorio) mediante el almacenamiento en caché de nivel de módulo para acortar los tiempos de compilación. Se aplica a las canalizaciones de calidad de código, de pila completa y de solo ensayo.

![Editar canalización que no sea de producción cuadro de diálogo que muestra las dos opciones de Estrategia de compilación que son Compilación completa y Compilación inteligente](/help/implementing/cloud-manager/release-notes/assets/non-production-pipeline-edit.png) *Editar canalización que no sea de producción cuadro de diálogo que muestra las dos opciones de Estrategia de compilación que son Compilación completa y Compilación inteligente.*

En el cuadro de diálogo **Agregar o editar canalización**, en la ficha **Código Source**, una nueva sección de **Estrategia de compilación** le permite elegir una de las siguientes opciones de compilación:

* **Compilación completa**: genera todos los módulos del repositorio en cada ejecución.
* **Compilación inteligente**: genera solo módulos que han cambiado desde la última confirmación, lo que acorta el tiempo de compilación general.

Usted controla qué canalizaciones utilizan **Smart Build**. Durante la versión beta, esta opción solo aparece para las canalizaciones **Calidad del código** y **Implementación de desarrolladores**.

¿Interesado? Envíe un correo electrónico a [beta_quickbuild_cmpipelines@adobe.com](mailto:beta_quickbuild_cmpipelines@adobe.com) con su identificador de organización de Adobe y el identificador de programa.

<!-- You can deactivate incremental builds at the pipeline level by setting the property `CM_BUILD_DISABLE_MODULE_CACHING` to `true` (effective during the `BUILD` step). For how to add pipeline variables, see [Pipeline Variables in Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md).-->



### Reversión en un solo clic para implementaciones de canalización {#one-click-rollback}

Vuelva rápidamente a una implementación anterior si el código fuente del cliente más reciente no funciona como se esperaba; no es necesario volver a ejecutar la canalización completa ni revertir las confirmaciones manualmente.<!--https://jira.corp.adobe.com/browse/CMGR-69556 -->

![Restaurar código fuente del cliente desde la tarjeta Entornos](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed.png) *La tarjeta Entornos muestra la opción **Restaurar**>**Código anterior implementado**&#x200B;para un entorno seleccionado.*

![Cuadro de diálogo Restaurar código anterior implementado](/help/implementing/cloud-manager/release-notes/assets/restore-previous-code-deployed-dialogbox.png)
*En el cuadro de diálogo **Restaurar código anterior implementado**, revise la versión implementada actualmente y la versión que desea restaurar, luego haga clic en **Confirmar***.

![Activación de Restaurando](/help/implementing/cloud-manager/release-notes/assets/restoring-previous-code-deployed-restoring.png)
*Cloud Manager revierte el entorno a la versión anterior, mantiene el contenido y la configuración intactos y marca el entorno **Restaurando**&#x200B;hasta que finalice la implementación.*

![Versión del código fuente en uso](/help/implementing/cloud-manager/release-notes/assets/environments-view-details-sourcecodeversion.png) *La vista de detalles del entorno, vista desde arriba, ahora también muestra la versión activa del código fuente en uso.*

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [restorecode@adobe.com](mailto:restorecode@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.

Consulte [Restaurar el código anterior implementado en AEM as a Cloud Service](/help/operations/restore-previous-code-deployed.md).

Consulte [Restauración de contenido en AEM as a Cloud Service](/help/operations/restore.md).

### Entorno de pruebas especializadas {#specialized-test-environment}

Cloud Manager ahora admite la adición de un nuevo tipo de entorno denominado **Entorno de prueba especializado**. El entorno está diseñado para ayudar a los equipos a validar las funciones en condiciones casi de producción antes de su lanzamiento. Este tipo de entorno es distinto de los entornos *Producción + Fase*, *Desarrollo* o *Desarrollo rápido*, y ofrece un espacio dedicado para ejecutar escenarios de validación avanzados.

**Mejoras recientes**

* Ahora puede configurar un entorno de prueba especializado en una canalización que no sea de producción a través de un flujo de trabajo más sencillo e intuitivo. La configuración optimizada acelera la finalización y reduce los errores de configuración.
* **Copiar contenido** ahora se admite en entornos de prueba especializados. Ahora puede ejecutar **Copiar contenido** de forma segura en entornos de prueba aislados que reflejen la producción. <!-- (CMGR‑68900) -->

Consulte [Adición de un entorno de prueba especializado](/help/implementing/cloud-manager/specialized-test-environment.md).

![Cuadro de diálogo Añadir entorno con el botón de opción Entorno de prueba especializado seleccionado](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

>[!NOTE]
>
>Adobe ha cerrado las solicitudes de acceso a la versión beta de los entornos de prueba especializados, tras haber alcanzado un número suficiente de participantes. La función se está preparando para su disponibilidad general.

<!--
If you are interested in testing this new feature and sharing your feedback, send an email to [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) from your email address associated with your Adobe ID. -->


### Traiga su propio Git (BYOG) {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Los clientes ahora pueden incorporar sus repositorios Git de Azure DevOps en Cloud Manager, con compatibilidad tanto con los repositorios modernos de Azure DevOps como con los repositorios heredados de VSTS (Visual Studio Team Services).

* Para los usuarios de Edge Delivery Services, el repositorio incorporado se puede utilizar para sincronizar e implementar el código del sitio.
* Para los usuarios de AEM as a Cloud Service y Adobe Managed Services (AMS), el repositorio se puede vincular a canalizaciones de pila completa y de front-end.

La compatibilidad con tipos de canalización adicionales y la validación de solicitudes de extracción a través de canalizaciones de calidad de código estará disponible pronto.

Consulte [Adición de repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Cuadro de diálogo Añadir repositorio](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. Be sure to include which Git platform you want to use and whether you are on a private/public or enterprise repository structure. -->

**Preguntas frecuentes sobre BYOG**

| Pregunta | Respuesta |
|---|---|
| *¿Cómo puede un proyecto volver al repositorio de Git administrado por Adobe si es necesario?* | Volver atrás es sencillo. [Actualice las canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) para que apunten al repositorio de Adobe y quite el repositorio externo si ya no es necesario. |
| *¿Es posible configurar diferentes repositorios para diferentes entornos (por ejemplo, no producción frente a producción) para permitir primero las pruebas en no producción?* | Sí, se pueden configurar diferentes repositorios para entornos independientes. Por ejemplo, la canalización de desarrollo o de calidad del código puede apuntar a un repositorio externo, mientras que la canalización de producción permanece conectada al repositorio de Adobe. Asegúrese de que el trabajo de sincronización entre los dos repositorios permanece activo durante esta configuración. |
| *¿Continúa funcionando la configuración existente, como las listas de `IP Allow`?* | Sí, las listas de `IP Allow` existentes siguen funcionando como de costumbre. Sin embargo, si el repositorio de Git externo está protegido por un firewall, las [direcciones IP de Adobe necesarias deben añadirse a la lista de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *¿Funcionan todas las URL del repositorio de GitLab? La URL del repositorio en uso sigue el formato `https://gitlab_dedicated_url.com/path/repo-name.git`, que difiere del ejemplo de la documentación.* | Sí, se admite cualquier repositorio de GitLab que admita API V3 o V4, incluidas las URL de GitLab autoalojado como la descrita en [Añadir repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Administrar tókenes de acceso{#manage-access-tokens}

Use **Administrar tokens de acceso** en Cloud Manager para ver, cambiar el nombre y eliminar los tokens de acceso asociados con repositorios BYOG externos, como GitHub Enterprise, GitLab, Bitbucket y Azure DevOps.

Consulte [Administración de tokens de acceso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


## Correcciones de errores {#bug-fixes}

No hay correcciones de errores significativas en la versión de octubre de Cloud Manager.


<!-- ## Known issues {#known-issues} -->

