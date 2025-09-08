---
title: API facturables de informes de transacciones
description: Lista de todas las API que se contabilizan como transacciones
feature: Adaptive Forms, Foundation Components
exl-id: 6dfcac3e-5654-4b4f-9134-0cd8be24332e
role: Admin, Developer, User
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 100%

---


# API facturables de informes de transacciones {#transaction-reports-billable-apis}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/transaction-reports/transaction-reports-billable-apis) |
| AEM as a Cloud Service | Este artículo |


AEM Forms ofrece varias API para enviar formularios, procesar documentos y representar documentos. Algunas API se contabilizan como transacciones y otras se pueden usar libremente. Este documento proporciona una lista de todas las API que se contabilizan como transacciones en un informe de transacciones. Estos son algunos escenarios comunes en los que se utiliza un API facturable:

* Enviar un formulario adaptable
* Convertir un documento de un formato a otro
* Acoplar un documento PDF dinámico
* Generar un documento de registro (mediante el servicio de Forms o el servicio de salida)
* Combinar un documento PDF interactivo con otro PDF
* Uso del paso para asignar tarea y de los pasos de API de comunicación de los flujos de trabajo de AEM

Las API de facturación no tienen en cuenta el número de páginas, la longitud de un documento o formulario o el formato final del documento representado. Un informe de transacciones divide las transacciones en dos categorías: formularios enviados y documentos representados.

* **Formularios enviados:** cuando los datos se envían desde cualquier tipo de formulario creado con AEM Forms y los datos se envían a cualquier repositorio de almacenamiento de datos o base de datos, se considera envío de formulario. Por ejemplo, enviar un formulario adaptable o un conjunto de formularios se considera un formulario enviado. Por ejemplo, si un conjunto de formularios tiene cinco formularios, cuando se envía el conjunto de formularios, el servicio de informes de transacciones lo contabiliza como cinco envíos.

* **Documentos representados:** generar un documento mediante la combinación de una plantilla y datos, la firma o certificación digitalmente de un documento, el uso de las API de servicios de documentos facturables para servicios de documento o la conversión de un documento de un formato a otro se contabilizan como documentos representados.

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_submission_graph_en"
>title="Rastreador de envíos de formularios"
>abstract="Este gráfico representa el recuento de los envíos de formularios adaptables durante períodos de tiempo específicos. El aumento de los envíos podría indicar que el formulario está ganando popularidad o que es necesario recopilar más datos de los usuarios. **Nota:** El gráfico proporciona datos específicos de la instancia actual, lo que le permite analizar rápidamente las tendencias y tomar decisiones fundamentadas. Para enviar datos de otras instancias, acceda simplemente al panel de control de la instancia correspondiente."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_conversions_graph_en"
>title="Rastreador de representación de documentos"
>abstract="Este gráfico representa el recuento de la representación de documentos durante períodos de tiempo específicos. **Nota:** El gráfico proporciona datos específicos de la instancia actual, lo que le permite analizar rápidamente las tendencias y tomar decisiones fundamentadas. Para enviar datos de otras instancias, acceda simplemente al panel de control de la instancia correspondiente."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_newForms_graph_en"
>title="Nuevo rastreador de formularios"
>abstract="El gráfico proporciona información sobre el número de formularios de nueva creación durante periodos de tiempo específicos. **Nota:** El gráfico proporciona datos específicos de la instancia de autor actual de AEM Forms. Para ver datos de otras instancias, acceda al panel de control de la instancia correspondiente."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_publishedForms_graph_en"
>title="Rastreador de formularios publicados"
>abstract="El gráfico proporciona información sobre el número de formularios que se han publicado con éxito durante periodos de tiempo específicos. **Nota:** El gráfico proporciona datos específicos de la instancia de publicación de AEM Forms actual. Para ver los datos de conversión de otras instancias, acceda al panel de control de la instancia correspondiente."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formCreationAvgDuration_graph_en"
>title="Duración media de la generación de formularios"
>abstract="El gráfico ilustra el tiempo medio necesario para crear un formulario. Cada barra del gráfico representa un formulario específico y la altura de la barra indica la duración media de creación del formulario durante ese lapso de tiempo."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formPublishAvgDuration_en"
>title="Duración media de creación de formularios"
>abstract="El gráfico muestra el tiempo medio que se tarda en crear y publicar un formulario, medido desde el día inicial en que se abrió el formulario para editarlo. **Nota:** El gráfico proporciona datos específicos de la instancia de autor actual de AEM Forms. Para ver datos de otras instancias, acceda al panel de control de la instancia correspondiente."


>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_formFragments_graph_en"
>title="Rastreador de fragmentos de formularios"
>abstract="Este gráfico le ayuda a ver cuántos fragmentos de formularios utiliza la gente en sus formularios. **Nota:** El gráfico proporciona datos específicos de la instancia de publicación de AEM Forms actual. Para ver los datos de conversión de otras instancias, acceda al panel de control de la instancia correspondiente."

