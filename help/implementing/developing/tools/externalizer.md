---
title: Externalización de direcciones URL
description: El externalizador es un servicio OSGi que le permite transformar mediante programación una ruta de recurso en una dirección URL externa y absoluta.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: ce43bdc94f14faa69add16139e22ea3f34dfc52f
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Externalización de direcciones URL {#externalizing-urls}

En AEM, **Externalizer** es un servicio OSGi que le permite transformar mediante programación una ruta de recursos (p. ej. `/path/to/my/page`) en una dirección URL externa y absoluta (por ejemplo, `https://www.mycompany.com/path/to/my/page`) añadiendo un prefijo a la ruta con un DNS preconfigurado.

Dado que una instancia de AEM como Cloud Service no puede saber su URL visible externamente y que a veces se debe crear un vínculo fuera del ámbito de la solicitud, este servicio proporciona un lugar central para configurar esas URL externas y crearlas.

Este artículo explica cómo configurar el servicio externalizador y cómo utilizarlo. Para obtener detalles técnicos del servicio, consulte [Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html).

## Comportamiento predeterminado del externalizador y cómo anular {#default-behavior}

De forma predeterminada, el servicio externalizador tiene valores como `author-p12345-e6789.adobeaemcloud.com` y `publish-p12345-e6789.adobeaemcloud.com`.

Para anular estos valores, utilice variables de entorno de Cloud Manager como se describe en el artículo [Configuración de OSGi para AEM como Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) y configure las variables predefinidas `AEM_CDN_DOMAIN_AUTHOR` y `AEM_CDN_DOMAIN_PUBLISH` .

## Configuración del servicio externalizador {#configuring-the-externalizer-service}

El servicio externalizador le permite definir de forma centralizada el dominio que se puede utilizar para prefijar programáticamente las rutas de recursos. El servicio externalizador solo debe utilizarse para aplicaciones con un solo dominio.

>[!NOTE]
>
>Al igual que al aplicar cualquier configuración [OSGi para AEM como Cloud Service,](/help/implementing/deploying/overview.md#osgi-configuration) los siguientes pasos deben realizarse en una instancia de desarrollador local y luego comprometerse con el código del proyecto para su implementación.

Para definir una asignación de dominio para el servicio externalizador:

1. Vaya al Administrador de configuración mediante:

   `https://<host>:<port>/system/console/configMgr`

1. Haga clic en **Day CQ Link Externalizer** para abrir el cuadro de diálogo de configuración.

   ![La configuración Externalizer OSGi](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >El enlace directo a la configuración es `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Defina una asignación de **Domains**. Una asignación consiste en un nombre único que se puede utilizar en el código para hacer referencia al dominio, un espacio y el dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Donde:

   * **`scheme`** generalmente es http o https, pero puede ser otro protocolo.

      * Se recomienda utilizar https para aplicar los vínculos https.
      * Se utilizará si el código de cliente no anula el esquema al solicitar la externalización de una URL.
   * **`server`** es el nombre de host (un nombre de dominio o una dirección ip).
   * **`port`** (opcional) es el número de puerto.
   * **`contextpath`** (opcional) solo se establece si AEM está instalado como una aplicación web en una ruta de contexto diferente.

   Por ejemplo: `production https://my.production.instance`

   Los siguientes nombres de asignación están predefinidos y siempre deben configurarse como AEM dependen de ellos:

   * `local` : la instancia local
   * `author` - el DNS del sistema de creación
   * `publish` - el sitio web DNS de cara al público

   >[!NOTE]
   >
   >Una configuración personalizada le permite agregar una nueva categoría, como `production`, `staging` o incluso sistemas no AEM externos como `my-internal-webservice`. Es útil evitar codificar dichas URL en distintos lugares de la base de código de un proyecto.

1. Haga clic en **Guardar** para guardar los cambios.

### Uso del servicio externalizador {#using-the-externalizer-service}

Esta sección muestra algunos ejemplos de cómo se puede utilizar el servicio externalizador.

>[!NOTE]
>
>No se deben crear vínculos absolutos en el contexto de HTML. Por lo tanto, esta utilidad no debe utilizarse en tales casos.

* **Para externalizar una ruta con el dominio &quot;publicar&quot;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Suponiendo la asignación de dominios:

   * `publish https://www.website.com`

   * `myExternalizedUrl` termina con el valor:

   * `https://www.website.com/contextpath/my/page.html`

* **Para externalizar una ruta con el dominio &quot;autor&quot;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Suponiendo la asignación de dominios:

   * `author https://author.website.com`

   * `myExternalizedUrl` termina con el valor:

   * `https://author.website.com/contextpath/my/page.html`

* **Para externalizar una ruta con el dominio &quot;local&quot;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Suponiendo la asignación de dominios:

   * `local https://publish-3.internal`

   * `myExternalizedUrl` termina con el valor:

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>Puede encontrar más ejemplos en [Javadocs](https://docs.adobe.com/content/help/en/experience-manager-cloud-service-javadoc/com/day/cq/commons/Externalizer.html).
