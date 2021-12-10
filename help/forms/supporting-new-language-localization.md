---
title: Compatibilidad con nuevas configuraciones regionales para la localización de Forms adaptable
seo-title: Supporting new locales for Adaptive Forms localization
description: AEM Forms le permite añadir nuevas configuraciones regionales para localizar Forms adaptable. Las configuraciones regionales compatibles de forma predeterminada son inglés, francés, alemán y japonés.
seo-description: AEM Forms allows you to add new locales for localizing Adaptive Forms. The supported locales by default are English, French, German, and Japanese.
uuid: 7f9fab6b-8d93-46bb-8c7c-7b723d5159ea
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: d4e2acb0-8d53-4749-9d84-15b8136e610b
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# Compatibilidad con nuevas configuraciones regionales para la localización de Forms adaptable{#supporting-new-locales-for-adaptive-forms-localization}

## Acerca de los diccionarios de configuración regional {#about-locale-dictionaries}

La localización de Forms adaptable se basa en dos tipos de diccionarios de configuración regional:

**Diccionario específico del formulario** Contiene cadenas utilizadas en Forms adaptable. Por ejemplo, etiquetas, nombres de campos, mensajes de error, descripciones de ayuda, etc. Se administra como un conjunto de archivos XLIFF para cada configuración regional y puede acceder a él en `https://<host>:<port>/libs/cq/i18n/translator.html`.

**Diccionarios globales** Hay dos diccionarios globales, administrados como objetos JSON, en AEM biblioteca de cliente. Estos diccionarios contienen mensajes de error predeterminados, nombres de mes, símbolos de moneda, patrones de fecha y hora, etc. Puede encontrar estos diccionarios en CRXDe Lite en /libs/fd/xfaforms/clientlibs/I18N. Estas ubicaciones contienen carpetas independientes para cada configuración regional. Debido a que los diccionarios globales generalmente no se actualizan con frecuencia, mantener archivos JavaScript separados para cada configuración regional permite a los navegadores almacenarlos en caché y reducir el uso del ancho de banda de red al acceder a diferentes Forms adaptables en el mismo servidor.

### Funcionamiento de la localización del formulario adaptable {#how-localization-of-adaptive-form-works}

Existen dos métodos para identificar la configuración regional del formulario adaptable. Cuando se procesa un formulario adaptable, identifica la configuración regional solicitada por :

* consulte `[local]` en la URL del formulario adaptable. El formato de la dirección URL es `http://host:port/content/forms/af/[afName].[locale].html?wcmmode=disabled`. Uso `[local]` permite almacenar en caché un formulario adaptable.

* observe los siguientes parámetros en el orden especificado:

   * Parámetro de solicitud `afAcceptLang`
Para anular la configuración regional del explorador de los usuarios, puede pasar la variable 
`afAcceptLang` para forzar la configuración regional. Por ejemplo, la siguiente dirección URL obligará a procesar el formulario en la configuración regional de japonés:
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

   * La configuración regional del explorador establecida para el usuario, que se especifica en la solicitud utilizando la variable `Accept-Language` encabezado.

   * Configuración de idioma del usuario especificado en AEM.

   * La configuración regional del explorador está habilitada de forma predeterminada. Para cambiar la configuración regional del navegador,
      * Abra el administrador de configuración. La dirección URL es `http://[server]:[port]/system/console/configMgr`
      * Busque y abra el **[!UICONTROL Formulario adaptable y canal web de comunicación interactiva]** configuración.
      * Cambiar el estado de la variable **[!UICONTROL Usar configuración regional del explorador]** y  **[!UICONTROL Guardar]** la configuración.

Una vez identificada la configuración regional, el Forms adaptable selecciona el diccionario específico del formulario. Si no se encuentra el diccionario específico del formulario para la configuración regional solicitada, utiliza el diccionario para el idioma en el que se creó el formulario adaptable.

Si no hay información de configuración regional, el formulario adaptable se entrega en el idioma original del formulario. El idioma original es el idioma utilizado al desarrollar el formulario adaptable.

Si no existe una biblioteca de cliente para la configuración regional solicitada, se busca una biblioteca de cliente para el código de idioma presente en la configuración regional. Por ejemplo, si la configuración regional solicitada es `en_ZA` (inglés sudafricano) y la biblioteca de clientes de `en_ZA` no existe, el formulario adaptable utilizará la biblioteca cliente para `en` (Inglés), si existe. Sin embargo, si no existe ninguno, el formulario adaptable utiliza el diccionario para `en` configuración regional.

