---
title: Configuración de la caché de Forms adaptable
seo-title: Configure Adaptive Forms cache
description: La caché de Forms adaptable está diseñada específicamente para Forms adaptable y documentos. Almacena en caché Forms adaptable y documentos adaptables con el objetivo de reducir el tiempo necesario para procesar un formulario adaptable o un documento en el cliente.
seo-description: The Adaptive Forms cache is designed specifically for Adaptive Forms and documents. It caches Adaptive Forms and adaptive documents with the objective of reducing the time required to render an Adaptive Form or document on the client.
uuid: ba8f79fd-d8dc-4863-bc0d-7c642c45505c
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 9fa6f761-58ca-4cd0-8992-b9337dc1a279
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 1%

---


# Configuración de la caché de Forms adaptable {#configure-adaptive-forms-cache}

Una caché es un mecanismo para acortar los tiempos de acceso a los datos, reducir la latencia y mejorar las velocidades de entrada y salida (E/S). La caché de Forms adaptable almacena únicamente el contenido de HTML y la estructura JSON de un formulario adaptable sin guardar datos precargados. Ayuda a reducir el tiempo necesario para procesar un formulario adaptable en el cliente. Está diseñado específicamente para Forms adaptable.

## Configuración de la caché de Forms adaptable en instancias de autor y publicación {#configure-adaptive-forms-caching-at-author-and-publish-instances}

1. Vaya a AEM administrador de configuración de la consola web en `https://[server]:[port]/system/console/configMgr`.
1. Haga clic en **[!UICONTROL Configuración del canal web de comunicaciones interactivas y formularios adaptables]** para editar sus valores de configuración.
1. En el [!UICONTROL editar valores de configuración] , especifique el número máximo de formularios o documentos en una instancia del AEM [!DNL Forms] el servidor puede almacenar en caché en la **[!UICONTROL Número de Forms adaptable]** campo . El valor predeterminado es 100.

   >[!NOTE]
   >
   >Para desactivar la caché, establezca el valor en el campo Número de Forms adaptable en **0**. La caché se restablece y todos los formularios y documentos se eliminan de la caché cuando se desactiva o cambia la configuración de la caché.

   ![Cuadro de diálogo de configuración para la caché del HTML de Forms adaptable](assets/cache-configuration-edit.png)

1. Haga clic en **[!UICONTROL Guardar]** para guardar la configuración.

Su entorno está configurado para utilizar la caché Forms adaptable y los recursos relacionados.


## (Opcional) Configurar la caché del formulario adaptable en Dispatcher {#configure-the-cache}

También puede configurar el almacenamiento en caché del formulario adaptable en Dispatcher para mejorar el rendimiento.

### Requisitos previos {#pre-requisites}

