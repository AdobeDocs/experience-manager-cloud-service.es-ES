---
title: Habilitar y configurar la interfaz de usuario asociada para comunicaciones interactivas
description: Obtenga información sobre cómo habilitar la Vista de asociación y configurar el flujo de trabajo para las actualizaciones en la Configuración de comunicaciones interactivas, de modo que los asociados puedan utilizar la IU de asociación.
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
exl-id: 5f8371f9-b4a6-4cae-a9d3-cfd744b66702
source-git-commit: ea372529b504ed70b74171e75d1d54f98fef432c
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---

# Habilitar y configurar la interfaz de usuario asociada para comunicaciones interactivas


En este artículo se describe cómo habilitar la interfaz de usuario de asociado para una comunicación interactiva (CI) y, opcionalmente, configurar un flujo de trabajo de AEM para los envíos. Los autores realizan estos pasos en **Configuración de la comunicación interactiva**.

Para obtener una descripción general de la interfaz de usuario asociada y las funciones de usuario, consulte [Interfaz de usuario asociada en el editor de comunicaciones interactivas](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md).

## Requisitos previos

Antes de habilitar y configurar la interfaz de usuario de Associate, asegúrese de lo siguiente:

- **Acceso de autor** al editor de comunicaciones interactivas.
- Se ha creado una **comunicación interactiva** con el diseño y los enlaces de datos necesarios.
- Se agregaron **usuarios asociados** al grupo **forms-associates** (necesario para que los asociados tengan acceso a la interfaz de usuario asociada).
- Se agregaron **autores** al grupo **forms-associates** (necesario para que los autores tengan acceso a la interfaz de usuario de Associate).

Cuando esté listo para integrar la interfaz de usuario de Associate con la aplicación e invocarla en la instancia de Publish, también necesitará un explorador con la compatibilidad emergente habilitada y la interfaz de usuario publicada. Consulte [Integrar la interfaz de usuario asociada en su aplicación](/help/forms/interactive-communication/invoke-associate-ui.md) para conocer todos los requisitos previos de integración.

## Habilitar la vista asociada (IU asociada)

Habilite la interfaz de usuario de asociado en el nivel de documento para que los asociados puedan utilizar las comunicaciones interactivas.

1. Abra la comunicación interactiva en el editor.
1. En la barra de acciones superior o en las opciones del documento, abra **Configuración de la comunicación interactiva** (o **Configuración**).

   ![Configuración de comunicación interactiva - Asociar propiedades con habilitar la edición de vista asociada](/help/forms/assets/associate-ui-settings.png)

1. En el panel izquierdo, asegúrese de que **Asociar propiedades** está seleccionado.
1. A la derecha, marque **Habilitar edición de vista asociada**.
1. Haga clic en **Aplicar cambios** y, a continuación, guarde el documento.

   ![Configuración de comunicación interactiva - Asociar propiedades con habilitar la edición de vista asociada](/help/forms/assets/associate-ui-enable-view.png)

Un mensaje puede recordarle que aplique los cambios y guarde el documento para habilitar la vista asociada. Después de guardar, la CI está disponible para su uso controlado por asociados.

### Permitir edición de IU asociada por componente

Una vez habilitada la Vista asociada para la CI, debe activar **Permitir la edición por asociado** para cada componente que los asociados puedan editar. Los componentes sin esta configuración activada siguen siendo de solo lectura en la interfaz de usuario de Associate.

1. En el editor de CI, seleccione el componente (por ejemplo, un campo de texto) en el lienzo o en la jerarquía de componentes.
1. En el panel derecho **Propiedades**, expanda **Asociar propiedades**.
1. Activar **Permitir edición por asociado** **Activado** para ese componente.
1. Repita el proceso para cada componente que se asocie que tenga que editar y, a continuación, guarde el documento.

![Permitir edición por asociado en las propiedades del componente](/help/forms/assets/associate-ui-allow-editing-by-associate.png)

>[!NOTE]
>
> **Asociar propiedades** también incluye opciones como **Tipografía** (fuente, tamaño y estilo para el campo en la interfaz de usuario asociada), **Información sobre herramientas** y **Patrones** (validaciones). Utilícelos para controlar el aspecto y el comportamiento del componente cuando los asociados lo editen; por ejemplo, defina patrones de validación para que los asociados introduzcan datos en el formato requerido.

## Configurar el flujo de trabajo para la IU asociada

Para ejecutar un flujo de trabajo de AEM cuando los usuarios envíen o actualicen datos desde la interfaz de usuario asociada, configure lo siguiente:

1. En **Configuración de comunicación interactiva**, seleccione **Flujo de trabajo** en el panel izquierdo (en Asociar propiedades).
1. Activar **Configurar flujo de trabajo para actualización** **Activado**.
1. En **Seleccionar modelo de flujo de trabajo**, elija el modelo de flujo de trabajo de AEM que desea ejecutar (por ejemplo, `conversionWorkflow` o una ruta como `/var/workflow/models/submit-workflow-1`).
1. **Mensaje de éxito del flujo de trabajo** establecido de forma opcional (mostrado al usuario una vez finalizado el flujo de trabajo).
1. Si lo desea, puede establecer **URL de redireccionamiento** para enviar al usuario a una página específica después del envío.
1. Haga clic en **Aplicar cambios** y guarde el documento.

   ![Configuración de comunicación interactiva - Configuración del flujo de trabajo para la interfaz de usuario asociada](/help/forms/assets/associate-ui-configure-workflow.png)

Al habilitar un flujo de trabajo, se ejecuta siempre que los usuarios envían desde la interfaz de usuario de Asociar. Para ver cómo funcionan el envío y el flujo de trabajo (dónde se ejecutan, quién usa qué instancia y las consideraciones clave), consulte [Flujo de trabajo de envío para la interfaz de usuario asociada](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior). Ese artículo también incluye un ejemplo de un flujo de trabajo que genera PDF a partir de envíos de CI.

## Completar la configuración de la IU asociada

Después de activar la opción Asociar vista y, opcionalmente, configurar el flujo de trabajo:

1. **Habilitar campos editables:** En las secciones requeridas de la CI, habilite los campos que los asociados pueden editar. Establezca las validaciones y el comportamiento obligatorio/de solo lectura según sea necesario.
1. **Publicar el IC** para que esté disponible en la instancia de publicación para asociados.
1. Compartir el vínculo CI publicado con los asociados. Se autentican (por ejemplo, mediante [Microsoft Entra ID](https://www.microsoft.com/en-us/security/business/identity-access/microsoft-entra-id)) y abren la interfaz de usuario de Associate, introducen o confirman los datos del cliente y generan la comunicación final. Si ha configurado un flujo de trabajo, se ejecuta al enviarlo. Para ver cómo funcionan el envío y el flujo de trabajo, consulte [Flujo de trabajo de envío para la IU asociada](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md#submission-and-workflow-behavior).

## Ver también

- [Asociar interfaz de usuario en el editor de comunicaciones interactivas](/help/forms/interactive-communication/associate-ui-in-interactive-communication-editor.md)
- [Integración de la interfaz de usuario asociada en la aplicación](/help/forms/interactive-communication/invoke-associate-ui.md)
- [Flujo de trabajo de envío para la interfaz de usuario asociada — IC Generate PDF Output](/help/forms/interactive-communication/submission-workflow-associate-ui-ic-pdf.md) — muestra cómo funcionan el envío y el flujo de trabajo, además de un flujo de trabajo de ejemplo que genera PDF a partir de los envíos de CI.
