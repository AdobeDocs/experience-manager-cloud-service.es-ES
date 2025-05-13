---
title: Notas de la versión 2025.5.0 de Cloud Manager
description: Obtenga información sobre la versión de Cloud Manager 2025.5.0 en Adobe Experience Manager as a Cloud Service.
feature: Release Information
role: Admin
exl-id: 24d9fc6f-462d-417b-a728-c18157b23bbe
source-git-commit: f9f4226bff8a0772878c144773eb8ff841a0a8d0
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 20%

---

# Notas de la versión para Cloud Manager 2025.5.0 en Adobe Experience Manager as a Cloud Service {#release-notes}

<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/Cloud+Manager+2025.03.0+Release -->

Obtenga información sobre el lanzamiento de Cloud Manager 2025.5.0 en AEM (Adobe Experience Manager) as a Cloud Service.

Consulte también las [notas de la versión actual de Adobe Experience Manager as a Cloud Service](/help/release-notes/release-notes-cloud/release-notes-current.md).

## Fechas de lanzamiento {#release-date}

La fecha de lanzamiento de Cloud Manager 2025.5.0 en AEM as a Cloud Service es el viernes, 08 de mayo de 2025.

La próxima versión planificada es para el viernes, 05 de junio de 2025.

## Novedades {#what-is-new}

### Configuración de la fuente de contenido en un solo clic para Edge Delivery Services

Adobe Experience Manager (AEM) Edge Delivery Services permite la entrega de contenido desde varias fuentes, como Google Drive, SharePoint o el propio AEM, mediante una red perimetral rápida y distribuida globalmente.

La configuración de la fuente de contenido difiere entre Helix 4 y Helix 5 del siguiente modo:

| Versión | Método de configuración de fuente de contenido |
| --- | --- |
| Helix 4 | Archivo YAML (`fstab.yaml`) |
| Helix 5 | API del servicio de configuración (*no`fstab.yaml`*) |

En este artículo se proporcionan pasos de configuración completos, ejemplos e instrucciones de validación para ambas versiones.

**Antes de comenzar**

Si usa [un clic en Edge Delivery en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site), su sitio es Helix 5 con un solo repositorio. Siga las instrucciones de Helix 5 y utilice la versión de instrucciones de Helix 4 YAML proporcionada como alternativa.

**Determine su versión de Helix**

* Helix 4: su proyecto incluye un archivo de `fstab.yaml`.
* Helix 5: el proyecto *no* usa `fstab.yaml` y se configuró mediante la interfaz de usuario o la API de Edge Delivery Services.

Confirme a través de los metadatos del repositorio o consulte con su administrador si aún no está seguro.

#### Configuración de la fuente de contenido para Helix 4

En Helix 4, el archivo fstab.yaml define el origen de contenido del sitio. Ubicado en la raíz del repositorio de GitHub, este archivo asigna prefijos de ruta de URL (llamados puntos de montaje) a orígenes de contenido externos. Un ejemplo típico tiene el siguiente aspecto:

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

Este ejemplo es solo ilustrativo. La dirección URL real debe apuntar al origen de contenido, como una carpeta específica de Google Drive, un directorio de SharePoint o una ruta de acceso de AEM.

**Para configurar el origen de contenido para Helix 4:**

Los pasos varían según el sistema de origen que utilice.

* **Unidad Google**

   1. Cree una carpeta de Google Drive.
   1. Compartir la carpeta con `helix@adobe.com`.
   1. Obtenga el vínculo de carpeta compartida.
   1. Actualice su `fstab.yaml` como se muestra a continuación:

      ```yaml
      mountpoints: 
          /: https://drive.google.com/drive/folders/<folder-id>
      ```

   1. Confirme y envíe los cambios a GitHub.

* **SharePoint**

   1. Crear una carpeta de SharePoint o una biblioteca de documentos.
   1. Compartir acceso con `helix@adobe.com`.
   1. Obtenga la dirección URL de la carpeta.
   1. Actualice su `fstab.yaml` como se muestra a continuación:

      ```yaml
      mountpoints:
        /: https://<tenant>.sharepoint.com/sites/<site>/Shared%20Documents/<folder>
      ```

   1. Confirme y envíe los cambios a GitHub.

* **AEM**

   1. Identifique la ruta del contenido de AEM.
   1. Utilice la URL de exportación de contenido de AEM como se muestra en la siguiente ilustración:

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. Confirme y envíe los cambios a GitHub.

##### Validación

* Con la extensión AEM Sidekick Chrome, haga clic en **Vista previa** > **Publicar** > **Probar el sitio activo**.
* Validar URL: `https://main--<repo>--<org>.hlx.page/`

#### Configuración de la fuente de contenido para Helix 5

