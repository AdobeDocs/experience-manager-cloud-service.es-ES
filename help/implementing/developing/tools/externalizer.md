---
title: Externalización de direcciones URL
description: El externalizador es un servicio OSGi que permite transformar mediante programación una ruta de recurso en una dirección URL externa y absoluta.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Externalización de direcciones URL {#externalizing-urls}

AEM En el caso de los **Externalizador** es un servicio OSGi que permite transformar mediante programación una ruta de recursos (por ejemplo, `/path/to/my/page`) en una dirección URL externa y absoluta (por ejemplo, `https://www.mycompany.com/path/to/my/page`) prefijando la ruta con un DNS preconfigurado.

AEM Debido a que una instancia as a Cloud Service de la aplicación no puede conocer su dirección URL visible externamente y a que a veces se debe crear un vínculo fuera del ámbito de la solicitud, este servicio proporciona un lugar central para configurar esas direcciones URL externas y crearlas.

Este artículo explica cómo configurar el servicio Externalizer y cómo utilizarlo. Para obtener detalles técnicos del servicio, consulte [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## Comportamiento predeterminado del externalizador y cómo anularlo {#default-behavior}

AEM De forma predeterminada, el servicio externalizador asigna un puñado de identificadores de dominio a prefijos de URL absolutos que coinciden con las URL de servicio de que se han generado para el entorno, como `author https://author-p12345-e6789.adobeaemcloud.com` y `publish https://publish-p12345-e6789.adobeaemcloud.com`. Las direcciones URL base para cada uno de estos dominios predeterminados se leen desde variables de entorno definidas por Cloud Manager.

Como referencia, la configuración OSGi predeterminada para `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` es efectivamente:

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
>El valor predeterminado `local`, `author`, `preview`, y `publish` Las asignaciones de dominio externalizador en la configuración OSGi deben conservarse con el original `$[env:...]` valores enumerados anteriormente.
>
>Implementación de un `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` AEM archivo a la que se va a crear un as a Cloud Service que omita cualquiera de estas asignaciones de dominio predeterminadas, lo que puede provocar un comportamiento impredecible en la aplicación.

Para anular la variable `preview` y `publish` Utilice las variables de entorno de Cloud Manager como se describe en el artículo [AEM Configuración de OSGi para la as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) y establecer el predefinido `AEM_CDN_DOMAIN_PUBLISH` y `AEM_CDN_DOMAIN_PREVIEW` variables.

## Configuración del servicio externalizador {#configuring-the-externalizer-service}

El servicio externalizador permite definir de forma centralizada el dominio que se puede utilizar para prefijar mediante programación las rutas de recursos. El servicio externalizador solo debe utilizarse para aplicaciones con un solo dominio.

>[!NOTE]
>
>Al igual que al aplicar cualquiera [AEM Configuraciones de OSGi para el as a Cloud Service de la,](/help/implementing/deploying/overview.md#osgi-configuration) los siguientes pasos deben realizarse en una instancia de desarrollador local y luego comprometerse con el código del proyecto para su implementación.

Para definir una asignación de dominio para el servicio externalizador:

1. Vaya al Administrador de configuración a través de:

   `https://<host>:<port>/system/console/configMgr`

1. Clic **Externalizador de vínculos CQ de día** para abrir el cuadro de diálogo de configuración.

   ![La configuración OSGi del externalizador](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >El vínculo directo a la configuración es `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Defina un **Domains** asignación. Una asignación consta de un nombre único que se puede utilizar en el código para hacer referencia al dominio, a un espacio y al dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Donde:

   * **`scheme`** suele ser http o https, pero puede ser otro protocolo.

      * Adobe recomienda utilizar https para aplicar vínculos https.
      * Se utiliza si el código de cliente no anula el esquema al solicitar la externalización de una dirección URL.

   * **`server`** es el nombre de host (un nombre de dominio o una dirección ip).
   * **`port`** (opcional) es el número de puerto.
   * **`contextpath`** AEM (opcional) solo se establece si se instala la aplicación web como una aplicación web en una ruta de contexto diferente.

   Por ejemplo: `production https://my.production.instance`

   AEM Los siguientes nombres de asignación están predefinidos y siempre deben configurarse, ya que se basa en ellos:

   * `local` - la instancia local
   * `author` - el sistema de creación DNS
   * `publish` - el sitio web público DNS

   >[!NOTE]
   >
   >Una configuración personalizada le permite agregar una nueva categoría, como `production`, `staging` AEM o incluso sistemas externos no relacionados con el uso de la, como `my-internal-webservice`. Es útil evitar codificar estas URL en diferentes lugares del código base de un proyecto.

1. Clic **Guardar** para guardar los cambios.

### Uso del servicio externalizador {#using-the-externalizer-service}

Esta sección muestra algunos ejemplos de cómo se puede utilizar el servicio Externalizer.

>[!NOTE]
>
>No se deben crear vínculos absolutos en el contexto de HTML. Por lo tanto, esta utilidad no debe utilizarse en estos casos.

* **Para externalizar una ruta con el dominio &quot;publicar&quot;:**

  ```java
  String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
  ```

  Suponiendo la asignación de dominio:

   * `publish https://www.website.com`

   * `myExternalizedUrl` termina con el valor:

   * `https://www.website.com/contextpath/my/page.html`

* **Para externalizar una ruta con el dominio &quot;author&quot;:**

  ```java
  String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
  ```

  Suponiendo la asignación de dominio:

   * `author https://author.website.com`

   * `myExternalizedUrl` termina con el valor:

   * `https://author.website.com/contextpath/my/page.html`

* **Para externalizar una ruta con el dominio &quot;local&quot;:**

  ```java
  String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
  ```

  Suponiendo la asignación de dominio:

   * `local https://publish-3.internal`

   * `myExternalizedUrl` termina con el valor:

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>Puede encontrar más ejemplos en la [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