## Agregar compatibilidad con la localización para configuraciones regionales no admitidas {#add-localization-support-for-non-supported-locales}

[!DNL AEM Forms] actualmente admite la localización de contenido de Forms adaptable en las configuraciones regionales de inglés (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués-brasileño (pt-BR), chino (zh-CN), chino-taiwanés (zh-TW) y coreano (ko-KR).

Para añadir compatibilidad con una nueva configuración regional en el tiempo de ejecución de Adaptive Forms:

1. [Añadir una configuración regional al servicio GuideLocalizationService](supporting-new-language-localization.md#p-add-a-locale-to-the-guide-localization-service-br-p)

1. [Agregar una biblioteca de cliente XFA para una configuración regional](supporting-new-language-localization.md#p-add-xfa-client-library-for-a-locale-br-p)

1. [Agregar la biblioteca de cliente de formulario adaptable para una configuración regional](supporting-new-language-localization.md#p-add-adaptive-form-client-library-for-a-locale-br-p)
1. [Agregar compatibilidad con la configuración regional para el diccionario](supporting-new-language-localization.md#p-add-locale-support-for-the-dictionary-br-p)
1. [Reinicio del servidor](supporting-new-language-localization.md#p-restart-the-server-p)

### Añadir una configuración regional al servicio de localización de guías {#add-a-locale-to-the-guide-localization-service-br}

1. Ir a `https://'[server]:[port]'/system/console/configMgr`.
1. Haga clic en para editar el **Servicio de localización de guías** componente.
1. Agregue la configuración regional que desee agregar a la lista de configuraciones regionales admitidas.

![GuideLocalizationService](assets/configservice.png)

### Agregar una biblioteca de cliente XFA para una configuración regional {#add-xfa-client-library-for-a-locale-br}

Crear un nodo de tipo `cq:ClientLibraryFolder` under `etc/<folderHierarchy>`, con categoría `xfaforms.I18N.<locale>`y agregue los siguientes archivos a la biblioteca de cliente:

* **I18N.js** definir `xfalib.locale.Strings` para el `<locale>` tal como se define en `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.

* **js.txt** que contiene lo siguiente:

```text
/libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js
```

### Agregar la biblioteca de cliente de formulario adaptable para una configuración regional {#add-adaptive-form-client-library-for-a-locale-br}

Crear un nodo de tipo `cq:ClientLibraryFolder` under `etc/<folderHierarchy>`, con categoría como `guides.I18N.<locale>` y dependencias como `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` y `guide.common`. &quot;

Agregue los siguientes archivos a la biblioteca de cliente:

* **i18n.js** definir `guidelib.i18n`, con patrones de &quot;calendarSymbols&quot;, `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols`, `typefaces` para el `<locale>` según las especificaciones XFA descritas en [Especificación de configuración regional](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf). También puede ver cómo se define para otras configuraciones regionales compatibles en `/etc/clientlibs/fd/af/I18N/fr/javascript/i18n.js`.
* **LogMessages.js** definir `guidelib.i18n.strings` y `guidelib.i18n.LogMessages` para el `<locale>` tal como se define en `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.
* **js.txt** que contiene lo siguiente:

```text
i18n.js
LogMessages.js
```

### Agregar compatibilidad con la configuración regional para el diccionario {#add-locale-support-for-the-dictionary-br}

Realice este paso solo si la variable `<locale>` está agregando que no está entre `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`.

1. Cree un `nt:unstructured` node `languages` under `etc`, si no está presente.

1. Agregar una propiedad de cadena de varios valores `languages` al nodo , si no está presente ya.
1. Agregue la variable `<locale>` valores de configuración regional predeterminados `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja`, `ko-kr`, si no está presente.

1. Agregue la variable `<locale>` a los valores de la variable `languages` propiedad de `/etc/languages`.

La variable `<locale>` aparecerá en `https://'[server]:[port]'/libs/cq/i18n/translator.html`.

### Reinicio del servidor {#restart-the-server}

Reinicie el servidor de AEM para que la configuración regional añadida entre en vigor.

## Bibliotecas de muestra para agregar compatibilidad con el español {#sample-libraries-for-adding-support-for-spanish}

Bibliotecas de cliente de muestra para agregar compatibilidad con el español

[Obtener archivo](assets/sample.zip)
