---
title: Configuración general de Dynamic Media
description: Obtenga información sobre cómo administrar la configuración general en Dynamic Media. Puede establecer el nombre del servidor de publicación y del servidor de origen aquí y establecer una opción de sobrescritura de imagen. También hay opciones de carga predeterminadas para el enmascaramiento de enfoque de imágenes y opciones de carga para cómo desea procesar archivos PostScript, Adobe Photoshop, PDF y Adobe Illustrator.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
exl-id: a4d28786-cffa-42ab-98d3-90a15313e401
source-git-commit: ccd52d147b1739330c3cb5a7d1952a7e9eec71ad
workflow-type: tm+mt
source-wordcount: '2525'
ht-degree: 4%

---

# Configuración general de Dynamic Media

<!-- hide: yes
hidefromtoc: yes -->

Configuración **[!UICONTROL Configuración general de Dynamic Media]** solo está disponible si:

* Tiene un *existente* **[!UICONTROL Configuración de Dynamic Media]** (en **[!UICONTROL Cloud Services]**) en Adobe Experience Manager as a Cloud Service. Consulte [Creación de una configuración de Dynamic Media en Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services).
* Es administrador del sistema Experience Manager con privilegios de administrador.

La Configuración general de Dynamic Media está diseñada para que la utilicen programadores y desarrolladores de sitios web con experiencia. Adobe Dynamic Media recomienda que los usuarios que cambien esta configuración de publicación estén familiarizados con Dynamic Media en Adobe Experience Manager y con la tecnología básica de creación de imágenes.

Al crear la cuenta, Adobe Dynamic Media proporciona automáticamente los servidores asignados a su empresa. Estos servidores se utilizan para construir cadenas de URL para el sitio web y las aplicaciones. Estas llamadas de URL son específicas de su cuenta de.

La página Configuración de publicación de Dynamic Media establece la configuración predeterminada que determina cómo se envían los recursos desde los servidores de Dynamic Media de Adobe a los sitios web o las aplicaciones. Si no se especifica ninguna configuración, el servidor de Dynamic Media de Adobe envía un recurso según una configuración predeterminada que se configuró en la página Configuración de publicación de Dynamic Media.

