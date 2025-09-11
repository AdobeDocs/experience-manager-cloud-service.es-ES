---
title: Notas de la versión 2025.9.0 de Cloud Manager
description: Obtenga información sobre la versión 2025.9.0 de Cloud Manager en Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 67fbd48d8cf4ac58d3bcff1eb314045b4ebd24b3
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 88%

---

# Notas de la versión 2025.9.0 de Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Obtenga información sobre la versión 2025.9.0 de Cloud Manager en AEM (Adobe Experience Manager) as a Cloud Service.

Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.9.0 en AEM as a Cloud Service fue el viernes, 04 de septiembre de 2025.

La próxima versión está planificada para el viernes, 02 de octubre de 2025.

## Novedades {#what-is-new}

* **Renovar manualmente los certificados de validación de dominios administrados por Adobe**

  Ahora puede renovar manualmente los certificados de validación de dominio (DV) administrados por Adobe que hayan dado error desde Cloud Manager o la API pública para actualizar los certificados de forma proactiva. <!-- CMGR-68738 -->

  ![renovación de certificado SSL](/help/implementing/cloud-manager/release-notes/assets/ssl-certificate-adobedv-renew.png)

* **Se ha agregado compatibilidad con las operaciones de desarrollo de Azure (repositorios privados)**

  Las actualizaciones de la documentación incluyen pasos de configuración para Traer su propio Git con Azure DevOps y validación de solicitudes de extracción. Consulte [Agregar repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

* **Brinde su propia compatibilidad con Git (BYOG) a las canalizaciones de configuración (repositorios privados)**

  Cloud Manager ahora admite canalizaciones de configuración con repositorios privados en GitHub, Bitbucket, Azure DevOps y GitLab. Esta compatibilidad acelera aún más el ciclo de desarrollo. Consulte [Comprobaciones de solicitudes de extracción para repositorios privados](/help/implementing/cloud-manager/managing-code/github-check-config.md).

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

### Agregar canalización de configuración de Edge Delivery {#add-eds-pipeline}

Ahora se admiten las canalizaciones de configuración para los sitios creados con Edge Delivery Services, lo que amplía esta capacidad más allá de los entornos de Cloud Service. Puede usar las **canalizaciones de configuración** para administrar las configuraciones como las reglas de filtrado de tráfico y las configuraciones WAF cuando corresponda. Consulte [Configuraciones compatibles](/help/operations/config-pipeline.md#configurations).

**Mejora reciente**

* Las canalizaciones de configuración de Edge Delivery ahora admiten secretos a través de variables de canalización de Cloud Manager.
* Las canalizaciones de Edge Delivery Services ahora muestran **Configuración** en la columna **Código implementado**, lo que permite identificar instantáneamente las implementaciones que son solo de configuración. <!-- CMGR‑69681 -->
* Cloud Manager muestra **Añadir canalización de Edge Delivery** cuando un programa contiene al menos un sitio de Edge Delivery Services y un dominio asignado. De lo contrario, la opción aparece desactivada y una ayuda contextual explica los requisitos que faltan. <!-- CMGR‑69680 -->
* La pestaña **Edge Delivery** muestra un nuevo widget de **canalizaciones Edge Delivery** que enumera el nombre, el estado, el repositorio y la rama de cada canalización. <!-- (CMGR-69052) -->

  ![Widget de canalización de Edge Delivery que muestra el nombre, el estado, el repositorio y la rama de la canalización](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

* El panel **Filtros** añade una sección **Tipo de envío**; incluye las casillas de verificación **Envío de Edge** y **Envío de publicación**. <!-- (CMGR-69682) -->

  ![Panel de filtro que muestra el nuevo tipo de envío de Edge y el envío de publicación](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

![Añadir canalización de Edge Delivery a la lista desplegable Añadir canalización](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Adición de una canalización de Edge Delivery desde la página **Información general del programa**, tarjeta **Canalizaciones**.*

![Cuadro de diálogo Añadir canalización de Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Cuadro de diálogo Añadir canalización de Edge Delivery.*

Consulte [Añadir canalización de Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.

## Correcciones de errores {#bug-fixes}

No hay correcciones de errores significativas en la versión de septiembre de Cloud Manager.


<!-- ## Known issues {#known-issues} -->

