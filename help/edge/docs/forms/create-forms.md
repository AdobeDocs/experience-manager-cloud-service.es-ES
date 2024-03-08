---
title: Introducción al servicio de entrega de AEM Forms Edge. Cree un formulario.
description: ¡Crea formas perfectas, rápido! ⚡ la creación basada en documentos de AEM Forms Edge Delivery = una velocidad increíble y formularios compatibles con SEO para usuarios y motores de búsqueda más felices.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 0cf881a2-3784-45eb-afe8-3435e5e95cf4
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# Crear un formulario mediante el bloque de formulario adaptable

En la era digital de hoy en día, la creación de formularios fáciles de usar es esencial para cualquier organización. AEM Forms Edge Delivery le permite crear formularios con herramientas conocidas, como documentos de Word o Google.

Estos formularios envían datos directamente a un archivo de Microsoft Excel o Google Sheets, lo que le permite utilizar un ecosistema dinámico y API sólidas de Google Sheets, Microsoft Excel y Microsoft Sharepoint para procesar fácilmente los datos enviados o iniciar un flujo de trabajo empresarial existente.

![Ecosistema de creación basado en documentos](/help/edge/assets/document-based-authoring-workflow-create-form.png)

AEM Forms Edge Delivery proporciona un bloque, conocido como bloque de formulario adaptable, para ayudarle a crear fácilmente formularios para capturar y almacenar los datos capturados. AEM Puede incluir el bloque de formulario adaptable en el proyecto de EDS de la para empezar a crear un formulario. Vamos a empezar:


## Requisitos previos

Antes de comenzar, asegúrese de haber completado los siguientes pasos:

