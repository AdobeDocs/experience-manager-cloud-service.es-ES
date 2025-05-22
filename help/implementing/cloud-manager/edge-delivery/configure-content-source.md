---
title: Configuración de la Source de contenido
description: Obtenga información sobre cómo configurar el origen de contenido del sitio de Edge Delivery. Utilice fstab.yaml con la arquitectura Helix 4 o utilice el asistente guiado en Cloud Manager (o la API del servicio de configuración) con la arquitectura Helix 5.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: f82eafc0-03d0-4c69-9b28-e769a012531b
source-git-commit: 71618a5603328990603db2ee7554048c9020a883
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 40%

---

# Configuración de la fuente de contenido en un solo clic para Edge Delivery Services {#config-content-source}

>[!IMPORTANT]
>
>*Helix* es el nombre interno de la arquitectura subyacente que permite a AEM Sites la creación basada en documentos. No es una función o un nombre de producto. En este artículo, *Helix* hace referencia a la versión de arquitectura utilizada por los sitios de Edge Delivery. Helix 5 es la versión actual de la arquitectura subyacente; Helix 4 es la versión anterior.

Adobe Experience Manager (AEM) Edge Delivery Services permite enviar contenido desde varios orígenes, como Google Drive, SharePoint o el propio AEM, mediante una red perimetral rápida y distribuida globalmente.

La configuración de la fuente de contenido difiere entre las dos versiones de arquitectura de la siguiente manera:

| Versión | Método de configuración de fuente de contenido |
| --- | --- |
| Helix 4 | Archivo YAML (`fstab.yaml`) |
| Helix 5 | API del servicio de configuración (*no`fstab.yaml`*) |

En este artículo se proporcionan pasos de configuración completos, ejemplos e instrucciones de validación para ambas versiones.

**Antes de comenzar**

Si usa [un clic en Edge Delivery en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md##one-click-edge-delivery-site), su sitio usa Helix 5 con un solo repositorio. [Siga las instrucciones de Helix 5](#config-helix5) y use la versión de YAML de Helix 4 proporcionada como alternativa.

**Determine su versión de Helix**

* Helix 4: su proyecto incluye un archivo `fstab.yaml`.
* Helix 5: el proyecto *no* usa `fstab.yaml` y se configuró mediante [Cloud Manager mediante el asistente guiado](/help/implementing/cloud-manager/edge-delivery/add-edge-delivery-site.md) o la API.

Confirme a través de los metadatos del repositorio o consulte con su administrador si aún no está seguro.

## Configuración de la fuente de contenido para Helix 4

En Helix 4, el archivo `fstab.yaml` define el origen de contenido del sitio. Ubicado en la raíz del repositorio de GitHub, este archivo asigna prefijos de ruta de URL (llamados puntos de montaje) a orígenes de contenido externos. Un ejemplo típico tiene el siguiente aspecto:

```yaml
mountpoints:
  /: https://drive.google.com/drive/folders/your-folder-id
```

El ejemplo anterior es solo ilustrativo. La dirección URL real debe apuntar al origen de contenido, como una carpeta de Google Drive, un directorio de SharePoint o una ruta de acceso de AEM.

**Para configurar el origen de contenido para Helix 4:**

Los pasos varían según el sistema de origen que utilice.

* **Google Drive**

   1. Cree una carpeta de Google Drive.
   1. Comparta la carpeta con `helix@adobe.com`.
   1. Obtenga el vínculo de la carpeta que se puede compartir.
   1. Actualice su `fstab.yaml` como se muestra a continuación:

      ```yaml
      mountpoints: 
          /: https://drive.google.com/drive/folders/<folder-id>
      ```

   1. Confirme e inserte los cambios en GitHub.

* **SharePoint**

   1. Cree una carpeta de SharePoint o una biblioteca de documentos.
   1. Comparta el acceso con `helix@adobe.com`.
   1. Obtenga la dirección URL de la carpeta.
   1. Actualice su `fstab.yaml` como se muestra a continuación:

      ```yaml
      mountpoints:
        /: https://<tenant>.sharepoint.com/sites/<site>/Shared%20Documents/<folder>
      ```

   1. Confirme e inserte los cambios en GitHub.

* **AEM**

   1. Identifique la ruta del contenido de AEM.
   1. Utilice la URL de exportación de contenido de AEM como se muestra a continuación:

      ```yaml
      mountpoints:
        /: https://author.<your-aem-instance>.com/bin/franklin.delivery/<org>/<repo>/main
      ```

   1. Confirme e inserte los cambios en GitHub.

### Validación

* Mediante la extensión de Chrome de AEM Sidekick, haga clic en **Vista previa** > **Publicar** > **Probar el sitio activo**.
* Valide la URL: `https://main--<repo>--<org>.hlx.page/`

## Configuración de la fuente de contenido para Helix 5 {#config-helix5}

Helix 5 no utiliza `fstab.yaml`, es compatible con varios sitios que comparten el mismo directorio. La configuración se administra mediante la API del servicio de configuración o la interfaz de usuario de Edge Delivery Sites. La configuración es a nivel de sitio (no de repositorio).

Las diferencias conceptuales son las siguientes:

| Aspecto | Helix 4 | Helix 5 |
| --- | --- | --- |
| Configuración | Listo hasta `fstab.yaml` | Se realiza mediante la API o la IU en lugar de YAML. |
| Puntos de montaje | Definido en `fstab.yaml`. | No es obligatorio. La raíz se entiende implícitamente. |

**Para configurar el origen de contenido de Helix 5:**

1. Con la API del servicio de configuración, realice la autenticación mediante una clave de API o un token de acceso.
1. Realice la siguiente llamada a la API `PUT`:

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

1. Valide la respuesta (se esperaba: HTTP 200 OK).

### Validación

* Mediante la extensión de Chrome de AEM Sidekick, haga clic en **Vista previa** > **Publicar** > **Probar el sitio activo**.
* Valide la URL: `https://main--<repo>--<org>.aem.page/`
* (Opcional) Inspeccione la configuración actual a través de la siguiente llamada de la API `GET`:

  ```bash
  GET /api/{program}/{programId}/site/{siteId}
  ```
