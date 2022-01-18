---
title: Introducción a Forms as a Cloud Service Communications
description: Combine datos automáticamente con plantillas XDP y PDF o genere resultados en los formatos PCL, ZPL y PostScript
exl-id: b6f05b2f-5665-4992-8689-d566351d54f1
source-git-commit: 8e20383a03f157f01da66bab930a3eccf674dde7
workflow-type: tm+mt
source-wordcount: '1840'
ht-degree: 1%

---

# Usar comunicaciones as a Cloud Service de AEM Forms {#frequently-asked-questions}

**La función Comunicaciones as a Cloud Service de AEM Forms está en versión beta.**

La funcionalidad de comunicaciones le ayuda a crear documentos estandarizados, personalizados y orientados a la marca, como correspondencia comercial, declaraciones, cartas de procesamiento de reclamaciones, avisos de beneficios, facturas mensuales o kits de bienvenida.


Puede generar un documento bajo demanda o crear un trabajo por lotes para generar varios documentos a intervalos definidos. Las API de comunicación proporcionan:

* funciones de generación de documentación por lotes y bajo demanda optimizadas

* proporcionar API de HTTP para una integración más sencilla con los sistemas existentes

* un acceso seguro a los datos. Las API de comunicaciones solo se conectan a datos de repositorios de datos designados por el cliente y acceden a ellos, por lo que no hacen copias locales de datos, lo que hace que las comunicaciones sean muy seguras.

* separe las API para operaciones de baja latencia y alto rendimiento, lo que convierte la generación de documentos en una tarea eficiente.

![Un extracto de tarjeta de crédito de muestra](assets/statement.png)

## ¿Cómo funciona?

