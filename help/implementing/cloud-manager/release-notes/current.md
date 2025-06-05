---
title: Notas de la versión 2025.6.0 de Cloud Manager
description: Obtenga información sobre la versión de Cloud Manager 2025.6.0 en Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 2d0153d9a7c18097266d94575c2a61e471ccd536
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 33%

---

# Notas de la versión para Cloud Manager 2025.6.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Obtenga información sobre el lanzamiento de Cloud Manager 2025.6.0 en AEM (Adobe Experience Manager) as a Cloud Service.

Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.6.0 en AEM as a Cloud Service es el viernes, 05 de junio de 2025.

La próxima versión planificada es para el viernes, 10 de julio de 2025.

## Novedades {#what-is-new}

* El panel de licencias de **(IU) ahora incluye la licencia de Edge Delivery Services**

  El uso de licencias de Edge Delivery Services ahora se muestra en el panel de licencias, lo que le proporciona una visibilidad más clara de sus derechos y estado. <!-- CMGR-67686 -->

  ![Tablero de licencias](/help/implementing/cloud-manager/assets/license-dashboard.png)

  Consulte [Tablero de licencias](/help/implementing/cloud-manager/license-dashboard.md).

* **(IU) Configuración del sitio de Edge Delivery actualizada**

  Se ha simplificado el flujo para agregar un sitio Edge Delivery al solicitar **Edge Delivery Origin** en lugar de **la URL del repositorio**, lo que hace que la incorporación y la configuración sean más rápidas e intuitivas <!-- CMGR-67686 -->

  ![Agregar cuadro de diálogo del sitio de Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-site.png)

  Consulte [Agregar un sitio Edge Delivery](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md).

