---
title: Notas de la versión 2025.5.0 de Cloud Manager
description: Obtenga información sobre la versión de Cloud Manager 2025.5.0 en Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: 8696cf8a7e7cfc439450b34fa6fda10b38cd415e
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 52%

---

# Notas de la versión para Cloud Manager 2025.5.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Obtenga información sobre el lanzamiento de Cloud Manager 2025.5.0 en AEM (Adobe Experience Manager) as a Cloud Service.

Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.5.0 en AEM as a Cloud Service es el jueves, 8 de mayo de 2025.

La próxima versión planificada es para el jueves, 5 de junio de 2025.

## Novedades {#what-is-new}

### Configuración de la fuente de contenido en un solo clic para Edge Delivery Services

Adobe Experience Manager (AEM) Edge Delivery Services permite enviar contenido desde varios orígenes, como Google Drive, SharePoint o el propio AEM, mediante una red perimetral rápida y distribuida globalmente.

La configuración de la fuente de contenido difiere entre Helix 4 y Helix 5. Conozca la diferencia y siga los pasos de configuración completos, ejemplos e instrucciones de validación para ambas versiones.

Consulte [Configurar el origen de contenido](/help/implementing/cloud-manager/edge-delivery/configure-content-source.md).


## Programa para primeros usuarios {#early-adoption}

Participe en el programa para primeros usuarios de Cloud Manager para obtener acceso exclusivo a las próximas funciones antes de su lanzamiento general.

Actualmente están disponibles las siguientes oportunidades para primeros usuarios:

### Agregar canalización de configuración de Edge Delivery {#add-eds-pipeline}

Las canalizaciones de configuración ahora son compatibles con los sitios creados con Edge Delivery Services, lo que expande esta capacidad más allá de los entornos de Cloud Service. Puede usar **Canalizaciones de configuración** para administrar la configuración, como las reglas de filtrado de tráfico y las configuraciones del firewall de aplicaciones web (WAF), cuando corresponda. Consulte [Configuraciones compatibles](/help/operations/config-pipeline.md#configurations).

![Agregar canalización de Edge Delivery en la lista desplegable Agregar canalización](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png)

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.

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


<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->

