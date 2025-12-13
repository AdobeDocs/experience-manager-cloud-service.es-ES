---
title: ¿Cómo puedo añadir compatibilidad con nuevas configuraciones regionales a un formulario adaptable basado en componentes principales?
description: Aprenda a agregar nuevas configuraciones regionales a un formulario adaptable.
feature: Adaptive Forms, Core Components
Role: Developer, Author
exl-id: bc06542b-84c8-4c6a-a305-effbd16d5630
role: User, Developer
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 98%

---

# Añadir una configuración regional para Formularios adaptables basada en componentes principales {#supporting-new-locales-for-adaptive-forms-localization}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| Componentes de base | [Haga clic aquí](supporting-new-language-localization.md) |
| Componentes principales | Este artículo |

<span class="preview"> La función de compatibilidad de idioma de derecha a izquierda está disponible en el programa para primeros usuarios. Puede escribir a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad. </span>

AEM Forms admite de forma predeterminada las configuraciones regionales de inglés (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués brasileño (pt-BR), chino (zh-CN), chino taiwanés (zh-TW) y coreano (ko-KR). También puede agregar compatibilidad con más configuraciones regionales, como Hindi (hi_IN). También puede presentar formularios adaptables en un idioma de derecha a izquierda (RTL) como árabe, persa y urdu si agrega estas configuraciones regionales.

>[!VIDEO](https://video.tv.adobe.com/v/3433132/adaptive-forms-rtl--arabic-hebrew-farsi)

## Aplicabilidad y casos de uso

### Seguro

## ¿AEM Forms es compatible con los casos de uso de seguros multilingües?

Sí. AEM Forms admite experiencias de formularios multilingües, lo que es importante para las aseguradoras que operan en diferentes regiones e idiomas.

## ¿Cómo determina AEM Forms la configuración regional de un formulario adaptable?

Comprender cómo AEM Forms selecciona la configuración regional para procesar un formulario adaptable es crucial para una localización adecuada. A continuación, se desglosa el proceso de selección:

### Selección de la configuración regional basada en la prioridad

AEM Forms prioriza los siguientes métodos para determinar la configuración regional de un formulario adaptable:

1. **Selector de configuración regional de URL ([locale])**:

   El sistema da prioridad a la configuración regional especificada en la dirección URL mediante el selector [locale]. Este formato permite el almacenamiento en caché para obtener un mejor rendimiento.

   Formato: la dirección URL adopta este formato: http:/[AEM Forms Server URL]/content/forms/af/[afName].[locale].html?wcmmode=disabled. 

   Ejemplo: https://[server]/content/forms/af/contact-us.hi.html procesa el formulario en hindi.


1. **Parámetro de solicitud afAcceptLang**:

   Para anular la configuración regional del explorador del usuario, puede utilizar el parámetro `afAcceptLang` en la dirección URL.

   Ejemplo: https://[server]/forms/af/survey.ca-fr.html?afAcceptLang=ca-fr fuerza al formulario a procesarse en francés de Canadá.

1. **Configuración regional del explorador del usuario (encabezado Accept-Language)**:

   Si no se especifica ninguna otra configuración regional, AEM Forms adopta la configuración regional del explorador del usuario enviada mediante el encabezado `Accept-Language`.


### Mecanismo de reserva:


* Si una biblioteca de cliente (proceso para añadir una nueva configuración regional, que se explica más adelante en este documento) para la configuración regional solicitada no está disponible, AEM Forms busca una biblioteca basada en el código de idioma de la configuración regional.

  Ejemplo: Si se solicita en_ZA (inglés sudafricano) y no hay ninguna biblioteca en_ZA, utiliza en (English, inglés) si está disponible.

  Si no se encuentra ninguna biblioteca de cliente adecuada, se utiliza el diccionario predeterminado (principalmente,`en`) para el idioma de creación del formulario.

  Si no hay información de configuración regional, el formulario adaptable se muestra en el idioma original utilizado durante el desarrollo.


## Requisitos previos para añadir una configuración regional

Antes de empezar a añadir una nueva configuración regional para sus Formularios adaptables, asegúrese de que dispone de lo siguiente:

**Software:**

* Editor de texto sin formato (IDE): aunque cualquier editor de texto sin formato puede funcionar, un entorno de desarrollo integrado (IDE) como [Microsoft Visual Studio Code](https://code.visualstudio.com/download) ofrece funciones avanzadas para facilitar la edición.

* Git: este sistema de control de versiones es necesario para administrar los cambios de código. Si no lo tiene instalado, descárguelo en [https://git-scm.com](https://git-scm.com).


**Repositorio de códigos:**

Clone el repositorio de componentes principales de formularios adaptables: necesita una biblioteca de cliente de este repositorio para añadir una configuración regional. Para clonar el repositorio, haga lo siguiente:

1. Abra la línea de comandos o la ventana de terminal.

1. Navegue hasta la ubicación deseada en el equipo donde desee almacenar el repositorio (por ejemplo, /adaptive-forms-core-components).

1. Ejecute el siguiente comando para clonar el repositorio:

   ```
   git clone https://github.com/adobe/aem-core-forms-components.git
   ```

   Este comando descarga el repositorio y crea una carpeta denominada `aem-core-forms-components` en su equipo. En esta guía, nos referimos a esta carpeta como `[Adaptive Forms Core Components repository]`.


## Añadir una configuración regional {#add-localization-support-for-non-supported-locales}

Para añadir compatibilidad con nuevas configuraciones regionales a un formulario adaptable basado en componentes principales, siga estos pasos:

### Clone su repositorio de Git de AEM as a Cloud Service

1. Abra la línea de comandos y seleccione un directorio para almacenar el repositorio de AEM as a Cloud Service, como `/cloud-service-repository/`.

1. Ejecute el siguiente comando para clonar el repositorio:

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<program id>/
   ```

   Para clonar el repositorio Git, necesita determinada información:

   * **Nombre de organización**: identifica al equipo o proyecto dentro de Adobe Experience Manager as a Cloud Service (AEM as a Cloud Service).

   * **ID de programa**: especifica el programa asociado al repositorio.

   * **Credenciales**: necesita un nombre de usuario y una contraseña (o un token de acceso personal) para acceder al repositorio de forma segura.

   **¿Dónde se encuentra esta información?**

   Para obtener instrucciones paso a paso sobre cómo localizar estos detalles, consulte el artículo de Adobe Experience League “[Acceder a Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git)”.

   **Su proyecto está listo.**

   Cuando el comando se complete correctamente, verá que se ha creado una nueva carpeta en su directorio local. Esta carpeta recibe el nombre de su programa (por ejemplo, program-id). Esta carpeta contiene todos los archivos y el código descargados del repositorio de Git de AEM as a Cloud Service.

   En esta guía, nos referimos a esta carpeta como `[AEMaaCS project directory]`.


### Añada la nueva configuración regional al Servicio de localización de guías

1. Abra la carpeta del repositorio en un editor.

   ![Carpeta de repositorio en un editor](/help/forms/assets/repository-folder-in-an-editor.png)

1. Guarde el archivo `Guide Localization Service.cfg.json`. Este archivo controla las configuraciones regionales admitidas por la aplicación de AEM Forms. Puede editar este archivo para añadir una nueva configuración regional.

   * **Archivo existente**: si el archivo ya existe, búsquelo en el directorio del proyecto de AEM Forms. La ubicación típica es:

     ```Shell
     [AEMaaCS project directory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config`. 
     ```

     Reemplace `<appid>` por el ID de aplicación específico del proyecto. Puede encontrar `<appid>` para su proyecto de AEM en el archivo `archetype.properties`.

     ![Propiedades de tipo de archivo](/help/forms/assets/archetype-properties.png)

   * **Nuevo archivo**: si el archivo no existe, debe crearlo en la misma ubicación mencionada anteriormente. No copie y pegue el nombre del archivo de este documento, sino que debe escribirlo manualmente el nombre. El nombre de archivo `Guide Localization Service.cfg.json` incluye espacios. Es intencionado y no se trata de un error tipográfico de la documentación.

     Un archivo de muestra con la lista de configuraciones regionales compatibles con OOTB es:

     ```
         {
             "supportedLocales":[
             "en",
             "fr",
             "de",
             "ja",
             "pt-br",
             "zh-cn",
             "zh-tw",
             "ko-kr",
             "it",
             "es"
             ]
         }
     ```

1. Añada el código de configuración regional del idioma deseado al archivo.
   1. Utilice la [Lista de códigos ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) para encontrar el código de dos letras que represente el idioma deseado.

   1. Añada el código de configuración regional al archivo `Guide Localization Service.cfg.json`. Estos son algunos ejemplos:

      * Idiomas de izquierda a derecha:
         * Inglés (Estados Unidos): en-US
         * Español (España): es-ES
         * Francés (Francia): fr-FR
      * Idiomas de derecha a izquierda:
         * Árabe (Emiratos Árabes Unidos): ar-ae
         * Hebreo: he (o iw para referencia histórica)
         * Farsi: fa

1. Después de realizar los cambios, asegúrese de que el archivo `Guide Localization Service.cfg.json` tiene el formato correcto de un archivo JSON válido. Los errores en el formato JSON pueden impedir que funcione correctamente. Guarde el archivo.



### Aproveche la biblioteca de cliente de ejemplo para añadir fácilmente configuraciones regionales

AEM Forms proporciona una biblioteca de cliente de ejemplo útil, `clientlib-it-custom-locale`, para simplificar la adición de nuevas configuraciones regionales. Esta biblioteca forma parte del [repositorio de componentes principales de formularios adaptables](https://github.com/adobe/aem-core-forms-components), disponible en GitHub.


Antes de comenzar, asegúrese de que dispone de una copia local del [repositorio de componentes principales de formularios adaptables]. Si no es así, puede clonarlo fácilmente con Git con el siguiente comando:

```SHELL
git clone https://github.com/adobe/aem-core-forms-components.git
```

Este comando descarga todo el repositorio, incluida la biblioteca clientlib-it-custom-locale, en un directorio llamado aem-core-forms-components de su equipo.

![Directorio del repositorio de componentes principales de formularios adaptables en el equipo local](/help/forms/assets/core-forms-components-repo-on-local-machine.png)

### Integre la biblioteca de cliente de ejemplo

Ahora, vamos a incorporar la biblioteca `clientlib-it-custom-locale` en su AEM as a Cloud Service, [directorio del proyecto AEMaaCS]:

1. Busque la biblioteca de cliente de ejemplo:

   En la copia local del [repositorio de componentes principales de formularios adaptables], navegue hasta la siguiente ruta:

   ```
       /aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs
   ```

1. Copie y pegue la biblioteca:

   1. Copie la carpeta `clientlib-it-custom-locale`.

      ![Copiando clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-copy.png)

   1. Navegue hasta el siguiente directorio dentro de su [directorio del proyecto AEMaaCS]:

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib
      ```

      **Importante**: reemplace `<app-id>` por el ID real de su aplicación.

   1. Pegue la carpeta `clientlib-it-custom-locale` copiada en este directorio.

      ![Pegando clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-paste.png)

1. Actualizar ruta `aemLangUrl` en `languageinit.js`

   1. Navegue hasta el siguiente directorio dentro de su [directorio del proyecto AEMaaCS]:

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib/clientlib-it-custom-locale/js
      ```

   1. Abra el archivo `languageinit.js` en el editor.
   1. Localice la línea siguiente en el archivo `languageinit.js`:

      `const aemLangUrl = /etc.clientlibs/forms-core-components-it/clientlibs/clientlib-it-custom-locale/resources/i18n/${lang}.json;`

   1. Reemplace `forms-core-components-it` con su `<app-id>` (ID real de su aplicación) en la línea anterior.

      `const aemLangUrl = '/etc.clientlibs/<app-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/${lang}.json';`

      ![language-init-file](/help/forms/assets/language-init-name-change.png)

>[!NOTE]
>  
> Si no reemplaza `forms-core-components-it` por su nombre de proyecto o `<app-id>`, el componente selector de fechas no se podrá traducir.

### Cree un archivo .json para la nueva configuración regional:

1. Vaya al directorio de configuración regional adecuado:

   Dentro de su `[AEMaaCS project directory]`, vaya a la siguiente ruta:

   ```
       /ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/
   ```

   **Importante**: reemplace `<program-id>` por su ID de aplicación real.

1. Busque el archivo de idioma inglés de ejemplo:

   AEM Forms proporciona un [archivo de configuración regional de ejemplo en inglés (.json) en GitHub](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json).

   El archivo en inglés incluye el conjunto predeterminado de cadenas como referencia. El archivo específico de la configuración regional debe imitar la estructura del archivo en inglés.

   En idiomas como el árabe, el hebreo y el persa, el texto se lee de derecha a izquierda (RTL) en lugar de izquierda a derecha (LTR) como el inglés. Para garantizar que los formularios se muestren correctamente en estos idiomas, se recomienda utilizar nuestros archivos de configuración regional de ejemplo como guía. Estos archivos proporcionan una referencia sobre cómo dar formato al texto, fechas y otros elementos para los idiomas RTL. Puede encontrar los archivos de configuración regional de ejemplo para los siguientes idiomas:

   * [Árabe](/help/forms/assets/ar-ae.json)
   * [Hebreo](/help/forms/assets/he.json)
   * [Farsi](/help/forms/assets/fa.json)

   Si aprovecha estos archivos de ejemplo, podrá asegurarse de que los formularios proporcionen una experiencia perfecta a los usuarios que trabajan con idiomas RTL.


1. Cree su archivo de configuración regional:

   1. Cree un nuevo archivo .json dentro del directorio `i18n`.
   1. Asigne un nombre al archivo utilizando el código de configuración regional adecuado para el idioma deseado (por ejemplo, fr-FR.json para francés y ar-ae.json para árabe). La estructura de este archivo debe reflejar el archivo de configuración regional en inglés.


1. Estructura y traducción:

   1. Abra el archivo recién creado en un editor de texto.

   1. Reemplace los valores en inglés por las traducciones correspondientes para su idioma de destino.

   1. Una vez que haya terminado de traducir las cadenas, guarde el archivo.




### Añadir la compatibilidad con la configuración regional al diccionario

Este paso solo se aplica a las configuraciones regionales que no sean las siguientes comúnmente admitidas: inglés (en), alemán (de), español (es), francés (fr), italiano (it), portugués de Brasil (pt-br), chino (simplificado - zh_cn), chino (tradicional - zh_tw), japonés (ja) y coreano (ko_kr).

1. Localice la carpeta de configuración:

   Navegue hasta el siguiente directorio en su [directorio del proyecto AEMaaCS]:

   ```
   /ui.content/src/main/content/jcr_root/etc
   ```

1. Cree las carpetas necesarias (si faltan):

   Si la carpeta `etc` no está dentro de la carpeta `jcr_root`, créela. Dentro de `etc`, cree otra carpeta llamada `languages` si falta.

1. Cree el archivo de configuración regional:

   En la carpeta `languages`, cree un nuevo archivo con el nombre `.content.xml`. No copie y pegue el nombre del archivo de este documento, sino que debe escribirlo manualmente el nombre.

   ![cree un nuevo archivo con el nombre `.content.xml`](etc-content-xml.png).

   Abra este archivo y pegue el siguiente contenido: [LOCALE_CODE] con el código de configuración regional real (por ejemplo, ar-ae para árabe).


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
         jcr:primaryType="nt:unstructured"
         languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

   ADVERTENCIA: No reemplace la lista existente. En su lugar, debe escribir el nuevo código de configuración regional entre corchetes, separados por comas, de esta manera (utilizando ar-ae como ejemplo):

   ```XML
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi,ar-ae]"
   ```

1. Incluya las carpetas nuevas en filter.xml:

   Vaya al archivo `/ui.content/src/main/content/meta-inf/vault/filter.xml` en su [directorio del proyecto AEMaaCS].

   Abra el archivo y añada la siguiente línea al final:

   ```
   <filter root="/etc/languages"/>
   ```

   ![Añada las carpetas creadas en `filter.xml` dentro de `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)

1. Guarde el archivo.

### Implemente la configuración regional recién creada en su entorno AEM

Ya está todo configurado para utilizar la nueva configuración regional con sus formularios adaptables. Puede hacer lo siguiente:

* Implementar AEM as a Cloud Service, [directorio del proyecto AEMaaCS], en su entorno de desarrollo local para probar la nueva configuración regional en el equipo local. Para implementarlo en su entorno de desarrollo local:

   1. Asegúrese de que el entorno de desarrollo local esté activo y en funcionamiento. Si aún no ha configurado un entorno de desarrollo local, consulte la guía de [Configuración del entorno de desarrollo local para AEM Forms](/help/forms/setup-local-development-environment.md).

   1. Abra la ventana del terminal o el símbolo del sistema.

   1. Vaya al [directorio del proyecto AEMaaCS]

   1. Ejecute el siguiente comando:

      ```
      mvn -PautoInstallPackage clean install
      ```

* Implemente AEM as a Cloud Service, [directorio del proyecto AEMaaCS], en su entorno de Cloud Service. Para implementarlo en el entorno de Cloud Service:

   1. Confirme los cambios:

      Después de añadir la nueva configuración regional, confirme los cambios con un mensaje Git claro que describa la adición de configuración regional (por ejemplo, &quot;Se ha añadido compatibilidad con [Nombre de configuración regional]&quot;).

   1. Implemente el código actualizado:

      Active una implementación del código a través de la [canalización de pila completa existente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline). Esto crea e implementa automáticamente el código actualizado con la nueva compatibilidad con la configuración regional.

      Si aún no ha configurado una canalización, consulte la guía sobre [cómo configurar una canalización para AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline).


## Vista previa de un formulario adaptable con la configuración regional recién añadida

Estos pasos le guían a través de la previsualización de un formulario adaptable con la configuración regional recién añadida:

1. Inicie sesión en la instancia de AEM Forms as a Cloud Service.
1. Vaya a **Formularios** > **Formularios y documentos**.
1. Seleccione un formulario adaptable y haga clic en **Agregar diccionario** y aparecerá el asistente **Agregar diccionario al proyecto de traducción**.
1. Especifique el **Título del proyecto** y seleccione los **Idiomas de destino** en el menú desplegable del asistente **Agregar diccionario al proyecto de traducción**.
1. Haga clic en **Listo** y ejecute el proyecto de traducción creado.
1. Vaya a **Formularios** > **Formularios y documentos**.
1. Seleccione el formulario adaptable y elija la opción **Previsualizar como HTML**.
1. Añada `&afAcceptLang=<locale-name>` a la URL de vista previa y pulse la tecla de retorno. Reemplace `<locale-name>` por su código de configuración regional real. El formulario adaptable se muestra en la configuración regional especificada.

## Prácticas recomendadas para la compatibilidad con localización nueva {#best-practices}

* Adobe recomienda crear un proyecto de traducción después de crear un formulario adaptable. Esto optimiza el proceso de localización.
* Cuando los componentes Cuadro numérico y Selector de fecha se traducen a una configuración regional específica, pueden surgir problemas de formato. Para mitigar esto, se ha incorporado una opción **Idioma** al cuadro de diálogo Configurar del [componente Selector de fechas](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker#format-tab) y el [componente Cuadro numérico](https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/numeric-box#formats-configure-tab).


* Gestión de nuevos campos:

   * **Traducción automática**: si utiliza la traducción automática, debe volver a crear el diccionario y volver a [ejecutar el proyecto de traducción](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md) después de añadir nuevos campos a un formulario adaptable existente. Los nuevos campos añadidos después del proyecto de traducción inicial permanecen sin traducir.

   * **Traducción humana**: exporte el diccionario mediante la IU de `[AEM Forms Server]/libs/cq/i18n/gui/translator.html`. Actualice el diccionario de los nuevos campos y cargue la versión revisada.


## Consulte también {#see-also}

{{see-also}}

* [Generar documento de registro para Formularios adaptables](/help/forms/generate-document-of-record-core-components.md)
* [Agregar un formulario adaptable a una página de AEM Sites o a un fragmento de experiencia](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