Las comunicaciones utilizan [Plantillas PDF y XFA](#supported-document-types) con [Datos XML](#form-data) para generar un solo documento bajo demanda o varios documentos utilizando un trabajo por lotes a un intervalo definido.

Una API de comunicaciones ayuda a combinar una plantilla (XFA o PDF) con datos de clientes ([Datos XML](#form-data)) para generar documentos en formatos de PDF e impresión como PS, PCL, DPL, IPL y ZPL.

Normalmente, se crea una plantilla mediante [Designer](use-forms-designer.md) y utilice API de comunicaciones para combinar datos con la plantilla. La aplicación puede enviar el documento de salida a una impresora de red, una impresora local o a un sistema de almacenamiento para su archivo. Los flujos de trabajo personalizados y típicos de fuera de la caja tienen el siguiente aspecto:

![Flujo de trabajo de comunicaciones](assets/communicaions-workflow.png)

Según el caso de uso, también puede hacer que estos documentos estén disponibles para su descarga a través de su sitio web o un servidor de almacenamiento.

## API de comunicación

Las comunicaciones proporcionan API de HTTP para la generación de documentos por lotes y bajo demanda:

* **[API sincrónicas](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/sync/)** son adecuados para escenarios de generación de documentos bajo demanda, baja latencia y de registro único. Estas API son más adecuadas para casos de uso basados en acciones del usuario. Por ejemplo, la generación de un documento después de que un usuario complete la cumplimentación de un formulario.

* **[API por lotes (API asíncronas)](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/api/batch/)** son adecuados para escenarios programados, de alto rendimiento y de generación de documentos múltiples. Estas API generan documentos por lotes. Por ejemplo, facturas telefónicas, extractos de tarjetas de crédito y extractos de beneficios generados cada mes.

## Incorporación

Las comunicaciones están disponibles como módulo independiente y de complemento para los usuarios as a Cloud Service de Forms. Puede ponerse en contacto con el equipo de ventas de Adobes o con su representante de Adobes para solicitar acceso.

Adobe posibilita el acceso a su organización y otorga los pertinentes privilegios a la persona de su organización designada como administrador. El administrador puede conceder acceso a los desarrolladores (usuarios) de AEM Forms de su organización para que utilicen las API.

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

## Consideraciones {#considerations-for-communications-apis}

Antes de empezar a generar documentos mediante API de comunicación, tenga en cuenta lo siguiente:

### Datos de formulario {#form-data}

Las API de comunicaciones aceptan un diseño de formulario que normalmente se crea en [Designer](use-forms-designer.md) y datos de formulario XML como entrada. Para rellenar un documento con datos, debe existir un elemento XML en los datos del formulario XML para cada campo de formulario que desee rellenar. El nombre del elemento XML debe coincidir con el nombre del campo. Se ignora un elemento XML si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML. El factor importante es que los elementos XML se especifican con los valores correspondientes.

Consideremos el siguiente ejemplo de formulario de solicitud de préstamo:

![Formulario de solicitud de préstamo](assets/loanFormData.png)

Para combinar datos en este diseño de formulario, cree un origen de datos XML que corresponda al formulario. El siguiente XML representa un origen de datos XML que corresponde al formulario de aplicación hipotecaria de ejemplo.

```XML
<?xml version="1.0" encoding="UTF-8" ?>
* <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
* <xfa:data>
* <data>
    * <Layer>
        <closeDate>1/26/2007</closeDate>
        <lastName>Johnson</lastName>
        <firstName>Jerry</firstName>
        <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
        <city>New York</city>
        <zipCode>00501</zipCode>
        <state>NY</state>
        <dateBirth>26/08/1973</dateBirth>
        <middleInitials>D</middleInitials>
        <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
        <phoneNumber>5555550000</phoneNumber>
    </Layer>
    * <Mortgage>
        <mortgageAmount>295000.00</mortgageAmount>
        <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
        <purchasePrice>300000</purchasePrice>
        <downPayment>5000</downPayment>
        <term>25</term>
        <interestRate>5.00</interestRate>
    </Mortgage>
</data>
</xfa:data>
</xfa:datasets>
```

### Tipos de documentos compatibles {#supported-document-types}

Para acceder completamente a las funciones de renderización de las API de comunicaciones, se recomienda utilizar un archivo XDP como entrada. A veces, se puede utilizar un archivo PDF. Sin embargo, el uso de un archivo PDF como entrada tiene las siguientes limitaciones:

Un documento PDF que no contiene un flujo XFA no se puede representar como PostScript, PCL o ZPL. Las API de comunicaciones pueden procesar documentos PDF con flujos XFA (es decir, formularios creados en [Designer](use-forms-designer.md)) en formatos láser y de etiqueta. Si el documento del PDF está firmado, certificado o contiene derechos de uso (aplicados mediante el servicio AEM Forms Reader Extensions), no se puede procesar en estos formatos de impresión.

<!-- Run-time options such as PDF version and tagged PDF are not supported for Acrobat forms. They are valid for PDF forms that contain XFA streams; however, these forms cannot be signed or certified. 

### Email support {#email-support}

For email functionality, you can create a process in Experience Manager Workflows that uses the Email Step. A workflow represents a business process that you are automating. -->

### Áreas imprimibles {#printable-areas}

El margen no imprimible predeterminado de 0,25 pulgadas no es exacto para impresoras de etiquetas y varía de impresora a impresora y de tamaño de etiqueta a tamaño de etiqueta. Se recomienda mantener el margen de 0,25 pulgadas o reducirlo. Sin embargo, se recomienda no aumentar el margen no imprimible. De lo contrario, la información del área imprimible no se imprime correctamente.

Asegúrese siempre de utilizar el archivo XDC correcto para la impresora. Por ejemplo, evite elegir un archivo XDC para una impresora de 300 ppp y envíe el documento a una impresora de 200 ppp.

### Scripts {#scripts}

Un diseño de formulario que se utiliza con las API de comunicaciones puede contener secuencias de comandos que se ejecutan en el servidor. Asegúrese de que el diseño de formulario no contenga secuencias de comandos que se ejecuten en el cliente. Para obtener información sobre la creación de secuencias de comandos de diseño de formulario, consulte [Ayuda de Designer](use-forms-designer.md).

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### Asignación de fuentes {#font-mapping}

Para diseñar un formulario que utilice fuentes residentes en la impresora, elija un nombre de tipo de letra en Designer que coincida con las fuentes disponibles en la impresora. Una lista de fuentes compatibles con PCL o PostScript se encuentra en los perfiles de dispositivo correspondientes (archivos XDC). Alternativamente, se puede crear una asignación de fuentes para asignar fuentes no residentes en la impresora a fuentes residentes en la impresora con un nombre de tipo de letra diferente. Por ejemplo, en un escenario PostScript, las referencias a la fuente Arial® se pueden asignar a la fuente Helvetica® residente en la impresora.

Si una fuente está instalada en un equipo cliente, está disponible en la lista desplegable de Designer. Si la fuente no está instalada, es necesario especificar el nombre de la fuente manualmente. La opción &quot;Reemplazar permanentemente fuentes no disponibles&quot; de Designer puede estar desactivada. De lo contrario, cuando el archivo XDP se guarda en Designer, el nombre de la fuente de sustitución se escribe en el archivo XDP. Significa que no se utiliza la fuente residente en la impresora.

Existen dos tipos de fuentes OpenType®. Un tipo es una fuente TrueType OpenType® compatible con PCL. El otro es CFF OpenType®. La salida de PDF y PostScript admite fuentes Type-1, TrueType y OpenType® incrustadas. La salida PCL admite fuentes TrueType incrustadas.

Las fuentes Type-1 y OpenType® no están incrustadas en la salida PCL. El contenido con formato Type-1 y OpenType® se rasteriza y genera como imagen de mapa de bits que puede ser grande y lento de generar.

Las fuentes descargadas o incrustadas se sustituyen automáticamente al generar salida PostScript, PCL o PDF. Significa que solo el subconjunto de los glifos de fuente que son necesarios para procesar correctamente el documento generado se incluye en la salida generada.

### Uso de archivos de perfil de dispositivo (archivo XDC) {#working-with-xdc-files}

Un perfil de dispositivo (archivo XDC) es un archivo de descripción de impresora en formato XML. Este archivo permite que las API de comunicaciones emitan documentos como formatos de impresora láser o de etiquetas. Las API de comunicaciones utilizan los archivos XDC, que incluyen lo siguiente:

* hppcl5c.xdc

* hppcl5e.xdc

* ps_plain_level3.xdc

* ps_plain.xdc

* zpl300.xdc

* zpl600.xdc

* zpl300.xdc

* ipl300.xdc

* ipl400.xdc

* tpcl600.xdc

* dpl300.xdc

* dpl406.xdc

* dpl600.xdc

Puede utilizar los archivos XDC proporcionados para generar documentos de impresión o modificarlos según sus necesidades.
&lt;!-* No es necesario modificar estos archivos para crear documentos. Sin embargo, puede modificarlas para satisfacer los requisitos empresariales. —>

Estos archivos son archivos XDC de referencia que admiten las características de impresoras específicas, como fuentes residentes, bandejas de papel y grapadora. El propósito de estas referencias es ayudarle a comprender cómo configurar sus propias impresoras mediante perfiles de dispositivo. La referencia también es un punto de partida para impresoras similares en la misma línea de productos.

### Uso del archivo de configuración XCI {#working-with-xci-files}

Las API de comunicaciones utilizan un archivo de configuración XCI para realizar tareas, como controlar si la salida es un solo panel o una paginación. Aunque este archivo contiene opciones que se pueden configurar, no es habitual modificar este valor. <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

Puede pasar un archivo XCI modificado mientras utiliza una API de comunicaciones. Al hacerlo, cree una copia del archivo predeterminado, cambie solo los valores que requieran modificación para satisfacer los requisitos comerciales y utilice el archivo XCI modificado.

Las API de comunicaciones empiezan con el archivo XCI predeterminado (o el archivo modificado). A continuación, aplica los valores especificados mediante las API de comunicaciones. Estos valores anulan la configuración de XCI.

La siguiente tabla especifica las opciones XCI.

| Opción XCI | Descripción |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config/actual/pdf/creator | Identifica al creador del documento mediante la entrada Creador del diccionario de información del documento. Para obtener información sobre este diccionario, consulte la guía de referencia del PDF. |
| config/actual/pdf/production | Identifica al productor del documento mediante la entrada Producer del diccionario de información del documento. Para obtener información sobre este diccionario, consulte la guía de referencia del PDF. |
| config/current/layout | Controla si la salida es un solo panel o paginado. |
| config/current/pdf/compression/level | Especifica el grado de compresión que se utilizará al generar un documento de PDF. |
| config/current/pdf/scriptModel | Controla si la información específica de XFA se incluye en el documento del PDF de salida. |
| config/current/common/data/adaptData | Controla si la aplicación XFA ajusta los datos después de la combinación. |
| config/actual/pdf/renderPolicy | Controla si la generación del contenido de la página se realiza en el servidor o se diferye al cliente. |
| config/current/common/locale | Especifica la configuración regional predeterminada utilizada en el documento de salida. |
| config/current/destination | Cuando está contenido en un elemento presente, especifica el formato de salida. Cuando está contenido en un elemento openAction, especifica la acción que se debe realizar al abrir el documento en un cliente interactivo. |
| config/current/output/type | Especifica el tipo de compresión que se aplicará a un archivo o el tipo de salida que se producirá. |
| config/current/common/temp/uri | Especifica el URI del formulario. |
| config/current/common/template/base | Proporciona una ubicación base para URIs en el diseño de formulario. Cuando este elemento está ausente o vacío, se utiliza como base la ubicación del diseño de formulario. |
| config/current/common/log/to | Controla la ubicación en la que se escriben los datos de registro o los datos de salida. |
| config/current/output/to | Controla la ubicación en la que se escriben los datos de registro o los datos de salida. |
| config/current/script/currentPage | Especifica la página inicial cuando se abre el documento. |
| config/current/script/exclude | Notifica a las API de servidor/comunicaciones de AEM Forms qué eventos se deben ignorar. |
| config/actual/pdf/linearized | Controla si el documento del PDF de salida está linealizado. |
| config/current/script/runScripts | Controla qué conjunto de secuencias de comandos se ejecuta AEM Forms. |
| config/actual/pdf/tagged | Controla la inclusión de etiquetas en el documento del PDF de salida. Las etiquetas, en el contexto del PDF, son información adicional incluida en un documento para exponer la estructura lógica del documento. Las etiquetas ayudan a facilitar la accesibilidad y a cambiar el formato. Por ejemplo, un número de página puede etiquetarse como un artefacto para que un lector de pantalla no lo enuncie en medio del texto. Aunque las etiquetas hacen que un documento sea más útil, también aumentan el tamaño del documento y el tiempo de procesamiento para crearlo. |
| config/actual/pdf/version | Especifica la versión del documento de PDF que se va a generar. |