Consulte también [Opcional: configuración de la configuración de Dynamic Media](/help/assets/dynamic-media/config-dm.md#optional-setup-and-configuration-of-dynamic-media-scene-mode-settings) para tareas de configuración más opcionales.

>[!NOTE]
>
>¿Desea actualizar de Dynamic Media Classic a Dynamic Media en Adobe Experience Manager? La página Configuración general y [Ajustes de publicación](/help/assets/dynamic-media/dm-publish-settings.md) Las páginas de Dynamic Media se rellenan previamente con los valores tomados de su cuenta de Dynamic Media Classic. Las excepciones son todos los valores enumerados en la variable **[!UICONTROL Opciones de carga predeterminadas]** de la página Configuración general. Estos valores ya están en Experience Manager. Como tal, cualquier cambio que realice en **[!UICONTROL Opciones de carga predeterminadas]**, en cualquiera de las cinco pestañas, a través de la interfaz de usuario del Experience Manager, se reflejan en Dynamic Media, no en Dynamic Media Classic. El resto de configuraciones y valores de la página Configuración general y la variable [Ajustes de publicación](/help/assets/dynamic-media/dm-publish-settings.md) Las páginas de se mantienen entre Dynamic Media Classic y Dynamic Media en Experience Manager.

**Para establecer la Configuración general de Dynamic Media:**

1. En el modo Autor del Experience Manager, seleccione el logotipo del Experience Manager para acceder a la consola de navegación global.
1. En el carril izquierdo, seleccione el icono Herramientas y vaya a **[!UICONTROL Assets]** > **[!UICONTROL Configuración general de Dynamic Media]**.
1. En la página Servidor, configure **[!UICONTROL Servidor de publicación]** y **[!UICONTROL Servidor de origen]** y, a continuación, utilice las cinco pestañas para configurar las opciones de carga predeterminadas de Image Editing y de los archivos Postscript, Photoshop, PDF y Illustrator.

   * [Servidor](#server-general-setting)
   * [Cargar a la aplicación](#upload-to-application)
   * [Edición de imágenes](#image-editing-tab) pestaña
   * [PostScript](#postscript-tab) pestaña
   * [Photoshop](#photoshop-tab) pestaña
   * [PDF](#pdf-tab) pestaña
   * [Illustrator](#illustrator-tab) pestaña

   ![Página Configuración general de Dynamic Media](/help/assets/assets-dm/dm-general-settings.png)
   *página Configuración general de Dynamic Media, con el **[!UICONTROL Edición de imágenes]**pestaña seleccionada.*<br><br>

1. Cuando haya terminado, cerca de la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

## Servidor {#server-general-setting}

Al crear la cuenta, Adobe Dynamic Media proporciona automáticamente los servidores asignados a su empresa. Estos servidores se utilizan para construir cadenas de URL para el sitio web y las aplicaciones. Estas llamadas de URL son específicas de su cuenta de.

| Opción | Descripción |
| --- | --- |
| **[!UICONTROL Servidor de publicación]** | Requerido.<br>El nombre debe utilizar `https://` en la ruta.<br>Este servidor es el servidor CDN (red de distribución de contenido) activo que se utiliza en todas las llamadas URL generadas por el sistema y específicas a su cuenta. No cambie este nombre de servidor a menos que el soporte técnico de Adobe se lo indique. |
| **[!UICONTROL Servidor de origen]** | Requerido.<br>Este servidor solo se utiliza para pruebas de garantía de calidad. No cambie este nombre de servidor a menos que el soporte técnico de Adobe se lo indique. |

## Cargar a la aplicación {#upload-to-application}

* **[!UICONTROL Sobrescribir imágenes]**

   Adobe Dynamic Media no permite que dos archivos tengan el mismo nombre. El ID de Dynamic Media de Adobe de cada elemento (el nombre de imagen menos la extensión del nombre de archivo) debe ser único. Debido a esta regla, **[!UICONTROL Cargar en la aplicación]** tiene una sobrescritura. El efecto exacto de esta opción depende de la opción Sobrescribir imágenes especificada que haya elegido. Estas opciones especifican cómo se cargan las imágenes de reemplazo: si reemplazan las imágenes originales o se convierten en imágenes duplicadas. Se cambia el nombre de las imágenes duplicadas por un `-1`. Por ejemplo, `chair.tif` ha cambiado el nombre `chair-1.tif`. Estas opciones afectan a las imágenes cargadas en una carpeta diferente al original o a las imágenes con una extensión de nombre de archivo diferente del original, como JPG, TIF o PNG.

   >[!NOTE]
   >
   >Para mantener la coherencia con Experience Manager, seleccione la opción Sobrescribir imágenes **[!UICONTROL Sobrescribir en la carpeta actual, mismo nombre/extensión de base]**.

   | Sobrescribir imágenes, opción | Descripción |
   | --- | --- |
   | **[!UICONTROL Sobrescribir en la carpeta actual, mismo nombre/extensión de base]** | *Predeterminado* solo para nuevas cuentas de Dynamic Media.<br>Esta opción es la regla más estricta para el reemplazo. Requiere que cargue la imagen de reemplazo en la misma carpeta que el original y que la imagen de reemplazo tenga la misma extensión de nombre de archivo que el original. Si no se cumplen estos requisitos, se crea un duplicado.<br>*Para mantener la coherencia con Experience Manager, seleccione esta opción*. |
   | **[!UICONTROL Sobrescribir en la carpeta actual, mismo nombre de base independientemente de la extensión]** | Requiere que cargue la imagen de reemplazo en la misma carpeta que el original, aunque la extensión del nombre del archivo puede ser diferente del original. Por ejemplo, chair.tif reemplaza chair.jpg. |
   | **[!UICONTROL Sobrescribir en cualquier carpeta con mismo nombre y ext. de recurso base]** | Requiere que la imagen de reemplazo tenga la misma extensión de nombre de archivo que la imagen original (por ejemplo, chair.jpg debe reemplazar chair.jpg, no chair.tif). Sin embargo, puede cargar la imagen de sustitución en una carpeta diferente a la original. La imagen actualizada reside en la nueva carpeta; el archivo ya no se puede encontrar en su ubicación original. |
   | **[!UICONTROL Sobrescribir en cualquier carpeta, mismo nombre de base independientemente de la extensión]** | Esta opción es la regla de reemplazo más inclusiva. Puede cargar una imagen de reemplazo en una carpeta diferente a la original, cargar un archivo con una extensión de nombre de archivo diferente y reemplazar el archivo original. Si el archivo original está en una carpeta diferente, la imagen de reemplazo reside en la nueva carpeta a la que se cargó. |

* **[!UICONTROL Conservar recorte]**

   Controla la conservación de cualquier definición de recorte manual existente.

   Consulte también `preserveCrop` in [UploadPostJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-upload-post-job.html) y [ReprocessAssetsJob](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/data-types/r-reprocess-assets-job.html), ambos en la Guía de referencia de visores de Dynamic Media.

## Opciones de carga predeterminadas {#default-upload-options}

### Pestaña Edición de imágenes {#image-editing-tab}

Este filtro le permite ajustar un efecto de filtro de enfoque en la imagen final con disminución de resolución. Ayuda a controlar la intensidad del efecto, el radio del efecto (medido en píxeles) y un umbral de contraste que se ignora.

El efecto Máscara de enfoque utiliza las mismas opciones que el filtro Máscara de enfoque de Photoshop. Al contrario de lo que su nombre sugiere, Máscara de enfoque es un filtro de enfoque.

| Opciones de máscara de enfoque | Descripción |
| --- | --- |
| **[!UICONTROL Cantidad]** | Requerido.<br>Controla la cantidad de contraste que se aplica a los píxeles del borde.<br>Piense en ello como la intensidad del efecto. La principal diferencia entre los valores de cantidad de Máscara de enfoque en Adobe Dynamic Media y los valores de cantidad en Adobe Photoshop es que Photoshop tiene un rango de cantidad del 1 % al 500 %. Mientras que en Adobe Dynamic Media, el intervalo de valores es `0.0` hasta `5.0`. Un valor de 5,0 en Adobe Dynamic Media es el equivalente aproximado de 500 % en Photoshop; un valor de 0,9 es el equivalente de 90 %, y así sucesivamente. |
| **[!UICONTROL Radio]** | Requerido.<br>Controla el radio del efecto.<br>El rango de valores es `0` hasta `250`. El efecto se ejecuta en todos los píxeles de una imagen y se irradia desde todos los píxeles en todas las direcciones. El radio se mide en píxeles. Por ejemplo, para obtener un efecto de enfoque similar para una imagen de 2000 x 2000 píxeles e imagen de 500 x 500 píxeles, debe establecer un radio de dos píxeles en la imagen de 2000 x 2000 píxeles. A continuación, defina un valor de radio de un píxel en la imagen de 500 x 500 píxeles. Se utiliza un valor mayor para una imagen que tiene más píxeles. |
| **[!UICONTROL Umbral]** | Requerido.<br>Umbral es un rango de contraste que se ignora cuando se aplica el filtro Máscara de enfoque. Este efecto es importante para que no se introduzca ningún &quot;ruido&quot; en una imagen cuando se utilice este filtro. El rango de valores es `0` - `255`, que es el número de pasos de brillo de una imagen en escala de grises. `0`=negro, `128`=50% gris y `255`=blanco.<br>Un valor de umbral de `12` ignora las ligeras variaciones del brillo del tono de la piel para evitar añadir ruido, pero sigue añadiendo contraste al borde de las áreas de contrastes, como cuando las pestañas tocan la piel.<br>Si tiene una foto de la cara de alguien, la máscara de enfoque afecta a las partes contrastadas de la imagen. Por ejemplo, donde las pestañas y la piel se juntan para crear una zona obvia de contraste, y la piel lisa en sí misma. Incluso la piel más suave muestra cambios sutiles en los valores de brillo. Si no utiliza un valor de umbral, el filtro acentúa estos cambios sutiles en los píxeles de la piel. A su vez, se crea un efecto ruidoso e indeseable mientras que el contraste en las pestañas aumenta, lo que aumenta la nitidez.<br>Para evitar este problema, se introduce un valor de umbral que indica al filtro que ignore los píxeles que no cambian de contraste de forma drástica, como la apariencia suave.<br>En el gráfico de la cremallera que se muestra anteriormente, observe la textura junto a las cremalleras. El ruido de la imagen se muestra porque los valores de umbral eran demasiado bajos para suprimir el ruido. |
| **[!UICONTROL Monocromo]** | Seleccione esta opción para resaltar el brillo (intensidad) de la imagen con máscara de enfoque.<br>Anule la selección para aplicar máscara de enfoque a cada componente de color por separado. |

Consulte también [Enfoque de imágenes en Adobe Dynamic Media y en Image Server](https://experienceleague.adobe.com/docs/experience-manager-65/assets/sharpening_images.pdf?lang=en).

### Ficha PostScript {#postscript-tab}

Puede rasterizar archivos de Adobe PostScript®, mantener fondos transparentes, elegir una resolución y elegir un espacio de color.

Puede utilizar archivos Adobe PostScript® (EPS) en Adobe Dynamic Media. Adobe Dynamic Media ofrece comandos para configurar estos archivos a medida que se cargan.

Al cargar archivos de imagen PostScript (EPS), puede aplicarles formato de varias formas. Puede rasterizar los archivos, mantener el fondo transparente, elegir una resolución y elegir un espacio de color.

| Opción PostScript | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | Elija Rasterizar para convertir los gráficos vectoriales del archivo al formato de mapa de bits. |
| **[!UICONTROL Mantener el fondo transparente en las imágenes procesadas]** | Conserva la transparencia de fondo del archivo. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo. |
| **[!UICONTROL Espacio de color]** | · **[!UICONTROL Detectar automáticamente]** - Conserva el espacio de color del archivo.<br>· **[!UICONTROL Forzar como RGB]** - Convierte al espacio de color del RGB.<br>· **[!UICONTROL Forzar como CMYK]** - Convierte al espacio de color CMYK.<br>· **[!UICONTROL Forzar como escala de grises]** - Se convierte al espacio de color de escala de grises. |

### Pestaña Photoshop {#photoshop-tab}

Puede crear plantillas a partir de archivos de Adobe ® Photoshop®, mantener las capas, especificar cómo se asignan los nombres a las capas, extraer el texto y especificar cómo se anclan las imágenes en las plantillas.

| Opción Photoshop | Descripción |
| --- | --- |
| **[!UICONTROL Mantener capas]** | Extrae las capas del PSD, si las hay, en recursos individuales. Las capas de recursos permanecen asociadas al PSD. Para verlos, abra el fichero PSD en Vista de detalles y seleccione el panel Capa. Consulte Visualización y edición de capas en un fichero de PSD. |
| **[!UICONTROL Crear plantilla]** | Crea una plantilla a partir de las capas del fichero de PSD. |
| **[!UICONTROL Extraer texto]** | Extrae el texto para que los usuarios puedan buscar texto en un visor. |
| **[!UICONTROL Extender las capas al tamaño del fondo]** | Amplía el tamaño de las capas de imagen copiadas al tamaño de la capa de fondo. |
| **[!UICONTROL Nombres de capas]** | Amplía el tamaño de las capas de imagen copiadas al tamaño de la capa de fondo.<br>· **[!UICONTROL Nombre de capa]** - Nombra las imágenes después de sus nombres de capa en el archivo PSD. Por ejemplo, una capa denominada Etiqueta de precio en el archivo PSD original se convierte en una imagen denominada Etiqueta de precio. Sin embargo, si los nombres de las capas del fichero de PSD son nombres de capas Photoshop por defecto (Fondo, Capa 1, Capa 2, etc.), las imágenes recibirán los nombres de sus números de capa en el fichero de PSD. <br>· **[!UICONTROL Photoshop y número de capa]** - Nombra las imágenes después de sus números de capa en el archivo PSD, ignorando los nombres de capa originales. Las imágenes se nombran con el nombre de archivo Photoshop y un número de capa anexado. Por ejemplo, la segunda capa de un archivo llamado `Spring Ad.psd` se llama `Spring Ad_2` incluso si tenía un nombre no predeterminado en Photoshop.<br>· **[!UICONTROL Photoshop y nombre de capa]** - Nombra las imágenes después del archivo de PSD seguido del nombre o número de capa. El número de capa se utiliza si los nombres de capa del fichero de PSD son nombres de capa de Photoshop por defecto. Por ejemplo, una capa denominada `Price Tag` en un archivo de PSD llamado `SpringAd` se llama `Spring Ad_Price Tag`. Se llama a una capa con el nombre predeterminado Capa 2 `Spring Ad_2`. |
| **[!UICONTROL Anclaje]** | Especifique cómo se anclan las imágenes en las plantillas que se generan a partir de la maquetación por capas producida a partir del fichero PSD. De forma predeterminada, el anclaje es el centro. Un anclaje central permite que las imágenes de reemplazo llenen mejor el mismo espacio, sin importar la proporción de aspecto de la imagen de reemplazo. Las imágenes con un aspecto diferente que reemplazan a esta imagen, al hacer referencia a la plantilla y utilizar la sustitución de parámetros, ocupan efectivamente el mismo espacio. Cambie a una configuración diferente si la aplicación requiere las imágenes de reemplazo para rellenar el espacio asignado en la plantilla. |

### pestaña PDF {#pdf-tab}

El número máximo de páginas para que un PDF se tenga en cuenta para la extracción es de 5000 para las nuevas cargas. Este límite cambiará a 100 páginas (para todos los PDF) el 31 de diciembre de 2022. Consulte también [Limitaciones de Dynamic Media](/help/assets/dynamic-media/limitations.md).

Puede elegir entre rasterizar los archivos, extraer palabras de búsqueda y vínculos, definir la resolución y elegir un espacio de color.

| opción de PDF | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | · **[!UICONTROL Ninguno]** - No se realiza ningún procesamiento del PDF.<br>· **[!UICONTROL Miniatura]** : rasga cada página del archivo del PDF y la convierte en una imagen en miniatura.<br> · **[!UICONTROL Rasterizar]** : rasga las páginas del archivo PDF y convierte los gráficos vectoriales en imágenes de mapa de bits. Para crear un catálogo electrónico, elija esta opción. |
| **[!UICONTROL Extraer]** | · **[!UICONTROL Ninguno]** : no se extraen palabras de búsqueda ni vínculos del PDF.<br>· **[!UICONTROL Palabras de búsqueda]** : extrae las palabras de búsqueda del archivo PDF para que se pueda buscar en el archivo por palabra clave en un visor de catálogos electrónicos.<br>· **[!UICONTROL Vínculos]** : extrae vínculos de los archivos del PDF y los convierte a mapas de imágenes que se utilizan en un visor de catálogos electrónicos.<br>· **[!UICONTROL Palabras de búsqueda y vínculos]** : extrae palabras de búsqueda y vínculos para utilizarlos en un visor de catálogos electrónicos. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo de PDF. El valor predeterminado es 150. |
| **[!UICONTROL Espacio de color]** | · **[!UICONTROL Detectar automáticamente]** - Mantiene el espacio de color del archivo del PDF.<br>· **[!UICONTROL Forzar como RGB]** - Convierte al espacio de color del RGB.<br>· **[!UICONTROL Forzar como CMYK]** - Convierte al espacio de color CMYK.<br>· **[!UICONTROL Forzar como escala de grises]** - Se convierte al espacio de color de escala de grises. |

### Pestaña Illustrator {#illustrator-tab}

Puede rasterizar archivos de Adobe Illustrator®, mantener fondos transparentes, elegir una resolución y elegir un espacio de color.

Puede utilizar archivos de Adobe ® Illustrator® (AI) en Adobe Dynamic Media. Adobe Dynamic Media ofrece comandos para configurar estos archivos a medida que se cargan.

Al cargar archivos de imagen de Illustrator (AI), puede aplicarles formato de varias formas. Puede rasterizar los archivos, mantener el fondo transparente, elegir una resolución y elegir un espacio de color. Las opciones para dar formato a los archivos PostScript y Illustrator están disponibles en la pantalla Cargar en Opciones PostScript y Opciones Illustrator en el cuadro Opciones del trabajo de carga.


| Opción Illustrator | Descripción |
| --- | --- |
| **[!UICONTROL Procesando]** | Elija Rasterizar para convertir los gráficos vectoriales del archivo al formato de mapa de bits. |
| **[!UICONTROL Mantener el fondo transparente en las imágenes procesadas]** | Conserva la transparencia de fondo del archivo. |
| **[!UICONTROL Resolución (píxel/pulgada)]** | Determina la configuración de resolución. Esta configuración determina cuántos píxeles se muestran por pulgada en el archivo. |
| **[!UICONTROL Espacio de color]** | · **[!UICONTROL Detectar automáticamente]** - Conserva el espacio de color del archivo.<br>· **[!UICONTROL Forzar como RGB]** - Convierte al espacio de color del RGB.<br>· **[!UICONTROL Forzar como CMYK]** - Convierte al espacio de color CMYK.<br>· **[!UICONTROL Forzar como escala de grises]** - Se convierte al espacio de color de escala de grises. |