>[!CONTEXTUALHELP]
>id="aemforms_cs_transaction_reporting_avgFormPerFragments_graph_en"
>title="Rastreador de tiempo medio de fragmento de formulario"
>abstract="El gráfico muestra el tiempo medio que se tarda en crear un fragmento de formulario, medido desde el día inicial en que se abrió el fragmento de formulario para editarlo. **Nota:** El gráfico proporciona datos específicos de la instancia de publicación de AEM Forms actual. Para ver los datos de conversión de otras instancias, acceda al panel de control de la instancia correspondiente."


<!-- 

>[!NOTE]
>
>Transaction Reports UI displays three categories: Forms Submitted, Documents Rendered, and Documents Processed. Both Documents Rendered and Documents Processed are accounted as Documents Rendered.
-->


<!--

## Billable Document Services APIs {#billable-document-services-apis}

### Generate PDF Service {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Distiller Service {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>Creates Adobe PDF from supported file types.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## API de servicios de documentos facturables {#billable-document-services-apis}

### Generar un servicio PDF {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#section/Before-you-start" target="_blank">createPDF</a></td>
   <td>Generar un documento PDF a partir de una plantilla y combinar los datos con ella;</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/Communications-Services/paths/~1adobe~1forms~1doc~1v1~1generatePrintedOutput/post" target="_blank">exportPDF</a></td>
   <td>Convierte un archivo XDP o un documento PDF en tipos de archivo compatibles.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Converts Adobe PDF to supported file types. </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>Creates PDF from HTML pages.</p> </td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>Creates PDF from URLs pointing to an HTML page.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>Optimizes PDF to reduce file size by stripping unnecessary metadata without affecting the quality.</td>
   <td>Documents Processed<br /> </td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

### Servicio de salida {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutput" target="_blank">generatePDFOutput</a></td>
   <td>Combina datos y plantillas para crear un documento de PDF.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PDFOutputOptions" target="_blank">generatePDFOutput (PDFOutputOptions)</a></td>
   <td>Combina datos y plantillas para crear un documento de PDF.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePDFOutputBatch</a></td>
   <td>Combina datos y plantillas para crear un conjunto de documentos PDF.</td>
   <td>Documentos procesados</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutput" target="_blank">generatePrintedOutput</a></td>
   <td>Convierte los documentos XDP y PDF a los formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-sync/#tag/PrintedOutputOptions" target="_blank">generatePrintedOutput (PrintedOutputOptions)</a></td>
   <td>Convierte los documentos XDP y PDF a los formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/output-batch/#tag/Batch-Configuration/operation/CreateBatchConfig" target="_blank">generatePrintedOutputBatch</a></td>
   <td>Convierte un conjunto de documentos XDP y PDF a un conjunto de formatos de archivo PostScript (PS), Printer Command Language (PCL) y ZPL. </td>
   <td>Documentos procesados</td>
   <td> <!-- The generatePDFOutputBatch API combines a form template with a record and generates a PDF. When you process a batch of records, the transaction reporting service counts each record as a separate PDF rendition. <br> You can use the <a href="https://developer.adobe.com/experience-manager/reference-materials/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> flag to combine multiple renditions to single PDF file. Irrespective of the status of flag, the service counts each record as a separate PDF rendition. --> </td>
  </tr>
 </tbody>
</table>

### Servicio DocAssurance {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/docassurance/#tag/DocAssurance" target="_blank">secureDocument</a><br /> </td>
   <td>Esta API le permite proteger su documento. Puede utilizar la API para firmar, certificar, leer, extender o cifrar un documento PDF.</td>
   <td>Documentos procesados</td>
   <td>Solo se factura la operación firmar y certificar de secureDocument.</td>
  </tr>
 </tbody>
</table>

### Servicio de documento de registro (DOR) {#document-of-record-dor-forms-service-and-output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://opensource.adobe.com/aem-forms-af-runtime/api/#tag/Generate-DoR/operation/generateDoR" target="_blank">render</a></td>
   <td>Invoca el método de representación especificado para generar un documento de registro utilizando los parámetros proporcionados.</td>
   <td>Documentos procesados mediante el servicio Forms</td>
   <td> </td>
  </tr>
  <!--<tr>
   <td><a href="" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed using Output Service</td>
   <td> </td>
  </tr>-->
 </tbody>
</table>

<!--

### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Convert PDF Service {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>Converts a PDF document to a list of image documents. Supported image formats are JPEG, JPEG2K, PNG, and TIFF.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>Converts a Flat PDF file to PostScript format using the options specified in the option spec.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

<!--
### Barcoded Forms Service {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
   <td>Decodes all the barcodes in a Document object and returns an org.w3c.dom.Document object that contains data that was retrieved from the barcode.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

