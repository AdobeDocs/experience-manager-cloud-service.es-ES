---
title: Etiquetas de marcado HTML compatibles en el PDF de envío (anteriormente, documento de registro)
description: Guía de referencia para etiquetas de marcado de HTML admitida al generar un PDF de envío (anteriormente, documento de registro), incluidas las consideraciones de comportamiento de procesamiento y accesibilidad.
feature: Adaptive Forms
role: Developer, User
exl-id: 8481b0dc-aae7-4bd2-acfe-1f1b6d747683
source-git-commit: 0b112a5a1830fac9d0170771e052bbb2ef3cadbf
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 6%

---


# Etiquetas de marcado HTML compatibles en el PDF de envío (anteriormente, documento de registro)

## ¿Qué abarca esta referencia?

AEM Forms ahora admite etiquetas de marcado de HTML en campos de texto enriquecido al generar un PDF de PDF de envío (anteriormente, documento de registro). En esta guía se explica qué etiquetas de marcado de HTML se pueden utilizar de forma segura en Forms adaptable y cómo se representan en el PDF de envío generado.

Si agrega contenido de texto enriquecido (como formato de negrita, listas o vínculos) a los formularios, es importante comprender qué etiquetas son compatibles y las limitaciones que pueden tener. Esta referencia le ayuda a elegir las etiquetas adecuadas para garantizar que el contenido se muestra correctamente y permanece accesible en la PDF de envío.

## Antes de comenzar

### Requisitos previos

Debe estar familiarizado con lo siguiente:

- Sintaxis básica de marcado de HTML
- [Aspectos básicos de PDF (anteriormente Documento de registro) de envío](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- Principios de accesibilidad y directrices WCAG
- Requisitos de accesibilidad de PDF
- Componentes de formularios adaptables que aceptan marcado de HTML

### Consideraciones

El PDF de envío (anteriormente, documento de registro) puede ser un PDF etiquetado, que ayuda a garantizar la accesibilidad y la estructura adecuada para las tecnologías de asistencia. Para habilitar la salida de PDF etiquetado, [establezca la propiedad XCI `config/present/pdf/tagged` en `true`](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#use-a-custom-xci-file). Después de generar el PDF, es importante comprobar que las etiquetas de accesibilidad se aplican correctamente. Puede usar [Adobe Acrobat para comprobar las etiquetas de accesibilidad](https://helpx.adobe.com/in/acrobat/using/create-verify-pdf-accessibility.html) y asegurarse de que el documento cumpla los estándares de accesibilidad.

### Novedades

La compatibilidad con texto enriquecido en PDF de envío es una mejora reciente. Anteriormente, el contenido de texto enriquecido aparecía como texto sin formato en documentos generados. Esta nueva funcionalidad permite que el contenido formateado se represente correctamente en las salidas de PDF.

## Referencia de compatibilidad con etiquetas de HTML

### Etiquetas totalmente compatibles

Estas etiquetas son totalmente compatibles con la creación adecuada de nodos de accesibilidad:

| Etiqueta de HTML | Descripción | Compatibilidad con PDF de envío | Accesibilidad | Ejemplo |
|----------|-------------|-------------|---------------|---------|
| `<p>` | Párrafo | Sí | Totalmente compatible: nodo `<P>` correcto | `<p>This is a paragraph.</p>` |
| `<br/>` | Salto de línea | Sí | Totalmente compatible: en el nodo `<P>` | `<p>Line 1<br/>Line 2</p>` |
| `<b>` | Texto en negrita | Sí | Totalmente compatible: en el nodo `<P>` | `<b>bold text</b>` |
| `<i>` | Texto en cursiva | Sí | Totalmente compatible: en el nodo `<P>` | `<i>italic text</i>` |
| `<span>` | Contenedor en línea genérico | Sí | dentro de elementos de bloque | `<span>styled text</span>` |
| `<sub>` | Subíndice | Sí | Totalmente compatible: dentro de elementos de bloque | `H<sub>2</sub>O` |
| `<sup>` | Superíndice | Sí | Totalmente compatible: dentro de elementos de bloque | `E=mc<sup>2</sup>` |
| `<a>` | Hipervínculo | Sí | Soporte limitado: necesita un anidamiento adecuado | `<a href="url">link text</a>` |


#### Problema de accesibilidad de lista

La representación de la lista actual crea `<P>` nodos en lugar de la estructura de lista adecuada:

```
Current: <P>1. First item
Current: <P>2. Second item

Expected: <L>
Expected:   <LI>
Expected:     <LBL>1.
Expected:     <LBody>First item
```

### Etiquetas no admitidas

Estas etiquetas no son compatibles y no se renderizarán correctamente:

| Etiqueta de HTML | Descripción | Solución alternativa |
|----------|-------------|---------------------|
| `<h1>` - `<h6>` | Etiquetas de encabezado | Usar etiquetas `<p>` con estilo o encabezados de nivel de diseño |
| `<img>` | Imágenes | Utilizar campos de imagen o plantillas de diseño independientes |
| `<code>` | Bloques de código | Usar fuentes monospace con estilo `<span>` |
| `<blockquote>` | Bloquear presupuestos | Usar etiquetas `<p>` con estilo con sangría |
| `<table>` | Tablas | Uso de componentes de tabla de formulario adaptable |

## Ejemplos de código

### Formato de texto básico

```html
<!--  Supported - renders correctly -->
<p>This paragraph contains <b>bold text</b> and <i>italic text</i>.</p>

<!--  Supported - combined formatting -->
<p>This text is <i><b>bold and italic</b></i>.</p>

<!--  Unsupported - headings don't work -->
<h1>This won't render as a heading</h1>
```

### Listas

```html
<!-- ⚠️ Partially supported - renders but not accessible -->
<ol>
  <li>First numbered item</li>
  <li>Second numbered item</li>
</ol>

<ul>
  <li>First bullet point</li>
  <li>Second bullet point</li>
</ul>
```

### Vínculos

```html
<!--  Supported - but must be within block elements -->
<p>Visit our <a href="https://example.com">website</a> for more information.</p>

<!--  Incorrect - link not properly nested -->
<a href="https://example.com">Standalone link</a>
```

### Notación científica

```html
<!--  Supported - but limited accessibility -->
<p>Water formula: H<sub>2</sub>O</p>
<p>Einstein's equation: E=mc<sup>2</sup></p>
```

## Contenido relacionado


- [Generar PDF de envío (anteriormente documento de registro) para Forms adaptable](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
- [Generar PDF de envío para componentes principales](/help/forms/generate-document-of-record-core-components.md)
- [Personalización de plantillas de PDF de envío](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md#customize-the-branding-information-in-document-of-record)

