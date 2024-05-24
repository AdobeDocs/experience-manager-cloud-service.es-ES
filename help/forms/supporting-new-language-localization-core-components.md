---
title: ¿Cómo puedo añadir compatibilidad con nuevas configuraciones regionales a un formulario adaptable basado en componentes principales?
description: Aprenda a agregar nuevas configuraciones regionales a un formulario adaptable.
feature: Adaptive Forms, Core Components
Role: Developer, Author
exl-id: bc06542b-84c8-4c6a-a305-effbd16d5630
source-git-commit: 9cb3b52d0cf172c16777eadbc4d78b267c3db513
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 12%

---

# Añadir una configuración regional para Formularios adaptables basada en componentes principales {#supporting-new-locales-for-adaptive-forms-localization}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| Componentes de base | [Haga clic aquí](supporting-new-language-localization.md) |
| Componentes principales | Este artículo |

<span class="preview"> La función de soporte de idiomas de derecha a izquierda está disponible en el programa de usuarios pioneros. Puede escribir a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad. </span>

AEM Forms admite de forma predeterminada las configuraciones regionales de inglés (en), español (es), francés (fr), italiano (it), alemán (de), japonés (ja), portugués brasileño (pt-BR), chino (zh-CN), chino taiwanés (zh-TW) y coreano (ko-KR). También puede agregar compatibilidad con más configuraciones regionales, como Hindi (hi_IN). También puede presentar formularios adaptables en un idioma de derecha a izquierda (RTL) como árabe, persa y urdu si agrega estas configuraciones regionales.

## ¿Cómo determina AEM Forms la configuración regional de un formulario adaptable?

Comprender cómo selecciona AEM Forms la configuración regional para procesar un formulario adaptable es crucial para una localización adecuada. Este es un desglose del proceso de selección:

### Selección de configuración regional basada en prioridad

AEM Forms prioriza los siguientes métodos para determinar la configuración regional de un formulario adaptable:

1. **Selector de configuración regional de URL ([locale])**:

   El sistema da prioridad a la configuración regional especificada en la dirección URL mediante [locale] selector. Este formato permite almacenar en caché para obtener un mejor rendimiento.

   Formato: La dirección URL sigue este formato: http:/[URL del servidor de AEM Forms]/content/forms/af/[afName].[locale].html?wcmmode=disabled.

   Ejemplo: https://[server]/content/forms/af/contact-us.hi.html procesa el formulario en hindi.


1. **Parámetro de solicitud afAcceptLang**:

   Para anular la configuración regional del explorador del usuario, puede utilizar el `afAcceptLang` en la dirección URL.

   Ejemplo: https://[server]/forms/af/survey.ca-fr.html?afAcceptLang=ca-fr fuerza al formulario a procesarse en francés canadiense.

1. **Configuración regional del explorador del usuario (encabezado Accept-Language)**:

   Si no se especifica ninguna otra configuración regional, AEM Forms considera la configuración regional del explorador del usuario enviada mediante `Accept-Language` encabezado.


### Mecanismo de reserva:


* Si una biblioteca de cliente (proceso para agregar una nueva configuración regional, explicado más adelante en este documento) para la configuración regional solicitada no está disponible, AEM Forms busca una biblioteca basada en el código de idioma de la configuración regional.

  Ejemplo: Si se solicita en_ZA (inglés sudafricano) y no hay ninguna biblioteca en_ZA, se utiliza en (inglés) si está disponible.

  Si no se encuentra ninguna biblioteca de cliente adecuada, el diccionario predeterminado (en su mayoría `en`) para el idioma de creación del formulario.

  Si no hay información de configuración regional, el formulario adaptable se muestra en el idioma original utilizado durante el desarrollo.


## Requisitos previos para agregar una configuración regional

Antes de empezar a añadir una nueva configuración regional para su Forms adaptable, asegúrese de que dispone de lo siguiente:

**Software:**