* Configure el proyecto de GitHub de los Edge Delivery Services AEM (EDS) mediante una plantilla de plantillas y clone el repositorio de GitHub correspondiente en el equipo local. Consulte [tutorial para desarrolladores](https://www.aem.live/developer/tutorial) para obtener más información. En este documento, la carpeta local del proyecto de los Edge Delivery Services (EDS) se denomina `[EDS Project repository]` .
* Asegúrese de que tiene acceso a las hojas de Google o a Microsoft SharePoint. Para configurar Microsoft SharePoint como fuente de contenido, consulte [Cómo usar Sharepoint](https://www.aem.live/docs/setup-customer-sharepoint)



## Creación de un formulario

+++ Paso 1: Añadir el bloque de formulario adaptable al proyecto de Edge Delivery Services (EDS).

El formulario adaptable permite a los usuarios crear formularios para un sitio de servicios de envío de Edge. AEM Sin embargo, este bloque no se incluye en la plantilla de plantillas predeterminada de la (utilizada para crear un proyecto de Edge Delivery Services). Para integrar a la perfección el bloque de formulario adaptable en su proyecto de Edge Delivery Services:

1. **Clone el repositorio de bloque de formulario adaptable**: Clone el [Repositorio de bloques de formularios adaptables](https://github.com/adobe-rnd/form-block) en el equipo local. Contiene el código para procesar el formulario en una página web de EDS. En este documento, la carpeta local del repositorio de bloques de Forms se denomina `[Adaptive Form Block repository]`.
1. **Busque el repositorio de bloques de formularios adaptables:** Acceda a la [Repositorio de bloques de formularios adaptables]/blocks/src y copie su contenido.

1. en el equipo local y copie el `form` carpeta.
1. **Pegue el código del bloque de formulario adaptable en el proyecto EDS:**
Vaya a [Repositorio del proyecto EDS]/blocks/ en el equipo local y cree una carpeta &quot;form&quot;. Pegue el `[Adaptive Form Block repository]/blocks/src content`, copiado en el paso anterior a `[EDS Project repository]/blocks/form` carpeta.
1. **Confirmar cambios en GitHub:** Marque en `[EDS Project repository]/blocks/form` y sus archivos subyacentes al proyecto de Edge Delivery Services en GitHub.

Después de completar estos pasos, el bloque de formulario adaptable se agrega correctamente al repositorio del proyecto de los Edge Delivery Services (EDS) en GitHub. Ahora puede crear y agregar formularios a una página de Sites de EDS.


**Solución de problemas de compilación de GitHub**

Asegúrese de que el proceso de generación de GitHub sea fluido y aborde los posibles problemas:

* **Resolver error de ruta del módulo:**
Si aparece el error &quot;No se puede resolver la ruta al módulo &quot;&#39;../../scripts/lib-franklin.js&quot;&quot;, vaya al [Proyecto EDS]Archivo /blocks/forms/form.js. Actualice la instrucción import reemplazando el archivo lib-franklin.js por el archivo aem.js.

* **Controlar errores de vinculación:**
Si encuentra algún error de linting, puede evitarlo. Abra el [Proyecto EDS]/package.json y modifique el script &quot;lint&quot; de &quot;lint&quot;: &quot;npm run lint:js &amp;&amp; npm run lint:css&quot; a &quot;lint&quot;: &quot;echo &#39;omitiendo linting por ahora&#39;&quot;. Guarde el archivo y confirme los cambios en su proyecto de GitHub.

+++

+++ Paso 2: Crear un formulario con Microsoft Excel o Google Sheet.

En lugar de navegar por procesos complejos, la creación de un formulario se puede lograr fácilmente mediante una hoja de cálculo. Puede definir las filas y columnas que compondrán la estructura del formulario. Cada fila representa a un individuo [campo de formulario](/help/edge/docs/forms/form-components.md#available-components) y los encabezados de columna definen la correspondiente [propiedades de campo](/help/edge/docs/forms/form-components.md#components-properties).

Por ejemplo, vea la siguiente hoja de cálculo en la que las filas describen los campos de un `enquiry` los encabezados de formulario y columna definen sus propiedades:

![Hoja de consulta](/help/edge/assets/enquiry-form-spreadsheet.png)

Para continuar con la creación del formulario:

1. AEM Acceda a la carpeta del proyecto Entrega de Edge de la cuenta de la cuenta de usuario en Microsoft SharePoint o Google Drive.

1. Cree un libro de Microsoft Excel o una hoja de Google AEM en cualquier lugar dentro del directorio del proyecto de entrega perimetral de. Por ejemplo, cree una hoja de cálculo llamada `enquiry` AEM en el directorio de proyectos de entrega de Edge en Google Drive.

1. AEM Asegúrese de que la hoja se comparte con el usuario de la aplicación correspondiente (por ejemplo, un usuario de la aplicación). `helix@adobe.com`) [según las configuraciones especificadas para su proyecto](https://www.aem.live/docs/setup-customer-sharepoint). Conceder al usuario permiso de edición para la hoja.

1. Abra la hoja de cálculo creada y cambie el nombre de la hoja predeterminada a &quot;shared-default&quot;.

   ![cambiar el nombre de la hoja predeterminada por &quot;shared-default&quot;](/help/edge/assets/rename-sheet-to-shared-default.png)

1. Para agregar los campos del formulario, inserte filas y encabezados de columna en la hoja &#39;shared-default&#39;. Cada fila debe representar un [campo de formulario](/help/edge/docs/forms/form-components.md#available-components), con encabezados de columna que definen el campo correspondiente [propiedades](/help/edge/docs/forms/form-components.md#components-properties).

   Para empezar rápidamente, considere la posibilidad de copiar el contenido de la [Hoja de consulta](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0) en la hoja de cálculo. Después de copiar el contenido, guarde la hoja de cálculo.

   >[!VIDEO](https://video.tv.adobe.com/v/3427468?quality=12&learn=on)


1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para previsualizar la hoja.

   ![Usar el AEM Sidekick para obtener una vista previa de la hoja](/help/edge/assets/preview-form.png)

   Al obtener una vista previa, las nuevas pestañas del explorador muestran el contenido de la hoja en formato JSON. Asegúrese de capturar la URL de vista previa, ya que es necesaria para procesar el formulario en junto a la sección. El formato de la URL es el siguiente:


   ```JSON
       https://<branch>--<repository>--<owner>.hlx.live/<form-path>/<form-file-name>.json
   ```

   * `<branch>` hace referencia a la rama del repositorio de GitHub.
   * `<repository>` indica su repositorio de GitHub.
   * `<owner>` hace referencia al nombre de usuario de la cuenta de GitHub que aloja el repositorio de GitHub.

   Por ejemplo, si el repositorio del proyecto se llama &quot;portal&quot;, está ubicado en la cuenta &quot;wkndforms&quot; y está usando la rama &quot;principal&quot;, la dirección URL tiene el siguiente aspecto:

   `https://main--portal--wkndforms.hlx.page/enquiry.json`


+++

+++ Paso 3: Previsualizar el formulario mediante la página de Edge Delivery Services (EDS).


Hasta ahora, ha agregado el bloque de formulario adaptable al proyecto EDS y ha preparado la estructura del formulario. Ahora, para obtener una vista previa del formulario:

1. **Acceda al directorio de su proyecto:** Abra la cuenta de Microsoft SharePoint o Google AEM Drive y vaya al directorio del proyecto de entrega perimetral de la red de distribución de la red de.

1. **Incrustar el formulario en un documento:** Abra un archivo de documento (por ejemplo, un archivo de índice) para incrustar el formulario. También puede crear un nuevo documento.

1. **Vaya a la ubicación que desee:** Desplácese hasta la ubicación deseada dentro del documento donde desee agregar el formulario.

1. **Agregar el bloque de formulario adaptable:** Para crear un bloque de formulario para procesar el formulario. Seleccione Insertar > Tabla y cree una tabla de una columna y dos filas. Asigne un nombre a la tabla &quot;Form&quot; y pegue la dirección URL de vista previa en la segunda fila. Asegúrese de que la dirección URL tenga el formato de hipervínculo, no de texto sin formato, como se muestra a continuación:

   | Formulario |
   |---|
   | [https://main--portal--wkndforms.hlx.live/enquiry.json](https://main--portal--wkndforms.hlx.live/enquiry.json) |

   Este bloque sirve como marcador de posición donde está incrustado el formulario. En la segunda fila del bloque, añada la URL de vista previa de su `<form>.json` archivo como hipervínculo.

   >[!IMPORTANT]
   >
   >
   > Asegúrese de que la dirección URL tenga formato de hipervínculo en lugar de mostrarse como texto sin formato.


1. Uso [AEM Sidekick](https://www.aem.live/developer/tutorial#preview-and-publish-your-content) para obtener una vista previa del documento. La página ahora muestra el formulario. Por ejemplo, este es el formulario basado en [hoja de cálculo](https://docs.google.com/spreadsheets/d/196lukD028RDK_evBelkOonPxC7w0l_IiJ-Yx3DvMfNk/edit#gid=0):


   [![Formulario EDS de ejemplo](/help/edge/assets/eds-form.png)](https://main--portal--wkndforms.hlx.live/)

   Ahora, rellene el formulario y haga clic en el botón Enviar . Se producirá un error similar al siguiente, ya que la hoja de cálculo aún no está configurada para aceptar los datos.

   ![error al enviar el formulario](/help/edge/assets/form-error.png)

+++


## Siguiente paso

[Preparar hoja de cálculo](/help/edge/docs/forms/submit-forms.md) para empezar a aceptar datos al enviar el formulario.




