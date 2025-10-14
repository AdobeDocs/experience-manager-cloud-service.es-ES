---
title: Crear apariciones personalizadas en formularios HTML5
description: Puede conectar widgets personalizados a formularios Mobile. Puede ampliar los widgets de jQuery existentes o desarrollar los suyos propios personalizados.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 76bd1e2d-9e65-452c-8cef-123d28886a62
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 92%

---

# Crear apariciones personalizadas en formularios HTML5{#create-custom-appearances-in-html-forms}

<span class="preview">: la funcionalidad HTML5 Forms se ofrece como parte del programa de acceso anticipado. Para solicitar acceso, envíe un correo electrónico con el ID de correo electrónico oficial (de trabajo) a aem-forms-ea@adobe.com.
</span>

Puede conectar widgets personalizados a formularios Mobile. Puede ampliar los widgets de jQuery existentes o desarrollar sus propios widgets personalizados mediante el marco de aspectos visuales. El motor XFA utiliza varios widgets, consulte [Marco de apariencia para formularios adaptables y HTML5](/help/forms/custom-widgets.md) para obtener información detallada.

![Ejemplo de widget predeterminado y personalizado &#x200B;](assets/custom-widgets.jpg)

Ejemplo de widget predeterminado y personalizado

## Integrar widgets personalizados con formularios HTML5 {#integrating-custom-widgets-with-html-forms}

### Crear un perfil  {#create-a-profile-nbsp}

Puede crear un perfil nuevo o elegir uno existente para agregar un widget personalizado. Para obtener más información sobre la creación de perfiles, consulte [Crear perfil personalizado](/help/forms/custom-profile.md).

### Crear un widget {#create-a-widget}

Los formularios HTML5 proporcionan una implementación de la estructura de widgets que se puede ampliar para crear widgets nuevos. La implementación es un widget jQuery *abstractWidget* que se puede ampliar para escribir un widget nuevo. El nuevo widget solo puede hacerse funcional al ampliar o anular las funciones mencionadas a continuación.

<table>
 <tbody>
  <tr>
   <td>Función/Clase</td>
   <td>Descripción</td>
  </tr>
  <tr>
   <td>procesar</td>
   <td>La función de procesamiento devuelve el objeto jQuery para el elemento HTML predeterminado del widget. El elemento HTML predeterminado debe ser de tipo enfocable. Por ejemplo, &lt;a&gt;, &lt;input&gt; y &lt;li&gt;. El elemento devuelto se usa como $userControl. Si $userControl especifica la restricción anterior, las funciones de la clase AbstractWidget funcionarán como se espera; de lo contrario, algunas de las API comunes (enfoque, clic) necesitarán cambios. </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>Devuelve un mapa para convertir eventos HTML en eventos XFA. <br /> {<br /> desenfoque: XFA_EXIT_EVENT,<br /> }<br /> Este ejemplo muestra que el desenfoque es un evento HTML y XFA_EXIT_EVENT es el evento XFA correspondiente. </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>Devuelve un mapa que proporciona detalles sobre qué acción realizar al cambiar una opción. Las claves son las opciones que se proporcionan al widget y los valores son las funciones a las que se llama cada vez que se detecta un cambio en esa opción. El widget proporciona controladores para todas las opciones comunes (excepto value y displayValue)</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>El marco de trabajo Widget carga la función cada vez que el valor del widget se guarda en el modelo XFAM (por ejemplo, en el evento de salida de un campo de texto). La implementación debe devolver el valor que se ha guardado en el widget. El controlador se proporciona con el nuevo valor para la opción.</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>De forma predeterminada, en XFA en el evento de entrada, se muestra el rawValue del campo. Se llama a esta función para mostrar rawValue al usuario. </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>De forma predeterminada, en XFA en el evento de salida se muestra el formattedValue del campo. Se llama a esta función para mostrar el formattedValue al usuario. </td>
  </tr>
 </tbody>
</table>

Para crear su propio widget, en el perfil creado anteriormente, incluya referencias del archivo JavaScript que contiene funciones anuladas y agregadas recientemente. Por ejemplo, *sliderNumericFieldWidget* es un widget para campos numéricos. Para utilizar el widget en el perfil en la sección del encabezado, incluya la siguiente línea:

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### Registrar un widget personalizado con el motor de scripts XFA  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

Cuando el código del widget personalizado esté listo, registre el widget con el motor de scripts mediante la `registerConfig` API para el [formulario Bridge](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/forms/developer-reference/form-bridge-apis). Toma widgetConfigObject como entrada.

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

La configuración del widget se proporciona como un objeto JSON (una colección de pares de valor clave) donde la clave identifica los campos y el valor representa el widget que se utilizará con esos campos. Una configuración de ejemplo tiene este aspecto:

```
*{*

*"identifier1" : "customwidgetname",
"identifier2" : "customwidgetname2",
..
}*
```

Donde “identifier” es un selector de CSS jQuery que representa un campo en particular, un conjunto de campos de un tipo en particular o todos los campos. A continuación, se enumera el valor del identificador en casos diferentes:

| Tipo de identificador | Identificador | Descripción |
|---|---|---|
| Campo particular con nombre fieldname | Identificador: “div.fieldname” | Todos los campos con el nombre “fieldname” se representan con el widget. |
| Todos los campos de tipo “type” (donde type es NumericField, DateField, etc.): | Identificador: “div.type” | Para Timefield y DateTimeField, el tipo es textfield, ya que estos campos no son compatibles. |
| Todos los campos | Identificador: “div.field” |  |
