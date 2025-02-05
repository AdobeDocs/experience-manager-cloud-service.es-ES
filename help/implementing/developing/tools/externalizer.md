---
title: Externalización de direcciones URL
description: El externalizador es un servicio OSGi que permite transformar mediante programación una ruta de recurso en una dirección URL externa y absoluta.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Externalización de direcciones URL {#externalizing-urls}

AEM En la práctica, **Externalizer** es un servicio OSGi que le permite transformar mediante programación una ruta de acceso de recursos (por ejemplo, `/path/to/my/page`) en una dirección URL externa y absoluta (por ejemplo, `https://www.mycompany.com/path/to/my/page`) al anteponer a la ruta de acceso un DNS preconfigurado.

Dado que una instancia de AEM as a Cloud Service no puede conocer su dirección URL visible externamente y que a veces debe crearse un vínculo fuera del ámbito de la solicitud, este servicio proporciona un lugar central para configurar esas direcciones URL externas y crearlas.

Este artículo explica cómo configurar el servicio Externalizer y cómo utilizarlo. Para obtener detalles técnicos del servicio, consulte [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## Comportamiento predeterminado del externalizador y cómo anularlo {#default-behavior}

AEM De forma predeterminada, el servicio externalizador asigna un puñado de identificadores de dominio a prefijos de URL absolutos que coinciden con las URL del servicio de que se han generado para el entorno, como `author https://author-p12345-e6789.adobeaemcloud.com` y `publish https://publish-p12345-e6789.adobeaemcloud.com`. Las direcciones URL base para cada uno de estos dominios predeterminados se leen desde variables de entorno definidas por Cloud Manager.

Como referencia, la configuración predeterminada de OSGi para `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` es efectivamente:

```json
{
   "externalizer.domains": [
      "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
      "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
      "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]",
      "preview $[env:AEM_EXTERNALIZER_PREVIEW;default=http://localhost:4503]"
   ]
}
```

>[!CAUTION]
>
>Las asignaciones de dominio del externalizador `local`, `author`, `preview` y `publish` predeterminadas en la configuración OSGi deben conservarse con los valores `$[env:...]` originales enumerados arriba.
>
>La implementación de un archivo personalizado `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` en AEM as a Cloud Service que omita cualquiera de estas asignaciones de dominio predeterminadas puede dar como resultado un comportamiento de aplicación impredecible.

Para anular los valores `preview` y `publish`, use las variables de entorno de Cloud Manager como se describe en el artículo [Configuración de OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) y configuración de las variables predefinidas `AEM_CDN_DOMAIN_PUBLISH` y `AEM_CDN_DOMAIN_PREVIEW`.

## Configuración del servicio externalizador {#configuring-the-externalizer-service}

El servicio externalizador permite definir de forma centralizada el dominio que se puede utilizar para prefijar mediante programación las rutas de recursos. El servicio externalizador solo debe utilizarse para aplicaciones con un solo dominio.

>[!NOTE]
>
>Al igual que al aplicar cualquier configuración de [OSGi para AEM as a Cloud Service](/help/implementing/deploying/overview.md#osgi-configuration), los siguientes pasos deben realizarse en una instancia de desarrollador local y luego comprometerse con el código del proyecto para su implementación.

Para definir una asignación de dominio para el servicio externalizador:

1. Vaya al Administrador de configuración a través de:

   `https://<host>:<port>/system/console/configMgr`

1. Haga clic en **Externalizador de vínculos CQ de día** para abrir el cuadro de diálogo de configuración.

   ![La configuración OSGi del externalizador](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >El vínculo directo a la configuración es `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Defina una asignación de **dominios**. Una asignación consta de un nombre único que se puede utilizar en el código para hacer referencia al dominio, a un espacio y al dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Donde:

   * **`scheme`** suele ser http o https, pero puede ser otro protocolo.

      * Adobe recomienda utilizar https para aplicar vínculos https.
      * Se utiliza si el código de cliente no anula el esquema al solicitar la externalización de una dirección URL.

   * **`server`** es el nombre de host (un nombre de dominio o una dirección ip).
   * **`port`** (opcional) es el número de puerto.
   * AEM **`contextpath`** (opcional) solo se establece si se instala la aplicación web como una aplicación web en una ruta de contexto diferente.

   Por ejemplo: `production https://my.production.instance`

   AEM Los siguientes nombres de asignación están predefinidos y siempre deben configurarse, ya que se basa en ellos:

   * `local`: la instancia local
   * `author`: DNS del sistema de creación
   * `publish`: DNS del sitio web público

   >[!NOTE]
   >
   >AEM Una configuración personalizada le permite agregar una nueva categoría, como `production`, `staging` o incluso sistemas externos que no son de tipo de sistema, como `my-internal-webservice`, que no son de tipo de sistema (no de tipo de sistema), como . Es útil evitar codificar estas URL en diferentes lugares del código base de un proyecto.

1. Haga clic en **Guardar** para guardar los cambios.

### Uso del servicio externalizador {#using-the-externalizer-service}

Esta sección muestra algunos ejemplos de cómo se puede utilizar el servicio Externalizer.

>[!NOTE]
>
>No se deben crear vínculos absolutos en el contexto de HTML. Por lo tanto, no utilice esta utilidad en estos casos.

* **Para externalizar una ruta de acceso con el dominio &#39;publicar&#39;:**

  ```java
  String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
  ```

  Suponiendo la asignación de dominio:

   * `publish https://www.website.com`

   * `myExternalizedUrl` termina con el valor:

   * `https://www.website.com/contextpath/my/page.html`

* **Para externalizar una ruta de acceso con el dominio &#39;author&#39;:**

  ```java
  String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
  ```

  Suponiendo la asignación de dominio:

   * `author https://author.website.com`

   * `myExternalizedUrl` termina con el valor:

   * `https://author.website.com/contextpath/my/page.html`

* **Para externalizar una ruta de acceso con el dominio &#39;local&#39;:**

  ```java
  String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
  ```

  Suponiendo la asignación de dominio:

   * `local https://publish-3.internal`

   * `myExternalizedUrl` termina con el valor:

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>Puede encontrar más ejemplos en [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
