---
title: ¿Cómo crear una secuencia de formularios de varios pasos?
description: con [!DNL Experience Manager Forms], puede definir una secuencia de paneles de formulario para que los usuarios naveguen y rellenen un formulario adaptable. Profundizar tomando un enfoque de caso de uso como ejemplo para crear una secuencia de formulario de varios pasos.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 6b3f9131-db6b-451b-a932-b57d809222eb
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Introducción a la secuencia de formularios en varios pasos {#introduction-to-multi-step-form-sequence}

Adaptive Forms permite a los autores de formularios crear experiencias de captura de datos en varios pasos con buena facilidad. Incorpora compatibilidad para crear varios paneles y asociar cada uno con diferentes patrones de navegación. Los autores de formularios pueden agrupar los campos de formulario en secciones lógicas y representar un grupo como un panel. La navegación general entre paneles se controla mediante el diseño del panel. Los autores pueden elegir organizar los paneles en diferentes diseños, por ejemplo, colocándolos secuencialmente utilizando el diseño del asistente o de forma ad hoc utilizando el diseño en Pestaña. Para obtener información sobre los diseños de panel, consulte [Funciones de diseño de Forms adaptable](layout-capabilities-adaptive-forms.md).

En una experiencia típica de rellenado de formularios, hay que seguir más pasos que capturar los datos. Un envío de formulario completo puede incluir otros pasos, como firmar el formulario digitalmente, verificar la información rellenada en el formulario, procesar pagos, etc. Difiere de un caso a otro.

Si el caso de uso requiere un conjunto de pasos para la captura de datos o hay regulaciones que necesitan seguir ciertos pasos, [!DNL Experience Manager Forms] proporciona una forma de aplicar esa estructura común en todos los formularios. La implementación premeditada de la estructura del formulario define la secuencia de pasos de un formulario. ![Ejemplo de secuencia de formulario de varios pasos](assets/formpipeline.png)

Ejemplo de secuencia de formulario de varios pasos

Veamos un caso de uso en el que debe crear una secuencia para los pasos de relleno, verificación, firma y confirmación de un formulario. Los pasos para crear una secuencia de este tipo son los siguientes:

1. Defina una plantilla de formulario y añada el panel requerido. Debe haber un panel para cada paso de la secuencia. Sin embargo, puede incluir subpaneles dentro de un panel.

   En este ejemplo, se pueden añadir los paneles siguientes:

   * **[!UICONTROL Relleno]**: Contiene campos de formulario para capturar datos. Aquí puede incluir subpaneles anidados para crear secciones para distintos tipos de información, como personal, familia, finanzas, etc.

   <!--* **[!UICONTROL Verify]**: It contains the **[!UICONTROL Verify]** component that can be used in an XFA-based Adaptive Form. It displays the information captured in the Fill panel in read-only mode for verification.-->


   * **[!UICONTROL Signo electrónico]**: Contiene el **[!UICONTROL Sign]** que se puede utilizar en un formulario adaptable basado en XFA. Proporciona los siguientes servicios de firma:

      * Servicios de Adobe Document Cloud eSign
      * Firma manuscrita
   * **[!UICONTROL Confirmación]**: Contiene el **[!UICONTROL Resumen]** que muestra un mensaje que confirma el envío del formulario después de que un usuario firme el formulario y llega al paso Confirmación (Resumen) de la secuencia. Los autores pueden configurar el texto del [!UICONTROL Resumen] , mostrar un mensaje de agradecimiento, mostrar un vínculo al PDF generado, etc.



1. Seleccione el diseño del panel raíz como **[!UICONTROL Asistente]**.
1. Complete los pasos restantes para crear la plantilla de formulario. <!-- For more information, see [Creating a custom Adaptive Form template](custom-adaptive-forms-templates.md). -->

Después de definir la secuencia del formulario en la plantilla de formulario, puede utilizarla para crear formularios que tengan la estructura básica definida como la secuencia en su lugar, aunque siempre puede personalizar el formulario para adaptarlo a sus necesidades.
