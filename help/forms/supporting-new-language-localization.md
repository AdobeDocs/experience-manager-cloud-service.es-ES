---
title: Agregar la compatibilidad con nuevas configuraciones regionales a un formulario adaptable
seo-title: Learn to add support for new locales to your adaptive forms
description: AEM Forms le permite agregar configuraciones regionales nuevas para localizar formularios adaptables. Configuraciones regionales en inglés (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués brasileño (pt-BR), chino (zh-CN), chino taiwanés (zh-TW) y coreano (ko-KR).
seo-description: AEM Forms allows you to add new locales for localizing adaptive forms. We support 10 locales out of the box curently, as  "en","fr","de","ja","pt-br","zh-cn","zh-tw","ko-kr","it","es".
source-git-commit: 659484f80d1f31794512af5e4d190b04a9f3e4e8
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 28%

---

# Compatibilidad con nuevas configuraciones regionales para la localización de formularios adaptables {#supporting-new-locales-for-adaptive-forms-localization}

AEM Forms es compatible de serie con las configuraciones regionales de inglés (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués brasileño (pt-BR), chino (zh-CN), chino taiwanés (zh-TW) y coreano (ko-KR). También puede agregar compatibilidad con más configuraciones regionales, como Hindi(hi_IN).

## Explicación de los diccionarios de configuración regional {#about-locale-dictionaries}

La localización de formularios adaptables se basa en dos tipos de diccionarios de configuración regional:

* **El diccionario específico del formulario**: contiene cadenas utilizadas en formularios adaptables. Por ejemplo, etiquetas, nombres de campo, mensajes de error, descripciones de ayuda, etc. Se administra como un conjunto de archivos XLIFF para cada configuración regional y puede acceder a él en `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **Los diccionarios globales**: hay dos diccionarios globales, administrados como objetos JSON en la biblioteca de cliente de AEM. Estos diccionarios contienen mensajes de error predeterminados, nombres de mes, símbolos de moneda, patrones de fecha y hora, etc. Puede encontrar estos diccionarios en `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. Estas ubicaciones contienen carpetas independientes para cada configuración regional. Dado que los diccionarios globales no se actualizan con frecuencia, utilizar archivos JavaScript independientes para cada configuración regional permite a los exploradores almacenarlos en caché y reducir el uso del ancho de banda de red al acceder a diferentes formularios adaptables en el mismo servidor.

## Agregar compatibilidad con nuevas configuraciones regionales {#add-support-for-new-locales}

Siga estos dos pasos para agregar compatibilidad con una nueva configuración regional:

1. [Agregar compatibilidad con la localización para configuraciones regionales no admitidas](#add-localization-support-for-non-supported-locales-add-localization-support-for-non-supported-locales)
1. [Usar configuraciones regionales agregadas en Forms adaptable](#use-added-locale-in-adaptive-forms-use-added-locale-in-af)

### Agregar compatibilidad con la localización para configuraciones regionales no admitidas {#add-localization-support-for-non-supported-locales}

AEM Forms admite actualmente la localización del contenido de Forms adaptable en las configuraciones regionales de Inglés (en), Español (es), Francés (fr), Italiano (it), Alemán (de), Japonés (ja), Portugués brasileño (pt-BR), Chino (zh-CN), Chino taiwanés (zh-TW) y Coreano (ko-KR).

Para añadir compatibilidad con una nueva configuración regional en el tiempo de ejecución de un formulario adaptable:

1. [Clone su repositorio](#1-clone-the-repository-clone-the-repository)
1. [Añada una configuración regional al servicio GuideLocalizationService.](#2-add-a-locale-to-the-guide-localization-service-add-a-locale-to-the-guide-localization-service-br)
1. [Agregar carpeta específica con nombre de configuración regional](#3-add-locale-name-specific-folder-client-library-add-locale-name-specific-folder)
1. [Agregar la compatibilidad con la configuración regional del diccionario.](#about-locale-dictionaries-about-locale-dictionaries)
1. [Confirme los cambios en el repositorio e implemente la canalización](#5-commit-the-changes-in-the-repository-and-deploy-the-pipeline-commit-chnages-in-repo-deploy-pipeline)

#### 1. Clone el repositorio {#clone-the-repository}

1. Desde la línea de comandos, vaya a donde desee clonar el repositorio del Cloud Service de Forms.
1. Ejecute el comando que ha [recuperado de Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html#accessing-git) Es similar a `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. Utilice el nombre de usuario y la contraseña de Git para clonar el repositorio.
1. Abra la carpeta clonada del repositorio del Cloud Service de Forms en su editor preferido.

#### 2. Añada una configuración regional al servicio de localización de guías {#add-a-locale-to-the-guide-localization-service-br}

1. Busque el `Guide Localization Service.cfg.json` y añada la configuración regional que desee añadir a la lista de configuraciones regionales admitidas.

   >[!NOTE]
   >
   >* Cree un archivo con el nombre `Guide Localization Service.cfg.json` archivo, si no está presente.


#### 3. Agregar una biblioteca de cliente de carpetas específica con nombre de configuración regional {#add-locale-name-specific-folder}

1. En la carpeta UI.content, cree `etc/clientlibs` carpeta.
1. Cree además una carpeta denominada como `locale-name` bajo `etc/clientlibs` para servir como contenedor para clientlibs xfa y af.

##### 3.1 Agregar la biblioteca de cliente XFA para una configuración regional en la carpeta locale-name

Cree un nodo con el nombre `[locale-name]_xfa` y escriba como `cq:ClientLibraryFolder` bajo `etc/clientlibs/locale_name`, con categoría `xfaforms.I18N.<locale>`y agregue los siguientes archivos:

* **I18N.js** definiendo `xfalib.locale.Strings` para `<locale>`, tal como se define en `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt**, que contiene lo siguiente:
   */libs/fd/xfaforms/clientlibs/I18N/Namespace.js I18N.js /etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2. Agregar la biblioteca de cliente de formulario adaptable para una carpeta locale-name {#add-adaptive-form-client-library-for-a-locale-br}

1. Cree un nodo con el nombre `[locale-name]_af` y escriba como `cq:ClientLibraryFolder` bajo `etc/clientlibs/locale_name`, con la categoría como `guides.I18N.<locale>` y dependencias como `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` y `guide.common`.
1. Cree una carpeta con el nombre `javascript` y agregue los siguientes archivos:

   * **i18n.js**, definiendo `guidelib.i18n` con los patrones de “calendarSymbols” `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols` y `typefaces` para `<locale>` según las especificaciones XFA descritas en [Especificación de la configuración regional](https://helpx.adobe.com/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **LogMessages.js**, definiendo `guidelib.i18n.strings` y `guidelib.i18n.LogMessages` para `<locale>` tal como se define en `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. Añadir **js.txt** que contenga lo siguiente:

   ```
     i18n.js
     LogMessages.js
   ```

#### 4. Agregue compatibilidad con la configuración regional al diccionario {#add-locale-support-for-the-dictionary-br}

Realice este paso solo si la configuración regional `<locale>` que está agregando que no está entre `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja` y `ko-kr`.

1. Crear una carpeta `languages` bajo `etc`, si no está presente.

1. Agregue una propiedad de cadena de varios valores `languages` al nodo, si no está presente ya.
1. Agregue los valores de configuración regional predeterminados `<locale-name>` `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja` y `ko-kr`, si no están presentes.

1. Agregue `<locale>` a los valores de la propiedad `languages` de `/etc/languages`.


```text
Add the newly created folders in the `filter.xml` under etc/META-INF/[folder hierarchy] as:
<filter root="/etc/clientlibs/[locale-name]"/>
<filter root="/etc/languages"/>
```

AEM Antes de confirmar los cambios en el repositorio de Git de la, debe acceder a su [Información del repositorio Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#accessing-git).

#### 5. Confirme los cambios en el repositorio e implemente la canalización {#commit-chnages-in-repo-deploy-pipeline}

Confirme los cambios en el repositorio de GIT después de agregar una nueva compatibilidad con la configuración regional. Implemente su código mediante la canalización de pila completa. Aprender [configuración de una canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=en#setup-pipeline) para agregar nueva compatibilidad con configuración regional.

AEM Una vez finalizada la canalización, la configuración regional recién agregada aparece en el entorno de la.

### Usar configuración regional agregada en Forms adaptable {#use-added-locale-in-af}

Siga estos pasos para utilizar y procesar un formulario adaptable mediante una configuración regional recién agregada:

1. AEM Inicie sesión en la instancia de autor de la.
1. Ir a **Forms** >  **Forms y documentos**.
1. Seleccione un formulario adaptable y haga clic en **Agregar diccionario** y **Agregar diccionario al proyecto de traducción** aparece el asistente.
1. Especifique el **Título del proyecto** y seleccione la **Idiomas de destino** en el menú desplegable de la pestaña **Agregar diccionario al proyecto de traducción** asistente.
1. Clic **Listo** y ejecute el proyecto de traducción creado.
1. Seleccione un formulario adaptable y haga clic en **Vista previa como HTML**.
1. Añadir `&afAcceptLang=<locale-name>` en la URL de un formulario adaptable.
1. Actualice la página y el formulario adaptable se procesará en una configuración regional especificada.

Existen dos métodos para identificar la configuración regional de un formulario adaptable. Cuando se procesa un formulario adaptable, este identifica la configuración regional solicitada de las siguientes formas:

* Recuperación de la `[local]` en la URL del formulario adaptable. El formato de la URL es el siguiente `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. El uso del selector `[local]` permite almacenar en caché un formulario adaptable.

* Recuperación de los siguientes parámetros en el orden indicado:

   * El parámetro de solicitud `afAcceptLang`. Para anular la configuración regional del explorador de los usuarios, puede pasar el parámetro de solicitud 
`afAcceptLang` para forzar la configuración regional. Por ejemplo, la siguiente URL obliga a procesar el formulario en la configuración regional canadiense-francesa:
      `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * La configuración regional del explorador establecida para el usuario, que se especifica en la solicitud utilizando el encabezado `Accept-Language`.

Si no existe una biblioteca de cliente para la configuración regional solicitada, se busca una biblioteca de cliente para el código de idioma presente en la configuración regional. Por ejemplo, si la configuración regional solicitada es `en_ZA` (Inglés sudafricano) y la biblioteca de cliente para `en_ZA` no existe, el formulario adaptable utiliza la biblioteca de cliente para `en` Idioma (inglés), si existe. Sin embargo, si no existe ninguna biblioteca, el formulario adaptable utiliza el diccionario de la configuración regional `en`.


Una vez identificada la configuración regional, el formulario adaptable selecciona el diccionario específico del formulario. Si no se encuentra el diccionario específico del formulario para la configuración regional solicitada, utiliza el diccionario del idioma en el que se crea el formulario adaptable.

Si no hay información de configuración regional, el formulario adaptable se entrega en el idioma original del formulario. El idioma original es el idioma utilizado al desarrollar el formulario adaptable.

Obtener [biblioteca de cliente de ejemplo](/help/forms/assets/locale-support-sample.zip) para agregar compatibilidad con la nueva configuración regional. Debe cambiar el contenido de la carpeta en la configuración regional requerida.

## Prácticas recomendadas para la compatibilidad con la nueva localización {#best-practices}

* El Adobe recomienda crear un proyecto de traducción después de crear un formulario adaptable.

* Cuando se agregan campos nuevos en un formulario adaptable existente:
   * **Para traducción automática**: Vuelva a crear el diccionario y ejecute el proyecto de traducción. Los campos agregados a un formulario adaptable después de crear un proyecto de traducción permanecen sin traducir.
   * **Para traducción humana**: Exporte el diccionario a través de `[server:port]/libs/cq/i18n/gui/translator.html`. Actualice el diccionario de los campos recién añadidos y cárguelo.
