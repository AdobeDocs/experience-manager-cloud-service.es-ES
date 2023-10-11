---
title: ¿Qué es la caché de formularios adaptables? AEM ¿y cómo almacenar en caché un formulario adaptable de la?
description: La memoria caché de Forms adaptable está diseñada para Forms y documentos adaptables con el objetivo de reducir el tiempo necesario para procesar un formulario o documento adaptable.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
source-git-commit: d33c7278d16a8cce76c87b606ca09aa91f1c3563
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 68%

---


# Configuración de la caché de los formularios adaptables {#configure-adaptive-forms-cache}

Una caché es un mecanismo para acortar los tiempos de acceso a los datos, reducir la latencia y mejorar las velocidades de entrada y salida (E/S). La caché de Forms adaptable almacena únicamente el contenido del HTML y la estructura JSON de un formulario adaptable sin guardar los datos rellenados previamente. Esto contribuye a reducir el tiempo necesario para representar un formulario adaptable en el cliente. Está diseñada específicamente para formularios adaptables.

## Configuración de la caché de los formularios adaptables en instancias de autor y publicación {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vaya al Administrador de configuración de la consola web de AEM en `https://[server]:[port]/system/console/configMgr`.
1. Haga clic en **[!UICONTROL Configuración del canal Web de comunicaciones interactivas y formularios adaptables]** para editar sus valores de configuración.
1. En el cuadro de diálogo [!UICONTROL Editar valores de configuración], especifique el número máximo de formularios o documentos que una instancia de AEM [!DNL Forms Server] puede almacenar en la caché en el campo **[!UICONTROL Número de formularios adaptables]**. El valor predeterminado es 100.

   >[!NOTE]
   >
   >Para deshabilitar la caché, establezca el valor del campo Número de formularios adaptables en **0**. La caché se restablece y todos los formularios y documentos se eliminan de ella cuando se desactiva o cambia su configuración.

   ![Cuadro de diálogo de configuración para la caché de HTML de los formularios adaptables](assets/cache-configuration-edit.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar la configuración.

Su entorno está configurado para utilizar la caché de los formularios adaptables y los recursos relacionados.


## (Opcional) Configuración de la caché de un formulario adaptable en Dispatcher {#configure-the-cache}

También puede configurar el almacenamiento en caché de un formulario adaptable en Dispatcher para mejorar el rendimiento.

### Requisitos previos {#pre-requisites}

* Habilite la [combinar o prerrellenar datos en el cliente](prepopulate-adaptive-form-fields.md#prefill-at-client) opción. Esto ayuda a combinar los datos únicos de cada instancia del formulario prerrellenado.
* [Habilite un agente de vaciado para cada instancia de publicación](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=es#invalidating-dispatcher-cache-from-a-publishing-instance). Esto le permitirá obtener un mejor rendimiento de almacenamiento en caché en los formularios adaptables. La URL predeterminada de los agentes de vaciado es `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### Consideraciones para almacenar los formularios adaptables en la caché en Dispatcher {#considerations}

* Cuando utilice la caché de los formularios adaptables, utilice [!DNL Dispatcher] de AEM para almacenar en caché las bibliotecas de cliente (CSS y JavaScript) de un formulario adaptable.
* Cuando desarrolle componentes personalizados, mantenga deshabilitada la caché de los formularios adaptables en el servidor utilizado para el desarrollo.
* Las URL sin extensión no se almacenan en caché. Por ejemplo, las URL con el patrón `/content/forms/[folder-structure]/[form-name].html` se almacenan en la caché, y el almacenamiento en la caché ignora las URL con el patrón `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Por lo tanto, utilice direcciones URL con extensiones para aprovechar las ventajas del almacenamiento en caché.
* Consideraciones para los formularios adaptables localizados:
   * En el entorno de Cloud Service, utilice el formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar una versión localizada de un formulario adaptable en lugar de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Deshabilite el uso de la configuración regional del explorador <!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) -->para URL con el formato `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Cuando se usa el formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`, y la opción **[!UICONTROL Usar configuración regional del explorador]** está desactivada en el Administrador de configuración, se proporciona la versión no localizada del formulario adaptable. El idioma no localizado es el utilizado al desarrollar el formulario adaptable. No se tendrá en cuenta la configuración local de su explorador (explorador local) y se proporcionará una versión no localizada del formulario adaptable.
   * Cuando se usa el formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`, y la opción **[!UICONTROL Usar configuración regional del explorador]** está activada en el Administrador de configuración, se proporciona una versión localizada del formulario adaptable, si está disponible. El idioma del formulario adaptable localizado se basará en la configuración local del explorador (explorador local). Puede llevar a [almacenar en caché solo la primera instancia de un formulario adaptable]. Para evitar que este problema se produzca en la instancia, consulte [Solución de problemas](#only-first-insatnce-of-adptive-forms-is-cached).

### Habilitación del almacenamiento en caché en Dispatcher

Siga los pasos que se indican a continuación para poder habilitar y configurar el almacenamiento en caché de los formularios adaptables en Dispatcher:

1. Abra la siguiente URL en cada una de las instancias de publicación de su entorno y configure el agente de replicación:
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Agregue lo siguiente al archivo dispatcher.any](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#automatically-invalidating-cached-files):

   ```JSON
      /invalidate
      {
      /0000
      {
      /glob "*"
      /type "deny"
      }
      /0001
      {
      # Consider all HTML files stale after an activation.
      /glob "*.html"
      /type "allow"
      }
      /0002
      {
      # Exclude htmls present in AF directories
      /glob "/content/forms/**/*.html"
      /type "deny"
      }
   ```

   Cuando haya agregado lo anterior:

   * El formulario adaptable permanecerá en la caché hasta que no se publique una versión actualizada.

   * Cuando se publica una versión más reciente de un recurso al que se hace referencia en un formulario adaptable, el formulario adaptable afectado se invalida automáticamente. Existen algunas excepciones a la hora de invalidar automáticamente los recursos a los que se hace referencia. Para obtener más información sobre las excepciones, consulte la [solución de problemas](#troubleshooting) sección.
1. [Añada las siguientes reglas: dispatcher.any o un archivo de reglas personalizadas](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#specifying-the-documents-to-cache). Esto excluirá las URL que no admitan el almacenamiento en caché; por ejemplo, comunicaciones interactivas.

   ```JSON
      /0000 {
            /glob "*"
            /type "allow"
      }
      ## Don't cache csrf login tokens
      /0001 {
            /glob "/libs/granite/csrf/token.json"
            /type "deny"
      }
      ## Don't cache IC - print channel
      /0002 {
            /glob "/content/forms/**/channels/print.html"
            /type "deny"
      }
      ## Don't cache IC - web channel
      /0003 {
            /glob "/content/forms/**/channels/web.html"
            /type "deny"
      }
   ```

1. [Añada los siguientes parámetros a la lista de los parámetros de URL ignorados](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=es#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

El entorno de AEM está configurado para almacenar en caché los formularios adaptables. Almacena en caché todo tipo de formularios adaptables. Si tiene que comprobar los permisos de acceso de los usuarios de una página antes de enviar la página almacenada en la caché, consulte [contenido protegido almacenado en caché](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html?lang=es).

## Solución de problemas {#troubleshooting}

### Algunos Forms adaptables que contienen imágenes o vídeos no se invalidan automáticamente en la caché de Dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema {#issue1}

Cuando selecciona y agrega imágenes o vídeos a un formulario adaptable mediante el explorador de recursos y se editan en el editor de recursos, estos recursos no se invalidan automáticamente en la caché de Dispatcher.

#### Solución {#Solution1}

Después de publicar las imágenes y el vídeo, cancele la publicación y publique de forma explícita el formulario adaptable que hace referencia a estos recursos.

### Algunos formularios adaptables que contienen fragmentos de contenido o fragmentos de experiencias no se invalidan automáticamente en la caché de Dispatcher {#content-or-experience-fragment-not-auto-invalidated}

#### Problema {#issue2}

Cuando se agrega un fragmento de contenido o de experiencia a un formulario adaptable y estos recursos se editan y publican de forma independiente, el Forms adaptable que los contiene no se invalida automáticamente de la caché de Dispatcher.

#### Solución {#Solution2}

Después de publicar un fragmento de contenido o un fragmento de experiencia actualizado, cancele la publicación del Forms adaptable que utiliza estos recursos y vuelva a publicarlo explícitamente.

### Solo se almacena en caché la primera instancia de un formulario adaptable{#only-first-insatnce-of-adptive-forms-is-cached}

#### Problema {#issue3}

Cuando la URL del formulario adaptable no contiene información de localización, y **[!UICONTROL Usar configuración regional del explorador]** en el administrador de configuración está habilitado. Se proporciona una versión localizada del formulario adaptable y solo se almacena en caché y se entrega a todos los usuarios subsiguientes la primera instancia.

#### Solución {#Solution3}

1. Abra conf.d/httpd-dispatcher.conf o cualquier otro archivo de configuración configurado para cargarse durante la ejecución.

1. Agregue el siguiente código al archivo y guárdelo. Es un código de ejemplo, puede modificarlo para adaptarlo a su entorno.

```XML
   <VirtualHost *:80>
        # Set log level high during development / debugging and then turn it down to whatever is appropriate
    LogLevel rewrite:trace6
        # Start Rewrite Engine
    RewriteEngine On
        # Handle actual URL convention (just pass through)
        RewriteRule "^/content/forms/af/(.*)[.](.*).html$" "/content/forms/af/$1.$2.html" [PT]
 
        # Handle selector based redirection basded on browser language
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two characters which most likely is the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
