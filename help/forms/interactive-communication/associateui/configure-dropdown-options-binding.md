---
title: Configurar las opciones desplegables de la interfaz de usuario asociada
description: Obtenga información sobre cómo configurar las opciones de enlace o las opciones estáticas manuales de los campos desplegables en el Editor de comunicaciones interactivas para que las opciones se representen correctamente en la IU asociada.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
badgeSaas: label="AEM Forms" type="Positive" tooltip="(Se aplica a AEM Forms)."
exl-id: configure-dropdown-options-associate-ui
source-git-commit: 7619c18a771191a1491447484195bc480b1d2708
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 2%

---


# Configurar las opciones desplegables de la interfaz de usuario asociada

Los campos desplegables del editor de comunicaciones interactivas utilizan un modelo centrado de **Enlace de opciones** para opciones dinámicas impulsadas por datos en la interfaz de usuario de Associate. **Enlace de datos** ya no se admite en los campos desplegables; los autores configuran **Enlace desde datos** (origen de datos enlazado) u opciones manuales estáticas en el panel **Propiedades**.

| Quién | Ventaja |
|-----|---------|
| **Autor (diseñador de comunicaciones interactivas)** | Ofrezca opciones desplegables precisas y basadas en datos a los asociados sin configuraciones de enlace de datos no admitidas. |
| **Asociar (agente/representante de servicio)** | Consulte la lista de opciones y el valor preseleccionados correctos al completar las comunicaciones con los clientes en la interfaz de usuario de asociado. |

## Antes de empezar

Habilite **Associate View** en la comunicación interactiva antes de configurar el comportamiento del menú desplegable para la interfaz de usuario de Associate. Ver [IU asociada en el editor de comunicaciones interactivas](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md).

Los asociados deben ser miembros del grupo **forms-associates**.

## Enlazar desde datos habilitados (opciones dinámicas)

Cuando **Options Source** está establecido en **Bind from Data**:

- Las opciones desplegables están totalmente controladas por el origen de datos enlazado configurado en **Opciones Ref**.
- Las opciones se representan y están disponibles para su selección en la interfaz de usuario de Associate.
- **Valor predeterminado** no está disponible; el primer valor de las opciones enlazadas se preseleccionará automáticamente cuando el formulario se presente a la asociada.

## Opciones manuales (opciones estáticas)

Cuando **Options Source** no está establecido en **Bind from Data**:

- Los autores agregan opciones manualmente a través del panel **Propiedades**.
- **Valor predeterminado** permanece disponible; el diseñador de formularios puede seleccionar explícitamente qué opción aparece como el valor preseleccionado en la interfaz de usuario de Associate.

## Configurar las opciones desplegables

1. Abra la comunicación interactiva en el Editor de comunicaciones interactivas.

1. En la ficha **Diseño**, seleccione el componente **Lista desplegable** en el lienzo de diseño.

1. Abra el panel **Propiedades**.

1. Configure el menú desplegable para la interfaz de usuario de Associate:

   - Definir **Pie de ilustración** en la etiqueta que los asociados ven en el panel de entrada de datos de la izquierda. Por ejemplo, ingrese **Mes de pago a plazos**.
   - En **Opciones de Source**, elija **Enlazar de datos** para rellenar opciones desde el modelo de datos o agregue opciones manuales para una lista estática.
   - Si seleccionó **Enlazar a partir de datos**, establezca **Opciones de referencia** en la ruta de datos que proporciona la lista de opciones. Por ejemplo, enlazar a `$.GMFletter.installmentDetails.installmentMonth`.

   No configure **Enlace de datos** en campos desplegables — use **Enlace de datos** o solamente opciones manuales.

   ![Configurar enlace de opciones desplegables](/help/forms/interactive-communication/assets/associate-ui-configure-drop-down1.png)

1. Activar **Permitir edición por asociado** para que los asociados puedan seleccionar un valor en la interfaz de usuario de asociado.

1. Si lo desea, puede configurar **Información sobre herramientas** y **Validaciones** en **Propiedades asociadas**.

1. Si usa opciones manuales, establezca **Valor predeterminado** según sea necesario.

1. Haga clic en **Guardar** y publique la comunicación interactiva.

## Verificar en la IU asociada

1. Abra la comunicación interactiva en la **vista asociada**.

1. Confirme que la lista desplegable aparece en el panel izquierdo de entrada de datos con el pie de ilustración que ha configurado. Por ejemplo, **Mes de pago a plazos** muestra opciones enlazadas como **Junio de 2026**, **Julio de 2026** y **Agosto de 2026**.

1. Compruebe que la primera opción de enlace está preseleccionada cuando se carga la interfaz de usuario de asociación.

1. Seleccione una opción diferente y confirme las actualizaciones de valor en la previsualización derecha. Por ejemplo, al seleccionar **Junio de 2026**, el texto del documento se actualiza a **Plazo mensual junio de 2026**.

   ![Verificar opciones desplegables en la IU asociada](/help/forms/interactive-communication/assets/associate-ui-configure-drop-down2.png)

## Consideraciones

- **No se admite el enlace de datos** para los campos desplegables. Use **Enlazar datos** para listas dinámicas u opciones manuales para listas estáticas.
- Con **Enlazar a partir de datos** habilitado, los asociados no pueden establecer un valor predeterminado personalizado; la primera opción enlazada siempre está preseleccionada.
- Con las opciones manuales, pruebe el **Valor predeterminado** en la vista previa de la interfaz de usuario asociada para confirmar que la opción esperada aparece antes de la publicación.
- **Permitir edición por asociado** debe estar habilitado para que el menú desplegable aparezca como un campo editable en el lado izquierdo de la interfaz de usuario de asociado.

## Preguntas frecuentes

**¿Por qué el valor predeterminado no está disponible para mi lista desplegable?**
El **valor predeterminado** está deshabilitado cuando **Opciones de Source** está establecido en **Enlazar desde datos**. El primer valor de la fuente de datos enlazada se preselecciona automáticamente en la interfaz de usuario de asociado.

**¿Puedo usar el enlace de datos y el enlace de opciones juntos en un menú desplegable?**
No. Los campos desplegables solo admiten **Enlazar a partir de datos** o opciones manuales. **Enlace de datos** no es compatible con los campos desplegables.

**¿Qué es el Ref. de opciones?**
**Ref. de opciones** es la ruta de referencia de datos que proporciona la lista de opciones cuando **Source de opciones** está establecido en **Enlazar desde datos**. Seleccione la ruta que apunta a la colección de valores de opción del modelo de datos de formulario.

**¿Cómo verifico las opciones desplegables antes de que los asociados utilicen la comunicación interactiva?**
Publique la comunicación interactiva y abra la vista previa de la interfaz de usuario de asociación. Confirme que las opciones enlazadas o manuales aparecen en el panel izquierdo de entrada de datos y que el valor preseleccionado coincide con la configuración.

## Ver también

- [Asociar interfaz de usuario en el editor de comunicaciones interactivas](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Configurar variables enlazadas y no enlazadas para la interfaz de usuario asociada](/help/forms/interactive-communication/associateui/configure-bound-unbound-variables-associate-ui.md)
- [Crear una comunicación interactiva](/help/forms/interactive-communication/create-interactive-communication.md)
