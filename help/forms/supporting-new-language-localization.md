---
title: Compatibilidad con configuraciones regionales nuevas para la localización de formularios adaptables
seo-title: Supporting new locales for adaptive forms localization
description: AEM Forms le permite agregar nuevas configuraciones regionales para localizar formularios adaptables. Español (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués-brasileño (pt-BR), chino (zh-CN), chino-taiwanés (zh-TW) y coreano (ko-KR).
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. We support 10 locales out of the box curently, as  "en","fr","de","ja","pt-br","zh-cn","zh-tw","ko-kr","it","es".
source-git-commit: eb722054f6a51320a7772bf666f656418f8392cd
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 32%

---

# Compatibilidad con nuevas configuraciones regionales para la localización de formularios adaptables{#supporting-new-locales-for-adaptive-forms-localization}

## Acerca de los diccionarios de configuración regional {#about-locale-dictionaries}

La localización de formularios adaptables se basa en dos tipos de diccionarios de configuración regional:

* **El diccionario específico del formulario**: contiene cadenas utilizadas en formularios adaptables. Por ejemplo, etiquetas, nombres de campo, mensajes de error, descripciones de ayuda, etc. Se administra como un conjunto de archivos XLIFF para cada configuración regional y puede acceder a él en `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **Los diccionarios globales**: hay dos diccionarios globales, administrados como objetos JSON en la biblioteca de cliente de AEM. Estos diccionarios contienen mensajes de error predeterminados, nombres de mes, símbolos de moneda, patrones de fecha y hora, etc. Puede encontrar estos diccionarios en `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. Estas ubicaciones contienen carpetas independientes para cada configuración regional. Debido a que los diccionarios globales no se actualizan con frecuencia, mantener archivos JavaScript separados para cada configuración regional permite a los navegadores almacenarlos en caché y reducir el uso del ancho de banda de red al acceder a diferentes formularios adaptables en el mismo servidor.

Pasos para admitir la nueva localización para AEM Forms:

1. [Agregar compatibilidad con la localización para configuraciones regionales no admitidas](#add-localization-support-for-non-supported-locales-add-localization-support-for-non-supported-locales)
1. [Uso de configuraciones regionales añadidas en Forms adaptable](#use-added-locale-in-adaptive-forms-use-added-locale-in-af)

## Agregar compatibilidad con la localización para configuraciones regionales no admitidas {#add-localization-support-for-non-supported-locales}

AEM Forms admite actualmente la localización de contenido de Adaptive Forms en las configuraciones regionales de inglés (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués-brasileño (pt-BR), chino (zh-CN), chino-taiwanés (zh-TW) y coreano (ko-KR).

Para añadir compatibilidad con una nueva configuración regional en el tiempo de ejecución de un formulario adaptable:

1. [Clonar el repositorio](#1-clone-the-repository-clone-the-repository)
1. [Añada una configuración regional al servicio GuideLocalizationService.](#1-add-a-locale-to-the-guide-localization-service-add-a-locale-to-the-guide-localization-service-br)
1. [Agregar carpeta específica de nombre de configuración regional](#3-add-locale-name-specific-folder-add-locale-name-specific-folder)
3.1 [Agregar una biblioteca de cliente XFA para una configuración regional](#3-add-xfa-client-library-for-a-locale)
3,2 [Agregar la biblioteca de cliente de formulario adaptable para una configuración regional](#4-add-adaptive-form-client-library-for-a-locale-add-adaptive-form-client-library-for-a-locale-br)
1. [Agregar la compatibilidad con la configuración regional del diccionario.](#5-add-locale-support-for-the-dictionary-add-locale-support-for-the-dictionary-br)
1. [Confirmar los cambios en el repositorio e implementar la canalización](#7-commit-the-changes-in-the-repository-and-deploy-the-pipeline-commit-changes-in-repo-deploy-pipeline)

### 1. Clonar el repositorio {#clone-the-repository}

1. Desde la línea de comandos, vaya a donde desee clonar el repositorio de Cloud Service de Forms.
1. Ejecute el comando que [recuperado de Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) Es similar a `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. Utilice el nombre de usuario y la contraseña de Git para clonar el repositorio.
1. Abra la carpeta del repositorio del Cloud Service de Forms clonada en su editor preferido.

### 2. Añadir una configuración regional al servicio de localización de guías {#add-a-locale-to-the-guide-localization-service-br}

1. Busque la variable `Guide Localization Service.cfg.json` y añada la configuración regional que desee agregar a la lista de configuraciones regionales admitidas.

   >[!NOTE]
   >
   >* Cree un archivo con el nombre como `Guide Localization Service.cfg.json` si todavía no está presente.


### 3. Agregar una biblioteca de cliente de carpeta específica de nombre de configuración regional {#add-locale-name-specific-folder}

1. En la carpeta UI.content , cree `etc/clientlibs` carpeta.
1. Cree una carpeta llamada como `locale-name` under `etc/clientlibs` para que sirva como contenedor para clientlibs xfa y af.

#### 3.1 Agregar la biblioteca de cliente XFA para una configuración regional en la carpeta locale-name

1. Cree un nodo denominado como `[locale-name]_xfa` y escriba como `cq:ClientLibraryFolder` under `etc/clientlibs/locale_name`, con categoría `xfaforms.I18N.<locale>`y agregue los siguientes archivos:
* **I18N.js** definiendo `xfalib.locale.Strings` para `<locale>`, tal como se define en `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt**, que contiene lo siguiente:
   */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

#### 3.2. Agregar la biblioteca de cliente de formulario adaptable para una carpeta locale-name {#add-adaptive-form-client-library-for-a-locale-br}

1. Cree un nodo denominado como `[locale-name]_af` y escriba como `cq:ClientLibraryFolder` under `etc/clientlibs/locale_name`, con categoría como `guides.I18N.<locale>` y dependencias como `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` y `guide.common`.
1. Cree una carpeta denominada como `javascript` y agregue los siguientes archivos:

   * **i18n.js**, definiendo `guidelib.i18n` con los patrones de “calendarSymbols” `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols` y `typefaces` para `<locale>` según las especificaciones XFA descritas en [Especificación de la configuración regional](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **LogMessages.js**, definiendo `guidelib.i18n.strings` y `guidelib.i18n.LogMessages` para `<locale>` tal como se define en `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. Agregar **js.txt** que contiene lo siguiente:

   ```text
     i18n.js
       LogMessages.js
   ```

### 4. Agregar compatibilidad con configuración regional para el diccionario {#add-locale-support-for-the-dictionary-br}

Realice este paso solo si la configuración regional `<locale>` que está agregando que no está entre `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja` y `ko-kr`.

1. Crear una carpeta `languages` under `etc`, si no está presente.

1. Agregue una propiedad de cadena de varios valores `languages` al nodo, si no está presente ya.
1. Agregue los valores de configuración regional predeterminados `<locale-name>` `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja` y `ko-kr`, si no están presentes.

1. Agregue `<locale>` a los valores de la propiedad `languages` de `/etc/languages`.


```text
Add the newly created folders in the `filter.xml` under etc/META-INF/[folder hierarchy] as:
<filter root="/etc/clientlibs/[locale-name]"/>
<filter root="/etc/languages"/>
```

Antes de confirmar los cambios en el repositorio de AEM Git, debe acceder a su [Información del repositorio de Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

### 5. Confirme los cambios en el repositorio e implemente la canalización {#commit-chnages-in-repo-deploy-pipeline}

Confirme los cambios en el repositorio GIT después de agregar una nueva compatibilidad con configuración regional. Implemente el código mediante la canalización de pila completa. Más información [configuración de una canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) para agregar compatibilidad con configuración regional nueva.

Una vez finalizada la canalización, la configuración regional recién añadida aparece en el entorno de AEM.

### Usar configuración regional añadida en Forms adaptable {#use-added-locale-in-af}

Pasos para utilizar y procesar un formulario adaptable con una configuración regional recién añadida:

1. Inicie sesión en la instancia de autor de AEM.
1. Vaya a **Forms** >  **Forms y documentos**.
1. Seleccione un formulario adaptable y haga clic en **Agregar diccionario** y **Agregar diccionario a proyecto de traducción** aparecerá el asistente.
1. Especifique la variable **Título del proyecto** y seleccione **Idiomas de destino** en el menú desplegable del **Agregar diccionario a proyecto de traducción** asistente.
1. Haga clic en **Listo** y ejecutar el proyecto de traducción creado.
1. Seleccione un formulario adaptable y haga clic en **Vista previa como HTML**.
1. Agregar `&afAcceptLang=<locale-name>` en la URL de un formulario adaptable.
1. Actualice la página y el formulario adaptable se procesará en una configuración regional especificada.

Existen dos métodos para identificar la configuración regional de un formulario adaptable. Cuando se procesa un formulario adaptable, este identifica la configuración regional solicitada de las siguientes formas:

* Al consultar el selector `[local]` de la URL del formulario adaptable. El formato de la URL es el siguiente `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. El uso del selector `[local]` permite almacenar en caché un formulario adaptable.

* observando los siguientes parámetros en el orden especificado:

   * El parámetro de solicitud `afAcceptLang`. Para anular la configuración regional del explorador de los usuarios, puede pasar el parámetro de solicitud 
`afAcceptLang` para forzar la configuración regional. Por ejemplo, la siguiente URL obliga a procesar el formulario en la configuración regional canadiense-francesa:
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * La configuración regional del explorador establecida para el usuario, que se especifica en la solicitud utilizando el encabezado `Accept-Language`.

Si no existe una biblioteca de cliente para la configuración regional solicitada, se busca una biblioteca de cliente para el código de idioma presente en la configuración regional. Por ejemplo, si la configuración regional solicitada es `en_ZA` (inglés sudafricano) y la biblioteca de clientes de `en_ZA` no existe, el formulario adaptable utiliza la biblioteca cliente para `en` (Inglés), si existe. Sin embargo, si no existe ninguna biblioteca, el formulario adaptable utiliza el diccionario de la configuración regional `en`.


Una vez identificada la configuración regional, el formulario adaptable selecciona el diccionario específico del formulario. Si no se encuentra el diccionario específico del formulario para la configuración regional solicitada, utiliza el diccionario para el idioma en el que se crea el formulario adaptable.

Si no hay información de configuración regional, el formulario adaptable se entrega en el idioma original del formulario. El idioma original es el idioma utilizado al desarrollar el formulario adaptable.

Get [biblioteca de cliente de ejemplo](/help/forms/assets/locale-support-sample.zip) para añadir compatibilidad con la nueva configuración regional. Debe cambiar el contenido de la carpeta en la configuración regional requerida.

### Prácticas recomendadas para admitir la nueva localización {#best-practices}

* Adobe recomienda crear un proyecto de traducción después de crear un formulario adaptable.

* Cuando se añaden campos nuevos en un formulario adaptable existente:
   * **Para traducción automática**: Vuelva a crear el diccionario y ejecute el proyecto de traducción. Los campos agregados a un formulario adaptable después de crear un proyecto de traducción siguen sin traducirse.
   * **Para traducción humana**: Exporte el diccionario a través de `[server:port]/libs/cq/i18n/gui/translator.html`. Actualice el diccionario para los campos recién añadidos y cárguelo.