### Servicio Assembler {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX">invoke</a></td>
   <td>Ejecuta el DDX en los documentos de entrada dados y devuelve un objeto que contiene los documentos de resultado</td>
   <td>Documentos procesados</td>
   <td>Las siguientes operaciones no se contabilizan como transacciones:
    <ul>
     <li>Crear paquetes o portafolios</li>
     <li>Configurar varios XDP </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/DDX-execution/operation/InvokeDDX" target="_blank">invoke</a></td>
   <td>Ejecuta el DDX en los documentos de entrada dados y devuelve un objeto que contiene los documentos de resultado</td>
   <td>Documentos procesados</td>
   <td>Todos los formatos de archivo de entrada compatibles con Generador de PDF, Formularios y Servicios de salida; el servicio Assembler admite todos esos formatos como formatos de archivo de salida. </td>
  </tr>
  <tr>
   <td><a href="https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/references/assembler-sync/#tag/Document-conversion/operation/ConvertToPDFA">toPDFA</a></td>
   <td>Convertir un documento especificado en PDF/A utilizando las opciones especificadas.</td>
   <td>Documentos procesados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

El uso de la API de invocación se cuenta como una transacción cuando realiza una o más de las siguientes operaciones:

1. Conversión de formatos que no son PDF a formatos PDF. <!--For instance, the conversion from XDP format to PDF format, catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. Conversión de formato PDF a formato PDF/A.
1. Conversión de formato PDF a formatos no PDF. Algunos ejemplos son la transformación de PDF a formato de imagen o la conversión de PDF a formato de texto.


>[!NOTE]
>
>* El API de invocación del servicio Assembler puede llamar internamente a un API facturable de otro servicio en función de la entrada. Por lo tanto, la API de invocación puede contabilizarse como ninguna, única o múltiples transacciones. El número de transacciones contabilizadas depende de la entrada y las API internas invocadas.
>* Un documento PDF único producido mediante el servicio Assembler puede contabilizarse como ninguna, única o múltiples transacciones. El número de transacciones contabilizadas depende del código proporcionado.
>

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. In order for a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>
-->

## API de captura de datos facturables {#billable-data-capture-apis}

Todos los eventos de envío de formularios adaptables se contabilizan como transacciones. De forma predeterminada, el envío de un formulario PDF no se contabiliza como una transacción. Utilice la [API de registro de transacciones](record-transaction-custom-implementation.md) proporcionada para registrar un envío de PDF Forms como una transacción.

### Formularios adaptables {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Caso práctico</p> </td>
   <td>Descripción</td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Enviar un formulario adaptable</td>
   <td>Envía un formulario adaptable a la acción de envío configurada. </td>
   <td>Formularios enviados</td>
   <td>
    <ul>
     <li>Cuenta de envíos correcta para una o dos transacciones. El número de transacciones contabilizadas depende del tipo de acción de envío utilizada para el envío. Por ejemplo, enviar al PDF mediante cuentas de acción de envío por correo electrónico para dos recuentos de transacciones. Una transacción para el envío de formularios y otra para el PDF generado mediante el servicio documento de registro (DOR). </li>
     <li>El uso del formulario adaptable en un formulario adaptable (conjunto de formularios de formulario adaptable) contabiliza solo una transacción. Puede tener cualquier número de formularios adaptables dentro de un formulario adaptable.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

<!--

### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Form set {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting a form set</td>
   <td>Submits form set to the submit URL configured in the form set.</td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
     <li>Every form in an HTML5 Forms form set accounts as a separate transaction. </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

## Flujos de trabajo de AEM centrados en formularios facturables {#billable--form-centric-aem-workflows}

Los pasos de asignación de tareas y servicios de documentos de los flujos de trabajo de AEM centrados en formularios se contabilizan como transacciones. Si un paso de flujo de trabajo cuenta una transacción y el flujo de trabajo no se completa, el recuento de transacciones no se invierte.

<!--
Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.
-->


<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/es/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->

### Flujos de trabajo de AEM centrados en formularios {#form-centric-aem-workflows}

<table>
 <tbody>
  <tr>
   <td><p>Caso de uso</p> </td>
   <td>Categoría del informe de transacción</td>
   <td>Información adicional</td>
  </tr>
  <tr>
   <td>Enviar un paso Asignar tarea</td>
   <td>Formularios enviados</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Enviar un punto de inicio de aplicación de flujo de trabajo </td>
   <td>Formularios enviados</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Registrar API facturables como transacciones para código personalizado {#recording-billable-apis-as-transactions-for-custom-code}

Las acciones como enviar un formulario PDF, utilizar la interfaz de usuario del agente para obtener una vista previa de una comunicación interactiva, usar el envío de formulario no estándar y las implementaciones personalizadas no se contabilizan como transacciones. AEM Forms proporciona un API para registrar esas acciones como transacciones. Puede llamar al API desde sus implementaciones personalizadas para [registrar una transacción](/help/forms/record-transaction-custom-implementation.md).

## Artículos relacionados {#related-articles}

* [Registrar una transacción para implementaciones personalizadas](/help/forms/record-transaction-custom-implementation.md)