* Active la variable [combinación o establecimiento de prefijos de datos en el cliente](prepopulate-adaptive-form-fields.md#prefill-at-client) . Ayuda a combinar datos únicos para cada instancia de un formulario prerellenado.
* [Habilitar el agente de vaciado para cada instancia de publicación](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/page-invalidate.html?lang=en#invalidating-dispatcher-cache-from-a-publishing-instance). Ayuda a obtener un mejor rendimiento de almacenamiento en caché para Forms adaptable. La dirección URL predeterminada de los agentes de vaciado es `http://[server]:[port]]/etc/replication/agents.publish/flush.html`.

### Consideraciones para almacenar en caché Forms adaptable en un despachante {#considerations}

* Cuando utilice la caché de Forms adaptable, utilice el AEM [!DNL Dispatcher] para almacenar en caché las bibliotecas de cliente (CSS y JavaScript) de un formulario adaptable.
* Durante el desarrollo de componentes personalizados, en el servidor utilizado para el desarrollo, mantenga deshabilitada la caché de Forms adaptable.
* Las direcciones URL sin extensión no se almacenan en caché. Por ejemplo, la dirección URL con patrón`/content/forms/[folder-structure]/[form-name].html` se almacenan en caché y el almacenamiento en caché ignora las direcciones URL con patrón `/content/dam/formsanddocument/[folder-name]/<form-name>/jcr:content`. Por lo tanto, utilice direcciones URL con extensiones para aprovechar las ventajas del almacenamiento en caché.
* Consideraciones para Forms adaptable localizado:
   * Usar formato de URL `http://host:port/content/forms/af/<afName>.<locale>.html` para solicitar una versión localizada de un formulario adaptable en lugar de `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`
   * Deshabilitar mediante la configuración regional del explorador <!-- [Disable using browser locale](supporting-new-language-localization.md#how-localization-of-adaptive-form-works) -->para direcciones URL con formato `http://host:port/content/forms/af/<adaptivefName>.html`.
   * Cuando se usa el formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`y **[!UICONTROL Usar configuración regional del explorador]** en configuration manager está desactivado, se proporciona la versión no localizada del formulario adaptable. El idioma no localizado es el idioma utilizado al desarrollar el formulario adaptable. No se tiene en cuenta la configuración regional configurada para el explorador (configuración regional del explorador) y se proporciona una versión no localizada del formulario adaptable.
   * Cuando se usa el formato de URL `http://host:port/content/forms/af/<adaptivefName>.html`y **[!UICONTROL Usar configuración regional del explorador]** en configuration manager está habilitado, se proporciona una versión localizada del formulario adaptable, si está disponible. El idioma del formulario adaptable localizado se basa en la configuración regional configurada para el explorador (configuración regional del explorador). Puede llevar a [almacenamiento en caché solo de la primera instancia de un formulario adaptable]. Para evitar que el problema se produzca en la instancia, consulte [solución de problemas](#only-first-insatnce-of-adptive-forms-is-cached).

### Habilitar el almacenamiento en caché en Dispatcher

Siga los pasos que se indican a continuación para habilitar y configurar el almacenamiento en caché de Forms adaptable en Dispatcher:

1. Abra la siguiente URL para cada instancia de publicación de su entorno y configure el agente de replicación:
   `http://[server]:[port]]/etc/replication/agents.publish/flush.html`

1. [Agregue lo siguiente a su archivo dispatcher.any](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#automatically-invalidating-cached-files):

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

   Cuando agregue lo anterior:

   * Un formulario adaptable permanece en la caché hasta que no se publique una versión actualizada del formulario.

   * Cuando se publica una versión más reciente del recurso al que se hace referencia en un formulario adaptable, el Forms adaptable afectado se invalida automáticamente. Existen algunas excepciones a la invalidación automática de los recursos a los que se hace referencia. Para obtener información sobre las excepciones, consulte [solución de problemas](#troubleshooting) para obtener más información.
1. [Añadir las siguientes reglas: dispatcher.any o archivo de reglas personalizadas](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#specifying-the-documents-to-cache). Excluye las direcciones URL que no admiten el almacenamiento en caché. Por ejemplo, Comunicación interactiva.

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

1. [Añada los siguientes parámetros a la lista de parámetros de URL ignorados](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=en#ignoring-url-parameters):

   ```JSON
      /ignoreUrlParams {
      /0001 { /glob "*" /type "deny" }
      # added for AEM forms specific use cases.
      /0003 { /glob "dataRef" /type "allow" }
      }
   ```

El entorno de AEM está configurado para almacenar en caché Forms adaptable. Almacena en caché todo tipo de Forms adaptable. Si tiene que comprobar los permisos de acceso de los usuarios para una página antes de enviar la página en caché, consulte [almacenamiento en caché de contenido seguro](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/permissions-cache.html).

## Solución de problemas {#troubleshooting}

### Algunas imágenes o vídeos de Forms adaptable que contienen no se invalidan automáticamente de la caché de Dispatcher {#videos-or-images-not-auto-invalidated}

#### Problema   {#issue1}

Al seleccionar y agregar imágenes o vídeos a través del navegador de recursos a un formulario adaptable y estas imágenes y vídeos se editan en el editor de Assets, el Forms adaptable que las contiene no se invalida automáticamente desde la caché del distribuidor.

#### Solución {#Solution1}

Después de publicar las imágenes y el vídeo, cancele la publicación de forma explícita y publique el Forms adaptable que hace referencia a estos recursos.

### Algunos fragmentos de contenido o experiencia de Forms adaptable que contienen fragmentos de contenido no se invalidan automáticamente desde la caché de Dispatcher {#content-or-experience-fragment-not-auto-invalidated}

#### Problema   {#issue2}

Cuando se agrega un fragmento de contenido o de experiencia a un formulario adaptable y estos recursos se editan y publican de forma independiente, Forms adaptable que los contiene no se invalida automáticamente de la caché del despachante.

#### Solución {#Solution2}

Después de publicar fragmento de contenido o fragmento de experiencia actualizado, cancele la publicación de Forms adaptable que utilice estos recursos de forma explícita.

### Solo se almacena en caché la primera instancia de un formulario adaptable{#only-first-insatnce-of-adptive-forms-is-cached}

#### Problema   {#issue3}

Cuando la URL del formulario adaptable no tiene información de localización, y **[!UICONTROL Usar configuración regional del explorador]** en configuration manager está habilitado, se proporciona una versión localizada del formulario adaptable y solo la primera instancia del formulario adaptable se almacena en caché y se entrega a todos los usuarios subsiguientes.

#### Solución {#Solution3}

Siga estos pasos para resolver el problema:

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
        # The Rewrite Cond(ition) is looking for the Accept-Lanague header and if found takes the first two character which most likely will be the desired language selector.
        RewriteCond %{HTTP:Accept-Language} ^(..).*$ [NC]
        RewriteRule "^/content/forms/af/(.*).html$" "/content/forms/af/$1.%1.html" [R]
   </VirtualHost>
```
