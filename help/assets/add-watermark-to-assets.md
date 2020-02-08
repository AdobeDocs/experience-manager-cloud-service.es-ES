---
title: Agregar una marca de agua a los recursos digitales
description: Aprenda a utilizar la función de marca de agua para añadir una marca de agua digital a los recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Marcas de agua {#watermarking}

La función de marca de agua de Recursos Adobe Experience Manager (AEM) le permite agregar una marca de agua digital a los recursos, lo que ayuda a los usuarios a comprobar la autenticidad y propiedad de los derechos de autor de los recursos. AEM Assets admite texto que se va a utilizar como marca de agua en archivos PNG y JPEG.

Para poder aplicar marcas de agua a los recursos, agregue el paso Marca de agua en el flujo de trabajo de recursos de actualización de DAM.

1. Toque o haga clic en el logotipo de AEM y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Flujo de trabajo]** > **[!UICONTROL Modelos]**.
1. En la página Modelos de flujo de trabajo, seleccione el flujo de trabajo de recursos **[!UICONTROL de actualización de]** DAM y haga clic en **[!UICONTROL Editar]**.

1. En el panel lateral, arrastre el paso **[!UICONTROL Agregar marca de agua]** al flujo de trabajo de recursos de actualización de DAM.

<!--  ![Darg add watermark step in the DAM update asset workflow](assets/add_watermark_step_aem_assets.png) -->

>[!NOTE]
>
>Coloque el paso Agregar marca de agua en cualquier lugar antes del paso Procesar miniatura.

1. Abra el paso **[!UICONTROL Agregar marca de agua]** para mostrar sus propiedades.
1. En la ficha **[!UICONTROL Argumentos]** , especifique valores válidos en los distintos campos, como texto, tipo de fuente, tamaño, color, posición, orientación, etc. Para confirmar los cambios, toque o haga clic en el icono Listo.

<!--   ![Provide the arguments in the add watermark step in Assets](assets/arguments_add_watermark_aem_assets.png) -->

1. Guarde el flujo de trabajo de recursos **[!UICONTROL de actualización de]** DAM con el paso de marca de agua.
1. En la interfaz de usuario de Recursos, cargue un recurso de ejemplo. La marca de agua aparece con el tamaño de fuente, el color, etc., en la posición configurada en los pasos anteriores.
