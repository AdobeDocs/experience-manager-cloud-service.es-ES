---
title: Introducción a Forms as a Cloud Service Communications
description: Combine datos automáticamente con plantillas XDP y PDF o genere resultados en los formatos PCL, ZPL y PostScript
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: fcde70f424d8e798469563397ba091547163bd77
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# Usar comunicaciones as a Cloud Service de AEM Forms {#frequently-asked-questions}

**Las API de manipulación de documentos de AEM Forms as a Cloud Service Communications están en fase beta y pueden cambiar significativamente antes de su lanzamiento real.**

La funcionalidad de comunicaciones le ayuda a crear documentos estandarizados, personalizados y aprobados por la marca, como correspondencia comercial, declaraciones, cartas de procesamiento de reclamaciones, avisos de beneficios, facturas mensuales o kits de bienvenida. La capacidad proporciona API para generar y manipular documentos. Puede generar o manipular un documento bajo demanda o crear un trabajo por lotes para generar varios documentos a intervalos definidos. Las API de comunicación proporcionan:

* Funciones de generación de documentación por lotes y bajo demanda optimizadas.

* Combine, reorganice y aumente los documentos del PDF y XDP y obtenga información sobre los documentos del PDF

* API HTTP para facilitar la integración con sistemas externos. Se incluyen API independientes para operaciones bajo demanda (baja latencia) y por lotes (operaciones de alto rendimiento). Hace que la generación de documentos sea una tarea eficaz.

* un acceso seguro a los datos. Las API de comunicaciones solo se conectan a datos de repositorios de datos designados por el cliente y acceden a ellos, por lo que no hacen copias locales de datos, lo que hace que las comunicaciones sean muy seguras.

![Un extracto de tarjeta de crédito de muestra](assets/statement.png)
Se puede crear un extracto de tarjeta de crédito mediante las API de comunicaciones. Este extracto de ejemplo utiliza la misma plantilla pero datos independientes para cada cliente según su uso de tarjeta de crédito.

## ¿Cómo funciona?

