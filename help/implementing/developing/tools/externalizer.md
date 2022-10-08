---
title: Externalización de direcciones URL
description: El externalizador es un servicio OSGi que le permite transformar mediante programación una ruta de recurso en una dirección URL externa y absoluta.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: ca849bd76e5ac40bc76cf497619a82b238d898fa
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Externalización de direcciones URL {#externalizing-urls}

En AEM, la variable **Externalizador** es un servicio OSGi que le permite transformar mediante programación una ruta de recursos (por ejemplo, `/path/to/my/page`) en una dirección URL externa y absoluta (por ejemplo, `https://www.mycompany.com/path/to/my/page`) añadiendo un prefijo a la ruta con un DNS preconfigurado.

Dado que una instancia as a Cloud Service AEM no puede saber su URL visible externamente y que a veces se debe crear un vínculo fuera del ámbito de la solicitud, este servicio proporciona un lugar central para configurar esas URL externas y crearlas.

Este artículo explica cómo configurar el servicio externalizador y cómo utilizarlo. Para obtener información técnica sobre el servicio, consulte la [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## Comportamiento predeterminado del externalizador y cómo ignorarlo {#default-behavior}

De forma predeterminada, el servicio externalizador asigna un puñado de identificadores de dominio a prefijos de URL absolutos que coinciden con las direcciones URL del servicio de AEM que se han generado para el entorno, como `author https://author-p12345-e6789.adobeaemcloud.com` y `publish https://publish-p12345-e6789.adobeaemcloud.com`. Las direcciones URL base de cada uno de estos dominios predeterminados se leen desde variables de entorno definidas por Cloud Manager.

Como referencia, la configuración OSGi predeterminada para `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` es eficaz:

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
>El valor predeterminado `local`, `author`, `preview`y `publish` Las asignaciones de dominio externalizador en la configuración OSGi deben conservarse con el `$[env:...]` valores enumerados anteriormente.
>
>Implementación de un `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` para AEM as a Cloud Service que omita cualquiera de estas asignaciones de dominio predeterminadas puede provocar un comportamiento de aplicación impredecible.

Para anular la variable `preview` y `publish` utilice las variables de entorno de Cloud Manager como se describe en el artículo [Configuración de OSGi para AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) y configurar los `AEM_CDN_DOMAIN_PUBLISH` y `AEM_CDN_DOMAIN_PREVIEW` variables.

## Configuración del servicio externalizador {#configuring-the-externalizer-service}

El servicio externalizador le permite definir de forma centralizada el dominio que se puede utilizar para prefijar programáticamente las rutas de recursos. El servicio externalizador solo debe utilizarse para aplicaciones con un solo dominio.

>[!NOTE]
>
>Como cuando se aplica cualquier [Configuraciones de OSGi para AEM as a Cloud Service,](/help/implementing/deploying/overview.md#osgi-configuration) los siguientes pasos deben realizarse en una instancia de desarrollador local y luego comprometerse con el código del proyecto para su implementación.

Para definir una asignación de dominio para el servicio externalizador:

1. Vaya al Administrador de configuración mediante:

   `https://<host>:<port>/system/console/configMgr`

1. Haga clic en **Externalizador de vínculos de CQ de día** para abrir el cuadro de diálogo de configuración.

   ![La configuración Externalizer OSGi](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >El vínculo directo a la configuración es `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Defina un **Dominios** asignación. Una asignación consiste en un nombre único que se puede utilizar en el código para hacer referencia al dominio, un espacio y el dominio:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   donde:

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
   >Una configuración personalizada le permite agregar una nueva categoría, como `production`, `staging` o incluso sistemas externos no AEM como `my-internal-webservice`. Es útil evitar codificar dichas URL en distintos lugares de la base de código de un proyecto.

1. Haga clic en **Guardar** para guardar los cambios.

### Uso del servicio externalizador {#using-the-externalizer-service}

Esta sección muestra algunos ejemplos de cómo se puede utilizar el servicio externalizador.

>[!NOTE]
>
>No se deben crear vínculos absolutos en el contexto del HTML. Por lo tanto, esta utilidad no debe utilizarse en tales casos.

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
>Puede encontrar más ejemplos en la sección [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
