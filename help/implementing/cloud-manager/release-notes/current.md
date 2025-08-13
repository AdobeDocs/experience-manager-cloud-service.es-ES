---
title: Notas de la versión 2025.8.0 de Cloud Manager
description: Obtenga información sobre la versión 2025.8.0 de Cloud Manager en Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: c93716b1a2453c26169020b32e66eb4207f13002
workflow-type: tm+mt
source-wordcount: '1377'
ht-degree: 57%

---

# Notas de la versión 2025.8.0 de Cloud Manager en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2025.08.0+Release -->

Obtenga información sobre la versión 2025.8.0 de Cloud Manager en AEM (Adobe Experience Manager) as a Cloud Service.

Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.8.0 en AEM as a Cloud Service fue el viernes, 07 de agosto de 2025.

La próxima versión está planificada para el viernes, 04 de septiembre de 2025.

## Novedades {#what-is-new}

* **Adobe Experience Hub próximamente**

  A partir del 19 de agosto de 2025, Adobe comienza un despliegue gradual del nuevo Experience Hub para todos los usuarios de Adobe Experience Manager.

  Experience Hub es un punto de partida unificado que ofrece experiencias personalizadas y contextuales para ayudar a los usuarios a lograr sus objetivos más rápido. El despliegue finaliza el 26 de agosto de 2025, y está disponible para todos los usuarios. Se puede acceder directamente al nuevo Experience Hub en [experience.adobe.com](https://experience.adobe.com/). Para obtener más información, consulta [Adobe Experience Hub](/help/implementing/cloud-manager/aem-home.md).

* **La licencia de Edge Delivery Services se puede incluir en un programa HIPAA en forma de autoservicio**

  Las organizaciones con requisitos de datos confidenciales o de atención médica ahora pueden utilizar Edge Delivery Services en forma de autoservicio, lo que permite que la HIPAA cumpla con estándares regulatorios estrictos. <!-- CMGR-70016 -->

* **BYOG ya está disponible para Edge Delivery Services**

  Cloud Manager ahora permite configurar repositorios Git externos, lo que permite flujos de trabajo flexibles de administración de código. <!--(CMGR‑69010, CMGR‑70988) --> También le permite extraer código de una rama elegida directamente en la interfaz de usuario de Cloud Manager, lo que reduce las tareas manuales del repositorio. Ver [Configuración del sitio de Edge Delivery para usar un repositorio Git externo](/help/implementing/cloud-manager/edge-delivery/config-edge-delivery-site-with-byog.md) <!-- (CMGR‑68085)(CMGR-69015) --> <!-- KT: https://wiki.corp.adobe.com/display/DMSArchitecture/%5B2025%5D+Cloud+Manager+-+Bring+Your+Own+Git+with+EDS -->

* **Aprovisionamiento automatizado para el nuevo complemento de Forms**

  Los clientes solo de Sites suelen necesitar una forma ligera y de bajo coste de crear formularios de marketing. El nuevo complemento de AEM Forms Sites satisface esas necesidades al agregar funciones limitadas de Forms a un programa de Sites. También crea una ruta de actualización clara a la oferta completa de AEM Forms. <!-- (CMGR-64301) --> <!-- KT: CMGR Provisioning Support for AEM Forms Sites Add-On SKU https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3578379797 -->

  El complemento:
   * Se adjunta a un programa de Sites y se implementa junto a él; no hay programa de Forms ni asignación de derechos independientes.
   * Se dirige a casos de uso de formularios de marketing sencillos.
   * Aparece en la lista **Soluciones y complementos** durante la creación del programa de producción o la edición del programa de producción, solo cuando la organización de IMS tiene licencias de complemento de Forms disponibles.

     ![Complementos de Forms](/help/implementing/cloud-manager/release-notes/assets/forms-add-on.png) *El complemento de Forms solo se puede agregar en el programa si las licencias de complemento de Forms están disponibles en su organización de IMS.*

     ![Complemento de Forms en soluciones y complementos al crear un programa de producción](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-creating-production-program.png) *Durante la creación del programa, puede seleccionar el complemento de Forms en la solución Sites.*

     ![Complemento de Forms al editar un programa de producción](/help/implementing/cloud-manager/release-notes/assets/forms-add-on-editing-production-program.png) *En **Editar programa**, seleccione el complemento de Forms para el programa de Sites y, a continuación, ejecute la canalización para activarla en los entornos.*

     Para obtener más información, consulte [Crear un programa de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).

## Programas de Beta {#private-beta-program}

Participe en los programas beta de Cloud Manager para obtener acceso exclusivo a las próximas funciones antes de su lanzamiento general.

Actualmente están disponibles las siguientes oportunidades:

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
* **Copiar contenido** ahora se admite en Entornos de prueba especializados. Ahora puede ejecutar **Copiar contenido** de forma segura en entornos de prueba aislados que reflejen Producción. <!-- (CMGR‑68900) -->

Consulte [Adición de un entorno de prueba especializado](/help/implementing/cloud-manager/specialized-test-environment.md).

![Cuadro de diálogo Añadir entorno con el botón de opción Entorno de prueba especializado seleccionado](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.


### Trae tu propio Git (BYOG) {#gitlab-bitbucket-azure-vsts}

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
| *¿La configuración existente, como las listas de `IP Allow`, sigue funcionando?* | Sí, las listas de `IP Allow` existentes siguen funcionando como de costumbre. Sin embargo, si el repositorio de Git externo está protegido por un firewall, las [direcciones IP de Adobe necesarias deben añadirse a la lista de IP permitidas](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *¿Funcionan todas las URL del repositorio de GitLab? La URL del repositorio en uso sigue el formato `https://gitlab_dedicated_url.com/path/repo-name.git`, que difiere del ejemplo de la documentación.* | Sí, se admite cualquier repositorio de GitLab que admita API V3 o V4, incluidas las URL de GitLab autoalojado como la descrita en [Añadir repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


#### Administrar tókenes de acceso{#manage-access-tokens}

Use **Administrar tokens de acceso** en Cloud Manager para ver, cambiar el nombre y eliminar los tokens de acceso asociados con repositorios BYOG externos, como GitHub Enterprise, GitLab, Bitbucket y Azure DevOps.

Consulte [Administración de tokens de acceso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md).

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) from your email address associated with your Adobe ID. -->


### Añadir canalización de configuración de Edge Delivery {#add-eds-pipeline}

Ahora se admiten las canalizaciones de configuración para los sitios creados con Edge Delivery Services, lo que amplía esta capacidad más allá de los entornos de Cloud Service. Puede usar las **canalizaciones de configuración** para administrar las configuraciones como las reglas de filtrado de tráfico y las configuraciones WAF cuando corresponda. Consulte [Configuraciones compatibles](/help/operations/config-pipeline.md#configurations).

**Mejora reciente**

* Las canalizaciones de Edge Delivery Services ahora muestran **Configuración** en la columna **Código implementado**, lo que permite identificar instantáneamente las implementaciones solo de configuración. <!-- CMGR‑69681 -->
* Cloud Manager muestra **Agregar canalización de Edge Delivery** una vez que un programa contiene al menos un sitio de Edge Delivery Services y un dominio asignado. De lo contrario, la opción aparece desactivada y la información del objeto explica los requisitos que faltan. <!-- CMGR‑69680 -->
* La pestaña **Edge Delivery** muestra un nuevo widget de **canalizaciones Edge Delivery** que enumera el nombre, el estado, el repositorio y la rama de cada canalización. <!-- (CMGR-69052) -->

  ![widget de canalización de Edge Delivery que muestra el nombre, el estado, el repositorio y la rama de la canalización](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

* El panel **Filtros** agrega una sección **Tipo de entrega**; incluye **envío de Edge** y **envío de publicación** casillas de verificación. <!-- (CMGR-69682) -->

  ![Panel de filtro que muestra el nuevo tipo de entrega de Edge y la entrega de publicación](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

![Añadir canalización de Edge Delivery a la lista desplegable Añadir canalización](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Adición de una canalización de Edge Delivery desde la página **Información general del programa**, tarjeta **Canalizaciones**.*

![Cuadro de diálogo Añadir canalización de Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Cuadro de diálogo Añadir canalización de Edge Delivery.*

Ver [Agregar canalización de Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/configuring-edge-delivery-pipeline.md)

<!-- If you are interested in testing this new feature and sharing your feedback, send an email to [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) from your email address associated with your Adobe ID. -->


## Correcciones de errores

* Las canalizaciones ahora solo entregan variables a la configuración de dominio de Edge Delivery Services activa, lo que omite cualquier configuración eliminada durante la recreación de la canalización. <!-- (CMGR‑70039) -->
* La ejecución de la canalización ahora se inicia de forma fiable; se ha corregido un problema por el que algunas canalizaciones no se iniciaban debido a errores de administración de recursos internos. <!-- (CMGR‑58167) -->
* La copia de contenido valida los permisos de Cloud Manager y bloquea los inicios de los usuarios que carecen de derechos de administrador o administrador de implementación. <!-- (CMGR‑62097) -->


<!-- ## Known issues {#known-issues} -->

