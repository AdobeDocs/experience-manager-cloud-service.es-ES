---
title: Cómo personalizar la plantilla de documento de registro generada automáticamente para Forms adaptable
description: Obtenga información sobre cómo descargar, personalizar y volver a cargar la plantilla de documento de registro (DoR) generada automáticamente para Forms adaptable mediante Adobe Forms Designer.
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="(Se aplica a AEM Forms)."
exl-id: 2416add3-0b9d-4a8d-a84d-d65c0762d8e8
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 5%

---

# Personalizar la plantilla del documento de registro generada automáticamente

<span class="preview"> Este artículo se aplica a **Componentes principales** y a **Componentes básicos** basados en Forms adaptable.</span>

Cuando se genera automáticamente un documento de registro (DoR) para un formulario adaptable, AEM Forms crea una plantilla predeterminada basada en la estructura del formulario. Puede personalizar esta plantilla generada automáticamente para que coincida con los requisitos de marca y diseño de su organización.

El flujo de trabajo de personalización consta de tres pasos:

1. Descargue la plantilla de DoR generada automáticamente desde Forms Manager.
1. Modifique la plantilla mediante Adobe Forms Designer.
1. Vuelva a cargar la plantilla personalizada en AEM Forms y configúrela como plantilla personalizada.

## Requisitos previos {#prerequisites}

Antes de empezar, asegúrese de que dispone de lo siguiente:

* Acceso a AEM Forms Manager con permisos para descargar y cargar plantillas.
* Adobe Forms Designer instalado en el equipo local.
* Un formulario adaptable con **[!UICONTROL Generar documento de registro]** habilitado.

## Paso 1: Descargar la plantilla de DoR generada automáticamente {#download-auto-generated-dor-template}

Para descargar la plantilla de DoR generada automáticamente (archivo XDP) para su formulario adaptable:

1. Inicie sesión en la instancia de autor de AEM Forms.
1. Vaya a **[!UICONTROL Forms]** > **[!UICONTROL Forms y documentos]**.
1. Seleccione el formulario adaptable para el que desea descargar la plantilla del DoR.
1. Abra las propiedades del formulario adaptable seleccionado.
1. En el panel de propiedades, seleccione la opción **[!UICONTROL Descargar documento de registro]** para descargar la plantilla de documento de registro (archivo XDP) generada automáticamente.
1. Guarde el archivo XDP descargado en el equipo local.


## Paso 2: Personalizar la plantilla con Adobe Forms Designer {#customize-template-using-designer}

Abra la plantilla XDP descargada en Adobe Forms Designer y modifíquela para adaptarla a las necesidades de su organización.

1. Abra el archivo XDP descargado en **Adobe Forms Designer**.
1. Personalice la plantilla según sea necesario. Algunos ejemplos de personalizaciones son:

   * **Varias páginas maestras**: agregue páginas maestras adicionales para definir diseños diferentes para páginas específicas del documento de registro. Por ejemplo, utilice una primera página distinta con membrete de la empresa y páginas posteriores con un diseño más sencillo.
   * **Colores y familias de fuentes**: cambie el color, el tamaño y la familia de fuentes para que se ajusten a las directrices de marca corporativa.
   * **Elementos personalizados**: agregue elementos como logotipos de empresa, encabezados, pies de página y texto de exención de responsabilidad legal para establecer una identidad de marca coherente.
   * **Diseño y estilo de página**: ajuste los márgenes, el espaciado y la estructura general de la página para mejorar la legibilidad.
   * **Estilo y posición de los campos**: modifique el aspecto y la posición de los campos de formulario para que coincidan con su diseño preferido.

1. Guarde la plantilla XDP personalizada.

>[!NOTE]
>
> No elimine ni modifique ningún script presente en la plantilla. La modificación de scripts puede afectar al enlace de datos y a la generación del documento de registro.

## Paso 3: Vuelva a cargar la plantilla personalizada en AEM {#reupload-customized-template}

Después de personalizar la plantilla, cárguela en AEM Forms y configure el formulario adaptable para que la utilice.