* Editor de texto sin formato (IDE): aunque cualquier editor de texto sin formato puede funcionar, un entorno de desarrollo integrado (IDE) como [Microsoft Visual Studio Code](https://code.visualstudio.com/download) ofrece funciones avanzadas para facilitar la edición.

* Git: este sistema de control de versiones es necesario para administrar los cambios de código. Si no lo tiene instalado, descárguelo desde [https://git-scm.com](https://git-scm.com).


**Repositorio de códigos:**

Clone el repositorio de componentes principales de Forms adaptable: necesita una biblioteca de cliente de este repositorio para agregar una configuración regional. Para clonar el repositorio, haga lo siguiente:

1. Abra la línea de comandos o la ventana de terminal.

1. Vaya a la ubicación deseada en el equipo donde desee almacenar el repositorio (por ejemplo, /adaptive-forms-core-components).

1. Ejecute el siguiente comando para clonar el repositorio:

   ```
   git clone https://github.com/adobe/aem-core-forms-components.git
   ```

   Este comando descarga el repositorio y crea una carpeta denominada `aem-core-forms-components` en su máquina. En esta guía, nos referimos a esta carpeta como `[Adaptive Forms Core Components repository]`


## Añadir una configuración regional {#add-localization-support-for-non-supported-locales}

Para añadir compatibilidad con nuevas configuraciones regionales a un formulario adaptable basado en componentes principales, siga estos pasos:

### AEM Clonar el repositorio de Git as a Cloud Service de

1. AEM Abra la línea de comandos y seleccione un directorio para almacenar el repositorio as a Cloud Service de la, como `/cloud-service-repository/`.

1. Ejecute el siguiente comando para clonar el repositorio:

   ```SHELL
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<program id>/
   ```

   Para clonar el repositorio Git, necesita alguna información:

   * **Nombre de organización**: Identifica al equipo o proyecto dentro de Adobe Experience Manager as a Cloud Service AEM (as a Cloud Service).

   * **ID de programa**: Esto especifica el programa asociado al repositorio.

   * **Credenciales**: Necesita un nombre de usuario y una contraseña (o un token de acceso personal) para acceder al repositorio de forma segura.

   **¿Dónde se encuentra esta información?**

   Para obtener instrucciones paso a paso sobre cómo localizar estos detalles, consulte el artículo de Adobe Experience League &quot;[Acceso a Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#accessing-git)&quot;.

   **Su proyecto está listo.**

   Cuando el comando se complete correctamente, verá una nueva carpeta creada en el directorio local. Esta carpeta recibe el nombre de su programa (por ejemplo, program-id). AEM Esta carpeta contiene todos los archivos y el código descargados del repositorio de Git as a Cloud Service de la.

   En esta guía, nos referimos a esta carpeta como `[AEMaaCS project directory]`.


### Añada la nueva configuración regional al servicio de localización de guías

1. Abra la carpeta del repositorio en un editor.

   ![Carpeta de repositorio en un editor](/help/forms/assets/repository-folder-in-an-editor.png)

1. Busque el `Guide Localization Service.cfg.json` archivo. Este archivo controla las configuraciones regionales admitidas por la aplicación de AEM Forms. Puede editar este archivo para agregar una nueva configuración regional.

   * **Archivo existente**: Si el archivo ya existe, búsquelo en el directorio del proyecto de AEM Forms. La ubicación típica es:

     ```Shell
     [AEMaaCS project directory]/ui.config/src/main/content/jcr_root/apps/<appid>/osgiconfig/config`. 
     ```

     Reemplazar `<appid>` con el ID de aplicación específico del proyecto. Puede encontrar `<appid>` AEM para su proyecto de en `archetype.properties` archivo.

     ![Propiedades de tipo de archivo](/help/forms/assets/archetype-properties.png)

   * **Nuevo archivo**: Si el archivo no existe, debe crearlo en la misma ubicación mencionada anteriormente. No copie y pegue el nombre del archivo de este documento, sino que escriba manualmente el nombre. El nombre del archivo `Guide Localization Service.cfg.json` incluye espacios. Esto es intencional y no es un error tipográfico en la documentación.

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
   1. Utilice el [Lista de códigos ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) para encontrar el código de dos letras que represente el idioma deseado.

   1. Incluya el código de configuración regional en `Guide Localization Service.cfg.json` archivo. Estos son algunos ejemplos:

      * Idiomas de izquierda a derecha:
         * Inglés (Estados Unidos): en-US
         * Español (España): es-ES
         * Francés (Francia): fr-FR
      * Idiomas de derecha a izquierda:
         * Árabe (Emiratos Árabes Unidos): ar-ae
         * Hebreo: he (o iw para referencia histórica)
         * Farsi: fa

1. Después de realizar los cambios, asegúrese de que `Guide Localization Service.cfg.json` tiene el formato correcto de un archivo JSON válido. Los errores en el formato JSON pueden impedir que funcione correctamente. Guarde el archivo.



### Aproveche la biblioteca de cliente de muestra para agregar configuraciones regionales fácilmente

AEM Forms proporciona una biblioteca de cliente de ejemplo útil, `clientlib-it-custom-locale`, para simplificar la adición de nuevas configuraciones regionales. Esta biblioteca forma parte del [Repositorio de componentes principales de Forms adaptable](https://github.com/adobe/aem-core-forms-components), disponible en GitHub.


Antes de comenzar, asegúrese de que dispone de una copia local del [Repositorio de componentes principales de Forms adaptable]. Si no es así, puede clonarlo fácilmente con Git con el siguiente comando:

```SHELL
git clone https://github.com/adobe/aem-core-forms-components.git
```

Este comando descarga todo el repositorio, incluida la biblioteca clientlib-it-custom-locale, en un directorio llamado aem-core-forms-components de su equipo.

![Directorio del repositorio de componentes principales de Forms adaptable en el equipo local](/help/forms/assets/core-forms-components-repo-on-local-machine.png)

### Integración de la biblioteca de cliente de ejemplo

Ahora, vamos a incorporar la `clientlib-it-custom-locale` AEM en su biblioteca de as a Cloud Service de, [Directorio del proyecto AEMaaCS]:

1. Busque la biblioteca de cliente de ejemplo:

   En la copia local del [Repositorio de componentes principales de Forms adaptable], vaya a la siguiente ruta:

   ```
       /aem-core-forms-components/it/apps/src/main/content/jcr_root/apps/forms-core-components-it/clientlibs
   ```

1. Copie y pegue la biblioteca:

   1. Copie el `clientlib-it-custom-locale` carpeta.

      ![Copiando clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-copy.png)

   1. Navegue hasta el siguiente directorio dentro de su [Directorio del proyecto AEMaaCS]:

      ```
      /ui.apps/src/main/content/jcr_root/apps/<app-id>/clientlib
      ```

      **Importante**: Reemplazar `<app-id>` con el ID real de su aplicación.

   1. Pegue el copiado `clientlib-it-custom-locale` en este directorio.

      ![Pegando clientlib-it-custom-locale](/help/forms/assets/clientlib-it-custom-locale-paste.png)


### Cree un archivo para la nueva configuración regional:

1. Vaya al directorio de configuración regional:

   Dentro de su `[AEMaaCS project directory]`, vaya a la siguiente ruta:

   ```
       /ui.apps/src/main/content/jcr_root/apps/<program-id>/clientlibs/clientlib-it-custom-locale/resources/i18n/
   ```

   **Importante**: Reemplazar `<program-id>` con su ID de aplicación real.

1. Busque el archivo de ejemplo en inglés:

   AEM Forms proporciona un [archivo de configuración regional de ejemplo en inglés (.json) en GitHub](https://github.com/adobe/aem-core-forms-components/blob/master/ui.af.apps/src/main/content/jcr_root/apps/core/fd/af-clientlibs/core-forms-components-runtime-all/resources/i18n/en.json).

   El archivo en inglés incluye el conjunto predeterminado de cadenas para referencia. El archivo específico de la configuración regional debe imitar la estructura del archivo en inglés.

   En idiomas como el árabe, el hebreo y el persa, el texto se lee de derecha a izquierda (RTL) en lugar de izquierda a derecha (LTR) como el inglés. Para garantizar que los formularios se muestren correctamente en estos idiomas, se recomienda utilizar nuestros archivos de configuración regional de ejemplo como guía. Estos archivos proporcionan una referencia sobre cómo dar formato al texto, las fechas y otros elementos para los idiomas RTL. Puede encontrar los archivos de configuración regional de ejemplo para:

   * [Árabe](/help/forms/assets/ar-ae.json)
   * [Hebreo](/help/forms/assets/he.json)
   * [Farsi](/help/forms/assets/fa.json)

   Al aprovechar estos archivos de ejemplo, puede asegurarse de que los formularios proporcionen una experiencia perfecta a los usuarios que trabajan en idiomas RTL.


1. Cree su archivo de configuración regional:

   1. Cree un nuevo archivo .json dentro de `i18n` directorio.
   1. Asigne un nombre al archivo utilizando el código de configuración regional adecuado para el idioma deseado (por ejemplo, fr-FR.json para francés y ar-ae.json para árabe). La estructura de este archivo debe reflejar el archivo de configuración regional en inglés.


1. Estructura y traducción:

   1. Abra el archivo recién creado en un editor de texto.

   1. Reemplace los valores en inglés con las traducciones correspondientes para su idioma de destino.

   1. Una vez que haya terminado de traducir las cadenas, guarde el archivo.




### Agregar compatibilidad con la configuración regional al diccionario

Este paso se aplica solo a las configuraciones regionales que no sean las siguientes comúnmente admitidas: inglés (en), alemán (de), español (es), francés (fr), italiano (it), portugués brasileño (pt-br), chino (simplificado - zh_cn), chino (tradicional - zh_tw), japonés (ja) y coreano (ko_kr).

1. Busque la carpeta de configuración:

   Navegue hasta el siguiente directorio en su [Directorio del proyecto AEMaaCS]:

   ```
   /ui.content/src/main/content/jcr_root/etc
   ```

1. Cree las carpetas necesarias (si falta):

   Si la variable `etc` la carpeta no existe en `jcr_root` carpeta, créela. Interior `etc`, cree otra carpeta llamada `languages` si falta...

1. Cree el archivo de configuración regional:

   Dentro de `languages` carpeta, cree un nuevo archivo llamado `.content.xml`. No copie y pegue el nombre del archivo de este documento, sino que escriba manualmente el nombre.

   ![cree un nuevo archivo llamado `.content.xml`](etc-content-xml.png)

   Abra este archivo y pegue el siguiente contenido: [LOCALE_CODE] con el código de configuración regional real (por ejemplo, ar-ae para árabe).


   ```XML
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:nt="http://www.jcp.org/jcr/nt/1.0"
         jcr:primaryType="nt:unstructured"
         languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi]"/>
   ```

   ADVERTENCIA: No reemplace la lista existente. En su lugar, anexe el nuevo código de configuración regional entre corchetes, separados por comas, de esta manera (utilizando ar-ae como ejemplo):

   ```XML
   languages="[de,es,fr,it,pt-br,zh-cn,zh-tw,ja,ko-kr,hi,ar-ae]"
   ```

1. Incluya las carpetas nuevas en filter.xml:

   Vaya a `/ui.content/src/main/content/meta-inf/vault/filter.xml` archivo en su [Directorio del proyecto AEMaaCS].

   Abra el archivo y añada la línea siguiente al final:

   ```
   <filter root="/etc/languages"/>
   ```

   ![Añada las carpetas creadas en `filter.xml` dentro de `/ui.content/src/main/content/meta-inf/vault/filter.xml`](langauge-filter.png)

1. Guarde el archivo.

### AEM Implemente la configuración regional recién creada en su entorno de

Ya está todo configurado para utilizar la nueva configuración regional con su Forms adaptable. Puede

* AEM Implementar el as a Cloud Service de la, [Directorio del proyecto AEMaaCS], en el entorno de desarrollo local para probar la nueva configuración regional en el equipo local. Para implementar en el entorno de desarrollo local:

   1. Asegúrese de que su entorno de desarrollo local esté en funcionamiento. Si aún no ha configurado un entorno de desarrollo local, consulte la guía de [Configuración del entorno de desarrollo local para AEM Forms](/help/forms/setup-local-development-environment.md).

   1. Abra la ventana de terminal o el símbolo del sistema.

   1. Vaya a [Directorio del proyecto AEMaaCS]

   1. Ejecute el siguiente comando:

      ```
      mvn -PautoInstallPackage clean install
      ```

* AEM Implementar el as a Cloud Service de la, [Directorio del proyecto AEMaaCS], a su entorno de Cloud Service. Para implementar en el entorno de Cloud Service:

   1. Confirme los cambios:

      Después de agregar la nueva configuración regional, confirme los cambios con un mensaje Git claro que describa la adición de configuración regional (por ejemplo, &quot;Se ha agregado compatibilidad con [Nombre de configuración regional]&quot;).

   1. Implemente el código actualizado:

      Déclencheur de una implementación del código a través de [canalización de pila completa existente](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline). Esto crea e implementa automáticamente el código actualizado con la nueva compatibilidad con configuración regional.

      Si aún no ha configurado una canalización, consulte la guía de [cómo configurar una canalización para AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=es#setup-pipeline).


## Vista previa de un formulario adaptable con la configuración regional recién agregada

Estos pasos le guían a través de la previsualización de un formulario adaptable con la configuración regional recién agregada:

1. Inicie sesión en la instancia as a Cloud Service de AEM Forms.
1. Vaya a **Formularios** > **Formularios y documentos**.
1. Seleccione un formulario adaptable y haga clic en **Agregar diccionario** y aparecerá el asistente **Agregar diccionario al proyecto de traducción**.
1. Especifique el **Título del proyecto** y seleccione los **Idiomas de destino** en el menú desplegable del asistente **Agregar diccionario al proyecto de traducción**.
1. Haga clic en **Listo** y ejecute el proyecto de traducción creado.
1. Vaya a **Formularios** > **Formularios y documentos**.
1. Seleccione el formulario adaptable y elija el **Vista previa como HTML** opción.
1. Añadir `&afAcceptLang=<locale-name>` Vaya a la URL de vista previa y pulse la tecla retorno. Reemplazar `<locale-name>` con su código de configuración regional real. El formulario adaptable se muestra en la configuración regional especificada.

## Prácticas recomendadas para la compatibilidad con localización nueva {#best-practices}

* El Adobe recomienda crear un proyecto de traducción después de crear un formulario adaptable. Esto optimiza el proceso de localización.


* Gestión de nuevos campos:

   * **Traducción automática**: si utiliza la traducción automática, debe volver a crear el diccionario y volver a crear el[ejecutar el proyecto de traducción](/help/forms/using-aem-translation-workflow-to-localize-adaptive-forms-core-components.md) después de agregar campos nuevos a un formulario adaptable existente. Los nuevos campos añadidos después del proyecto de traducción inicial permanecen sin traducir.

   * **Traducción humana**: para flujos de trabajo de traducción humana, exporte el diccionario mediante la interfaz de usuario en `[AEM Forms Server]/libs/cq/i18n/gui/translator.html`. Actualice el diccionario de los nuevos campos y cargue la versión revisada.


## Ver también {#see-also}

{{see-also}}

* [Generar documento de registro para Formularios adaptables](/help/forms/generate-document-of-record-core-components.md)
* [Agregar un formulario adaptable a una página de AEM Sites o a un fragmento de experiencia](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)