Helix 5 no utiliza `fstab.yaml`, es compatible con varios sitios que comparten el mismo directorio. La configuración se administra mediante la API del servicio de configuración o la IU de Edge Delivery Services. La configuración es de nivel de sitio (no de repositorio).

Las diferencias conceptuales son las siguientes:

| Aspecto | Helix 4 | Helix 5 |
| --- | --- | --- |
| Configuración | Listo hasta `fstab.yaml` | Se realiza mediante la API o la IU en lugar de YAML. |
| Puntos de montaje | Definido en `fstab.yaml`. | No es obligatorio. La raíz se entiende implícitamente. |

**Para configurar el origen de contenido de Helix 5:**

1. Con la API del servicio de configuración, realice la autenticación mediante una clave de API o un token de acceso.
1. Realizar la siguiente llamada a la API `PUT`:

   ```bash {.line-numbering}
   PUT /api/{program}/{programId}/site/{siteId}
   Content-Type: application/json
   
   {
     "sitename": "my-site",
     "branchName": "main",
     "version": "v5",
     "repo": "my-content-repo-link"
   }
   ```

1. Validar respuesta (se esperaba: HTTP 200 OK).

##### Validación

* Con la extensión AEM Sidekick Chrome, haga clic en **Vista previa** > **Publicar** > **Probar el sitio activo**.
* Validar URL: `https://main--<repo>--<org>.aem.page/`
* (Opcional) Inspeccione la configuración actual a través de la siguiente llamada de API `GET`:

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```

<!--
* **AI-powered build summaries now available for internal use**

    Internal users can now use AI-powered build summaries to simplify build log analysis. The feature provides actionable recommendations and helps identify the root causes of build failures.

    ![Build Summary dialog box](/help/implementing/cloud-manager/release-notes/assets/build-summary.png)
-->


## Programa para primeros usuarios {#early-adoption}

Participe en el programa de usuarios que adoptan anticipadamente Cloud Manager para obtener acceso exclusivo a las próximas funciones antes de su lanzamiento general.

Actualmente están disponibles las siguientes oportunidades para los usuarios que las adoptaron por primera vez:

### Añadir canalización de Edge Delivery {#add-eds-pipeline}

Ahora se admiten **canalizaciones** para sitios creados con Edge Delivery Services, lo que amplía esta capacidad más allá de los entornos de Cloud Service. Puede usar **Canalizaciones** para administrar configuraciones como las reglas de filtrado de tráfico y las configuraciones de Firewall de aplicaciones web (WAF), cuando corresponda. Consulte [Configuraciones compatibles](/help/operations/config-pipeline.md#configurations).

<!-- ![Add Edge Delivery pipeline in Add Pipeline drop-down list](/help/implementing/cloud-manager/release-notes/assets/add-edge-delivery-pipeline.png) -->

Si está interesado en probar esta nueva característica y compartir sus comentarios, envíe un mensaje de correo electrónico a [grp-aemeds-config-pipeline-adopter@adobe.com](mailto:grp-aemeds-config-pipeline-adopter@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID.

### Traiga su propio Git: ahora compatible con Azure DevOps {#gitlab-bitbucket-azure-vsts}

<!-- BOTH CS & AMS -->

Los clientes ahora pueden incorporar sus repositorios de Git de Azure DevOps en Cloud Manager, con compatibilidad tanto con los repositorios modernos de Azure DevOps como con los repositorios heredados de VSTS (Visual Studio Team Services).

* Para los usuarios de Edge Delivery Services, el repositorio incorporado se puede utilizar para sincronizar e implementar el código del sitio.
* Para los usuarios de AEM as a Cloud Service y Adobe Managed Services (AMS), el repositorio se puede vincular a canalizaciones de pila completa y de front-end.

La compatibilidad con tipos de canalización adicionales y la validación de solicitudes de extracción a través de canalizaciones de calidad de código estará disponible pronto.

Consulte [Adición de repositorios externos en Cloud Manager](/help/implementing/cloud-manager/managing-code/external-repositories.md).

![Cuadro de diálogo Añadir repositorio](/help/implementing/cloud-manager/release-notes/assets/azure-repo.png)

Si le interesa probar esta nueva función y compartir sus comentarios, envíe un correo electrónico a [Grp-CloudManager_BYOG@adobe.com](mailto:grp-cloudmanager_byog@adobe.com) desde su dirección de correo electrónico asociada a su Adobe ID. Asegúrese de incluir qué plataforma Git desea utilizar y si se encuentra en una estructura de repositorio privado/público o de empresa.

<!--
## Bug fixes

* Issue

* Issue

* Issue
-->

<!-- ## Known issues {#known-issues} -->

