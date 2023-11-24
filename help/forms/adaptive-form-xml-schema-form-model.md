---
title: Cómo diseñar un esquema XML para un formulario adaptable
description: Aprenda a crear un esquema XML para un formulario adaptable y a un formulario adaptable basado en el esquema para generar datos de quejas de esquema.
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 5b8ad9a8-77d4-4234-a4d7-c8964b975e96
source-git-commit: 57e421a865b664c0adb7af93b33bd4b6b32049ab
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 100%

---

# Diseño de un esquema XML para un formulario adaptable {#creating-adaptive-forms-using-xml-schema}

## Requisitos previos {#prerequisites}

La creación de un formulario adaptable con un esquema XML como modelo de formulario requiere una comprensión básica de los esquemas XML. Además, se recomienda leer el siguiente contenido antes que este artículo.

* [Crear un formulario adaptable](creating-adaptive-form.md)
* [Esquema XML](https://www.w3.org/TR/xmlschema-2/)

## Uso de un esquema XML como modelo de formulario {#using-an-xml-schema-as-form-model}

[!DNL Experience Manager Forms] admite la creación de un formulario adaptable utilizando un esquema XML existente como modelo de formulario. Este esquema XML representa la estructura en la que el sistema back-end de su organización produce o consume datos.

Estas son las características clave del uso de un esquema XML:

* La estructura del XSD se muestra como un árbol en la pestaña Buscador de contenido en el modo Autor de un formulario adaptable. Puede arrastrar y agregar un elemento de la jerarquía XSD al formulario adaptable.
* Puede rellenar previamente el formulario utilizando XML que cumpla con el esquema asociado.
* Al realizar el envío, los datos introducidos por el usuario se envían como XML que se ajusta al esquema asociado.

Un esquema XML consta de tipos de elementos simples y complejos. Los elementos tienen atributos que agregan reglas al elemento. Cuando estos elementos y atributos se arrastran a un formulario adaptable, se asignan automáticamente al componente del formulario adaptable correspondiente.

Esta asignación de elementos XML a componentes de formulario adaptable es la siguiente:

<table>
 <tbody>
  <tr>
   <th><strong>Elemento o atributo XML </strong></th>
   <th><strong>Componente de formulario adaptable</strong></th>
  </tr>
  <tr>
   <td><code>xs:string</code></td>
   <td>Cuadro de texto</td>
  </tr>
  <tr>
   <td><code>xs:boolean</code></td>
   <td>Casilla de verificación</td>
  </tr>
  <tr>
   <td>
    <ul>
     <li><code>xs:unsignedInt</code></li>
     <li><code>xs:xs:int</code></li>
     <li><code class="code">xs:decimal
        </code></li>
     <li>Todos los tipos de valores numéricos</li>
    </ul> </td>
   <td>Cuadro numérico</td>
  </tr>
  <tr>
   <td><code>xs:date</code></td>
   <td>Selector de fecha</td>
  </tr>
  <tr>
   <td><code class="code">xs:enumeration
      </code></td>
   <td>Desplegable</td>
  </tr>
  <tr>
   <td>Cualquier elemento de tipo complejo</td>
   <td>Panel</td>
  </tr>
 </tbody>
</table>

## Esquema XML de ejemplo {#sample-xml-schema}

Este es un ejemplo de esquema XML.

```xml
<?xml version="1.0" encoding="utf-8" ?>
    <xs:schema targetNamespace="https://adobe.com/sample.xsd"
                    xmlns="https://adobe.com/sample.xsd"
                    xmlns:xs="https://www.w3.org/2001/XMLSchema"
                >

        <xs:element name="sample" type="SampleType"/>

        <xs:complexType name="SampleType">
            <xs:sequence>
                <xs:element name="leaderName" type="xs:string" default="Enter Name"/>
                <xs:element name="assignmentStartBirth" type="xs:date"/>
                <xs:element name="gender" type="GenderEnum"/>
                <xs:element name="noOfProjectsAssigned" type="IntType"/>
                <xs:element name="assignmentDetails" type="AssignmentDetails"
                                            minOccurs="0" maxOccurs="10"/>
            </xs:sequence>
        </xs:complexType>

        <xs:complexType name="AssignmentDetails">
            <xs:attribute name="name" type="xs:string" use="required"/>
            <xs:attribute name="durationOfAssignment" type="xs:unsignedInt" use="required"/>
            <xs:attribute name="numberOfMentees" type="xs:unsignedInt" use="required"/>
             <xs:attribute name="descriptionOfAssignment" type="xs:string" use="required"/>
             <xs:attribute name="financeRelatedProject" type="xs:boolean"/>
       </xs:complexType>
  <xs:simpleType name="IntType">
            <xs:restriction base="xs:int">
            </xs:restriction>
        </xs:simpleType>
  <xs:simpleType name="GenderEnum">
            <xs:restriction base="xs:string">
                <xs:enumeration value="Female"/>
                <xs:enumeration value="Male"/>
            </xs:restriction>
        </xs:simpleType>
    </xs:schema>
```

>[!NOTE]
>
>Asegúrese de que el esquema XML tenga solo un elemento raíz. No se admiten esquemas XML con más de un elemento raíz.

## Adición de propiedades especiales a campos mediante un esquema XML {#adding-special-properties-to-fields-using-xml-schema}

Puede añadir los siguientes atributos a los elementos de esquema XML para añadir propiedades especiales a los campos del formulario adaptable asociado.

<table>
 <tbody>
  <tr>
   <th><strong>Propiedad de esquema</strong></th>
   <th><strong>Uso en el formulario adaptable</strong></th>
   <th><strong>Admitido en </strong></th>
  </tr>
  <tr>
   <td><code>use=required </code></td>
   <td>Marca un campo obligatorio<br /> </td>
   <td>Atributo</td>
  </tr>
  <tr>
   <td><code>default="default value"</code></td>
   <td>Agrega un valor predeterminado</td>
   <td>Elemento y atributo</td>
  </tr>
  <tr>
   <td><code>minOccurs="3"</code></td>
   <td><p>Especifica ocurrencias mínimas</p> <p>(Para subformularios repetibles (tipos complejos))</p> </td>
   <td>Elemento (tipo complejo)</td>
  </tr>
  <tr>
   <td><code class="code">maxOccurs="10"
      </code></td>
   <td><p>Especifica el número máximo de ocurrencias</p> <p>(Para subformularios repetibles (tipos complejos))</p> </td>
   <td>Elemento (tipo complejo)</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Al arrastrar un elemento de esquema a un formulario adaptable, se genera una descripción predeterminada de las siguientes formas:
>
>* al poner en mayúscula el primer carácter del nombre del elemento;
>* al insertar un espacio en blanco en los límites de Camel Case.
>
>Por ejemplo, si agrega el elemento de esquema `userFirstName`, la descripción generada en el formulario adaptable es `User First Name`.

## Limitar los valores aceptables para un componente de formulario adaptable {#limit-acceptable-values-for-an-adaptive-form-component}

Puede añadir las siguientes restricciones a los elementos de esquema XML para limitar los valores aceptables para un componente de formulario adaptable:

<table>
 <tbody>
  <tr>
   <td><p><strong> Propiedad de esquema</strong></p> </td>
   <td><p><strong>Tipo de datos</strong></p> </td>
   <td><p><strong>Descripción</strong></p> </td>
   <td><p><strong>Componente</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>totalDigits</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el número máximo de dígitos permitidos en un componente. El número de dígitos especificado debe ser mayor que cero.</p> </td>
   <td>
    <ul>
     <li>Cuadro numérico</li>
     <li>Stepper numérico</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el límite superior para valores numéricos y fechas. Se incluye el valor máximo de forma predeterminada.</p> </td>
   <td>
    <ul>
     <li>Cuadro numérico</li>
     <li>Stepper numérico<br /> </li>
     <li>Selector de fecha</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el límite inferior para valores numéricos y fechas. Se incluye el valor mínimo de forma predeterminada.</p> </td>
   <td>
    <ul>
     <li>Cuadro numérico</li>
     <li>Stepper numérico</li>
     <li>Selector de fecha</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Si es true, el valor numérico o la fecha especificados en el componente del formulario deben ser menores que el valor numérico o la fecha especificados para la propiedad máxima.</p> <p>Si es false, el valor numérico o la fecha especificados en el componente del formulario deben ser menores o iguales al valor numérico o a la fecha especificados para la propiedad máxima.</p> </td>
   <td>
    <ul>
     <li>Cuadro numérico</li>
     <li>Stepper numérico</li>
     <li>Selector de fecha</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booleano</p> </td>
   <td><p>Si es true, el valor numérico o la fecha especificados en el componente del formulario deben ser mayores que el valor numérico o la fecha especificados para la propiedad mínima.</p> <p>Si es false, el valor numérico o la fecha especificados en el componente del formulario deben ser mayores o iguales al valor numérico o la fecha especificados para la propiedad mínima.</p> </td>
   <td>
    <ul>
     <li>Cuadro numérico</li>
     <li>Stepper numérico</li>
     <li>Selector de fecha</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el número mínimo de caracteres permitidos en un componente. La longitud mínima debe ser igual o mayor de cero.</p> </td>
   <td>
    <ul>
     <li>Cuadro de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>maxLength</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el número máximo de caracteres permitidos en un componente. La longitud máxima debe ser mayor que cero.</p> </td>
   <td>
    <ul>
     <li>Cuadro de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>length</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el número exacto de caracteres permitidos en un componente. La longitud debe ser igual o mayor que cero.</p> </td>
   <td>
    <ul>
     <li>Cuadro de texto</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>fractionDigits</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica el número máximo de decimales permitido en un componente. fractionDigits debe ser igual o mayor que cero.</p> </td>
   <td>
    <ul>
     <li> Cuadro numérico con tipo de datos flotante o decimal</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Cadena</p> </td>
   <td><p>Especifica la secuencia de caracteres. Un componente acepta los caracteres si se ajustan al patrón especificado.</p> <p>La propiedad pattern se asigna al patrón de validación del componente de formulario adaptable correspondiente.</p> </td>
   <td>
    <ul>
     <li>Todos los componentes de formulario adaptable asignados a un esquema XSD </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## Preguntas frecuentes {#frequently-asked-questions}

**Tengo una estructura larga y compleja en el Buscador de contenido. ¿Cómo puedo encontrar un elemento específico?**

Tiene dos opciones:

* Desplazarse por la estructura de árbol
* Utilizar el cuadro Buscar para buscar un elemento

**¿Qué es bindRef?**

`bindRef` es la conexión entre un componente de formulario adaptable y un elemento o atributo de esquema. Determina en qué `XPath` está disponible el valor capturado de este componente o campo en el XML de salida. `bindRef` también se utiliza cuando se rellena previamente un valor de campo de un XML prerellenado (rellenado previamente).

**¿Por qué no puedo arrastrar elementos individuales de un subformulario (estructura generada a partir de cualquier tipo complejo) para subformularios repetibles (los valores minOccours o maxOccurs son superiores a 1)?**

En un subformulario repetible, debe utilizar el subformulario Completo. Si solo le interesan los campos selectivos, utilice toda la estructura y elimine los no deseados.

>[!MORELIKETHIS]
>
>* [Diseño de un esquema JSON para un formulario adaptable](/help/forms/adaptive-form-json-schema-form-model.md)