* **(IU) Favoritos de canalización**

  En esta versión, Cloud Manager introduce la capacidad de fijar canalizaciones favoritas, lo que le permite marcar canalizaciones específicas como favoritas para que aparezcan en la parte superior de la lista en la página **Canalizaciones**. Esta mejora facilita la búsqueda y ejecución de las canalizaciones a las que se accede con frecuencia. <!-- CMGR-68293 -->

  ![Canalizaciones marcadas como favoritas](/help/implementing/cloud-manager/release-notes/assets/pipeline-favorites.png) *Dos canalizaciones marcadas como favoritas.*

  Consulte [Marcar favoritos de canalización](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#pipeline-favorites).


## Programa para primeros usuarios {#early-adoption}

Participe en el programa para primeros usuarios de Cloud Manager para obtener acceso exclusivo a las próximas funciones antes de su lanzamiento general.

Actualmente están disponibles las siguientes oportunidades para primeros usuarios:


### Administrar tokens de acceso{#manage-access-tokens}

Use **Administrar tokens de acceso** en Cloud Manager para ver, cambiar el nombre y eliminar los tokens de acceso asociados con repositorios externos de Git propios, como GitHub Enterprise, GitLab, Bitbucket y Azure DevOps.

Ver [Administrar tokens de acceso](/help/implementing/cloud-manager/managing-code/manage-access-tokens.md)

Si está interesado en probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a desde su dirección de correo electrónico asociada a su Adobe ID.


### Entorno de pruebas especializadas {#specialized-test-environment}

Cloud Manager ahora admite la adición de un nuevo tipo de entorno denominado **Entorno de prueba especializado**. El entorno está diseñado para ayudar a los equipos a validar las funciones en condiciones casi de producción antes de lanzarse. Este tipo de entorno es distinto de los entornos *Production + Stage*, *Development* o *Rapid Development*, y ofrece un espacio centrado para ejecutar escenarios de validación avanzados.

Consulte [Agregar un entorno de prueba especializado](/help/implementing/cloud-manager/specialized-test-environment.md).

![Cuadro de diálogo Agregar entorno con el botón de opción Entorno de prueba especializado seleccionado](/help/implementing/cloud-manager/release-notes/assets/specialized-test-environment.png)

Si está interesado en probar esta nueva característica y compartir sus comentarios, envíe un mensaje de correo electrónico a [grp-earlyadopter_cs_advtestenvironment@adobe.com](mailto:grp-earlyadopter_cs_advtestenvironment@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.


### Traiga su propio Git, ahora con compatibilidad para Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Los clientes ahora pueden incorporar sus repositorios Git de Azure DevOps en Cloud Manager, con compatibilidad tanto con los repositorios modernos de Azure DevOps como con los repositorios heredados de VSTS (Visual Studio Team Services).

* Para los usuarios de Edge Delivery Services, el repositorio incorporado se puede utilizar para sincronizar e implementar el código del sitio.
* Para los usuarios de AEM as a Cloud Service y Adobe Managed Services (AMS), el repositorio se puede vincular a canalizaciones de pila completa y de front-end.

La compatibilidad con tipos de canalización adicionales y la validación de solicitudes de extracción a través de canalizaciones de calidad de código estará disponible pronto.

Consulte [Adición de repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Cuadro de diálogo Añadir repositorio](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID. Asegúrese de incluir qué plataforma Git desea utilizar y si se encuentra en una estructura de repositorio privado/público o de empresa.


#### Preguntas frecuentes sobre Traer su propio Git

| Pregunta | Respuesta |
|---|---|
| *¿Cómo puede un proyecto volver al repositorio Git administrado por Adobe si es necesario?* | Volver atrás es sencillo. [Actualice las canalizaciones](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md) para que apunten al repositorio de Adobe y elimine el repositorio externo si ya no es necesario. |
| *¿Es posible configurar diferentes repositorios para diferentes entornos (por ejemplo, no producción frente a producción) para permitir primero las pruebas en no producción?* | Sí, se pueden configurar diferentes repositorios para entornos independientes. Por ejemplo, la canalización de desarrollo o de calidad del código puede señalar a un repositorio externo mientras que la canalización de producción permanece conectada al repositorio de Adobe. Asegúrese de que el trabajo de sincronización entre los dos repositorios permanece activo durante esta configuración. |
| *¿La configuración existente, como las listas de permitidos IP, sigue funcionando?* | Sí, las listas de permitidos IP existentes siguen funcionando como de costumbre. Sin embargo, si el repositorio Git externo está protegido por un firewall, las [direcciones IP de Adobe necesarias deben agregarse a la lista de permitidos](/help/implementing/cloud-manager/ip-allow-lists/introduction.md). |
| *¿Funcionan todas las URL del repositorio de GitLab? La dirección URL del repositorio en uso sigue el formato `https://gitlab_dedicated_url.com/path/repo-name.git`, que difiere del ejemplo de la documentación.* | Sí, se admite cualquier repositorio de GitLab que admita API V3 o V4, incluidas las URL de GitLab autoalojadas como la descrita en [Agregar repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md) (`https://git-vendor-name.com/org-name/repo-name.git`). |


### Agregar canalización de configuración de Edge Delivery {#add-eds-pipeline}

Las canalizaciones de configuración ahora son compatibles con los sitios creados con Edge Delivery Services, lo que expande esta capacidad más allá de los entornos de Cloud Service. Puede usar **Canalizaciones de configuración** para administrar la configuración, como las reglas de filtrado de tráfico y las configuraciones del firewall de aplicaciones web (WAF), cuando corresponda. Consulte [Configuraciones compatibles](/help/operations/config-pipeline.md#configurations).

![Agregar canalización de Edge Delivery en la lista desplegable Agregar canalización](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add.png) *Agregar una canalización de Edge Delivery desde la página **Información general del programa**, tarjeta **Canalizaciones**.*

![Agregar cuadro de diálogo de canalización de Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-add-dialogbox.png) *Agregar cuadro de diálogo de canalización de Edge Delivery.*

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.


## Correcciones de errores

* Los entornos de zona protegida previamente marcados como `HIBERNATED` ya no permanecen atascados en ese estado, lo que permite que la ejecución o implementación de la canalización se realice según lo esperado. <!-- CMGR-67705 -->
* AEM Cloud Manager ahora asigna correctamente los errores de compilación de Maven causados por errores 409 (conflictos) al recuperar artefactos del cliente en un error causado por el cliente. Este cambio mejora los mensajes de error al distinguir entre errores internos y problemas relacionados con la configuración del entorno del cliente. <!-- CMGR-66673 -->


<!-- ## Known issues {#known-issues} -->

