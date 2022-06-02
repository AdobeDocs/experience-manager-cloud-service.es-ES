---
title: Rellene previamente los campos del formulario adaptable
seo-title: Prefill Adaptive Form fields
description: Utilice los datos existentes para rellenar previamente los campos de un formulario adaptable.
seo-description: With Adaptive Forms, you users can prefill basic information in a form by logging in with their social profiles. This article describes how you can accomplish this.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
source-git-commit: 6b3c0abbbd7a5b3c9a3790937b933699389b0cd2
workflow-type: tm+mt
source-wordcount: '1948'
ht-degree: 0%

---


# Rellene previamente los campos del formulario adaptable{#prefill-adaptive-form-fields}

## Introducción {#introduction}

Puede rellenar previamente los campos de un formulario adaptable utilizando los datos existentes. Cuando un usuario abre un formulario, los valores de esos campos se rellenan previamente. Para rellenar previamente los datos en un formulario adaptable, haga que los datos de usuario estén disponibles como un XML/JSON de relleno previo en el formato que se adhiera a la estructura de datos de relleno previo de Forms adaptable.

## Estructura de los datos de relleno previo {#the-prefill-structure}

Un formulario adaptable puede tener una combinación de campos enlazados y no enlazados. Los campos enlazados son campos que se arrastran desde la pestaña Buscador de contenido y que contienen campos que no están vacíos `bindRef` valor de propiedad en el cuadro de diálogo de edición de campos. Los campos no enlazados se arrastran directamente desde el navegador de componentes de la barra de tareas y tienen un espacio vacío `bindRef` valor.

Puede rellenar previamente los campos enlazados y no enlazados de un formulario adaptable. Los datos de relleno previo contienen las secciones afBoundData y afUnBoundData para rellenar previamente los campos enlazados y no enlazados de un formulario adaptable. La variable `afBoundData` contiene los datos de rellenado previo de los campos y paneles enlazados. Estos datos deben cumplir con el esquema del modelo de formulario asociado:

