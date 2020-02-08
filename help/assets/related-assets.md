---
title: Recursos relacionados
description: Obtenga información sobre cómo relacionar recursos que comparten determinados atributos comunes. También puede utilizar la función para crear relaciones de origen/derivadas entre recursos.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Activos relacionados {#related-assets}

Recursos Adobe Experience Manager (AEM) le permite relacionar recursos manualmente en función de las necesidades de su organización mediante la función Recursos relacionados. Por ejemplo, puede relacionar un archivo de licencia con un recurso o una imagen o vídeo en un tema similar. Puede relacionar recursos que comparten determinados atributos comunes. También puede utilizar la función para crear relaciones de origen/derivadas entre recursos. Por ejemplo, si tiene un archivo PDF que se genera a partir de un archivo INDD, puede relacionar el archivo PDF con su archivo INDD de origen.

De este modo, tiene la flexibilidad de compartir un archivo de baja resolución (por ejemplo, PDF/JPG) con proveedores/agencias y de poner a disposición el archivo de alta resolución (por ejemplo, INDD) únicamente si lo solicita.

## Relate assets {#relating-assets}

1. En la interfaz de Recursos, abra la página de propiedades de un recurso que desee relacionar. Como alternativa, seleccione el recurso en la vista de lista. También puede seleccionar el recurso de una colección.
1. Para relacionar otro recurso con el recurso seleccionado, toque o haga clic en el icono **[!UICONTROL Relacionar]** de la barra de herramientas.
1. Realice una de las acciones siguientes:

   * Para relacionar el archivo de origen del recurso, seleccione **[!UICONTROL Origen]** en la lista.
   * Para relacionar un archivo derivado, seleccione **[!UICONTROL Derivado]** en la lista.
   * Para crear una relación bidireccional entre los recursos, seleccione **[!UICONTROL Otros]** en la lista.

1. En la pantalla **[!UICONTROL Seleccionar recurso]** , navegue hasta la ubicación del recurso que desee relacionar y selecciónelo.

1. Toque o haga clic en el icono **[!UICONTROL Confirmar]** .
1. Toque o haga clic en **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo. En función de la elección de la relación en el paso 3, el activo relacionado se incluye en una categoría adecuada en la sección **[!UICONTROL Relacionado]** . Por ejemplo, si el recurso relacionado es el archivo de origen del recurso actual, aparece en **[!UICONTROL Origen]**.
1. Para desrelacionar un recurso, toque o haga clic en el icono **[!UICONTROL Desrelacionar]** de la barra de herramientas.
1. Seleccione los recursos que desea desrelacionar en el cuadro de diálogo **[!UICONTROL Eliminar relaciones]** y toque o haga clic en **[!UICONTROL Desrelacionar]**.
1. Haga clic o toque **[!UICONTROL Aceptar]** para cerrar el cuadro de diálogo. Los recursos para los que se han eliminado relaciones se eliminan de la lista de recursos relacionados en la sección **[!UICONTROL Relacionado]** .

## Traducir recursos relacionados {#translating-related-assets}

La creación de relaciones de origen y derivadas entre recursos mediante la función Recursos relacionados también resulta útil en los flujos de trabajo de traducción. Al ejecutar un flujo de trabajo de traducción en un recurso derivado, Recursos AEM obtiene automáticamente cualquier recurso al que hace referencia el archivo de origen y lo incluye para su traducción. De este modo, el recurso al que hace referencia el recurso de origen se traduce junto con el recurso de origen y los recursos derivados. Por ejemplo, imaginemos un escenario en el que la copia en inglés incluye un recurso derivado y su archivo de origen como se muestra.

Si el archivo de origen está relacionado con otro recurso, AEM Assets obtiene el recurso al que se hace referencia y lo incluye para su traducción.

1. Traduzca los recursos de la carpeta de origen a un idioma de destino siguiendo los pasos de [Creación de un nuevo proyecto](/help/assets/translate-assets.md#create-a-new-translation-project)de traducción. Por ejemplo, en este caso, traduzca sus recursos al francés.
1. En la página Proyectos, abra la carpeta de traducción.
1. Toque o haga clic en el mosaico del proyecto para abrir la página de detalles.
1. Toque o haga clic en las elipses debajo de la tarjeta Trabajo de traducción para ver el estado de la traducción.
1. Seleccione el recurso y, a continuación, toque o haga clic en **[!UICONTROL Mostrar en recursos]** en la barra de herramientas para ver el estado de traducción del recurso.
1. Para comprobar si los recursos relacionados con el origen se han traducido, toque o haga clic en el recurso de origen.
1. Seleccione el recurso relacionado con el origen y, a continuación, toque o haga clic en **[!UICONTROL Mostrar en recursos]**. Se muestra el recurso relacionado traducido.
