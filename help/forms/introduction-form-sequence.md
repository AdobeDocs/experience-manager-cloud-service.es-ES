---
title: Cómo crear una secuencia de formularios de varios pasos
description: Con [!DNL Experience Manager Forms], puede definir una secuencia de paneles de formulario para que los usuarios se desplacen por un formulario adaptable y lo rellenen. Obtenga información más detallada utilizando un caso de uso como ejemplo para crear una secuencia de formulario de varios pasos.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: ca0c9f102488c38dbe8c969b54be7404748cbc00
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 89%

---

# Introducción a la secuencia de formulario de varios pasos {#introduction-to-multi-step-form-sequence}

<span class="preview"> Adobe recomienda utilizar la captura de datos moderna y ampliable [Componentes principales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=es) para [crear un nuevo Forms adaptable](/help/forms/creating-adaptive-form-core-components.md) o [adición de Forms adaptable a páginas de AEM Sites](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). Estos componentes representan un avance significativo en la creación de Forms adaptable, lo que garantiza experiencias de usuario impresionantes. Este artículo describe un enfoque más antiguo para crear Forms adaptable mediante componentes de base. </span>

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí.](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/introduction-form-sequence.html) |
| AEM as a Cloud Service | Este artículo |

Los formularios adaptables permiten a los autores de formularios crear experiencias de captura de datos de varios pasos con gran facilidad. Estos formularios incluyen compatibilidad para crear varios paneles y asociar cada uno con diferentes patrones de navegación. Los autores de formularios pueden agrupar los campos de formulario en secciones lógicas y representar un grupo como un panel. La navegación general entre los paneles se controla mediante el diseño del panel. Los autores pueden elegir organizar los paneles en diferentes diseños, por ejemplo, colocándolos secuencialmente utilizando el diseño Asistente o de forma ad hoc utilizando el diseño en pestañas. Para obtener información sobre los diseños de panel, consulte [Funciones de diseño de formularios adaptables](layout-capabilities-adaptive-forms.md).

Normalmente, durante la experiencia de rellenado de un formulario, hay que seguir más pasos además de capturar los datos. Un envío de formulario completo puede incluir otros pasos, como firmar el formulario de forma digital, verificar la información con la que se ha rellenado el formulario, procesar pagos, etc. Cada caso es diferente.

Si su caso de uso requiere seguir un conjunto de pasos para la captura de datos o hay algún reglamento que exige que se sigan unos pasos específicos, [!DNL Experience Manager Forms] proporciona una forma de aplicar esa estructura común a todos los formularios. La implementación planificada de la estructura del formulario define la secuencia de pasos de ese formulario. ![Ejemplo de secuencia de formulario de varios pasos](assets/formpipeline.png)

Ejemplo de secuencia de formulario de varios pasos

Veamos un caso de uso en el que debe crear una secuencia para los pasos de rellenado, verificación, firma y confirmación de un formulario. Los pasos para crear una secuencia de este tipo son los siguientes:

1. Defina una plantilla de formulario y añádale el panel requerido. Debe haber un panel para cada uno de los pasos de la secuencia. No obstante, puede incluir subpaneles dentro de un mismo panel.

   En este ejemplo, podemos añadir los siguientes paneles:

   * **[!UICONTROL Rellenado]**: contiene campos de formulario para capturar datos. Aquí puede incluir subpaneles anidados para crear secciones para distintos tipos de información, como personal, familiar, financiera, etc.

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL Firma electrónica]**: contiene el componente **[!UICONTROL Firma]**, que se puede utilizar en un formulario adaptable basado en XFA. Proporciona los siguientes servicios de firma:

      * Servicios de firma electrónica de Adobe Document Cloud
      * Firma manuscrita

   * **[!UICONTROL Confirmación]**: contiene el componente **[!UICONTROL Resumen]** que muestra un mensaje que confirma el envío del formulario una vez que el usuario lo ha firmado y llega al paso Confirmación (Resumen) de la secuencia. Los autores pueden configurar el texto del componente [!UICONTROL Resumen], mostrar un mensaje de agradecimiento, mostrar un vínculo al PDF generado, etc.

1. Seleccione el diseño del panel raíz como **[!UICONTROL Asistente]**.
1. Complete los pasos restantes para crear la plantilla de formulario. <!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

Después de definir la secuencia del formulario en la plantilla de formulario, puede utilizarla para crear formularios que tengan la estructura básica definida como dicha secuencia, aunque siempre puede personalizar el formulario para adaptarlo a sus necesidades.