- Para Forms adaptable mediante la variable [Plantilla de formulario XFA](#xfa-based-af), utilice el XML de rellenado previo compatible con el esquema de datos de la plantilla XFA.
- Para Forms adaptable mediante [Esquema XML](#xml-schema-af), utilice el XML de rellenado previo compatible con la estructura de esquema XML.
- Para Forms adaptable mediante [esquema JSON](#json-schema-based-adaptive-forms), utilice el JSON de rellenado previo compatible con el esquema JSON.
- Para Adaptive Forms mediante el esquema FDM, utilice el JSON de relleno previo compatible con el esquema FDM.
- Para Forms adaptable con [sin modelo de formulario](#adaptive-form-with-no-form-model), no hay datos enlazados. Cada campo es un campo independiente y se rellena previamente utilizando el XML independiente.

### Ejemplo de estructura XML de prerelleno {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         .
         .
    </data>
  </afUnboundData>
</afData>
```

### Ejemplo de estructura JSON de relleno previo {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

Para los campos enlazados con los mismos campos bindref o unbound con el mismo nombre, los datos especificados en la etiqueta XML o el objeto JSON se rellenan en todos los campos. Por ejemplo, dos campos de un formulario se asignan al nombre `textbox` en los datos de relleno previo. Durante el tiempo de ejecución, si el primer campo de cuadro de texto contiene &quot;A&quot;, entonces &quot;A&quot; se rellena automáticamente en el segundo cuadro de texto. Esta vinculación se denomina vinculación activa de los campos del formulario adaptable.

### Formulario adaptable con plantilla de formulario XFA {#xfa-based-af}

La estructura de XML de relleno previo y el XML enviado para Forms adaptable basado en XFA es la siguiente:

- **Prerellenar estructura XML**: El XML de relleno previo para el formulario adaptable basado en XFA debe ser compatible con el esquema de datos de la plantilla de formulario XFA. Para rellenar previamente los campos no enlazados, ajuste la estructura XML de relleno previo en `/afData/afBoundData` etiqueta.

- **Estructura XML enviada**: Cuando no se utiliza ningún XML de relleno previo, el XML enviado contiene datos para los campos enlazados y no enlazados en `afData` etiqueta envolvente. Si se utiliza un XML de relleno previo, el XML enviado tiene la misma estructura que el XML de relleno previo. Si el XML de relleno previo comienza con la variable `afData` raíz, el XML de salida también tiene el mismo formato. Si el XML de relleno previo no tiene `afData/afBoundData`wrapper y en su lugar comienza directamente desde la etiqueta raíz del esquema como `employeeData`, el XML enviado también comienza con el `employeeData` etiqueta.

Prefill-Submit-Data-ContentPackage.zip

[Obtener archivo](assets/prefill-submit-data-contentpackage.zip)
Ejemplo que contiene datos de relleno previo y datos enviados

### Forms adaptable basado en esquemas XML  {#xml-schema-af}

La estructura de XML de relleno previo y XML enviado para Forms adaptable basado en esquema XML es la siguiente:

- **Prerellenar estructura XML**: El XML de relleno previo debe ser compatible con el esquema XML asociado. Para rellenar previamente los campos no enlazados, ajuste la estructura XML de relleno previo a la etiqueta /afData/afBoundData .
- **Estructura XML enviada**: si no se utiliza ningún XML de relleno previo, el XML enviado contiene datos para los campos enlazados y no enlazados en `afData` etiqueta envolvente. Si se utiliza el XML de relleno previo, el XML enviado tiene la misma estructura que el XML de relleno previo. Si el XML de relleno previo comienza con la variable `afData` etiqueta raíz, el XML de salida tiene el mismo formato. Si el XML de relleno previo no tiene `afData/afBoundData` wrapper y en su lugar, comenzar directamente desde la etiqueta raíz del esquema como `employeeData`, el XML enviado también comienza con el `employeeData` etiqueta.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">

    <xs:element name="sample" type="SampleType"/>

    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

Para los campos cuyo modelo es un esquema XML, los datos se rellenan previamente en la variable `afBoundData` como se muestra en el ejemplo XML siguiente. Se puede utilizar para marcar un formulario adaptable como prefijo con uno o más campos de texto no enlazados.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>Se recomienda no utilizar campos no enlazados en paneles enlazados (paneles con no vacío) `bindRef` que se ha creado arrastrando componentes de la barra de tareas o de la ficha Fuentes de datos). Puede causar la pérdida de datos de estos campos independientes. Además, se recomienda que los nombres de los campos sean únicos en todo el formulario, especialmente para los campos independientes.

#### Un ejemplo sin afData y afBoundData wrapper {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### Forms adaptable basado en esquemas JSON {#json-schema-based-adaptive-forms}

Para Forms adaptable basado en el esquema JSON, la estructura de JSON de relleno previo y JSON enviado se describe a continuación. Para obtener más información, consulte [Creación de Forms adaptable mediante el esquema JSON](adaptive-form-json-schema-form-model.md).

- **Precompletar estructura JSON**: El JSON de relleno previo debe ser compatible con el esquema JSON asociado. Opcionalmente, se puede ajustar en el objeto /afData/afBoundData si desea rellenar previamente también los campos no enlazados.
- **Estructura JSON enviada**: si no se utiliza un JSON de relleno previo, el JSON enviado contiene datos para los campos enlazados y no enlazados en la etiqueta de envoltura afData. Si se utiliza el JSON de relleno previo, el JSON enviado tiene la misma estructura que el JSON de relleno previo. Si el JSON de relleno previo comienza con el objeto raíz afData, el JSON de salida tiene el mismo formato. Si el JSON de relleno previo no tiene un envoltorio afData/afBoundData y en su lugar comienza directamente desde el objeto raíz de esquema como usuario, el JSON enviado también comienza con el objeto de usuario.

```json
{
  "id": "https://some.site.somewhere/entry-schema#",
  "$schema": "https://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "address": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string"
        },
        "age": {
          "type": "integer"
        }
      }
    }
  }
}
```

Para los campos que utilizan el modelo de esquema JSON, los datos se rellenan previamente en el objeto afBoundData como se muestra en el archivo JSON de muestra siguiente. Se puede utilizar para marcar un formulario adaptable como prefijo con uno o más campos de texto no enlazados. A continuación se muestra un ejemplo de datos con `afData/afBoundData` envolvente:

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

A continuación se muestra un ejemplo sin `afData/afBoundData` envolvente:

```json
{
  "user": {
    "address": {
      "city": "Noida",
      "country": "India"
    }
  }
}
```

>[!NOTE]
>
> El uso de campos no enlazados en paneles enlazados (paneles con bindRef no vacío que se han creado arrastrando componentes de la barra de tareas o la ficha Fuentes de datos) es **not** recomendado, ya que podría causar la pérdida de datos de los campos independientes. Se recomienda tener nombres de campo únicos en todo el formulario, especialmente en los campos no enlazados.

### Formulario adaptable sin modelo de formulario {#adaptive-form-with-no-form-model}

Para Forms adaptable sin modelo de formulario, los datos de todos los campos se encuentran en la sección `<data>` etiqueta de `<afUnboundData> tag`.

Asimismo, tome nota de lo siguiente:

Las etiquetas XML para los datos de usuario enviados para varios campos se generan utilizando el nombre de los campos. Por lo tanto, los nombres de campo deben ser únicos.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## Configuración del servicio de prefill {#configuring-prefill-service-using-configuration-manager}

Utilice la variable `alloweddataFileLocations` propiedad de la variable **Configuración predeterminada del servicio de precarga** para establecer la ubicación de los archivos de datos o un regex (expresión regular) para las ubicaciones de los archivos de datos.

El siguiente archivo JSON muestra un ejemplo:

```JSON
  {
  "alloweddataFileLocations": "`file:///C:/Users/public/Document/Prefill/.*`"
  }
