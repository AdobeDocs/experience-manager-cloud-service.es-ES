---
title: Integración nativa de AEM Assets con Adobe Express
description: La integración nativa de AEM Assets con Adobe Express permite acceder directamente a los recursos almacenados en AEM Assets desde la interfaz de usuario de Adobe Express.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
feature: Collaboration
role: User
source-git-commit: 257930bc2633a0d31ad3bd28305b8159597befa5
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 8%

---

# Integración nativa con Adobe Express {#native-integration-adobe-express}

AEM Assets se integra de forma nativa con Adobe Express, lo que le permite acceder directamente a los recursos almacenados en AEM Assets desde la interfaz de usuario de Adobe Express. Puede colocar contenido administrado en AEM Assets en el lienzo Express y, a continuación, guardar contenido nuevo o editado en un repositorio de AEM Assets. La integración ofrece las siguientes ventajas clave:

* AEM Se ha aumentado la reutilización del contenido mediante la edición y el guardado de nuevos recursos en los recursos de.

* Se ha reducido el tiempo y esfuerzo generales para crear nuevos recursos o crear nuevas versiones de los recursos existentes.

## Requisitos previos {#prerequisites}

Derechos para acceder al Adobe Express y al menos a un entorno dentro de AEM Assets. El entorno puede ser cualquiera de los repositorios de los Assets Essentials as a Cloud Service de Assets.


## Uso de AEM Assets en el editor de Adobe Express {#use-aem-assets-in-express}

Siga estos pasos para empezar a utilizar AEM Assets en el editor de Adobe Express:

1. Abra la aplicación web de Adobe Express.

2. Abra un nuevo lienzo en blanco cargando una nueva plantilla o proyecto, o creando un recurso.

3. Haga clic en **[!UICONTROL Assets]**, disponible en el panel de navegación izquierdo. El Adobe Express muestra la lista de repositorios a los que puede acceder junto con la lista de recursos y carpetas disponibles en el nivel raíz.

4. Examine o busque recursos en su repositorio para arrastrarlos y colocarlos en el lienzo. Puede filtrar recursos mediante varios filtros disponibles, como el tipo de archivo, el tipo MIME y las dimensiones.

   >[!NOTE]
   >
   >El filtro por dimensión no se aplica a los vídeos.

   ![Incluir recursos del complemento Recursos](assets/adobe-express-native-integration.png)


## Guardar proyectos de Adobe Express en AEM Assets {#save-express-projects-in-assets}

Después de incorporar las modificaciones adecuadas en el lienzo Express, puede guardarlo en el repositorio de AEM Assets.

1. Haga clic en **[!UICONTROL Compartir]** para abrir el cuadro de diálogo **[!UICONTROL Compartir]**.

   AEM ![Guardar recursos en el archivo de recursos](assets/adobe-express-share.png)

2. En la sección Almacenamiento del panel derecho, seleccione **AEM Assets**. El Adobe Express muestra el cuadro de diálogo de carga.
3. Seleccione **Página actual** o **Todas las páginas**. Especifique un nombre y un formato para los recursos que desea exportar. Puede exportar el contenido del lienzo en los formatos PNG, JPEG, PDF, MP4, MP4+PNG o MP4+JPEG. El formato se ajusta automáticamente en función de los recursos de las páginas de lienzo.
Al seleccionar **Página actual**, se guardará el recurso de la página actual en la carpeta de destino. Si selecciona **Todas las páginas** y el formato de exportación no es PDF, todas las páginas de lienzo se guardarán como archivos independientes en una nueva carpeta dentro de la carpeta de destino. Si el formato de exportación es PDF, todas las páginas del lienzo se guardan como un solo archivo de PDF en la carpeta de destino.

4. Haga clic en el icono de la carpeta en **Carpeta de destino** para seleccionar una ubicación y guardar los recursos.

   AEM ![Guardar recursos en el archivo de recursos](/help/assets/assets/page-selection-and-destination-folder.svg)

5. Opcional: puede agregar metadatos de campaña para la carga mediante el campo **Nombre del proyecto o de la campaña**. Puede utilizar un nombre existente o crear uno nuevo. Puede definir varios nombres de proyecto o campaña para la carga. Para registrar el nombre, simplemente escriba el nombre y pulse Intro.
Como práctica recomendada, Adobe recomienda especificar valores en el resto de los campos, así como crear una experiencia de búsqueda mejorada para los recursos cargados.

6. Del mismo modo, defina los valores para los campos **[!UICONTROL Palabras clave]** y **[!UICONTROL Canales]**.

7. Haga clic en **[!UICONTROL Cargar]** para cargar los recursos en AEM Assets.

## Limitaciones {#limitations}

1. Para importar y exportar, el tipo de archivo de vídeo admitido es MP4.

2. Para importar vídeo MP4:

   1. El tamaño máximo de archivo admitido es de 200 MB. Si este límite supera, se muestra un mensaje de alerta.
   2. La resolución máxima admitida es de 3840 X 3840 píxeles.
   3. No se admiten vídeos con fondos transparentes (canal alfa).

3. Para exportar vídeo MP4:

   1. El tamaño máximo de archivo admitido es de 200 MB. Si este límite supera, una alerta sugiere recortar el vídeo a 200 MB o menos, o cargarlo manualmente en la carpeta de destino de AEM Assets después de descargarlo.



