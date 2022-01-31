---
title: 'Problemas conocidos '
description: Prácticas recomendadas de comunicaciones, problemas conocidos y limitaciones
source-git-commit: c38a34519822449ff2577a9474b1294d5d45d3ae
workflow-type: tm+mt
source-wordcount: '1666'
ht-degree: 0%

---


# Considerations known issues, and best practices {#best-practices-known-issues-and-limitations}

Before you begin using Communication APIs, review the following considerations, known issues, and frequently asked questions:

## Consideraciones  {#considerations-for-communications-apis}

### Form data {#form-data}

Las API de comunicaciones aceptan un diseño de formulario que se suele crear en Designer y los datos de formulario XML como entrada. Para rellenar un documento con datos, debe existir un elemento XML en los datos del formulario XML para cada campo de formulario que desee rellenar. El nombre del elemento XML debe coincidir con el nombre del campo. Se ignora un elemento XML si no se corresponde con un campo de formulario o si el nombre del elemento XML no coincide con el nombre del campo. No es necesario coincidir con el orden en que se muestran los elementos XML. El factor importante es que los elementos XML se especifican con los valores correspondientes.

Consideremos el siguiente ejemplo de formulario de solicitud de préstamo:

![Formulario de solicitud de préstamo](assets/loanFormData.png)

Para combinar datos en este diseño de formulario, cree un origen de datos XML que corresponda al formulario. El siguiente XML representa un origen de datos XML que corresponde al formulario de aplicación hipotecaria de ejemplo.

