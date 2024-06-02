---
title: Integración nativa de AEM Assets con Adobe Express
description: La integración nativa de AEM Assets con Adobe Express permite acceder directamente a los recursos almacenados en AEM Assets desde la interfaz de usuario de Adobe Express.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 69d890eaae30468db89b9aff975a2a421f53fcff
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 9%

---

# Integración nativa con Adobe Express {#native-integration-adobe-express}

AEM Assets se integra de forma nativa con Adobe Express, lo que le permite acceder directamente a los recursos almacenados en AEM Assets desde la interfaz de usuario de Adobe Express. Puede colocar contenido administrado en AEM Assets en el lienzo Express y, a continuación, guardar contenido nuevo o editado en un repositorio de AEM Assets. La integración ofrece las siguientes ventajas clave:

* AEM Se ha aumentado la reutilización del contenido mediante la edición y el guardado de nuevos recursos en los recursos de.

* Se ha reducido el tiempo y esfuerzo generales para crear nuevos recursos o crear nuevas versiones de los recursos existentes.

## Requisitos previos {#prerequisites}

Derechos para acceder al Adobe Express y al menos a un entorno dentro de AEM Assets. El entorno puede ser cualquiera de los repositorios de Assets as a Cloud Service o Assets Essentials.


## Uso de AEM Assets en el editor de Adobe Express {#use-aem-assets-in-express}

Siga estos pasos para empezar a utilizar AEM Assets en el editor de Adobe Express:

1. Abra la aplicación web de Adobe Express.

2. Abra un nuevo lienzo en blanco cargando una nueva plantilla o proyecto, o creando un recurso.

3. Clic **[!UICONTROL Assets]** disponible en el panel de navegación izquierdo. El Adobe Express muestra la lista de repositorios a los que puede acceder junto con la lista de recursos y carpetas disponibles en el nivel raíz.

4. Examine o busque recursos en su repositorio para arrastrarlos y colocarlos en el lienzo. Puede filtrar recursos mediante varios filtros disponibles, como tipo de archivo, tipo MIME y dimensiones.

   >[!NOTE]
   >
   >El filtro por dimensión no se aplica a los vídeos.

   ![Incluir recursos del complemento Recursos](assets/adobe-express-native-integration.png)


## Guardar proyectos de Adobe Express en AEM Assets {#save-express-projects-in-assets}

Después de incorporar las modificaciones adecuadas en el lienzo Express, puede guardarlo en el repositorio de AEM Assets.

1. Clic **[!UICONTROL Compartir]** para abrir **[!UICONTROL Compartir]** diálogo.

   ![AEM Guardado de recursos en el](assets/adobe-express-share.png)

2. En la sección Almacenamiento del panel derecho, seleccione. **AEM Assets**. El Adobe Express muestra el cuadro de diálogo de carga.
3. Especifique un nombre y un formato para el recurso. Puede guardar el contenido del lienzo en los formatos PNG, JPEG, PDF, MP4, MP4+PNG o MP4+JPEG. El formato se ajusta automáticamente en función de los recursos.

   >[!NOTE]
   >
   >Al seleccionar &quot;Página actual&quot;, se guarda el archivo en la carpeta de destino. Al seleccionar &quot;Todas las páginas&quot;, se crea una nueva carpeta en el destino para todos los archivos que no sean del PDF y se guardan allí, mientras que los archivos del PDF se guardan como un solo archivo en la carpeta de destino.

4. Haga clic en el área de texto debajo de **Carpeta de destino** para seleccionar una ubicación y guardar los recursos.

   ![AEM Guardado de recursos en el](/help/assets/assets/page-selection-and-destination-folder.png)

5. Opcional: puede añadir metadatos de campaña para la carga mediante la variable **Nombre del proyecto o campaña** field. Puede utilizar un nombre existente o crear uno nuevo. Puede definir varios nombres de proyecto o campaña para la carga. Para registrar el nombre, simplemente escriba el nombre y pulse Intro.
Como práctica recomendada, Adobe recomienda especificar valores en el resto de los campos, así como crear una experiencia de búsqueda mejorada para los recursos cargados.

6. Del mismo modo, defina los valores de **[!UICONTROL Palabras clave]** y **[!UICONTROL Canales]** campos.

7. Clic **[!UICONTROL Cargar]** para cargar el recurso en AEM Assets.




## Restricciones {#limitations}

1. Para importar y exportar, el tipo de archivo de vídeo admitido es MP4.

2. Para importar vídeo MP4:

   a) El tamaño máximo de archivo admitido es de 200 MB. Si se supera este límite, aparecerá un mensaje de alerta.
b) La resolución máxima admitida es de 3840 X 3840 píxeles.
c) No se admiten vídeos con fondos transparentes (canal alfa).

3. Para exportar vídeo MP4:

   a) El tamaño máximo de archivo admitido es de 200 MB. Si este límite supera, aparece un mensaje de alerta con una sugerencia de solución alternativa, como se muestra en la siguiente imagen
   ![alerta con solución](/help/assets/assets/alert-with-workaround.png).