```

Para establecer los valores de una configuración, [Generación de configuraciones de OSGi mediante el SDK de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) y [implementar la configuración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) a su instancia de Cloud Service.

>[!NOTE]
>
> - De forma predeterminada, se permite el rellenado previo mediante archivos crx para todos los tipos de Forms adaptable (XSD, XDP, JSON, FDM y sin modelo de formulario). El rellenado previo solo se permite con archivos JSON y XML.
> - El protocolo crx se encarga de la seguridad de los datos rellenados previamente y, por lo tanto, está permitido de forma predeterminada. La cumplimentación previa a través de otros protocolos usando regex genéricos puede causar vulnerabilidad. En la configuración, especifique una configuración de URL segura para proteger los datos.


## El curioso caso de los paneles repetibles {#the-curious-case-of-repeatable-panels}

Por lo general, los campos enlazados (esquema de formulario) y no enlazados se crean en el mismo formulario adaptable, pero las siguientes son algunas excepciones en caso de que el enlace sea repetible:

- Los paneles repetibles no enlazados no son compatibles con Adaptive Forms que utiliza la plantilla de formulario XFA, XSD, el esquema JSON o el esquema FDM.
- No utilice campos independientes en paneles repetibles enlazados.

>[!NOTE]
>
> Como regla general, no mezcle campos enlazados y no enlazados si están intersectados en datos rellenados por el usuario final en campos no enlazados. Si es posible, debe modificar el esquema o la plantilla de formulario XFA y agregar una entrada para los campos no enlazados, de modo que también se convierta en enlazado y sus datos estén disponibles como otros campos en los datos enviados.

## Protocolos admitidos para prefijar datos de usuario {#supported-protocols-for-prefilling-user-data}

Forms adaptable se puede rellenar previamente con datos de usuario en formato de datos de relleno previo mediante los protocolos siguientes cuando se configura con regex válido:

### El protocolo crx:// {#the-crx-protocol}

```javascript
http
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

El nodo especificado debe tener una propiedad denominada `jcr:data` y mantenga los datos.

### El protocolo file://  {#the-file-protocol-nbsp}

```javascript
https://`servername`/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

El archivo de referencia debe estar en el mismo servidor.

### El protocolo https:// {#the-http-protocol}

```javascript
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://servername/somesamplexmlfile.xml
```

### El protocolo service:// {#the-service-protocol}

```javascript
https://`servername`/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

