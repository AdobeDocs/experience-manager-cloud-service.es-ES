---
title: Subformulario en el editor de comunicaciones interactivas
description: Los subformularios del Editor de comunicaciones interactivas administran los diseños, controlan la colocación de los objetos y definen cómo fluye el contenido entre las páginas.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
hide: true
index: false
hidefromtoc: true
source-git-commit: 0c84fa812b74368184d7085fecbb11a1ce4dbfd9
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 10%

---


# Subformulario en el editor de comunicaciones interactivas

>[!NOTE]
>
> La capacidad de comunicación interactiva está disponible en el programa de usuarios pioneros. Envíe un correo electrónico desde su dirección de trabajo a `aem-forms-ea@adobe.com` para solicitar acceso.

>[!IMPORTANT]
>
> **Documentación sujeta a cambios**: esta biblioteca de indicaciones se está probando actualmente con el producto y está sujeta a actualizaciones y revisiones. Las indicaciones, ejemplos y prácticas recomendadas pueden cambiar a medida que Forms Experience Builder sigue evolucionando durante el programa para primeros usuarios.

## &#x200B;1. Introducción

Un subformulario en el editor de comunicaciones interactivas es un objeto contenedor utilizado para agrupar campos, objetos y componentes en una sección lógica. Ayuda a administrar diseños, controlar la colocación de objetos y definir cómo fluye el contenido entre páginas. Los subformularios son esenciales para crear comunicaciones estructuradas, reutilizables y adaptables, especialmente cuando se trata de contenido dinámico o repetido.

Mediante el uso de subformularios, los autores pueden mantener la coherencia, administrar la paginación y enlazar secciones completas a fuentes de datos estructuradas.

## &#x200B;2. Propiedades

2.1 Diseños de diseño de formulario

- **Diseño fijo:** Los objetos mantienen posiciones exactas en la página. Ideal para diseños estáticos en los que se requiere una colocación precisa (por ejemplo, facturas o cartas oficiales).

- **Diseño variable:** Los objetos se ajustan dinámicamente según la longitud del contenido y el tamaño de la pantalla. Adecuado para comunicaciones que requieren un diseño interactivo o diferentes longitudes de datos.

2.2 Colocación de subformularios

- **Paginación:** Controle cómo se dividen los subformularios en varias páginas. Las opciones incluyen mantener juntos los subformularios o permitir saltos de página dentro de ellos.

- **Posición:** Especifique si el subformulario se coloca en relación con su contenedor principal o si fluye de forma natural dentro del diseño.

- **Aspecto:** Defina el fondo, los bordes y el estilo para que el subformulario separe visualmente el contenido.

- **Presencia:** Configure las opciones de visibilidad (Visible, Oculto o Condicional) según las reglas de negocio o los valores de datos.

2.3 Enlace de datos

- Los subformularios se pueden enlazar directamente a **nodos o matrices del modelo de datos de formulario (FDM)**.

- El enlace permite que el subformulario se repita dinámicamente para cada registro de una colección (por ejemplo, varias directivas, transacciones o direcciones).

- Admite la población estática y dinámica de contenido en función de la estructura de datos.

## &#x200B;3. Uso

Los subformularios se utilizan ampliamente para:

- Estructurar documentos en secciones como encabezado, cuerpo y pie de página.

- Repetir contenido como tablas, listas desglosadas o listas de directivas.

- Administración de la paginación para que el contenido agrupado permanezca unido.

- Visualización condicional de secciones basadas en reglas o valores de datos.

- Aplicar el control de diseño (fijo o variable) según el tipo de comunicación.

Los autores pueden arrastrar un subformulario desde la Biblioteca de objetos al lienzo y ajustar su diseño, posición y enlace desde el Panel de propiedades.

## &#x200B;4. Prácticas recomendadas

- **Elija bien el diseño:** Utilice un diseño fijo para los formularios que requieran una ubicación exacta y un diseño fluido para las comunicaciones dinámicas basadas en datos.

- **Enlazar colecciones con cuidado:** Para listas o matrices, enlace subformularios directamente a colecciones FDM con filas de plantilla.

- **Optimizar paginación:** Evite los saltos incómodos al agrupar objetos relacionados en un subformulario.

- **Usar presencia condicional:** Ocultar o mostrar subformularios dinámicamente basados en valores de datos.

- **Mantener jerarquía:** Anide subformularios lógicamente para que los diseños complejos sean más fáciles de administrar.

- **Prueba con datos variados:** vista previa con conjuntos de datos cortos, largos y vacíos para garantizar que el diseño se adapte correctamente.

Al aprovechar los subformularios de forma eficaz, los autores pueden lograr diseños más limpios, un mejor control del contenido dinámico y garantizar que las comunicaciones se adapten sin problemas a escenarios estáticos y basados en datos.
