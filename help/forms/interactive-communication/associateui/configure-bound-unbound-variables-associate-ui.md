---
title: Configurar variables enlazadas y no enlazadas para la interfaz de usuario asociada
description: 'Aprenda a configurar variables enlazadas y no enlazadas en Componentes de texto para la interfaz de usuario asociada: edite todo el bloque de texto en la vista previa del documento o edite variables individuales en el panel de entrada de datos.'
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="Se aplica a AEM Forms."
exl-id: configure-bound-unbound-variables-associate-ui
source-git-commit: b11e1b28aabba9e03553dc9e9394bff111facfee
workflow-type: tm+mt
source-wordcount: '1404'
ht-degree: 1%

---


# Configurar variables enlazadas y no enlazadas para la interfaz de usuario asociada

Las variables enlazadas y no enlazadas en los componentes **Texto** permiten que los asociados introduzcan o confirmen valores en la interfaz de usuario asociada. Una **variable enlazada** está enlazada a un campo del modelo de datos de formulario. Una **variable independiente** se define en el documento y no está vinculada al modelo de datos.

Los autores habilitan la edición asociada con **Permitir la edición por asociado** en el componente **Texto** o en variables individuales, no en ambos componentes **Texto**.

| Quién | Ventaja |
|-----|---------|
| **Autor (diseñador de comunicaciones interactivas)** | Elija si asocia la edición en línea en la vista previa o campo a campo en el panel de entrada de datos. |
| **Asociar (representante de servicio)** | Introduzca los datos en el flujo de trabajo que mejor se ajuste a la comunicación: edición en línea o entrada estructurada en panel. |

## Antes de empezar

Habilite **Associate View** en la comunicación interactiva antes de configurar las variables para la interfaz de usuario de Associate. Ver [IU asociada en el editor de comunicaciones interactivas](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md).

Los asociados deben ser miembros del grupo **forms-associates**.

## Variables enlazadas

Una variable enlazada se asigna a un campo del modelo de datos de formulario (por ejemplo, `deptName` en `GMFletter`).

- Inserte arrastrando un campo del panel **Modelo de datos** a un componente **Texto**.
- El panel de propiedades **Field** muestra **Name**, **Value**, **Display type** y **Binding**.

## Variables independientes

Una variable independiente se crea directamente en un componente **Text** y no está vinculada al modelo de datos de formulario (por ejemplo, `unboundvar`).

- El panel de propiedades **Field** muestra **Name**, **Value**, **Display type** y **Binding**.
- En **Asociar propiedades**, puede configurar **Información sobre herramientas** y **Validaciones**.


## Editar todo el componente Texto en la vista previa del documento

Active **Permitir edición por asociado** en el componente **Texto** y déjelo desactivado para cada variable enlazada y no enlazada dentro del texto. En la Vista asociada, el asociado selecciona el bloque de texto en la vista previa del documento. Aparece todo el componente **Texto** con un límite púrpura y una barra de herramientas de formato.

### Configuración

1. Abra la comunicación interactiva en el Editor de comunicaciones interactivas, en la ficha **Diseño**.

1. En el panel **Jerarquía de componentes**, seleccione el componente **Texto** que contiene las variables enlazadas y no enlazadas; por ejemplo, **Texto7**.

1. Confirme que el texto incluye variables enlazadas y no enlazadas. Por ejemplo:

   - **Enlace de datos: deptName**
   - **Sin enlazar: unboundvar**

   ![Seleccionar componente de texto con variables enlazadas y no enlazadas](/help/forms/interactive-communication/assets/bound-unbound-variable1.png)

1. En el panel de propiedades **Texto**, confirme que **Permitir edición por asociado** es **de descuento** para cada variable enlazada y no enlazada dentro del texto.

1. Con el componente **Texto** aún seleccionado, active **Permitir edición por asociado** en el panel de propiedades de **Texto**.

1. Haga clic en **Guardar** y publique la comunicación interactiva.

### Verificar en la IU asociada

1. Abra la comunicación interactiva en **vista asociada**.

1. Seleccione el bloque de texto en la vista previa del documento. Confirme que el componente **Texto** aparece con un límite púrpura y una barra de herramientas de formato.

1. Edite contenido directamente en la vista previa; por ejemplo, actualice **Departamento de aplicaciones: enlazado a datos** e introduzca un valor después de **Sin enlazar:**. Confirme que las variables enlazadas y no enlazadas se han actualizado correctamente.

   ![Editar todo el componente de texto en línea en la IU asociada](/help/forms/interactive-communication/assets/bound-unbound-variable2.png)

