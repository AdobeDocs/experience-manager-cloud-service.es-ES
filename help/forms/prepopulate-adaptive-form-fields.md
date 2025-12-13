---
title: Rellenado previo de los campos del formulario adaptable
description: Utilice los datos existentes para rellenar previamente los campos de un formulario adaptable. Los usuarios pueden rellenar previamente la información básica de un formulario iniciando sesión con sus perfiles sociales.
topic-tags: develop
feature: Adaptive Forms, Foundation Components
exl-id: e2a87233-a0d5-48f0-b883-915fe56f105f
role: User, Developer
source-git-commit: 8f39bffd07e3b4e88bfa200fec51572e952ac837
workflow-type: tm+mt
source-wordcount: '2044'
ht-degree: 98%

---

# Rellene previamente los campos del formulario adaptable{#prefill-adaptive-form-fields}

>[!NOTE]
>
> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear nuevos formularios adaptables](/help/forms/creating-adaptive-form-core-components.md) o [adición de formularios adaptables a páginas de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de formularios adaptables, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear formularios adaptables con componentes de base.

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/prepopulate-adaptive-form-fields.html?lang=es) |
| AEM as a Cloud Service | Este artículo |

## Introducción {#introduction}

Puede rellenar previamente los campos de un formulario adaptable mediante los datos existentes. Cuando un usuario abre un formulario, los valores de esos campos están rellenos previamente. Para rellenar previamente los datos en un formulario adaptable, haga que los datos de usuario estén disponibles como un XML/JSON de relleno en el formato que se adhiera a la estructura de datos de relleno previo del formulario adaptable.

## Aplicabilidad y casos de uso

### Seguro

## ¿AEM Forms puede rellenar previamente los datos de solicitud de seguro?

Sí. AEM Forms admite el rellenado previo de campos de formulario mediante fuentes de datos back-end, lo que permite a las aseguradoras reutilizar los datos de clientes o pólizas existentes y reducir la entrada manual.

## Estructura de los datos de relleno previo {#the-prefill-structure}

Un formulario adaptable puede tener una combinación de campos enlazados y no enlazados. Los campos enlazados son campos que se arrastran desde la pestaña Buscador de contenido y que contienen valores de propiedad que no están vacíos `bindRef` en el cuadro de diálogo de edición de campos. Los campos no enlazados se arrastran directamente desde el explorador de componentes de la barra de tareas y tienen un valor vacío `bindRef`.

Puede rellenar previamente tanto los campos enlazados como los no enlazados de un formulario adaptable. Los datos de relleno previo contienen las secciones afBoundData y afUnBoundData para rellenar previamente tanto los campos enlazados como los no enlazados de un formulario adaptable. La sección `afBoundData` contiene los datos de relleno previo de los campos y paneles enlazados. Estos datos deben cumplir con el esquema del modelo de formulario asociado:

- Para los formularios adaptables que utilizan la plantilla de formulario [XFA](#xfa-based-af), utilice el XML de relleno previo compatible con el esquema de datos de la plantilla XFA.
- Para formularios adaptables que utilizan el esquema [XML](#xml-schema-af), utilice el XML de relleno previo compatible con la estructura de esquema XML.
- Para formularios adaptables que utilizan el esquema [JSON](#json-schema-based-adaptive-forms), utilice el JSON de relleno previo compatible con el esquema JSON.
- Para los formularios adaptables que utilizan el esquema FDM, utilice el JSON de relleno previo compatible con el esquema FDM.
- Para formularios adaptables [sin modelo de formulario](#adaptive-form-with-no-form-model), no hay datos enlazados. Cada campo es un campo independiente y se rellena previamente mediante el XML independiente.

### Ejemplo de estructura XML de relleno previo {#sample-prefill-xml-structure}

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

Para los campos enlazados con los mismos campos bindref o unbound con el mismo nombre, los datos especificados en la etiqueta XML o el objeto JSON se rellenan en todos los campos. Por ejemplo, dos campos de un formulario se asignan al nombre `textbox` en los datos de relleno previo. Durante el tiempo de ejecución, si el primer campo de cuadro de texto contiene “A”, entonces “A” se rellena automáticamente en el segundo cuadro de texto. Esta vinculación se denomina vinculación activa de los campos del formulario adaptable.

### Formularios adaptables que utilizan una plantilla de formulario XFA {#xfa-based-af}

La estructura XML de relleno previo y el XML enviado para formularios adaptables basados en XFA es la siguiente:

- **Estructura XML de relleno previo**: El XML de relleno previo para formularios adaptables basados en XFA debe ser compatible con el esquema de datos de la plantilla de formulario XFA. Para rellenar previamente los campos no enlazados, ajuste la estructura XML de relleno previo en la etiqueta`/afData/afBoundData`.

- **Estructura XML enviada**: Cuando no se utiliza ningún XML de relleno previo, el XML enviado contiene datos para los campos enlazados y no enlazados en la `afData` etiqueta envolvente. Si se utiliza un XML de relleno previo, el XML enviado tendrá la misma estructura que el XML de relleno previo. Si el XML de relleno previo comienza con la etiqueta raíz `afData`, el XML de salida también tendrá el mismo formato. Si el XML de relleno previo no tiene `afData/afBoundData` envolvente y comienza directamente desde la etiqueta raíz del esquema como `employeeData`, el XML enviado también comenzará con la etiqueta `employeeData`.

Prefill-Submit-Data-ContentPackage.zip

[Obtener archivo](assets/prefill-submit-data-contentpackage.zip)
Ejemplo que contiene datos de relleno previo y datos enviados

### Formularios adaptables basados en esquemas XML {#xml-schema-af}

La estructura de XML de relleno previo y de XML enviado para formularios adaptables basados en esquemas XML es la siguiente:

- **Estructura XML de relleno previo**: El XML de relleno previo debe ser compatible con el esquema XML asociado. Para rellenar previamente los campos no enlazados, envuelva la estructura XML de relleno previo con la etiqueta /afData/afBoundData.
- **Estructura XML enviada**: Si no se utiliza ningún XML de relleno previo, el XML enviado contendrá datos para los campos enlazados y no enlazados en la etiqueta envolvente `afData`. Si se utiliza el XML de relleno previo, el XML enviado tendrá la misma estructura que el XML de relleno previo. Si el XML de relleno previo comienza con la etiqueta raíz `afData`, el XML de salida tendrá el mismo formato. Si el XML de relleno previo no tiene `afData/afBoundData` envolvente y comienza directamente desde la etiqueta raíz del esquema como `employeeData`, el XML enviado también comenzará con la etiqueta `employeeData`.

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

Para los campos cuyo modelo es un esquema XML, los datos se rellenan previamente en la etiqueta `afBoundData` como se muestra en el siguiente ejemplo XML. Se puede utilizar para rellenar previamente un formulario adaptable con uno o más campos de texto no enlazados.

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
>Se recomienda no utilizar campos no enlazados en paneles enlazados (paneles no vacíos `bindRef` que se hayan creado al arrastrar componentes de la barra de tareas o de la pestaña Fuentes de datos). Podría causar la pérdida de los datos de estos campos independientes. Además, se recomienda que los nombres de los campos sean únicos en todo el formulario, especialmente para los campos independientes.

#### Un ejemplo sin los envoltorios afData y afBoundData  {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### Formularios adaptables basados en esquemas JSON {#json-schema-based-adaptive-forms}

Para formularios adaptables basados en el esquema JSON, la estructura de JSON de relleno previo y JSON enviado se describe a continuación. Para obtener más información, consulte [Crear formularios adaptables mediante el esquema JSON](adaptive-form-json-schema-form-model.md).

- **Estructura JSON de relleno previo**: El JSON de relleno previo debe ser compatible con el esquema JSON asociado. Opcionalmente, se puede envolver en el objeto /afData/afBoundData si también desea rellenar previamente los campos no enlazados.
- **Estructura JSON enviada**: Si no se utiliza un JSON de relleno previo, el JSON enviado contiene datos para los campos enlazados y no enlazados en la etiqueta de envoltorio afData. Si se utiliza el JSON de relleno previo, el JSON enviado tendrá la misma estructura que el JSON de relleno previo. Si el JSON de relleno previo comienza con el objeto raíz afData, el JSON de salida tendrá el mismo formato. Si el JSON de relleno previo no tiene un envoltorio afData/afBoundData y en su lugar comienza directamente desde el objeto raíz del esquema como usuario, el JSON enviado también comenzará con el objeto de usuario.

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

Para los campos que utilizan el modelo de esquema JSON, los datos se rellenan previamente en el objeto afBoundData como se muestra en el siguiente archivo JSON de ejemplo. Se puede utilizar para rellenar previamente un formulario adaptable con uno o más campos de texto no enlazados. A continuación se muestra un ejemplo de datos con `afData/afBoundData` envoltorio:

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
> **No** se recomienda el uso de campos no enlazados en paneles enlazados (paneles con bindRef no vacíos que se hayan creado al arrastrar componentes de la barra de tareas o la pestaña Fuentes de datos) recomendado, ya que podría causar la pérdida de datos de los campos independientes. Se recomienda tener nombres de campo únicos en todo el formulario, especialmente en los campos no enlazados.
>

### Formulario adaptable sin modelo de formulario {#adaptive-form-with-no-form-model}

Para formularios adaptables sin modelo de formulario, los datos de todos los campos se encuentran en la etiqueta `<data>` de `<afUnboundData> tag`.

Asimismo, tome nota de lo siguiente:

Las etiquetas XML para los datos de usuario enviados para varios campos se generan al utilizar el nombre de los campos. Por lo tanto, los nombres de campo deben ser únicos.

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

## Configuración del servicio de relleno previo {#configuring-prefill-service-using-configuration-manager}

Utilice la propiedad `alloweddataFileLocations` de la configuración **predeterminada del servicio de relleno previo** para establecer la ubicación de los archivos de datos o una regex (expresión regular) para las ubicaciones de los archivos de datos.

El siguiente archivo JSON muestra un ejemplo:

```JSON
  {
  "alloweddataFileLocations": "`file:///C:/Users/public/Document/Prefill/.*`"
  }
```

Para establecer los valores de una configuración, consulte [Generar configuraciones de OSGi mediante el SDK de AEM](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=es#generating-osgi-configurations-using-the-aem-sdk-quickstart) e [implemente la configuración](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=es#deployment-process) a su instancia de Cloud Service.

>[!NOTE]
>
> - De forma predeterminada, se permite el relleno previo mediante archivos crx para todos los tipos de formularios adaptables (XSD, XDP, JSON, FDM y sin modelo de formulario). El relleno previo solo se permite con archivos JSON y XML.
> - El protocolo crx se encarga de la seguridad de los datos rellenos previamente y, por lo tanto, está permitido de forma predeterminada. El relleno previo a través de otros protocolos mediante regex genéricas puede causar vulnerabilidad. En la configuración, especifique una configuración de URL segura para proteger los datos.

## El curioso caso de los paneles repetibles {#the-curious-case-of-repeatable-panels}

Por lo general, los campos enlazados (esquema de formulario) y no enlazados se crean en el mismo formulario adaptable, pero las siguientes son algunas excepciones en caso de que el enlace sea repetible:

- Los paneles repetibles no enlazados no son compatibles con los formularios adaptables que utilizan la plantilla de formulario XFA, XSD, el esquema JSON o el esquema FDM.
- No utilice campos independientes en paneles repetibles enlazados.

>[!NOTE]
>
> Como regla general, no mezcle campos enlazados y no enlazados si están intersectados en datos rellenos por el usuario final en campos no enlazados. Si es posible, debe modificar el esquema o la plantilla de formulario XFA y agregar una entrada para los campos no enlazados, de modo que también se conviertan en enlazados y sus datos estén disponibles como otros campos en los datos enviados.

## Protocolos admitidos para rellenar previamente datos de usuario {#supported-protocols-for-prefilling-user-data}

Los formularios adaptables se pueden rellenar previamente con datos de usuario en formato de datos de relleno previo cuando se configura con una regex válida mediante los siguientes protocolos:

### El protocolo crx:// {#the-crx-protocol}

```javascript
http
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

El nodo especificado debe tener una propiedad denominada `jcr:data` y mantener los datos.

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

- SERVICE_NAME hace referencia al nombre del servicio de relleno previo OSGI. Consulte [Crear y ejecutar un servicio de relleno previo](prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
- IDENTIFIER se refiere a cualquier metadato que requiera el servicio de relleno previo OSGI para recuperar los datos. Un identificador para el usuario que ha iniciado sesión es un ejemplo de metadatos que se pueden utilizar.

>[!NOTE]
>
> No se admite el paso de parámetros de autenticación.

### Configurar el atributo de datos en slingRequest {#setting-data-attribute-in-slingrequest}

También puede configurar el atributo `data` en `slingRequest`, donde el atributo `data` es una cadena que contiene XML o JSON, como se muestra en el siguiente código de ejemplo (el ejemplo es para XML):

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

Puede escribir una cadena XML o JSON simple que contenga todos los datos y establecerlos en slingRequest. Esto se puede hacer fácilmente en el JSP del procesador para cualquier componente que quiera incluir en la página donde puede establecer el atributo de datos slingRequest.

Por ejemplo, donde quiera un diseño específico para la página con un tipo específico de encabezado. Para lograrlo, puede escribir su propio `header.jsp`, que puede incluir en el componente de página y establecer el atributo`data`.

Otro buen ejemplo es un caso de uso en el que le gustaría rellenar previamente los datos de inicio de sesión a través de cuentas en redes sociales como Facebook, Twitter o LinkedIn. En este caso, puede incluir un JSP simple en `header.jsp`, que obtenga datos de la cuenta de usuario y establezca el parámetro de los datos.

prefill-page component.zip

[Obtener archivo](assets/prefill-page-component.zip)
Ejemplo de prefill.jsp en el componente de página

## [!DNL AEM Forms] servicio de relleno previo personalizado {#aem-forms-custom-prefill-service}

Puede utilizar el servicio de relleno previo personalizado para escenarios en los que se lean constantemente datos de una fuente predefinida. El servicio de relleno previo lee datos de orígenes de datos definidos y prefiere los campos del formulario adaptable con contenido del archivo de datos de relleno previo. También le ayuda a asociar de forma permanente los datos rellenos previamente con un formulario adaptable.

### Crear y ejecutar un servicio de relleno previo {#create-and-run-a-prefill-service}

El servicio de relleno previo es un servicio OSGi y se empaqueta a través del paquete OSGi. Puede crear el paquete OSGi, cargarlo e instalarlo en paquetes [!DNL AEM Forms]. Antes de empezar a crear el paquete, haga lo siguiente:

- [Descargue el  [!DNL AEM Forms] Cliente SDK](https://helpx.adobe.com/es/aem-forms/kb/aem-forms-releases.html)
- Descargue el paquete de plantillas

- Coloque el archivo de datos (datos de relleno previo) en el repositorio crx. Puede colocar el archivo en cualquier ubicación de la carpeta \content del repositorio crx.

[Obtener archivo](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Crear un servicio de relleno previo {#create-a-prefill-service}

El paquete de plantillas (paquete de servicio de relleno previo de muestra) contiene una implementación de muestra del servicio de relleno previo [!DNL AEM Forms]. Abra el paquete de plantillas en un editor de código. Por ejemplo, abra el proyecto de plantillas en Eclipse para editarlo. Después de abrir el paquete de plantillas en un editor de código, realice los siguientes pasos para crear el servicio.

1. Abra el archivo src\main\java\com\adobe\test\Prefill.java para editarlo.
1. En el código, establezca el siguiente valor:

   - `nodePath:` La variable de ruta del nodo que señala a la ubicación del repositorio crx contiene la ruta del archivo de datos (relleno previo). Por ejemplo, /content/prefilldata.xml
   - `label:` El parámetro Etiqueta especifica el nombre para mostrar del servicio. Por ejemplo, Servicio de relleno previo predeterminado

1. Guarde y cierre el archivo `Prefill.java`.
1. Agregue el paquete `AEM Forms Client SDK` a la ruta de la versión del proyecto de las plantillas.
1. Compile el proyecto y cree el .jar para el paquete.

#### Iniciar y utilizar el servicio de relleno previo {#start-and-use-the-prefill-service}

Para iniciar el servicio de relleno previo, cargue el archivo JAR en la [!DNL AEM Forms] consola web y active el servicio. Ahora, el servicio aparecerá en el editor de formularios adaptables. Para asociar un servicio de relleno previo a un formulario adaptable, haga lo siguiente:

1. Abra el formulario adaptable en el editor de formularios y abra el panel Propiedades del contenedor de formularios.
1. En la consola Propiedades, navegue hasta [!DNL AEM Forms] contenedor > Básico > Servicio de relleno previo.
1. Seleccione el servicio de relleno previo predeterminado y haga clic en **[!UICONTROL Guardar]**. El servicio estará asociado al formulario.

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