1. Cargue la plantilla XDP personalizada en la instancia de AEM Forms:
   * Vaya a **[!UICONTROL Forms]** > **[!UICONTROL Forms y documentos]**.
   * Seleccione **[!UICONTROL Crear]** > **[!UICONTROL Carga de archivo]** y cargue el archivo XDP personalizado.

A continuación, configure el formulario para que utilice la plantilla personalizada. Los pasos difieren según si el formulario se basa en componentes principales o en componentes de base.

>[!BEGINTABS]

>[!TAB Componentes principales]

Para Forms adaptable basado en componentes principales:

1. Abra el formulario adaptable en el editor al que desee aplicar la plantilla personalizada.
1. En el árbol de contenido, seleccione **[!UICONTROL Contenedor de guía]** (panel raíz).
1. Abra **[!UICONTROL Propiedades]** y haga clic en el icono **[!UICONTROL Documento de registro]** (DoR) para abrir las propiedades del documento de registro.
1. En la ficha **[!UICONTROL Básico]**, abra el menú desplegable **[!UICONTROL Plantilla]** y seleccione **[!UICONTROL Personalizado]**.
1. Explore y seleccione la plantilla XDP personalizada cargada.
1. Seleccione la marca de verificación para guardar.

   ![Propiedades del documento de registro - Plantilla establecida en Personalizada (componentes principales)](/help/forms/assets/submission-pdf-dor-custom-template.png)

>[!TAB Componentes de base]

Para Forms adaptable basado en componentes de base:

1. Abra el formulario adaptable en el editor al que desee aplicar la plantilla personalizada.
1. Seleccione el panel raíz (contenedor de formulario).
1. Abra **[!UICONTROL Propiedades del documento de registro]** (en el panel Propiedades o en la ficha DoR).
1. En la ficha **[!UICONTROL Básico]**, abra el menú desplegable **[!UICONTROL Plantilla]** y seleccione **[!UICONTROL Personalizado]**.
1. Explore y seleccione la plantilla XDP personalizada cargada.
1. Seleccione **[!UICONTROL Listo]** para guardar.

   ![Propiedades del documento de registro - Plantilla establecida en Personalizada (componentes de base)](/help/forms/assets/dor-custom-template-foundation-components.png)

>[!ENDTABS]

El formulario adaptable ahora utiliza la plantilla personalizada al generar el documento de registro.

## Verificar la plantilla personalizada {#verify-customized-template}

Para confirmar que la plantilla personalizada se aplica correctamente:

1. Envíe una entrada de prueba para el formulario adaptable.
1. Generar el documento de registro.
1. Compruebe que el PDF generado refleje sus personalizaciones, incluidos logotipos, fuentes, cambios de diseño y otros elementos de marca.

## Solución de problemas {#troubleshooting}

| Problema | Resolución |
|---|---|
| La plantilla personalizada no se carga. | Asegúrese de que el archivo XDP sea válido y no esté dañado. Compruebe que dispone de los permisos necesarios para cargar archivos en AEM Forms. |
| Las personalizaciones no aparecen en el documento de registro generado. | Confirme que seleccionó la plantilla personalizada correcta en la sección **[!UICONTROL Configuración de la plantilla del documento de registro]** de las propiedades del formulario. |
| Problemas de diseño o formato en el PDF generado. | Compruebe que las personalizaciones de Adobe Forms Designer siguen las [convenciones de plantillas base](/help/forms/generate-document-of-record-core-components.md#base-template-conventions). Asegúrese de que todos los elementos estén correctamente colocados dentro de la estructura de la plantilla. |

## Ver también {#see-also}

* [Generar documento de registro para formularios adaptables (Componentes principales)](/help/forms/generate-document-of-record-core-components.md)
* [Generar documento de registro para Forms adaptable (componentes de base)](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [Plantilla base de un documento de registro](/help/forms/generate-document-of-record-core-components.md#base-template-of-a-document-of-record)
* [Personalizar información de marca en el documento de registro](/help/forms/generate-document-of-record-core-components.md#customize-the-branding-information-in-document-of-record)
