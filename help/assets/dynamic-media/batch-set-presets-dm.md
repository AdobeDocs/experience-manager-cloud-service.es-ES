---
title: Valores preestablecidos de conjunto por lotes
description: Obtenga información sobre cómo automatizar la creación de conjuntos de imágenes y conjuntos de giros mediante ajustes preestablecidos de conjunto por lotes en Dynamic Media.
contentOwner: Rick Brough
feature: Image Presets,Viewer Presets
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '3434'
ht-degree: 0%

---

# Acerca de los ajustes preestablecidos del lote {#about-bsp}

Use **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** para crear y organizar varios recursos en un conjunto de imágenes o conjunto de giros en el momento de cargar archivos de recursos en una carpeta, ya sea de forma individual o mediante la ingesta masiva. Puede hacer que el ajuste preestablecido se ejecute junto con los trabajos de importación de recursos que programe en [!DNL Dynamic Media]. Cada ajuste preestablecido es un conjunto de instrucciones independientes con un nombre único que define cómo construir el conjunto de imágenes o el conjunto de giros utilizando imágenes que coinciden con las convenciones de nomenclatura definidas en la fórmula de ajuste preestablecido.

>[!IMPORTANT]
>
>¿Está usando ajustes preestablecidos de conjunto por lotes en [!DNL Dynamic Media Classic] y migrando de [!DNL Dynamic Media Classic] a Adobe Experience Manager as a Cloud Service? Si es así, debe volver a crear manualmente las definiciones de ajustes preestablecidos del conjunto de lotes en [!DNL Adobe Experience Manager as a Cloud Service].

**Práctica recomendada**: al trabajar con ajustes preestablecidos de conjunto de lotes, Adobe recomienda el siguiente flujo de trabajo:

1. Cree un ajuste preestablecido de conjunto de lotes. Consulte [Crear un ajuste preestablecido de conjunto por lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp).
1. Cree una carpeta de recursos o use una carpeta de recursos existente y asegúrese de que esté sincronizada con [!DNL Dynamic Media]. Consulte [Crear carpetas](/help/assets/manage-digital-assets.md#creating-folders).
1. Aplique el ajuste preestablecido del conjunto de lotes a la carpeta de recursos. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjuntos de lotes a las carpetas](#apply-bsp).
1. Cargue imágenes en la carpeta de recursos. Consulte [Cargar recursos para conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [Cargar recursos para conjuntos de giros](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets) o [Agregar recursos digitales a Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. El conjunto de imágenes o el conjunto de giros se genera automáticamente en la carpeta deseada.
1. Publique el conjunto de imágenes o de giros. Consulte [Publicar Dynamic Media Assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Crear un ajuste preestablecido de conjunto por lotes para un conjunto de imágenes o un conjunto de giros {#creating-bsp}

Para crear ajustes preestablecidos de conjunto de lotes, es deseable estar un poco familiarizado y comprender las expresiones regulares.

Lo ideal es que su compañía ya haya definido una convención de nombres para la forma en que se agrupan los recursos en un conjunto.
Para ayudarle a comprender la importancia de utilizar una convención de nombres, suponga que la convención de nombres definida por su compañía es `<style>-<color>-<view>`. Además, el nombre base del conjunto siempre debe ser `<style>-<color>` y la extensión del nombre del conjunto debe ser `-SET`. Si carga una imagen denominada `0123-RED-01`, se creará un conjunto denominado `0123-RED-SET`. Si más adelante carga las imágenes `0123-RED-03` y `0123-BLUE-01`, la imagen `RED-03` se agregará al conjunto en la segunda posición porque está ordenada por debajo de `01`. Sin embargo, la imagen `BLUE-01` formaría parte de un nuevo conjunto denominado `0123-BLUE-SET`. Para la siguiente carga de recursos, agregue los archivos `0123-RED-02` y `0123-BLUE-02`. Cada recurso se agregaría a su conjunto respectivo. La imagen `RED-02` se ordenaría automáticamente entre las imágenes `01` y `03` existentes debido al criterio de ordenación.

La página **[!UICONTROL Ajuste preestablecido de conjunto de lotes]** de [!DNL Dynamic Media] le permite crear, editar o eliminar ajustes preestablecidos de conjunto de lotes y aplicar o quitar ajustes preestablecidos de conjunto de lotes a o desde carpetas de recursos. Puede usar las listas desplegables del campo de formulario para definir un ajuste preestablecido de conjunto por lotes o usar el campo **[!UICONTROL Código sin procesar]**, que le permite escribir la sintaxis de la expresión regular.

Puede crear muchos ajustes preestablecidos de conjuntos de lotes para cubrir todos los trabajos de ingesta de recursos que necesite.

### Acerca de la convención de nombres de recursos

El área **[!UICONTROL Convención de nomenclatura de activos]** de la página **[!UICONTROL Ajuste preestablecido de conjunto de lotes]** tiene dos elementos que puede usar para definir el ajuste preestablecido de conjunto de lotes: **[!UICONTROL Coincidencia]** y **[!UICONTROL Nombre base]**. Estos elementos permiten definir una convención de nombres e identificar la parte de la convención utilizada para asignar un nombre al conjunto en el que están contenidos. <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

La convención de nombres individual de una compañía suele utilizar una o más líneas de definición de cada uno de estos dos elementos. Puede utilizar tantas líneas para la definición única y agruparlas en elementos distintos, como para la imagen principal, el elemento Color, el elemento de vista alternativo y el elemento Muestra.

Por ejemplo, la sintaxis de una expresión regular de coincidencia literal podría ser similar a la siguiente:

`(\w+)-\w+-\w+`

### Acerca del Orden de Secuencias

Si lo desea, puede definir el orden en que se mostrarán las imágenes después de agrupar el conjunto de imágenes o el conjunto de giros en [!DNL Dynamic Media]. De forma predeterminada, los recursos se solicitan alfanuméricamente. Sin embargo, puede utilizar una lista de expresiones regulares separadas por comas para definir el orden.

Con respecto a la automatización de la ordenación de secuencias, puede especificar reglas para forzar la ordenación de recursos de una determinada manera, si es necesario. Por ejemplo, suponga que su primer recurso siempre se llama `_main` y que desea que lo sigan `_alt1`, `_alt2`, `_alt3`, etc. En estos casos, puede crear una regla de orden de secuencias con la siguiente sintaxis:

`.*_main,.*_alt[0-9]`

Aunque es posible realizar una secuencia de ordenación forzada, lo mejor es confiar en la numeración alfanumérica para ordenar la secuencia, en la medida de lo posible. Además, puede utilizar las herramientas del editor de conjuntos de imágenes o conjuntos de giros de [!DNL Dynamic Media] para reorganizar el orden de secuencia de los recursos, o bien, agregar y eliminar nuevos recursos del conjunto mediante la operación de arrastrar y soltar.

Cuando termine de crear un ajuste preestablecido de conjunto de lotes, aplíquelo a una o varias carpetas que haya creado. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjuntos de lotes a las carpetas](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**Para crear un ajuste preestablecido de conjunto por lotes para un conjunto de imágenes o un conjunto de giros:**

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos por lotes]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. En la página **[!UICONTROL Ajustes preestablecidos por lotes]**, cerca de la esquina superior derecha, seleccione **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Crear ajuste preestablecido de conjunto de lotes]**, en el campo de texto **[!UICONTROL Nombre de ajuste preestablecido]**, escriba un nombre descriptivo. El nombre del ajuste preestablecido no se puede editar si posteriormente decide cambiarlo.

1. En la lista desplegable **[!UICONTROL Tipo de ajuste preestablecido]**, seleccione **[!UICONTROL Conjunto de imágenes]** o **[!UICONTROL Conjunto de giros]**. Asegúrese de elegir el tipo de ajuste preestablecido correcto, ya que no se podrá editar más adelante.
1. Seleccione **[!UICONTROL Crear]**.
1. A la derecha de la página **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]**, establezca las opciones editables que desee en los encabezados **[!UICONTROL Detalles de ajustes preestablecidos]** y **[!UICONTROL Convención de nomenclatura de conjuntos]**.
Para obtener más información sobre las opciones editables disponibles, consulte [Detalles de ajustes preestablecidos, Convención de nombres de conjuntos y Resultados de reglas - Opciones de RegX](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. Cree uno o varios grupos de expresiones regulares.

   * A la izquierda de la página **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]**, en **[!UICONTROL Coincidencia]**, **[!UICONTROL Nombre base]** o **[!UICONTROL Orden de secuencias]**, seleccione **[!UICONTROL Agregar grupo]**.
   * El campo **[!UICONTROL Coincidencia]** es obligatorio. **[!UICONTROL Nombre base]** es obligatorio solo si el campo **[!UICONTROL Coincidencia]** no especifica ya un nombre base mediante una agrupación de corchetes. **[!UICONTROL Ordenar secuencias]** es opcional.
   * Mediante las listas desplegables y los cuadros de texto del formulario del grupo, especifique el grupo de expresiones que desee utilizar para definir los criterios de nomenclatura de los miembros del recurso de conjunto de imágenes o de conjunto de giros.
      * A medida que selecciona y especifica expresiones para un grupo, observe que la sintaxis de expresión regular real se refleja cerca de la parte inferior derecha de la página, bajo el encabezado **[!UICONTROL Resultados de la regla - RegX]**. Para ver la cadena de expresión regular actualizada en la parte inferior derecha, seleccione en cualquier lugar fuera del área del formulario. Estas cadenas de expresión regular representan el patrón que desea hacer coincidir en una búsqueda de [!DNL Dynamic Media] recursos para crear su conjunto de imágenes o conjunto de giros.
      * Si ha agregado un grupo y desea eliminarlo, seleccione **[!UICONTROL X]**.
   * Cuando agregue dos o más grupos, en la lista desplegable **[!UICONTROL And]**, seleccione **[!UICONTROL And]** para combinar un grupo recién agregado con cualquier grupo de expresiones anterior que haya agregado. O bien, seleccione **[!UICONTROL O]** para agregar una alternancia entre el grupo de expresiones anterior y el nuevo grupo que cree. El operando **[!UICONTROL Or]** se define mediante el uso de un carácter de línea vertical `|` en la propia sintaxis de la expresión regular.

1. Realice una de las siguientes acciones:

   * Para agregar otro grupo nuevo, bajo **[!UICONTROL Coincidencia]**, **[!UICONTROL Nombre base]** o **[!UICONTROL Orden de secuenciación]**, seleccione **[!UICONTROL Agregar grupo]**. Cree otro grupo de expresiones regulares como en el paso anterior.
   * Revise la sintaxis de la expresión regular en el área **[!UICONTROL Resultados de la regla - RegX]**. Si debe cambiar la sintaxis, realice las ediciones en el grupo correspondiente de la izquierda de la página.
   * Si ha terminado de crear grupos de expresiones, continúe con el siguiente paso.

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

Ya está listo para aplicar el ajuste preestablecido del conjunto de lotes a una carpeta de recursos. A continuación, cargue los recursos en esa carpeta. Este flujo de trabajo da como resultado la generación automática del conjunto de imágenes o del conjunto de giros. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjuntos de lotes a carpetas de recursos](#apply-bsp).

### Detalles de ajustes preestablecidos, convención de nombres de conjuntos y resultados de reglas: opciones de RegX {#features-options-bsp}

Estas opciones están disponibles en la página **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]** al crear o editar un ajuste preestablecido de conjunto de lotes.

Consulte [Crear un ajuste preestablecido de conjunto por lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp) o [Editar un ajuste preestablecido de conjunto por lotes](#edit-bsp).

| **[!UICONTROL Detalles de ajustes preestablecidos]** | Descripción |
| --- | --- |
| Nombre de ajuste preestablecido  | Sólo lectura. El nombre que especificó la primera vez que creó el conjunto de lotes. Si debe cambiar el nombre del ajuste preestablecido, puede copiar el ajuste preestablecido del conjunto de lotes existente y especificar un nuevo nombre. Consulte [Copiar un ajuste preestablecido de conjunto de lotes existente](#copy-bsp). |
| Tipo | Sólo lectura. El tipo se especificó la primera vez que creó el conjunto de lotes. Copiar un ajuste preestablecido de conjunto de lotes existente no le permite cambiar su [!UICONTROL Tipo]; en su lugar, debe crear un ajuste preestablecido. |
| Incluir recursos derivados | Opcional. Para que el IPS (Image Production System) de [!DNL Dynamic Media] incluya imágenes generadas o &quot;derivadas&quot; con el conjunto de giros o el conjunto de imágenes, seleccione **[!UICONTROL Sí]** (predeterminado). Un recurso derivado es una imagen que un usuario no cargó directamente. En su lugar, IPS produjo el recurso cuando se cargó un recurso principal. Por ejemplo, un recurso de imagen que IPS generó a partir de una página en un PDF, en el momento en que el PDF se cargó en [!DNL Dynamic Media], se considera un recurso derivado. |
| Carpeta de destino | Opcional. Si define una gran cantidad de conjuntos de imágenes o conjuntos de giros, Adobe recomienda mantener estos conjuntos separados de las carpetas que contienen los propios recursos. Considere la posibilidad de crear una carpeta de conjuntos de imágenes o conjuntos de giros y redirija la aplicación para colocar aquí los conjuntos generados por lotes.<br>En tal caso, especifique qué carpeta de la estructura de carpetas de Experience Manager Assets (`/content/dam`) tiene el ajuste preestablecido de conjunto de lotes activo. Asegúrese de que la carpeta está habilitada para la sincronización de [!DNL Dynamic Media] con el fin de permitirla como carpeta de destino. Consulte [Configurar la publicación selectiva en el nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>Más de una carpeta puede tener un conjunto preestablecido de lotes asignado, si aplica el ajuste preestablecido mediante las **[!UICONTROL Propiedades]** de la carpeta. Consulte [Aplicar ajustes preestablecidos de conjunto de lotes desde la página Propiedades de una carpeta de recursos](#apply-bsp-to-folders-via-properties).<br>Si no especifica una carpeta, el conjunto de giros o el conjunto de imágenes predeterminado del conjunto de lotes generado se creará en la misma carpeta que la carpeta de recursos que cargó en. |
| **[!UICONTROL Convención de nomenclatura de conjuntos]** |  |
| Prefijo<br>o<br>Sufijo | Opcional. Introduzca un prefijo, un sufijo o ambos en los campos respectivos.<br>Los campos de prefijo y sufijo permiten crear muchos ajustes preestablecidos de conjunto de lotes utilizando una convención de nombres de archivo alternativa y personalizada para un conjunto determinado de contenido. Este método es especialmente útil en casos en los que hay una excepción al esquema de nombres predeterminado definido de una compañía.<br>El prefijo o sufijo se agrega al **[!UICONTROL Nombre base]** que defina en el área **[!UICONTROL Convención de nomenclatura de recursos]**. Al agregar un prefijo o sufijo, se asegura de que el conjunto de imágenes o de giros se cree de forma exclusiva e independiente de otros recursos. También puede servir para ayudar a otros a identificar tipos de archivos. Por ejemplo, para determinar un modo de color utilizado, puede agregar como prefijo o sufijo `rgb` o `cmyk`.<br>Aunque no es necesario especificar una convención de nombres de conjunto para utilizar la funcionalidad de ajuste preestablecido de conjunto por lotes, se recomienda que utilice la convención de nombres de conjunto. Esta práctica le permite definir tantos elementos de la convención de nombres como desee agrupar en un conjunto para ayudar a optimizar la creación de conjuntos de lotes. |
| **[!UICONTROL Resultados de la regla - RegX]** |  |
| Convención de nomenclatura de recursos - Coincidencia | Sólo lectura. Muestra la sintaxis de la expresión regular en función de las opciones de Formulario de coincidencia seleccionadas para el código sin procesar introducido. |
| Convención de nomenclatura de activos: nombre base | Sólo lectura. Muestra la sintaxis de la expresión regular en función de las opciones del formulario Nombre base que haya elegido para el código sin procesar introducido. |
| Ordenación de secuencias - Coincidencia | Sólo lectura. Muestra la sintaxis de la expresión regular en función de las opciones de formulario que haya elegido o del código sin procesar introducido. |

## Acerca de la aplicación de ajustes preestablecidos de conjunto de lotes a carpetas de recursos {#apply-bsp}

Cuando se asignan ajustes preestablecidos de conjunto de lotes a una o varias carpetas de recursos, las subcarpetas heredan automáticamente los ajustes preestablecidos de su carpeta principal.

Puede aplicar varios ajustes preestablecidos de conjunto de lotes a una carpeta de recursos.

Las carpetas que tienen un ajuste preestablecido por lotes asignado se indican en la interfaz de usuario con el nombre del ajuste preestablecido en la carpeta, en la vista **[!UICONTROL Tarjeta]**.

Para aplicar ajustes preestablecidos de conjunto de lotes a las carpetas de recursos, utilice uno de los dos métodos siguientes:

* [Aplicar ajustes preestablecidos de conjunto de lotes a las carpetas de recursos desde la página Ajustes preestablecidos de conjunto de lotes](#apply-bsp-to-folders-via-bsp-page): este método le ofrece la mayor flexibilidad. Puede aplicar uno o varios ajustes preestablecidos a una o varias carpetas.
* [Aplicar ajustes preestablecidos de conjunto de lotes desde la página Propiedades de una carpeta de recursos](#apply-bsp-to-folders-via-properties): este método permite aplicar uno o más ajustes preestablecidos de conjunto de lotes a una sola carpeta.

Como práctica recomendada, asegúrese de que las carpetas de recursos estén sincronizadas [!DNL Dynamic Media] y, a continuación, aplique los ajustes preestablecidos que desee.

Vuelva a procesar los recursos en una carpeta si se da cualquiera de las dos situaciones siguientes:

* Desea ejecutar un ajuste preestablecido de conjunto por lotes en una carpeta de recursos existente que ya tenga recursos cargados en ella.
* Posteriormente, edite un ajuste preestablecido de conjunto de lotes existente que se haya aplicado anteriormente a una carpeta de recursos.

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### Aplique ajustes preestablecidos de conjunto de lotes a las carpetas de recursos desde la página Ajustes preestablecidos de conjunto de lotes {#apply-bsp-to-folders-via-bsp-page}

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos por lotes]**.
1. En la página **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, active la casilla de verificación de cada ajuste preestablecido de conjunto de lotes que desee aplicar a las carpetas.
1. En la barra de herramientas, seleccione **[!UICONTROL Aplicar ajuste preestablecido de lotes a las carpetas]**.
1. En la página **[!UICONTROL Seleccionar carpetas]**, active la casilla de verificación de cada carpeta a la que desee aplicar los ajustes preestablecidos del conjunto de lotes.
1. En la esquina superior derecha de la página **[!UICONTROL Seleccionar carpetas]**, seleccione **[!UICONTROL Aplicar]**.

### Aplicar ajustes preestablecidos de conjunto de lotes desde la página Propiedades de una carpeta de recursos {#apply-bsp-to-folders-via-properties}

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Vaya a la carpeta en la que desea aplicar uno o más ajustes preestablecidos de conjunto de lotes.
1. En la página, a la izquierda de la columna **[!UICONTROL Nombre]**, active la casilla de verificación de una carpeta.
1. En la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.
1. En la página Propiedades de la carpeta, seleccione la ficha **[!UICONTROL Procesamiento de Dynamic Media]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. En **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, en el cuadro de lista desplegable **[!UICONTROL Nombre de ajuste preestablecido]**, seleccione el nombre de un ajuste preestablecido de conjunto de lotes que desee aplicar. La captura de pantalla anterior muestra dos ajustes preestablecidos de conjunto por lotes seleccionados que se aplican a la carpeta de recursos.

   Si no existen nombres de ajustes preestablecidos de conjunto de lotes en el cuadro de lista desplegable **[!UICONTROL Nombre de ajuste preestablecido]**, significa que aún no ha creado ningún ajuste preestablecido de conjunto de lotes. Consulte [Crear un ajuste preestablecido de conjunto por lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp).

   Para quitar un ajuste preestablecido de conjunto de lotes aplicado, seleccione **[!UICONTROL X]** a la derecha del tipo de ajuste preestablecido.

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar y cerrar]**.

## Editar un ajuste preestablecido de conjunto de lotes {#edit-bsp}

Puede editar un ajuste preestablecido de conjunto de lotes existente que haya creado. Puede cambiar cualquiera de los grupos de expresiones que creó para la convención de nomenclatura de recursos o el orden de secuencia. Si es necesario, también puede actualizar la carpeta de destino y establecer convenciones de nomenclatura.

Sin embargo, no puede cambiar el nombre ni el tipo de ajuste preestablecido (Conjunto de imágenes o Conjunto de giros). Si es necesario cambiar el nombre de un ajuste preestablecido, copie el ajuste preestablecido existente y especifique un nombre nuevo. Consulte [Copiar un ajuste preestablecido de conjunto por lotes](#copy-bsp).

Si edita un ajuste preestablecido de conjunto de lotes que se aplicó anteriormente a una carpeta, el ajuste preestablecido de conjunto de lotes recién editado se aplicará solo a los nuevos recursos cargados en esa carpeta.

Si desea que el ajuste preestablecido recién editado se vuelva a aplicar a los recursos existentes en la carpeta, debe volver a procesar la carpeta. <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->De este modo, los recursos existentes ahora cumplen los requisitos para formar parte de un conjunto de imágenes o de giros, y se agregarán. Además, los recursos existentes que ya se incluían en el conjunto de imágenes o el conjunto de giros (según el ajuste preestablecido de conjunto de lotes utilizado anteriormente) no se eliminan y se muestran tal cual. Este escenario supone que ya no se califican en función del ajuste preestablecido recién editado.

**Para editar un ajuste preestablecido de conjunto por lotes:**

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos por lotes]**.
1. En la página **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, compruebe el ajuste preestablecido de conjunto de lotes que desea cambiar.
1. En la barra de herramientas, seleccione **[!UICONTROL Editar conjunto de lotes preestablecido]**.
1. Edite el ajuste preestablecido según sea necesario.
1. En la esquina superior derecha de la página **[!UICONTROL Ajuste preestablecido por lotes]**, seleccione **[!UICONTROL Guardar]**.

## Copiar un ajuste preestablecido de conjunto de lotes existente {#copy-bsp}

Puede copiar un ajuste preestablecido de conjunto de lotes existente para evitar tener que volver a crear manualmente un ajuste preestablecido complejo o si simplemente desea cambiar el nombre de un ajuste preestablecido. Sin embargo, no se puede cambiar el tipo de ajuste preestablecido utilizado (conjunto de imágenes o conjunto de giros).

Si copia un ajuste preestablecido existente al que hacen referencia las carpetas de recursos, estas carpetas no se verán afectadas.

**Copiar un ajuste preestablecido de conjunto de lotes existente:**

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos por lotes]**.
1. En la página **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, active la casilla del ajuste preestablecido de conjunto de lotes que desee copiar.
1. En la barra de herramientas, seleccione **[!UICONTROL Copiar]**.
1. En el cuadro de diálogo **[!UICONTROL Copiar ajuste preestablecido de conjunto de lotes]**, en el cuadro de texto **[!UICONTROL Título]**, escriba un nuevo nombre para el ajuste preestablecido.

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. Seleccione **[!UICONTROL Copiar]**.

## Eliminar ajustes preestablecidos de conjuntos de lotes de carpetas {#remove-bsp-from-folder}

Al eliminar los ajustes preestablecidos del conjunto de lotes de las carpetas, los nuevos recursos que cargue en estas carpetas no tendrán aplicado el ajuste preestablecido del conjunto de lotes. Los recursos existentes en la carpeta que ya se añadieron al conjunto de imágenes o al conjunto de impresión en función del ajuste preestablecido del conjunto de lotes que se aplicó a la carpeta siguen mostrándose tal cual.

Si desea *eliminar* ajustes preestablecidos de carpetas, consulte [Eliminar ajustes preestablecidos de conjuntos de lotes](#delete-bsp).

Puede utilizar dos métodos para eliminar los ajustes preestablecidos del conjunto de lotes de las carpetas.

* [Elimine los ajustes preestablecidos del conjunto de lotes de las carpetas mediante la página Ajustes preestablecidos del conjunto de lotes](#remove-bsp-from-folders-via-bsp-page). Este método le ofrece la mayor flexibilidad. Puede quitar uno o varios ajustes preestablecidos de una o varias carpetas.
* [Quitar ajustes preestablecidos de conjunto de lotes de la página Propiedades de una carpeta](#remove-bsp-from-folders-via-properties): este método permite quitar uno o más ajustes preestablecidos de conjunto de lotes de una sola carpeta.

### Elimine los ajustes preestablecidos del conjunto de lotes de las carpetas mediante la página Ajustes preestablecidos de conjuntos de lotes {#remove-bsp-from-folders-via-bsp-page}

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos por lotes]**.
1. En la página **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, active la casilla de uno o más ajustes preestablecidos de conjunto de lotes que desee eliminar de una o varias carpetas.
1. En la barra de herramientas, seleccione **[!UICONTROL Quitar ajuste preestablecido de lotes de las carpetas]**.

1. En la página **[!UICONTROL Seleccionar carpetas]**, seleccione una o varias carpetas en las que desee eliminar los ajustes preestablecidos del conjunto de lotes.
1. En la esquina superior derecha de la página **[!UICONTROL Seleccionar carpetas]**, seleccione **[!UICONTROL Quitar]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. En el cuadro de diálogo **[!UICONTROL Quitar perfil]**, seleccione **[!UICONTROL Quitar]**.

### Elimine los ajustes preestablecidos del conjunto de lotes de la página Propiedades de una carpeta {#remove-bsp-from-folders-via-properties}

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Assets]** > **[!UICONTROL Archivos]**.
1. Vaya a la carpeta en la que desea eliminar uno o más ajustes preestablecidos de conjunto de lotes.
1. En la página, a la izquierda de la columna **[!UICONTROL Nombre]**, active la casilla de verificación de una carpeta.
1. En la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.
1. En la página Propiedades de la carpeta, seleccione **[!UICONTROL Procesamiento de Dynamic Media]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. En **[!UICONTROL Ajustes preestablecidos por lotes]**, seleccione **[!UICONTROL X]** a la derecha del tipo de ajuste preestablecido.

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar y cerrar]**.

## Eliminar ajustes preestablecidos del conjunto de lotes {#delete-bsp}

Puede eliminar los ajustes preestablecidos del conjunto de lotes para quitarlos de forma permanente de [!DNL Dynamic Media]. Es decir, ya no se muestran en la página [!UICONTROL Ajuste preestablecido de conjunto de lotes] ni en la lista desplegable **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** de la pestaña **[!UICONTROL Procesamiento de Dynamic Media]** de la página **[!UICONTROL Propiedades]** de la carpeta. Como tal, el ajuste preestablecido no se aplica a los recursos existentes al volver a procesar una carpeta o cuando se cargan nuevos recursos en la carpeta.

Si elimina un ajuste preestablecido que se haya aplicado anteriormente a una o varias carpetas, los conjuntos de imágenes o conjuntos de giros creados a partir de recursos de esas carpetas se seguirán mostrando tal cual.

Si desea *eliminar* ajustes preestablecidos de las carpetas, consulte [Eliminar ajustes preestablecidos de conjuntos de lotes de las carpetas](#remove-bsp-from-folder).

**Para eliminar los ajustes preestablecidos del conjunto de lotes:**

1. Seleccione el logotipo de Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Assets]** > **[!UICONTROL Ajustes preestablecidos por lotes]**.
1. En la página **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, active la casilla de uno o más ajustes preestablecidos de conjunto de lotes que desee eliminar.
1. En la barra de herramientas, seleccione **[!UICONTROL Eliminar ajustes preestablecidos del conjunto de lotes]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. En el cuadro de diálogo **[!UICONTROL Eliminar ajustes preestablecidos de conjunto de lotes]**, seleccione **[!UICONTROL Eliminar]**.

   Si una carpeta de recursos hace referencia al ajuste preestablecido que está eliminando, seleccione **[!UICONTROL Forzar eliminación]** en su lugar.

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [Conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md)
>* [Conjuntos de giros](/help/assets/dynamic-media/spin-sets.md)
>* [Configurar la publicación selectiva en el nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder). Consulte &quot;Modo de sincronización&quot; en el tema si desea obtener más información acerca de la sincronización de una sola carpeta con [!DNL Dynamic Media].
>* [Crear una configuración de Dynamic Media en Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services). Consulte &quot;Modo de sincronización de Dynamic Media&quot; en el tema si desea obtener más información sobre cómo sincronizar todas las carpetas con [!DNL Dynamic Media].
