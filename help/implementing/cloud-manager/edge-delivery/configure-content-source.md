---
title: Configuración de la Source de contenido
description: Aprenda a configurar el origen de contenido de su sitio de Edge Delivery mediante fstab.yaml en Helix 4 o la interfaz de usuario de Edge Delivery Services (o la API del servicio de configuración) en Helix 5.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8696cf8a7e7cfc439450b34fa6fda10b38cd415e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 1%

---

# Configuración de la fuente de contenido en un solo clic para Edge Delivery Services {#config-content-source}

Adobe Experience Manager (AEM) Edge Delivery Services permite la entrega de contenido desde varias fuentes, como Google Drive, SharePoint o el propio AEM, mediante una red perimetral rápida y distribuida globalmente.

La configuración de la fuente de contenido difiere entre Helix 4 y Helix 5 del siguiente modo:

| Versión | Método de configuración de fuente de contenido |
| --- | --- |
| Helix 4 | Archivo YAML (`fstab.yaml`) |
| Helix 5 | API del servicio de configuración (*no`fstab.yaml`*) |

En este artículo se proporcionan pasos de configuración completos, ejemplos e instrucciones de validación para ambas versiones.

**Antes de comenzar**

Si usa [un clic en Edge Delivery en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site), su sitio es Helix 5 con un solo repositorio. [Siga las instrucciones de Helix 5](#config-helix5) y use la versión de YAML de Helix 4 proporcionada como alternativa.

**Determine su versión de Helix**

* Helix 4: su proyecto incluye un archivo de `fstab.yaml`.
* Helix 5: el proyecto *no* usa `fstab.yaml` y se configuró mediante la [interfaz de usuario de Edge Delivery Services](#config-helix5) o la API.

Confirme a través de los metadatos del repositorio o consulte con su administrador si aún no está seguro.

## Configuración de la fuente de contenido para Helix 4

En Helix 4, el archivo fstab.yaml define el origen de contenido del sitio. Ubicado en la raíz del repositorio de GitHub, este archivo asigna prefijos de ruta de URL (llamados puntos de montaje) a orígenes de contenido externos. Un ejemplo típico tiene el siguiente aspecto:

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

Este ejemplo es solo ilustrativo. La dirección URL real debe apuntar al origen de contenido, como una carpeta de Google Drive, un directorio de SharePoint o una ruta de acceso de AEM.

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

### Validación

* Con la extensión AEM Sidekick Chrome, haga clic en **Vista previa** > **Publicar** > **Probar el sitio activo**.
* Validar URL: `https://main--<repo>--<org>.hlx.page/`

## Configuración de la fuente de contenido para Helix 5 {#config-helix5}

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

### Validación

* Con la extensión AEM Sidekick Chrome, haga clic en **Vista previa** > **Publicar** > **Probar el sitio activo**.
* Validar URL: `https://main--<repo>--<org>.aem.page/`
* (Opcional) Inspeccione la configuración actual a través de la siguiente llamada de API `GET`:

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```
