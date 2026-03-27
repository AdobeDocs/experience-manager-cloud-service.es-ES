---
title: Crear una tabla dinámica en el editor de comunicaciones interactivas
description: Crear una función de tabla dinámica que permita a los autores crear tablas controladas por datos.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="(Se aplica a AEM Forms)."
source-git-commit: 322183c28719db5b8657d9532ef234e1d18821cd
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---


# Crear una tabla dinámica en el editor de comunicaciones interactivas

## Información general

El Editor de comunicaciones interactivas proporciona una tabla dinámica
función que permite a los autores crear tablas impulsadas por datos cuyo contenido se rellena automáticamente durante la ejecución a partir de fuentes de datos estructuradas.

A diferencia de las tablas estáticas, donde las filas deben crearse manualmente, las tablas dinámicas se expanden o se contraen automáticamente en función de los registros devueltos desde un origen de datos enlazado. Esto las hace útiles para escenarios como extractos de facturación, historiales de transacciones, listas de productos o programaciones de directivas.

En este artículo se explica cómo insertar y configurar una tabla dinámica con enlace de datos, administrar el flujo de tablas de varias páginas y validar los recuentos de filas.

## Insertar una tabla dinámica

1. Abra **Editor de comunicaciones interactivas**.
1. Desde el **panel de componentes**, arrastre el **componente Tabla** al
lienzo.
1. Especifique el **número de columnas** y **filas iniciales** en el cuadro de diálogo, asegúrese de que se incluya la **fila de encabezado** y, a continuación, haga clic en Aceptar para crear la tabla.

### Enlazar datos a la tabla dinámica

Las tablas dinámicas rellenan filas automáticamente enlazándolas a un origen de datos repetible.

![Buscar documento CI](/help/forms/interactive-communication/assets/databinding-in-table.png)

Para enlazar datos a la tabla:

1. Seleccione la **fila de tabla** del panel de jerarquía.

1. Abra **Enlace de datos** desde el panel lateral.

1. Asegúrese de que el esquema de datos seleccionado sea de tipo matriz.

1. Arrastre y suelte el esquema de datos de matriz en la fila de tabla seleccionada para enlazar los datos.

### Habilitar flujo de página

Las tablas dinámicas pueden expandirse más allá de una sola página. Para permitir que la tabla crezca y continúe en todas las páginas, colóquela dentro de un contenedor de **contenido de posición variable**.

![Buscar documento CI](/help/forms/interactive-communication/assets/table-data-binding.png)

Para habilitar el flujo de página:

1. Seleccione el **contenedor de diseño principal** de la tabla.

1. Abra el panel Propiedades y establezca el Tipo de contenido en **De posición variable**.

1. Seleccione la tabla y asegúrese de que también está configurada para admitir contenido de flujo.

1. Previsualice la comunicación para comprobar que la tabla continúa en la página siguiente a medida que se procesan filas adicionales.

### Permitir Salto De Página En La Tabla

![Buscar documento CI](/help/forms/interactive-communication/assets/table-data-binding.png)

Para asegurarse de que la tabla se divide correctamente entre las páginas:

1. Seleccione la **tabla** en el lienzo.
1. Abra el panel **Propiedades**.
1. Habilitar **Permitir Salto De Página En El Contenido**.

Cuando se habilita, la tabla se divide automáticamente al final de una página y continúa en la siguiente página, con la fila de encabezado repetida.

### Configurar validación de filas

Puede controlar cuántas filas puede representar la tabla dinámica.

* **Filas mínimas:** Garantiza que la tabla procese al menos el número de filas especificado.
* **Filas máximas:** Limita el total de filas procesadas desde el origen de datos.
* **Filas iniciales:** define cuántas filas aparecen en el editor durante la vista previa en tiempo de diseño.

>[!NOTE]
>
> Si establece **Filas iniciales** en alrededor de **3-5** obtendrá una vista previa de diseño más realista antes de que se apliquen los datos de tiempo de ejecución.

## Capacidades clave

* Enlace de datos de columna: enlace cada columna a un campo del modelo de datos.

* Contenido de posición variable: permite que la tabla se expanda y continúe en todas las páginas.

* Compatibilidad con saltos de página: habilita los saltos de página en el nivel de fila dentro de la tabla.

* Mínimo de filas: Garantiza que se procese un número mínimo de filas.

* Máximo de filas: limita el total de filas procesadas desde el origen de datos.

* Filas iniciales: define las filas predeterminadas que se muestran durante la vista previa en tiempo de diseño.

La función Tabla dinámica del Editor de comunicaciones interactivas permite a los autores crear tablas flexibles controladas por datos sin escribir código personalizado. Al enlazar la tabla a una matriz de datos, habilitar el contenido de flujo, permitir saltos de página y configurar la validación de filas, los autores pueden producir comunicaciones estructuradas que se adapten sin problemas a distintos volúmenes de datos y, al mismo tiempo, mantengan un diseño coherente.