1. Si lo desea, seleccione **Vista previa de impresión** para confirmar que la salida generada coincida con la vista previa.


## Editar variables individuales en el panel de entrada de datos

Desactive **Permitir edición por asociado** en el componente **Texto**. Actívelo para cada variable enlazada o no enlazada que desee que editen los asociados. En la Vista asociada, cada variable habilitada aparece como un campo independiente en el panel de entrada de datos de la izquierda.

### Configuración

1. Abra la comunicación interactiva en el Editor de comunicaciones interactivas, en la ficha **Diseño**.

1. En el panel **Jerarquía de componentes**, seleccione la variable enlazada; por ejemplo, **deptName[1]**.

1. En el panel de propiedades **Campo**:

   - Confirme que **Name** está establecido en `deptName`.
   - Establezca **Tipo de presentación** según sea necesario (por ejemplo, **Sin patrón**).
   - Activar **Permitir edición por asociado**.

   ![Configurar la variable enlazada deptName para la interfaz de usuario asociada](/help/forms/interactive-communication/assets/bound-unbound-variable3.png)

1. En el panel **Jerarquía de componentes**, seleccione la variable independiente; por ejemplo, **unboundvar**.

1. En el panel de propiedades **Campo**:

   - Confirme que **Name** está establecido en `unboundvar`.
   - Activar **Permitir edición por asociado**.
   - Si lo desea, puede configurar **Información sobre herramientas** y **Validaciones** en **Propiedades asociadas**.

   ![Configurar variable independiente unboundvar para la interfaz de usuario asociada](/help/forms/interactive-communication/assets/bound-unbound-variable4.png)

1. Confirmar que **Permitir la edición por asociado** está **desactivado** en el componente **Texto** principal.

1. Haga clic en **Guardar** y publique la comunicación interactiva.

### Verificar en la IU asociada

1. Abra la comunicación interactiva en **vista asociada**.

1. Confirme que cada variable con **Permitir edición por asociado** habilitado aparece en el panel izquierdo de entrada de datos, por ejemplo, **deptName** y **unboundvar**.

1. Escriba **Departamento de aplicaciones** para **deptName**. Deje **unboundvar** vacío y confirme que la vista previa del documento muestra el nombre de la variable como un marcador de posición; por ejemplo, **Sin enlazar: unboundvar**.

   ![Verificar variables enlazadas y no enlazadas en el panel de entrada de datos de la IU asociada](/help/forms/interactive-communication/assets/bound-unbound-variable5.png)

1. Escriba **Variable independiente** para **unboundvar** y confirme las actualizaciones de la vista previa del documento en tiempo real:

   - **Enlace de datos: Departamento de APP** refleja el valor ingresado para la variable enlazada.
   - **Sin enlazar: la variable sin enlazar** refleja el valor ingresado para la variable sin enlazar.

   ![Verificar el valor de la variable independiente en la interfaz de usuario asociada](/help/forms/interactive-communication/assets/bound-unbound-variable6.png)

1. Si lo desea, seleccione **Vista previa de impresión** para confirmar que la salida generada coincida con la vista previa.


## Nombres de variables duplicados (enlazados y no enlazados)

Cuando las variables enlazadas y no enlazadas con el mismo nombre aparecen en varias ubicaciones en el lienzo de diseño, solo aparece una instancia de cada nombre de variable en el panel de entrada de datos de la izquierda. La asociada introduce cada valor una vez; se propaga automáticamente a todas las apariciones correspondientes en la vista previa del documento.

### Configuración

1. Abra la comunicación interactiva en el Editor de comunicaciones interactivas, en la ficha **Diseño**.

1. Agregue un **subformulario** o componentes **Texto** adicionales en el lienzo de diseño e inserte variables enlazadas y no enlazadas duplicadas en cada ubicación. Por ejemplo, añada dos bloques que contengan cada uno:

   - **Enlace de datos: deptName**
   - **Sin enlazar: unboundvar**

   ![Configurar variables enlazadas y no enlazadas duplicadas en subformularios](/help/forms/interactive-communication/assets/bound-unbound-variable7.png)

1. En el panel **Jerarquía de componentes**, seleccione cada variable enlazada y no enlazada y active **Permitir edición por asociado** en el panel de propiedades **Campo**.

1. Confirmar que **Permitir la edición por asociado** está **desactivado** en los componentes **Texto** principales.

1. Haga clic en **Guardar** y publique la comunicación interactiva.

### Verificar en la IU asociada

1. Abra la comunicación interactiva en **vista asociada**.

1. Confirme solo un campo **deptName** y un campo **unboundvar** que aparecen en el panel de entrada de datos de la izquierda, incluso cuando cada variable se produce en varias ubicaciones en el lienzo de diseño.