- SERVICE_NAME hace referencia al nombre del servicio de relleno previo OSGI. Consulte [Creación y ejecución de un servicio de relleno previo](prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
- IDENTIFIER se refiere a cualquier metadato que requiera el servicio de rellenado previo OSGI para recuperar los datos de rellenado previo. Un identificador para el usuario que ha iniciado sesión es un ejemplo de metadatos que se pueden utilizar.

>[!NOTE]
>
> No se admite el paso de parámetros de autenticación.

### Configuración del atributo de datos en slingRequest {#setting-data-attribute-in-slingrequest}

También puede configurar la variable `data` atributo en `slingRequest`, donde la variable `data` es una cadena que contiene XML o JSON, como se muestra en el código de ejemplo siguiente (el ejemplo es para XML):

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

Puede escribir una cadena XML o JSON simple que contenga todos los datos y definirlos en slingRequest. Esto se puede hacer fácilmente en el JSP del procesador para cualquier componente, que desea incluir en la página donde puede establecer el atributo de datos slingRequest .

Por ejemplo, donde desea un diseño específico para la página con un tipo específico de encabezado. Para lograrlo, puede escribir su propio `header.jsp`, que puede incluir en el componente de página y establecer la variable `data` atributo.

Otro buen ejemplo es un caso de uso en el que le gustaría rellenar previamente los datos de inicio de sesión a través de cuentas sociales como Facebook, Twitter o LinkedIn. En este caso, puede incluir un JSP simple en `header.jsp`, que obtiene datos de la cuenta de usuario y establece el parámetro data .

prefill-page component.zip

[Obtener archivo](assets/prefill-page-component.zip)
Ejemplo de prefill.jsp en el componente de página

## [!DNL AEM Forms] servicio de prerelleno personalizado {#aem-forms-custom-prefill-service}

Se puede utilizar el servicio de rellenado previo personalizado para las situaciones en las que se leen constantemente datos de una fuente predefinida. El servicio de rellenado previo lee datos de orígenes de datos definidos y prefiere los campos del formulario adaptable con el contenido del archivo de datos de rellenado previo. También le ayuda a asociar permanentemente los datos prerellenados con un formulario adaptable.

### Creación y ejecución de un servicio de relleno previo {#create-and-run-a-prefill-service}

El servicio de prefill es un servicio OSGi y se empaqueta a través del paquete OSGi. Puede crear el paquete OSGi, cargarlo e instalarlo en [!DNL AEM Forms] paquetes. Antes de comenzar a crear el paquete:

- [Descargue el [!DNL AEM Forms] Client SDK](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html)
- Descargar el paquete repetitivo

- Coloque el archivo de datos (datos de relleno previo) en el repositorio crx. Puede colocar el archivo en cualquier ubicación de la carpeta \content del repositorio crx.

[Obtener archivo](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Creación de un servicio de rellenado previo {#create-a-prefill-service}

El paquete repetitivo (paquete de servicio prefill de muestra) contiene una implementación de muestra de [!DNL AEM Forms] servicio de precarga. Abra el paquete repetitivo en un editor de código. Por ejemplo, abra el proyecto repetitivo en Eclipse para editarlo. Después de abrir el paquete repetitivo en un editor de código, realice los siguientes pasos para crear el servicio.

1. Abra el archivo src\main\java\com\adobe\test\Prefill.java para editarlo.
1. En el código, establezca el valor de:

   - `nodePath:` La variable de ruta de nodo que señala a la ubicación del repositorio crx contiene la ruta del archivo de datos (prefill). Por ejemplo, /content/prefilldata.xml
   - `label:` El parámetro label especifica el nombre para mostrar del servicio. Por ejemplo, el servicio de precarga predeterminado

1. Guarde y cierre el `Prefill.java` archivo.
1. Agregue la variable `AEM Forms Client SDK` al trazado de compilación del proyecto repetitivo.
1. Compile el proyecto y cree el .jar para el paquete.

#### Inicio y uso del servicio de precarga {#start-and-use-the-prefill-service}

Para iniciar el servicio de rellenado previo, cargue el archivo JAR en [!DNL AEM Forms] Consola Web y activar el servicio. Ahora, el servicio empieza a aparecer en el editor de Forms adaptable. Para asociar un servicio de rellenado previo a un formulario adaptable:

1. Abra el Formulario adaptable en el Editor de Forms y abra el panel Propiedades del contenedor de formularios.
1. En la consola Propiedades, vaya a [!DNL AEM Forms] contenedor > Básico > Servicio de relleno previo.
1. Seleccione el servicio de relleno predeterminado y haga clic en **[!UICONTROL Guardar]**. El servicio está asociado al formulario.

<!-- ## Prepopulate data at client {#prefill-at-client}

When you prefill an Adaptive Form, the [!DNL AEM Forms] server merges data with an Adaptive Form and delivers the filled form to you. By default, the data merge action takes place at the server.

You can configure the [!DNL AEM Forms] server to perform the data merge action at the client instead of the server. It significantly reduces the time required to prefill and render Adaptive Forms. By default, the feature is disabled. You can enable it from the Configuration Manager or command line.

* To enable or disable from configuration manager:
  1. Open AEM Configuration Manager.
  1. Locate and open the Adaptive Form and Interactive Communication Web Channel Configuration
  1. Enable the Configuration.af.clientside.datamerge.enabled.name option
* To enable or disable from the command line:
  * To enable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

  * To disable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   To take full advantage of the prepopulate data at client option, update your prefill service to return [FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) and [CustomContext](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) -->