Las comunicaciones utilizan [Plantillas PDF y XFA](#supported-document-types) con [Datos XML](#form-data) para generar un solo documento bajo demanda o varios documentos utilizando un trabajo por lotes a un intervalo definido.

Las API de comunicaciones ayudan a combinar una plantilla (XFA o PDF) con datos de clientes ([Datos XML](#form-data)) para generar documentos en formatos de PDF e impresión como PS, PCL, DPL, IPL y ZPL.

Normalmente, se crea una plantilla mediante [Designer](use-forms-designer.md) y utilice API de comunicaciones para combinar datos con la plantilla. La aplicación puede enviar el documento de salida a una impresora de red, una impresora local o a un sistema de almacenamiento para su archivo. Los flujos de trabajo personalizados y típicos de fuera de la caja tienen el siguiente aspecto:

![Flujo de trabajo de comunicaciones](assets/communicaions-workflow.png)

Según el caso de uso, también puede hacer que estos documentos estén disponibles para su descarga a través de su sitio web o un servidor de almacenamiento.

## API de comunicación

Las comunicaciones proporcionan API de HTTP para la generación de documentos por lotes y bajo demanda:

* **[API sincrónicas](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/)** son adecuados para escenarios de generación de documentos bajo demanda, baja latencia y de registro único. Estas API son más adecuadas para casos de uso basados en acciones del usuario. Por ejemplo, la generación de un documento después de que un usuario complete la cumplimentación de un formulario.

* **[API por lotes (API asíncronas)](https://www.adobe.io/experience-manager-forms-cloud-service-developer-reference/)** son adecuados para escenarios programados, de alto rendimiento y de generación de documentos múltiples. Estas API generan documentos por lotes. Por ejemplo, facturas telefónicas, extractos de tarjetas de crédito y extractos de beneficios generados cada mes.

Algunos de los principales usos de las API de comunicación son:

### Creación de documentos de PDF {#create-pdf-documents}

Puede utilizar las API de generación de documentos para crear un documento PDF basado en un diseño de formulario y datos de formulario XML. El resultado es un documento de PDF no interactivo. Es decir, los usuarios no pueden introducir ni modificar datos del formulario. Un flujo de trabajo básico es combinar datos de formulario XML con un diseño de formulario para crear un documento PDF. La siguiente ilustración muestra la combinación de un diseño de formulario y datos de formulario XML para producir un documento PDF.

![Crear documentos de PDF](assets/outPutPDF_popup.png)

### Crear documento PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) {#create-PS-PCL-ZPL-documents}

Puede utilizar las API de generación de documentos para crear un documento PostScript (PS), Printer Command Language (PCL) y Zebra Printing Language (ZPL) basado en un diseño de formulario XDP o un documento PDF. Estas API ayudan a combinar un diseño de formulario con datos de formulario para generar un documento. Puede guardar el documento en un archivo y desarrollar un proceso personalizado para enviarlo a una impresora.

<!-- ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.

 -->

### Procesamiento de datos por lotes para crear varios documentos {#processing-batch-data-to-create-multiple-documents}

Puede utilizar las API de generación de documentos para crear documentos independientes para cada registro dentro de un origen de datos por lotes XML. Puede generar documentos en modo masivo y asincrónico. Puede configurar varios parámetros para la conversión y luego iniciar el proceso por lotes. <!-- You can can also create a single document that contains all records (this functionality is the default).  Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents. -->

<!-- The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents. -->

### Acoplar documentos PDF interactivos {#flatten-interactive-pdf-documents}

Puede utilizar las API de generación de documentos para transformar un documento PDF interactivo (por ejemplo, un formulario) en un documento PDF no interactivo. Un documento PDF interactivo permite a los usuarios introducir o modificar datos ubicados en los campos del documento PDF. El proceso de transformar un documento de PDF interactivo en un documento de PDF no interactivo se denomina aplanamiento. Cuando se aplana un documento PDF, un usuario no puede modificar los datos ubicados en los campos del documento. Una razón para acoplar un documento PDF es garantizar que no se puedan modificar los datos.

Puede acoplar los siguientes tipos de documentos PDF:

* Documentos de PDF interactivo creados en Designer (que contienen flujos XFA).

* PDF forms de Acrobat

Si intenta acoplar un documento PDF no interactivo, se producirá una excepción.

### Mantener estado del formulario {#retain-form-state}

Un documento PDF interactivo contiene varios elementos que constituyen un formulario. Estos elementos pueden incluir campos (para aceptar o mostrar datos), botones (para realizar sucesos de déclencheur) y secuencias de comandos (comandos para realizar una acción específica). Al hacer clic en un botón, puede generarse un déclencheur con un evento que cambia el estado de un campo. Por ejemplo, si se elige una opción de género, puede cambiar el color de un campo o el aspecto del formulario. Este es un ejemplo de un suceso manual que provoca que cambie el estado del formulario.

Cuando un documento PDF interactivo de este tipo se acopla con las API de comunicaciones, el estado del formulario no se conserva. Para asegurarse de que el estado del formulario se conserva incluso después de que se acopla, defina el valor booleano _keepFormState_ como True para guardar y conservar el estado del formulario.

### Montaje de documentos de PDF

Puede utilizar las API de fabricación de documentos para ensamblar dos o más documentos PDF en un único documento PDF o Portfolio PDF. También puede aplicar funciones al documento del PDF que ayuden a la navegación o mejoren la seguridad. A continuación se indican algunas formas de ensamblar documentos PDF:

* Montaje de un documento PDF sencillo
* Creación de un Portfolio de PDF
* Montaje de documentos cifrados
* Montaje de documentos utilizando la numeración Bates
* Acoplar y ensamblar documentos

### Desmontar documentos del PDF

Puede utilizar las API de fabricación de documentos para desmontar un documento PDF. El servicio puede extraer páginas del documento de origen o dividir un documento de origen basado en marcadores. Normalmente, esta tarea resulta útil si el documento del PDF se creó originalmente a partir de muchos documentos individuales, como una colección de instrucciones.

* Extraer páginas de un documento de origen
* Dividir un documento de origen basado en marcadores

### Conversión y validación de documentos compatibles con el PDF/A

Puede utilizar las API de fabricación de documentos para convertir un documento PDF a una versión compatible con el PDF/A y para determinar si un documento PDF es compatible con el PDF/A. PDF/A es un formato de archivo diseñado para la preservación a largo plazo del contenido del documento. Las fuentes están incrustadas en el documento y el archivo no está comprimido. Como resultado, un documento PDF/A suele ser más grande que un documento PDF estándar. Además, un documento PDF/A no contiene contenido de audio y vídeo.

## Incorporación

Las comunicaciones están disponibles como módulo independiente y de complemento para los usuarios as a Cloud Service de Forms. Puede ponerse en contacto con el equipo de ventas de Adobes o con su representante de Adobes para solicitar acceso. Adobe posibilita el acceso a su organización y otorga los pertinentes privilegios a la persona de su organización designada como administrador. El administrador puede conceder acceso a los desarrolladores (usuarios) de AEM Forms de su organización para que utilicen las API.

Después de la confirmación, para habilitar las comunicaciones para su entorno as a Cloud Service de Forms:

1. Inicie sesión en Cloud Manager y abra la instancia as a Cloud Service de AEM Forms.

1. Abra la opción Editar programa , vaya a la pestaña Soluciones y complementos y seleccione la opción **[!UICONTROL Forms: comunicaciones]** .

   ![Comunicaciones](assets/communications.png)

   Si ya ha habilitado la variable **[!UICONTROL Forms: inscripción digital]** y, a continuación, seleccione **[!UICONTROL Forms: complemento de comunicaciones]** .

   ![Addon](assets/add-on.png)

1. Haga clic en **[!UICONTROL Actualizar]**.

1. Ejecute la canalización de compilación.

Una vez que la canalización de compilación se haya realizado correctamente, las API de comunicación se habilitan para su entorno.


<!--

Communication help you combine a template and XML data to generate print documents in various formats. The service allows you to generate documents in synchronous and batch modes. The APIs enables you to create applications that let you:

  * Generate documents by populating template files (PDF and XDP) with XML data.
  * Generate output forms in various formats, including non-interactive PDF print streams.

Consider a scenario where you have one or more templates and multiple records of XML data for each template. You can use Communications APIs to generate a print document for each record.  You can also combine the records into a single document.  The result is a non-interactive PDF document. A non-interactive PDF document does not let users enter data into its fields.

 There are two main Communications APIs. The _generatePDFOutput_ generates PDFs, while the _generatePrintedOutput_ generates PostScript, ZPL, and PCL formats. These APIs are available as REST endpoints on your environment, both on author and publish instances. Since the publish instances are configured to scale faster than the author instances, it is recommended use these APIs via publish instances.

The first parameter of both the operations accept the path and name of the template file (for example ExpenseClaim.xdp). You can specify a fully qualified path, reference path of your AEM Repository, or path of a binary file. The second parameter accepts an XML document that is merged with the template while generating the output document.  

The [API reference documentation](https://documentcloud.adobe.com/link/track?uri=urn:aaid:scds:US:b1223732-ae0f-4921-bdc0-c31e48b56044) provides detailed information about all the parameters, authentication methods, and various services provided by APIs. The API reference documentation is also available in the .yaml format. You can download the .yaml for [Batch APIs](assets/batch-api.yaml) or [non-Batch API.yaml](assets/non-batch-api.yaml) file and upload it to postman to check functionality of APIs.

>[!VIDEO](https://video.tv.adobe.com/v/335771)

Uploading Communication APIs .yaml file to postman to check functionality of APIs.

## Using the Communications APIs {#workflows}

Typically, you create a template using [Designer](use-forms-designer.md) and use communications APIs ( generatePDFOutput and generatePrintedOutput) to:

* Convert these templates to various formats, including PDF, PostScript, ZPL, and PCL.
* Merge XML form data with a form design to generate a document.
* Generate a document without merging XML form data into the document. However, the primary workflow is merging data into the document.

Then, the output document is stored to a file. You can design custom workflows to send the file to a network printer, a local printer, or to a storage system for archival. A typical out of the box and custom workflows look like the following:

![Communications Workflow](assets/communicaions-workflow.png)

### Create PDF documents {#create-pdf-documents}

You can use the _generatePDFOutput_ API to create PDF document that is based on a form design and XML form data. The output is a non-interactive PDF document. That is, users cannot enter or modify form data. A basic workflow is to merge XML form data with a form design to create a PDF document. The following illustration shows the merging of a form design and XML form data to produce a PDF document.

![Create PDF Documents](assets/outPutPDF_popup.png)

### Create PostScript (PS), Printer Command Language (PCL), Zebra Printing Language (ZPL) document {#create-PS-PCL-ZPL-documents}

You can use Communications APIs to create PostScript (PS), Printer Command Language (PCL), and Zebra Printing Language (ZPL) document that are based on a XDP form design or PDF document. The _generatePrintedOutput_ API merges a form design with form data to generate a document. You can save the document to a file and develop a custom process to send it to a printer.

 ### Processing batch data to create multiple documents

Communications APIs can create separate documents for each record within an XML batch data source. The APIs can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you instruct the APIs to create a separate document for each record (for example, PDF documents). As a result, the APIs generate ten PDF documents.

The following illustration also shows Communications APIs processing an XML data file that contains multiple records. However, assume that you instruct the APIs to create a single PDF document that contains all data records. In this situation, the APIs generate one document that contains all of the records.

The following illustration shows Communications APIs processing an XML data file that contains multiple records. Assume that you instruct the Communications APIs to create a separate PDF document for each data record. In this situation, the APIs generates a separate PDF document for each data record.



### Processing batch data to create multiple documents {#processing-batch-data-to-create-multiple-documents}

You create separate documents for each record within an XML batch data source. You can can also create a single document that contains all records (this functionality is the default). Assume that an XML data source contains ten records and you have a requirement to create a separate document for each record (for example, PDF documents). You can use the Communication APIs to generate ten PDF documents.

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. However, assume that you instruct the Communication APIs to create a single PDF document that contains all data records. In this situation, the Communication APIs generate one document that contains all of the records.

![Create PDF Documents](assets/ou_OutputBatchSingle_popup.png)

The following illustration shows the Communication APIs processing an XML data file that contains multiple records. Assume that you instruct the Communication APIs to create a separate PDF document for each data record. In this situation, the Communication APIs generates a separate PDF document for each data record.

![Create PDF Documents](assets/ou_OutputBatchMany_popup.png)

For detailed information on using Batch APIs, see Communication APIs: Processing batch data to create multiple documents.

### Flatten interactive PDF documents {#flatten-interactive-pdf-documents}

You can use the Communications APIs to transform an interactive PDF document (for example, a form) to a non-interactive PDF document. An interactive PDF document lets users enter or modify data located in the PDF document fields. The process of transforming an interactive PDF document to a non-interactive PDF document is called flattening. When a PDF document is flattened, a user cannot modify the data located in the document’s fields. One reason to flatten a PDF document is to ensure that data cannot be modified.

You can flatten the following types of PDF documents:

* Interactive PDF documents created in Designer (that contain XFA streams).

* Acrobat PDF forms

If you attempt to flatten a non-interactive PDF document, an exception occurs.

### Retain Form State {#retain-form-state}

An interactive PDF document contains various elements that constitute a form. These elements may include fields (to accept or display data), buttons (to trigger events), and scripts (commands to perform a specific action). Clicking a button may trigger an event that changes the state of a field. For example, choosing a gender option may change the color of a field or the appearance of the form. This is an example of a manual event causing the form state to change.

When such an interactive PDF document is flattened using the Communications APIs, the state of the form is not retained. To ensure that the state of the form is retained even after the form is flattened, set the Boolean value _retainFormState_ to True to save and retain the state of the form.  -->