1. Escriba **Departamento de aplicaciones** para **deptName**. Deje **unboundvar** vacío y confirme ambas ocurrencias en la actualización de la vista previa del documento; por ejemplo, cada bloque muestra **Departamento de APP** y **Independiente: unboundvar**.

   ![Verificar la propagación de variables duplicadas en la interfaz de usuario asociada](/help/forms/interactive-communication/assets/bound-unbound-variable8.png)

1. Si lo desea, seleccione **Vista previa de impresión** para confirmar que la salida generada coincida con la vista previa.


## Consideraciones

**Nombres de variables duplicados (enlazados y no enlazados)**

Cuando las variables enlazadas y no enlazadas comparten el mismo nombre de variable:

- Solo aparece una instancia en el panel de entrada de datos de la izquierda.
- En la vista previa del documento solo se actualizan las variables para las que está habilitada la edición asociada.
- La asociada introduce el valor una vez en el panel de entrada de datos; se propaga automáticamente a todas las apariciones correspondientes en la vista previa del documento.

**Variables no enlazadas con el mismo nombre pero con valores predeterminados diferentes**

Cuando varias variables independientes comparten un nombre de variable pero utilizan valores predeterminados diferentes, la interfaz de usuario de asociación muestra el valor predeterminado de la primera variable para la que la edición de asociaciones está habilitada en el panel de entrada de datos de la izquierda.

**Variables enlazadas con el mismo nombre pero diferentes rutas de referencia de datos**

Cuando varias variables enlazadas comparten un nombre de variable pero utilizan diferentes rutas de referencia de datos, el panel izquierdo de entrada de datos muestra el valor de la primera variable para la que está habilitada la edición de asociaciones. Cualquier valor introducido o actualizado por la asociada en el panel de entrada de datos se propaga a todas las variables con ese nombre, independientemente de sus rutas de referencia de datos.

**Exclusividad mutua**

**Permitir la edición por asociado** en el componente **Texto** y en variables individuales enlazadas o no enlazadas dentro de él son mutuamente excluyentes. Habilitar un enfoque por componente **Texto**.

**Variables no enlazadas sin valor**

Cuando una variable independiente tiene habilitada la edición asociada pero no se introduce ningún valor, la vista previa del documento puede mostrar el nombre de la variable (por ejemplo, `unboundvar`) hasta que la asociada proporcione un valor en el panel de entrada de datos.

## Preguntas frecuentes

**¿Cuál es la diferencia entre editar todo el componente Texto y editar variables individuales?**
Cuando habilita la edición asociada en el componente **Texto**, la asociada edita todo el bloque de texto en línea en la vista previa del documento (límite púrpura). Cuando habilita la edición asociada en variables individuales, cada variable habilitada aparece como un campo independiente en el panel de entrada de datos de la izquierda.

**¿Por qué no puedo habilitar la edición asociada en el componente Texto y en las variables individuales?**
La edición asociada en el componente **Texto** y en las variables enlazadas o no enlazadas dentro de él es mutuamente excluyente. Habilitar la edición en todo el bloque de texto o en variables individuales, no en ambas.

**¿Por qué mi variable independiente muestra el nombre de la variable en lugar de un valor en la vista previa?**
Es probable que la asociada aún no haya introducido un valor. Con la edición asociada habilitada en variables individuales y sin ningún **valor** predeterminado configurado, la vista previa puede mostrar el nombre de la variable hasta que se introduzcan datos en el panel de entrada de datos.

**¿Cuál es la diferencia entre una variable enlazada y una independiente?**
Una variable enlazada está enlazada a un campo del modelo de datos de formulario a través de la configuración **Enlace**. Una variable independiente se define en el documento y no está vinculada al modelo de datos.

**¿Qué sucede cuando dos variables comparten el mismo nombre?**
Solo aparece una instancia en el panel de entrada de datos de la izquierda. La asociada introduce el valor una vez en el panel de entrada de datos y se propaga automáticamente a todas las apariciones correspondientes en la vista previa del documento.

## Ver también

- [Asociar interfaz de usuario en el editor de comunicaciones interactivas](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Configurar las opciones desplegables de la interfaz de usuario asociada](/help/forms/interactive-communication/associateui/configure-dropdown-options-binding.md)
- [Habilitar y configurar la interfaz de usuario asociada para comunicaciones interactivas](/help/forms/interactive-communication/enable-configure-associate-ui.md)
- [Componente de variable independiente en el editor de comunicaciones interactivas](/help/forms/interactive-communication/unbound-variable.md)