```XML
<?xml version="1.0" encoding="UTF-8" ?>
- <xfa:datasets xmlns:xfa="http://www.xfa.org/schema/xfa-data/1.0/">
- <xfa:data>
- <data>
    - <Layer>
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
    - <Mortgage>
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

Para acceder completamente a las funciones de renderización de las API de comunicaciones, se recomienda utilizar un archivo XDP como entrada. A veces, se puede utilizar un archivo PDF. Sin embargo, el uso de un archivo PDF como entrada tiene las limitaciones:

Un documento PDF que no contiene un flujo XFA no se puede representar como PostScript, PCL o ZPL. Communications APIs can render PDF documents with XFA streams (that is, forms created in Designer) into laser and label formats. Si el documento del PDF está firmado, certificado o contiene derechos de uso (aplicados mediante el servicio AEM Forms Reader Extensions), no se puede procesar en estos formatos de impresión.


### Áreas imprimibles {#printable-areas}

El margen no imprimible predeterminado de 0,25 pulgadas no es exacto para impresoras de etiquetas y varía de impresora a impresora y de tamaño de etiqueta a tamaño de etiqueta. Sin embargo, se recomienda mantener el margen de 0,25 pulgadas o reducirlo. Sin embargo, se recomienda no aumentar el margen no imprimible. De lo contrario, la información del área imprimible no se imprime correctamente.

Asegúrese siempre de utilizar el archivo XDC correcto para la impresora. Por ejemplo, evite elegir un archivo XDC para una impresora de 300 ppp y envíe el documento a una impresora de 200 ppp.

### Solo secuencias de comandos para formularios XFA (XDP/PDF) {#scripts}

Un diseño de formulario que se utiliza con las API de comunicaciones puede contener secuencias de comandos que se ejecutan en el servidor. Asegúrese de que el diseño de formulario no contenga secuencias de comandos que se ejecuten en el cliente. For information about creating form design scripts, see [Designer Help](use-forms-designer.md).

<!-- #### Working with Fonts
 Document Considerations for Working with Fonts>> -->

### Asignación de fuentes {#font-mapping}

Para diseñar un formulario que utilice fuentes residentes en la impresora, elija un nombre de tipo de letra en Designer que coincida con las fuentes disponibles en la impresora. Una lista de fuentes compatibles con PCL o PostScript se encuentra en los perfiles de dispositivo correspondientes (archivos XDC). Alternativamente, se puede crear una asignación de fuentes para asignar fuentes no residentes en la impresora a fuentes residentes en la impresora con un nombre de tipo de letra diferente. Por ejemplo, en un escenario PostScript, las referencias a la fuente Arial® se pueden asignar a la fuente Helvetica® residente en la impresora.

Si una fuente está instalada en un equipo cliente, está disponible en la lista desplegable de Designer. Si la fuente no está instalada, es necesario especificar el nombre de la fuente manualmente. La opción &quot;Reemplazar permanentemente fuentes no disponibles&quot; de Designer puede estar desactivada. De lo contrario, cuando el archivo XDP se guarda en Designer, el nombre de la fuente de sustitución se escribe en el archivo XDP. It means that the printer-resident font is not used.

Existen dos tipos de fuentes OpenType®. One type is a TrueType OpenType® font that PCL supports. The other is CFF OpenType®. La salida de PDF y PostScript admite fuentes Type-1, TrueType y OpenType® incrustadas. La salida PCL admite fuentes TrueType incrustadas.

Type-1 and OpenType® fonts are not embedded in PCL output. El contenido con formato Type-1 y OpenType® se rasteriza y genera como imagen de mapa de bits que puede ser grande y lento de generar.

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
<!-- It is not necessary to modify these files to create documents. However, you can modify them to meet your business requirements. -->

Estos archivos son archivos XDC de referencia que admiten las características de impresoras específicas, como fuentes residentes, bandejas de papel y grapadora. El propósito de estas referencias es ayudarle a comprender cómo configurar sus propias impresoras mediante perfiles de dispositivo. La referencia también es un punto de partida para impresoras similares en la misma línea de productos.

### Uso del archivo de configuración XCI {#working-with-xci-files}

Las API de comunicaciones utilizan un archivo de configuración XCI para realizar tareas, como controlar si la salida es un solo panel o una paginación. Aunque este archivo contiene opciones que se pueden configurar, no es habitual modificar este valor. <!-- The default.xci file is located in the svcdata\XMLFormService folder. -->

Puede pasar un archivo XCI modificado mientras utiliza una API de comunicaciones. Al hacerlo, cree una copia del archivo predeterminado, cambie solo los valores que requieran modificación para satisfacer los requisitos comerciales y utilice el archivo XCI modificado.

Las API de comunicaciones empiezan con el archivo XCI predeterminado (o el archivo modificado). A continuación, aplica los valores especificados mediante las API de comunicaciones. Estos valores anulan la configuración de XCI.

The following table specifies XCI options.

| Opción XCI | Descripción |
| ------------------------------------| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| config/actual/pdf/creator | Identifica al creador del documento mediante la entrada Creador del diccionario de información del documento. Para obtener información sobre este diccionario, consulte la guía de referencia del PDF. |
| config/present/pdf/producer | Identifica al productor del documento mediante la entrada Producer del diccionario de información del documento. Para obtener información sobre este diccionario, consulte la guía de referencia del PDF. |
| config/current/layout | Controla si la salida es un solo panel o paginado. |
| config/current/pdf/compression/level | Especifica el grado de compresión que se utilizará al generar un documento de PDF. |
| config/present/pdf/scriptModel | Controla si la información específica de XFA se incluye en el documento del PDF de salida. |
| config/current/common/data/adaptData | Controls whether the XFA application adjusts the data after merging. |
| config/actual/pdf/renderPolicy | Controla si la generación del contenido de la página se realiza en el servidor o se diferye al cliente. |
| config/current/common/locale | Especifica la configuración regional predeterminada utilizada en el documento de salida. |
| config/current/destination | Cuando está contenido en un elemento presente, especifica el formato de salida. Cuando está contenido en un elemento openAction, especifica la acción que se debe realizar al abrir el documento en un cliente interactivo. |
| config/current/output/type | Especifica el tipo de compresión que se aplicará a un archivo o el tipo de salida que se producirá. |
| config/current/common/temp/uri | Especifica el URI del formulario. |
| config/current/common/template/base | Proporciona una ubicación base para URIs en el diseño de formulario. Cuando este elemento está ausente o vacío, se utiliza como base la ubicación del diseño de formulario. |
| config/present/common/log/to | Controls the location that log data or output data is written to. |
| config/present/output/to | Controls the location that log data or output data is written to. |
| config/current/script/currentPage | Especifica la página inicial cuando se abre el documento. |
| config/current/script/exclude | Informs to AEM Forms server/Communications APIs which events to ignore. |
| config/actual/pdf/linearized | Controla si el documento del PDF de salida está linealizado. |
| config/current/script/runScripts | Controla qué conjunto de secuencias de comandos se ejecuta AEM Forms. |
| config/actual/pdf/tagged | Controla la inclusión de etiquetas en el documento del PDF de salida. Las etiquetas, en el contexto del PDF, son información adicional incluida en un documento para exponer la estructura lógica del documento. Las etiquetas ayudan a facilitar la accesibilidad y a cambiar el formato. Por ejemplo, un número de página puede etiquetarse como un artefacto para que un lector de pantalla no lo enuncie en medio del texto. Aunque las etiquetas hacen que un documento sea más útil, también aumentan el tamaño del documento y el tiempo de procesamiento para crearlo. |
| config/actual/pdf/version | Especifica la versión del documento de PDF que se va a generar. |


## Problemas conocidos

* Puede utilizar un tipo de renderización específico (PDF, PRINT) solo una vez en la lista de opciones de impresión. For example, you cannot have two PRINT options each specifying a PCL render type.

* Para una configuración por lotes, solo una instancia de combinación de valores de OutputType(PDF, PRINT) y RenderType(PostScript, PCL, IPL, ZPL, etc.) is allowed.

## Prácticas recomendadas  

* Adobe recomienda alojar los archivos de datos en el almacén de contenedores de blob en la región de la nube utilizada por AEM Cloud Service.

## Preguntas frecuentes {#faq}

**¿Puedo utilizar una carpeta vigilada u otros mecanismos de almacenamiento para almacenar entradas y salidas?**

En este momento, puede utilizar el almacenamiento de Microsoft Azure para guardar datos de entrada y documentos generados. Microsoft Azure storage provides various options to [automate data movement operations](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

**¿Se incluye una cuenta de almacenamiento de Microsoft Azure con licencia de Cloud Service de Experience Manager Forms?**

La cuenta de almacenamiento de Microsoft Azure es independiente de la licencia de Cloud Service de Experience Manager Forms.

**¿Las API de comunicación almacenan datos en los servidores Cloud Service de Experience Manager Forms?**

Los datos de entrada y salida solo se guardan en el almacenamiento de Microsoft Azure.

**Are Communication APIs available only for Experience Manager Forms Cloud Service? Can I get similar functionality on on-premise environment?**

Puede utilizar el servicio de salida de AEM Forms para combinar una plantilla (XFA o PDF) con datos de clientes para generar documentos en los formatos PDF, PS, PCL y ZPL.

En comparación con el entorno local, el Cloud Service ofrece beneficios adicionales de escalado automático y rentabilidad.

<!--**Where is data processed?**

**Who has access to data?**

**Is data encrypted?**

**Where is data hosted?** -->

**¿Puedo ejecutar varias operaciones por lotes simultáneamente?**
Sí, puede ejecutar varias operaciones por lotes de forma similar. Always use different source and destination folders for every operation to avoid any conflicts.
