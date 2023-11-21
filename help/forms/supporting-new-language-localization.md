---
title: ¿Cómo puedo añadir compatibilidad con nuevas configuraciones regionales a un formulario adaptable basado en componentes de base?
description: Para el Forms adaptable, puede añadir configuraciones regionales para más idiomas, aparte de la que se proporciona de forma predeterminada.
exl-id: 4c7d6caa-1adb-4663-933f-b09129b9baef
source-git-commit: 8ed477ec0c54bb0913562b9581e699c0bdc973ec
workflow-type: tm+mt
source-wordcount: '1266'
ht-degree: 80%

---

# Compatibilidad con nuevas configuraciones regionales para la localización de formularios adaptables {#supporting-new-locales-for-adaptive-forms-localization}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo Forms adaptable](/help/forms/creating-adaptive-form-core-components.md) o [adición de Forms adaptable a páginas de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de Forms adaptable, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Forms adaptable mediante componentes de base. </span>


| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/manage-administer-aem-forms/supporting-new-language-localization.html?lang=es) |
| Componentes principales | [Haga clic aquí](supporting-new-language-localization-core-components.md) |
| Componentes de base | Este artículo |

AEM Forms admite de forma predeterminada las configuraciones regionales de inglés (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués brasileño (pt-BR), chino (zh-CN), chino taiwanés (zh-TW) y coreano (ko-KR). También puede agregar compatibilidad con más configuraciones regionales, como Hindi (hi_IN).

## Explicación de los diccionarios de configuración regional {#about-locale-dictionaries}

La localización de formularios adaptables se basa en dos tipos de diccionarios de configuración regional:

* **El diccionario específico del formulario**: contiene cadenas utilizadas en formularios adaptables. Por ejemplo, etiquetas, nombres de campos, mensajes de error y descripciones de ayuda. Se administra como un conjunto de archivos XLIFF para cada configuración regional y puede acceder a él en `[author-instance]/libs/cq/i18n/gui/translator.html`.

* **Diccionarios globales** AEM Hay dos diccionarios globales, administrados como objetos JSON, en la biblioteca de cliente de. Estos diccionarios contienen mensajes de error predeterminados, nombres de mes, símbolos de moneda, patrones de fecha y hora, etc. Puede encontrar estos diccionarios en `[author-instance]/libs/fd/xfaforms/clientlibs/I18N`. Estas ubicaciones contienen carpetas independientes para cada configuración regional. Dado que los diccionarios globales no se actualizan con frecuencia, utilizar archivos JavaScript independientes para cada configuración regional permite a los exploradores almacenarlos en caché y reducir el uso del ancho de banda de red al acceder a diferentes formularios adaptables en el mismo servidor.

## Agregar compatibilidad con nuevas configuraciones regionales {#add-support-for-new-locales}

Realice los siguientes pasos para agregar compatibilidad con una nueva configuración regional:

1. [Agregar compatibilidad con la localización para configuraciones regionales no admitidas](#add-localization-support-for-non-supported-locales)
1. [Usar configuraciones regionales agregadas en Formularios adaptables](#use-added-locale-in-af)

### Agregar compatibilidad con la localización para configuraciones regionales no admitidas {#add-localization-support-for-non-supported-locales}

AEM Forms admite actualmente la localización del contenido de los formularios adaptables en las configuraciones regionales de inglés (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués brasileño (pt-BR), chino (zh-CN), chino taiwanés (zh-TW) y coreano (ko-KR).

Para añadir compatibilidad con una nueva configuración regional en el tiempo de ejecución de Forms adaptable:

1. [Clone su repositorio](#clone-the-repository)
1. [Añada una configuración regional al servicio GuideLocalizationService.](#add-a-locale-to-the-guide-localization-service)
1. [Agregar carpeta específica con nombre de configuración regional](#add-locale-name-specific-folder)
1. [Agregar la compatibilidad con la configuración regional del diccionario.](#add-locale-support-for-the-dictionary)
1. [Confirme los cambios en el repositorio e implemente la canalización](#commit-changes-in-repo-deploy-pipeline)

#### 1. Clonar el repositorio {#clone-the-repository}

1. Desde la línea de comandos, vaya a donde desee clonar el repositorio de Cloud Service de Forms.
1. Ejecute el comando que [ha recuperado de Cloud Manager.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git) Es similar a `git clone https://git.cloudmanager.adobe.com/<my-org>/<my-program>/`.
1. Utilice el nombre de usuario y la contraseña de Git para clonar el repositorio.
1. Abra la carpeta clonada del repositorio de Cloud Service de Forms en su editor preferido.

#### 2. Añadir una configuración regional al servicio de localización de guías {#add-a-locale-to-the-guide-localization-service}

1. Busque el archivo `Guide Localization Service.cfg.json` y agregue la configuración regional que desee añadir a la lista de configuraciones regionales admitidas.

   >[!NOTE]
   >
   > Cree un archivo con el nombre de archivo `Guide Localization Service.cfg.json`, si no está presente.

#### 3. Agregar una biblioteca de cliente de carpetas específica con nombre de configuración regional {#add-locale-name-specific-folder}

1. En la carpeta UI.content, cree la carpeta `etc/clientlibs`.
1. Cree además una carpeta denominada como `locale-name` bajo `etc/clientlibs` para servir como contenedor para clientlibs xfa y af.

##### 3.1 Agregar la biblioteca de cliente XFA para una configuración regional en una carpeta con nombre de configuración regional

Cree un nodo con el nombre `[locale-name]_xfa` y escriba como `cq:ClientLibraryFolder` bajo `etc/clientlibs/locale_name`, con categoría `xfaforms.I18N.<locale>`, y agregue los siguientes archivos:

* **I18N.js** definiendo `xfalib.locale.Strings` para `<locale>`, tal como se define en `/etc/clientlibs/fd/xfaforms/I18N/ja/I18N`.
* **js.txt**, que contiene lo siguiente:
  */libs/fd/xfaforms/clientlibs/I18N/Namespace.js
I18N.js
/etc/clientlibs/fd/xfaforms/I18N/LogMessages.js*

##### 3.2. Agregar la biblioteca de cliente de Formulario Adaptable para una configuración regional en la carpeta locale-name

1. Cree un nodo con el nombre `[locale-name]_af` y tipo `cq:ClientLibraryFolder` en `etc/clientlibs/locale_name`, con categoría `guides.I18N.<locale>` y dependencias `xfaforms.3rdparty`, `xfaforms.I18N.<locale>` y `guide.common`.
1. Cree una carpeta con el nombre como `javascript` y agregue los siguientes archivos:

   * **i18n.js**, definiendo `guidelib.i18n` con los patrones de “calendarSymbols” `datePatterns`, `timePatterns`, `dateTimeSymbols`, `numberPatterns`, `numberSymbols`, `currencySymbols` y `typefaces` para `<locale>` según las especificaciones XFA descritas en [Especificación de la configuración regional](https://helpx.adobe.com/es/content/dam/Adobe/specs/xfa_spec_3_3.pdf).
   * **LogMessages.js**, definiendo `guidelib.i18n.strings` y `guidelib.i18n.LogMessages` para `<locale>` tal como se define en `/etc/clientlibs/fd/af/I18N/fr/javascript/LogMessages.js`.

1. Agregue **js.txt** que contenga lo siguiente:

   ```
     i18n.js
     LogMessages.js
   ```

#### 4. Agregar compatibilidad de configuración regional para el diccionario {#add-locale-support-for-the-dictionary}

Realice este paso solo si la configuración regional `<locale>` que está agregando no está entre `en`, `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja` y `ko-kr`.

1. Crear una carpeta `languages` bajo `etc`, si no está presente.

1. Agregue una propiedad de cadena de varios valores `languages` al nodo, si no está presente ya.
1. Agregue los valores de configuración regional predeterminados `<locale-name>` `de`, `es`, `fr`, `it`, `pt-br`, `zh-cn`, `zh-tw`, `ja` y `ko-kr`, si no están presentes.

1. Agregue `<locale>` a los valores de la propiedad `languages` de `/etc/languages`.
1. Añada las carpetas creadas en `filter.xml` bajo etc/META-INF/[jerarquía de carpetas] como:

   ```
   <filter root="/etc/clientlibs/[locale-name]"/>
   <filter root="/etc/languages"/>
   ```

Antes de confirmar los cambios en el repositorio de Git de AEM, debe acceder a su [Información del repositorio de Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git).

#### 5. Confirmar los cambios en el repositorio e implementar la canalización {#commit-changes-in-repo-deploy-pipeline}

Confirme los cambios en el repositorio de GIT después de agregar una compatibilidad con la configuración regional. Implemente el código mediante la canalización de pila completa. Aprenda a [configurar una canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline) para añadir compatibilidad con una nueva configuración regional.
Una vez finalizada la canalización, la configuración regional recién agregada aparece en el entorno de AEM.

### Uso de una configuración regional añadida en formularios adaptables {#use-added-locale-in-af}

Siga estos pasos para utilizar y procesar un formulario adaptable mediante la configuración regional recién agregada:

1. Inicie sesión en la instancia de autor de AEM.
1. Vaya a **Formularios** > **Formularios y documentos**.
1. Seleccione un formulario adaptable y haga clic en **Agregar diccionario** y aparecerá el asistente **Agregar diccionario al proyecto de traducción**.
1. Especifique el **Título del proyecto** y seleccione los **Idiomas de destino** en el menú desplegable del asistente **Agregar diccionario al proyecto de traducción**.
1. Haga clic en **Listo** y ejecute el proyecto de traducción creado.
1. Seleccione un formulario adaptable y haga clic en **Previsualizar como HTML**.
1. Añada `&afAcceptLang=<locale-name>` en la URL de un formulario adaptable.
1. Actualice la página y el formulario adaptable se procesará en la configuración regional especificada.

Existen dos métodos para identificar la configuración regional de un formulario adaptable. Cuando se procesa un formulario adaptable, este identifica la configuración regional solicitada de las siguientes formas:

* Recuperando el selector `[local]` en la URL del formulario adaptable. El formato de la URL es el siguiente `http://host:[port]/content/forms/af/[afName].[locale].html?wcmmode=disabled`. El uso del selector `[local]` permite almacenar en caché un formulario adaptable.

* Recuperando los siguientes parámetros en el orden indicado:

   * Parámetro de solicitud `afAcceptLang`
Para anular la configuración regional del explorador de los usuarios, puede pasar el `afAcceptLang` para forzar la configuración regional. Por ejemplo, la siguiente URL obliga a procesar el formulario en la configuración regional francés canadiense:
     `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ca-fr`

   * La configuración regional del explorador establecida para el usuario, que se especifica en la solicitud utilizando el encabezado `Accept-Language`.

Si no existe una biblioteca de cliente para la configuración regional solicitada, se busca una biblioteca de cliente para el código de idioma presente en la configuración regional. Por ejemplo, si la configuración regional solicitada es `en_ZA` (inglés sudafricano) y la biblioteca de cliente `en_ZA` no existe, el formulario adaptable utiliza la biblioteca de cliente del idioma `en` (inglés), si existe. Sin embargo, si no existe ninguna biblioteca, el formulario adaptable utiliza el diccionario de la configuración regional `en`.


Una vez identificada la configuración regional, el formulario adaptable elige el diccionario específico del formulario. Si no se encuentra el diccionario específico del formulario para la configuración regional solicitada, utiliza el diccionario del idioma en el que se crea el formulario adaptable.

Si no hay información de configuración regional, el formulario adaptable se entrega en el idioma original del formulario. El idioma original es el idioma utilizado al desarrollar el formulario adaptable.

Obtenga una [biblioteca de cliente de ejemplo](/help/forms/assets/locale-support-sample.zip) para agregar compatibilidad con la nueva configuración regional. Debe cambiar el contenido de la carpeta en la configuración regional requerida.

## Prácticas recomendadas para la compatibilidad con localización nueva {#best-practices}

* El Adobe recomienda crear un proyecto de traducción después de crear un formulario adaptable.

* Cuando se agregan campos nuevos en un formulario adaptable existente:
   * **Para traducción automática**: vuelva a crear el diccionario y ejecute el proyecto de traducción. Los campos añadidos a un formulario adaptable después de crear un proyecto de traducción permanecen sin traducir.
   * **Para traducción humana**: exporte el diccionario a través de `[server:port]/libs/cq/i18n/gui/translator.html`. Actualice el diccionario de los campos recién añadidos y cárguelo.


## Vea también {#see-also}

{{see-also}}