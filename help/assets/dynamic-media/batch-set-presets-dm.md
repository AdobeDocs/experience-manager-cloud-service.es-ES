---
title: Valores preestablecidos de conjunto por lotes
description: Descubra cómo automatizar la creación de conjuntos de imágenes y conjuntos de giros mediante valores preestablecidos de conjunto por lotes en Dynamic Media.
contentOwner: Rick Brough
feature: Image Presets,Viewer Presets
role: User
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '3442'
ht-degree: 1%

---

# Acerca de los ajustes preestablecidos de conjuntos de lotes {#about-bsp}

Uso **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** para crear y organizar varios recursos en un conjunto de imágenes o un conjunto de giros en el momento de cargar archivos de recursos en una carpeta, ya sea de forma individual o mediante la ingesta masiva. Puede hacer que el ajuste preestablecido se ejecute junto con los trabajos de importación de recursos que programe en [!DNL Dynamic Media]. Cada ajuste preestablecido es un conjunto de instrucciones con un nombre único e independiente que define cómo construir el conjunto de imágenes o el conjunto de giros utilizando imágenes que coinciden con las convenciones de nomenclatura definidas en la fórmula preestablecida.

>[!IMPORTANT]
>
>¿Está utilizando ajustes preestablecidos de conjuntos de lotes en [!DNL Dynamic Media Classic]y migrando desde [!DNL Dynamic Media Classic] a Adobe Experience Manager as a Cloud Service? Si es así, debe volver a crear manualmente las definiciones de los ajustes preestablecidos de conjuntos de lotes en [!DNL Adobe Experience Manager as a Cloud Service].

**Práctica recomendada** - Al trabajar con ajustes preestablecidos de conjuntos de lotes, el Adobe recomienda el siguiente flujo de trabajo:

1. Cree un ajuste preestablecido de conjunto de lotes. Consulte [Crear un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp).
1. Cree una carpeta de recursos o utilice una carpeta de recursos existente y asegúrese de que está sincronizada con [!DNL Dynamic Media]. Consulte [Crear carpetas](/help/assets/manage-digital-assets.md#creating-folders).
1. Aplique el ajuste preestablecido de conjunto de lotes a la carpeta de recursos. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjuntos de lotes a carpetas](#apply-bsp).
1. Cargar imágenes a la carpeta de recursos. Consulte [Cargar recursos para conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [Cargar recursos para conjuntos de giros](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets)o [Adición de recursos digitales a Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. El conjunto de imágenes o el conjunto de giros se generan automáticamente en la carpeta deseada.
1. Publique el conjunto de imágenes o el conjunto de giros. Consulte [Publicar recursos de Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Crear un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros {#creating-bsp}

Para crear ajustes preestablecidos de conjuntos de lotes, es deseable que tenga cierta familiaridad y comprensión de las expresiones regulares.

Lo ideal es que su empresa ya haya definido una convención de nomenclatura para saber cómo se agrupan los recursos en un conjunto.
Para ayudarle a comprender la importancia de utilizar una convención de nombres, supongamos que la convención de nombres definida de su empresa es `<style>-<color>-<view>`. Y, el nombre base del conjunto siempre debe ser `<style>-<color>`y la extensión del nombre del conjunto se `-SET`. Si carga una imagen con el nombre `0123-RED-01`, se crearía un conjunto con el nombre `0123-RED-SET`. Si más tarde carga imágenes `0123-RED-03` y `0123-BLUE-01`, luego la variable `RED-03` la imagen se agregaría al conjunto en la segunda posición porque está ordenada por debajo de `01`. Sin embargo, la variable `BLUE-01` la imagen formaría parte de un nuevo conjunto denominado `0123-BLUE-SET`. Para la siguiente carga de recursos, agregue archivos `0123-RED-02` y `0123-BLUE-02`. Cada recurso se agregaría a su conjunto respectivo. La variable `RED-02` la imagen se ordenaría automáticamente entre los `01` y `03` por el orden.

La variable **[!UICONTROL Ajuste preestablecido de conjunto de lotes]** en [!DNL Dynamic Media] permite crear, editar o eliminar ajustes preestablecidos de conjuntos de lotes y aplicar o quitar ajustes preestablecidos de conjuntos de lotes de las carpetas de recursos o desde ellas. Puede utilizar las listas desplegables de campos de formulario para definir un ajuste preestablecido de conjunto de lotes o utilizar la variable **[!UICONTROL Código sin procesar]** , que permite escribir la sintaxis de la expresión regular.

Puede crear muchos ajustes preestablecidos de conjuntos de lotes para cubrir todos los trabajos de ingesta de recursos que necesite.

### Acerca de la Convención de nomenclatura de recursos

La variable **[!UICONTROL Convención de nomenclatura de recursos]** en el **[!UICONTROL Ajuste preestablecido de conjunto de lotes]** tiene dos elementos que puede utilizar para definir el ajuste preestablecido de conjunto de lotes: **[!UICONTROL Coincidencia]** y **[!UICONTROL Nombre base]**. Estos elementos permiten definir una convención de nombres e identificar la parte de la convención utilizada para asignar un nombre al conjunto en el que están contenidos. <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

La convención de nombres individual de una empresa a menudo utiliza una o más líneas de definición de cada uno de estos dos elementos. Puede utilizar tantas líneas para su definición única y agruparlas en elementos distintos, como Imagen principal, Elemento de color, Elemento de vista alternativa y Elemento de muestra.

Por ejemplo, la sintaxis de una expresión regular de coincidencia literal podría ser similar a la siguiente:

`(\w+)-\w+-\w+`

### Acerca del orden de secuencias

Si lo desea, puede definir el orden en el que se muestran las imágenes después de agrupar el conjunto de imágenes o el conjunto de giros [!DNL Dynamic Media]. De forma predeterminada, los recursos se ordenan alfanuméricamente. Sin embargo, puede utilizar una lista de expresiones regulares separadas por coma para definir el orden.

En cuanto a la automatización de la ordenación de secuencias, se especifican reglas para forzar la ordenación de los recursos de una determinada manera, si es necesario. Por ejemplo, suponga que el primer recurso siempre tiene un nombre `_main` y desea que se le siga con `_alt1`, `_alt2`, `_alt3`, etc. En estos casos, puede crear una regla de orden de secuencia con la siguiente sintaxis:

`.*_main,.*_alt[0-9]`

Aunque es posible ordenar una secuencia a fuerza, lo mejor es utilizar la numeración alfanumérica para ordenar secuencias en la medida de lo posible. Además, puede utilizar el conjunto de imágenes o las herramientas del editor de conjuntos de giros en [!DNL Dynamic Media] para reorganizar el orden de las secuencias de los recursos o agregar y eliminar nuevos recursos en el conjunto mediante una operación de arrastrar y soltar.

Cuando termine de crear un ajuste preestablecido de conjunto de lotes, debe aplicarlo a una o varias carpetas que haya creado. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjuntos de lotes a carpetas](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**Para crear un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros:**

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. En el **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** página, cerca de la esquina superior derecha, seleccione **[!UICONTROL Crear]**.
1. En el **[!UICONTROL Crear ajuste preestablecido de conjunto de lotes]** en el **[!UICONTROL Nombre de ajuste preestablecido]** campo de texto, introduzca un nombre descriptivo. El nombre del ajuste preestablecido no se puede editar si más adelante decide cambiarlo.

1. En el **[!UICONTROL Tipo de ajuste preestablecido]** lista desplegable, seleccione **[!UICONTROL Conjunto de imágenes]** o **[!UICONTROL Conjunto de giros]**. Asegúrese de elegir el tipo de ajuste preestablecido correcto; no se puede editar más tarde.
1. Seleccione **[!UICONTROL Crear]**.
1. A la derecha del **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]** establezca las opciones editables que desee en la sección **[!UICONTROL Detalles de ajustes preestablecidos]** y **[!UICONTROL Definir convención de nomenclatura]** encabezados.
Para obtener más información sobre las opciones editables que están disponibles, consulte [Detalles de ajustes preestablecidos, Convención de asignación de nombres y Resultados de reglas: opciones de RegX](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. Cree uno o más grupos de expresiones regulares.

   * A la izquierda del **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]** página, en **[!UICONTROL Coincidencia]**, **[!UICONTROL Nombre base]** o **[!UICONTROL Orden de secuencias]**, seleccione **[!UICONTROL Agregar grupo]**.
   * La variable **[!UICONTROL Coincidencia]** es obligatorio. **[!UICONTROL Nombre base]** solo es obligatorio si la variable **[!UICONTROL Coincidencia]** El campo no especifica todavía un nombre base mediante una agrupación de corchetes. **[!UICONTROL Orden de secuencias]** es opcional.
   * Mediante las listas desplegables y los cuadros de texto del formulario del grupo, especifique un grupo de expresiones que desee utilizar para definir los criterios de nomenclatura para el conjunto de imágenes o los miembros del recurso de conjuntos de giros.
      * Al seleccionar y especificar expresiones para un grupo, observe que la sintaxis real de la expresión regular se refleja cerca de la parte inferior derecha de la página, debajo de la variable **[!UICONTROL Resultados de regla - RegX]** encabezado. Para ver la cadena de expresión regular actualizada en la parte inferior derecha, seleccione cualquier lugar fuera del área del formulario. Estas cadenas de expresión regular representan el patrón que desea que coincida en una búsqueda de [!DNL Dynamic Media] recursos para crear el conjunto de imágenes o el conjunto de giros.
      * Si ha agregado un grupo y desea eliminarlo, seleccione **[!UICONTROL X]**.
   * Cuando agregue dos o más grupos, en la variable **[!UICONTROL Y]** lista desplegable, seleccione **[!UICONTROL Y]** para combinar un grupo recién agregado con cualquier grupo de expresiones anterior que haya agregado. O bien, seleccione **[!UICONTROL O]** para agregar una alternativa entre el grupo de expresiones anterior y el nuevo grupo que cree. La variable **[!UICONTROL O]** operando se define mediante el uso de un carácter de línea vertical `|` en la sintaxis de expresión regular.

1. Realice una de las acciones siguientes:

   * Para agregar otro grupo nuevo, en **[!UICONTROL Coincidencia]**, **[!UICONTROL Nombre base]** o **[!UICONTROL Orden de secuencia]**, seleccione **[!UICONTROL Agregar grupo]**. Cree otro grupo de expresiones regulares como en el paso anterior.
   * Revise la sintaxis de la expresión regular en la **[!UICONTROL Resultados de regla - RegX]** . Si debe cambiar la sintaxis, realice las ediciones en el grupo correspondiente de la izquierda de la página.
   * Si ha terminado de crear grupos de expresiones, continúe con el siguiente paso.

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar]**.

Ya está listo para aplicar el ajuste preestablecido de conjunto de lotes a una carpeta de recursos. A continuación, cargue los recursos en esa carpeta. Este flujo de trabajo genera automáticamente el conjunto de imágenes o el conjunto de giros. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjuntos de lotes a carpetas de recursos](#apply-bsp).

### Detalles de ajustes preestablecidos, Convención de asignación de nombres y Resultados de reglas: opciones de RegX {#features-options-bsp}

Estas opciones están disponibles en la **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]** cuando cree o edite un ajuste preestablecido de conjunto de lotes.

Consulte [Crear un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp) o [Edición de un ajuste preestablecido de conjunto de lotes](#edit-bsp).

| **[!UICONTROL Detalles del ajuste preestablecido]** | Descripción |
| --- | --- |
| Nombre de ajuste preestablecido  | Solo lectura. El nombre especificado al crear el conjunto de lotes por primera vez. Si debe cambiar el nombre del ajuste preestablecido, puede copiar el ajuste preestablecido de conjunto de lotes existente y especificar un nuevo nombre. Consulte [Copiar un ajuste preestablecido de conjunto de lotes existente](#copy-bsp). |
| Tipo | Solo lectura. El tipo se especificó la primera vez que creó el conjunto de lotes. La copia de un ajuste preestablecido de conjunto de lotes existente no permite cambiar su [!UICONTROL Tipo]; en su lugar, debe crear un ajuste preestablecido. |
| Incluir recursos derivados | Opcional. Para [!DNL Dynamic Media]Los IPS de (Image Production System) incluyen imágenes generadas o &quot;derivadas&quot; con su conjunto de giros o conjunto de imágenes, seleccione **[!UICONTROL Sí]** (predeterminado). Un recurso derivado es una imagen que un usuario no ha cargado directamente. En su lugar, IPS produjo el recurso cuando se cargó un recurso maestro. Por ejemplo, un recurso de imagen que IPS generó a partir de una página en un PDF en el momento en que se cargó el PDF en [!DNL Dynamic Media], se considera un recurso derivado. |
| Carpeta de destino | Opcional. Si define un gran número de conjuntos de imágenes o conjuntos de giros, Adobe recomienda mantener estos conjuntos separados de las carpetas que contienen los propios recursos. Como tal, considere la posibilidad de crear una carpeta Conjuntos de imágenes o Conjuntos de giros y redirija la aplicación para colocar conjuntos de lotes generados aquí.<br>En este caso, especifique qué carpeta dentro de la estructura de carpetas de Experience Manager Assets (`/content/dam`) tiene activo el ajuste preestablecido de conjunto de lotes. Asegúrese de que la carpeta esté habilitada para [!DNL Dynamic Media] como carpeta de destino. Consulte [Configurar la publicación selectiva en el nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>Si se aplica el ajuste preestablecido mediante el ajuste preestablecido de la carpeta, puede asignarse a más de una carpeta un conjunto de lotes determinado preestablecido **[!UICONTROL Propiedades]**. Consulte [Aplicar ajustes preestablecidos de conjuntos de lotes desde la página Propiedades de una carpeta de recursos](#apply-bsp-to-folders-via-properties).<br>Si no especifica ninguna carpeta, el conjunto de lotes preestablecido de conjunto de imágenes generado o el conjunto de giros se crea en la misma carpeta que la carpeta de recursos cargada en. |
| **[!UICONTROL Establezca la convención de asignación de nombres]** |  |
| Prefijo<br>o<br>Sufijo | Opcional. Introduzca un prefijo, un sufijo o ambos en los campos correspondientes.<br>Los campos prefijo y sufijo permiten crear muchos ajustes preestablecidos de conjuntos de lotes utilizando una convención de nombres de archivo personalizada y alternativa para un conjunto de contenido determinado. Este método es especialmente útil en casos en los que hay una excepción al esquema de nombres predeterminado definido por la empresa.<br>El prefijo o sufijo se agrega al **[!UICONTROL Nombre base]** usted define en el **[!UICONTROL Convención de nomenclatura de recursos]** . Al agregar un prefijo o sufijo, se asegura de que el conjunto de imágenes o el conjunto de giros se creen de forma exclusiva e independiente de otros recursos. También puede servir para ayudar a otros a identificar tipos de archivos. Por ejemplo, para determinar un modo de color utilizado, puede agregar como prefijo o sufijo `rgb` o `cmyk`.<br>Aunque no es necesario especificar una convención de nombres de conjuntos para utilizar la funcionalidad preestablecida de conjuntos de lotes, se recomienda utilizar la convención de nombres de conjuntos. Esta práctica permite definir tantos elementos de la convención de nombres como desee agrupar en un conjunto para ayudar a optimizar la creación de conjuntos de lotes. |
| **[!UICONTROL Resultados de la regla - RegX]** |  |
| Convención de nomenclatura de recursos - Coincidencia | Solo lectura. Muestra la sintaxis de la expresión regular en función de las opciones de formulario de coincidencia que haya elegido o del código sin procesar que haya introducido. |
| Convención de nombres de recursos - Nombre base | Solo lectura. Muestra la sintaxis de la expresión regular en función de las opciones de formulario Nombre base que haya elegido o del código sin procesar que haya introducido. |
| Orden de secuencias: Coincidencia | Solo lectura. Muestra la sintaxis de la expresión regular en función de las opciones de formulario que haya elegido o el código sin procesar que haya introducido. |

## Acerca de la aplicación de ajustes preestablecidos de conjuntos de lotes a carpetas de recursos {#apply-bsp}

Cuando asigna ajustes preestablecidos de conjuntos de lotes a una o varias carpetas de recursos, las subcarpetas heredan automáticamente los ajustes preestablecidos de su carpeta principal.

Puede aplicar varios ajustes preestablecidos de conjuntos de lotes a una carpeta de recursos.

Las carpetas que tienen un ajuste preestablecido de lote asignado se indican en la interfaz de usuario con el nombre del ajuste preestablecido que aparece en la carpeta , en la **[!UICONTROL Tarjeta]** vista.

Para aplicar ajustes preestablecidos de conjuntos de lotes a carpetas de recursos, utilice uno de los dos métodos siguientes:

* [Aplicar ajustes preestablecidos de conjuntos de lotes a carpetas de recursos desde la página Ajuste preestablecido de conjuntos de lotes](#apply-bsp-to-folders-via-bsp-page) - Este método le ofrece la mayor flexibilidad. Puede aplicar uno o varios ajustes preestablecidos a una o varias carpetas.
* [Aplicar ajustes preestablecidos de conjuntos de lotes desde la página Propiedades de una carpeta de recursos](#apply-bsp-to-folders-via-properties) - Este método permite aplicar uno o más ajustes preestablecidos de conjuntos de lotes a una única carpeta.

Como práctica recomendada, asegúrese de que las carpetas de recursos están sincronizadas [!DNL Dynamic Media]y, a continuación, aplique los ajustes preestablecidos que desee.

Volver a procesar los recursos en una carpeta si se da alguna de las dos situaciones siguientes:

* Desea ejecutar un ajuste preestablecido de conjunto de lotes en una carpeta de recursos existente que ya tenga activos cargados en ella.
* Posteriormente, edita un ajuste preestablecido de conjunto de lotes existente que se aplicaba anteriormente a una carpeta de recursos.

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### Aplicar ajustes preestablecidos de conjuntos de lotes a carpetas de recursos desde la página Ajuste preestablecido de conjuntos de lotes {#apply-bsp-to-folders-via-bsp-page}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**.
1. En el **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** a la izquierda del **[!UICONTROL Nombre de ajuste preestablecido]** , active la casilla de verificación de cada ajuste preestablecido de conjunto de lotes que desee aplicar a las carpetas.
1. En la barra de herramientas, seleccione **[!UICONTROL Aplicar ajustes preestablecidos de lote a carpetas]**.
1. En el **[!UICONTROL Seleccionar carpetas]** , active la casilla de verificación de cada carpeta a la que desee aplicar los ajustes preestablecidos de conjunto de lotes.
1. En la esquina superior derecha de la variable **[!UICONTROL Seleccionar carpetas]** página, seleccione **[!UICONTROL Aplicar]**.

### Aplicar ajustes preestablecidos de conjuntos de lotes desde la página Propiedades de una carpeta de recursos {#apply-bsp-to-folders-via-properties}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**.
1. Vaya a la carpeta en la que desee aplicar uno o varios ajustes preestablecidos de conjuntos de lotes.
1. En la página , a la izquierda del **[!UICONTROL Nombre]** , seleccione la casilla de verificación de una carpeta.
1. En la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.
1. En la página Propiedades de la carpeta, seleccione la opción **[!UICONTROL Procesamiento de Dynamic Media]** pestaña .

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. En **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, en la **[!UICONTROL Nombre de ajuste preestablecido]** cuadro de lista desplegable, seleccione el nombre de un ajuste preestablecido de conjunto de lotes que desee aplicar. La captura de pantalla anterior muestra dos ajustes preestablecidos de conjuntos de lotes seleccionados que se aplican a la carpeta de recursos.

   Si no existen nombres de ajustes preestablecidos de conjuntos de lotes en la variable **[!UICONTROL Nombre de ajuste preestablecido]** cuadro de lista desplegable, significa que aún no ha creado ningún ajuste preestablecido de conjunto de lotes. Consulte [Crear un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp).

   Para quitar un ajuste preestablecido de conjunto de lotes aplicado, seleccione **[!UICONTROL X]** a la derecha del tipo de ajuste preestablecido.

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar y cerrar]**.

## Edición de un ajuste preestablecido de conjunto de lotes {#edit-bsp}

Puede editar un ajuste preestablecido de conjunto de lotes existente que haya creado. Puede cambiar cualquiera de los grupos de expresiones creados para la convención de nombres de recursos o el orden de secuencia. Si es necesario, también puede actualizar la carpeta de destino y establecer las convenciones de nomenclatura.

Sin embargo, no se puede cambiar el nombre o el tipo de ajuste preestablecido (conjunto de imágenes o conjunto de giros). Si es necesario cambiar el nombre de un ajuste preestablecido, copie el ajuste preestablecido existente y especifique un nuevo nombre. Consulte [Copiar un ajuste preestablecido de conjunto de lotes](#copy-bsp).

Si edita un ajuste preestablecido de conjunto de lotes que se haya aplicado anteriormente a una carpeta, el ajuste preestablecido de conjunto de lotes recién editado se aplicará únicamente a los nuevos recursos cargados en esa carpeta.

Si desea que el ajuste preestablecido recién editado se vuelva a aplicar a los recursos existentes en la carpeta, debe volver a procesar la carpeta. <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->De este modo, los recursos existentes ahora cumplirían los requisitos para formar parte de un conjunto de imágenes o un conjunto de giros y se añadirían. Además, los activos existentes que ya estaban incluidos en el conjunto de imágenes o el conjunto de giros (según el conjunto de lotes preestablecido utilizado) no se eliminan ni se muestran tal cual. En este escenario se supone que ya no cumplen los requisitos según el ajuste preestablecido recién editado.

**Para editar un ajuste preestablecido de conjunto de lotes:**

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**.
1. En el **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** a la izquierda del **[!UICONTROL Nombre de ajuste preestablecido]** , compruebe el ajuste preestablecido del conjunto de lotes que desea cambiar.
1. En la barra de herramientas, seleccione **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]**.
1. Edite el ajuste preestablecido según sea necesario.
1. En la esquina superior derecha de la variable **[!UICONTROL Ajuste preestablecido de conjunto de lotes]** página, seleccione **[!UICONTROL Guardar]**.

## Copiar un ajuste preestablecido de conjunto de lotes existente {#copy-bsp}

Puede copiar un ajuste preestablecido de conjunto de lotes existente para evitar tener que volver a crear manualmente un ajuste preestablecido complejo, o si simplemente desea cambiar el nombre de un ajuste preestablecido. Sin embargo, no se puede cambiar el tipo de ajuste preestablecido utilizado (conjunto de imágenes o conjunto de giros).

Si copia un ajuste preestablecido existente al que hacen referencia las carpetas de recursos, estas carpetas no se verán afectadas.

**Copiar un ajuste preestablecido de conjunto de lotes existente:**

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**.
1. En el **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** a la izquierda del **[!UICONTROL Nombre de ajuste preestablecido]** , seleccione la casilla de verificación del ajuste preestablecido de conjunto de lotes que desea copiar.
1. En la barra de herramientas, seleccione **[!UICONTROL Copiar]**.
1. En el **[!UICONTROL Copiar ajuste preestablecido de conjunto de lotes]** en el **[!UICONTROL Título]** , escriba un nombre nuevo para el ajuste preestablecido.

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. Select **[!UICONTROL Copiar]**.

## Acerca de la eliminación de ajustes preestablecidos de conjuntos de lotes de carpetas {#remove-bsp-from-folder}

Al quitar los ajustes preestablecidos de conjuntos de lotes de las carpetas, los recursos nuevos que cargue en estas carpetas no tendrán el ajuste preestablecido de conjuntos de lotes aplicado. Los recursos existentes en la carpeta que ya se habían agregado al conjunto de imágenes o al conjunto de giros en función del ajuste preestablecido de conjunto de lotes que se aplicó a la carpeta siguen mostrándose tal cual.

Si desea *delete* ajustes preestablecidos de carpetas, consulte [Eliminar ajustes preestablecidos de conjuntos de lotes](#delete-bsp).

Existen dos métodos que puede utilizar para eliminar los ajustes preestablecidos de conjuntos de lotes de las carpetas.

* [Eliminar los ajustes preestablecidos de conjuntos de lotes de las carpetas mediante la página Ajuste preestablecido de conjuntos de lotes](#remove-bsp-from-folders-via-bsp-page) - Este método le ofrece la mayor flexibilidad. Puede quitar uno o varios ajustes preestablecidos de una carpeta o carpetas únicas.
* [Eliminar los ajustes preestablecidos de conjuntos de lotes de la página Propiedades de una carpeta](#remove-bsp-from-folders-via-properties) - Este método permite eliminar uno o más ajustes preestablecidos de conjuntos de lotes de una única carpeta.

### Eliminar los ajustes preestablecidos de conjuntos de lotes de las carpetas mediante la página Ajuste preestablecido de conjuntos de lotes {#remove-bsp-from-folders-via-bsp-page}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**.
1. En el **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** a la izquierda del **[!UICONTROL Nombre de ajuste preestablecido]** , active la casilla de verificación de uno o varios ajustes preestablecidos de conjuntos de lotes que desee eliminar de una o varias carpetas.
1. En la barra de herramientas, seleccione **[!UICONTROL Quitar ajustes preestablecidos de lote de carpetas]**.

1. En el **[!UICONTROL Seleccionar carpetas]** seleccione una o varias carpetas en las que desea eliminar los ajustes preestablecidos de conjuntos de lotes.
1. En la esquina superior derecha de la variable **[!UICONTROL Seleccionar carpetas]** página, seleccione **[!UICONTROL Eliminar]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. En el **[!UICONTROL Eliminar perfil]** cuadro de diálogo, seleccione **[!UICONTROL Eliminar]**.

### Eliminar los ajustes preestablecidos de conjuntos de lotes de la página Propiedades de una carpeta {#remove-bsp-from-folders-via-properties}

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Recursos]** > **[!UICONTROL Archivos]**.
1. Desplácese a la carpeta en la que desee eliminar uno o varios ajustes preestablecidos de conjuntos de lotes.
1. En la página , a la izquierda del **[!UICONTROL Nombre]** , seleccione la casilla de verificación de una carpeta.
1. En la barra de herramientas, seleccione **[!UICONTROL Propiedades]**.
1. En la página Propiedades de la carpeta, seleccione **[!UICONTROL Procesamiento de Dynamic Media]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. En **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, seleccione **[!UICONTROL X]** a la derecha del tipo de ajuste preestablecido.

1. En la esquina superior derecha de la página, seleccione **[!UICONTROL Guardar y cerrar]**.

## Eliminar ajustes preestablecidos de conjuntos de lotes {#delete-bsp}

Puede eliminar los ajustes preestablecidos de conjuntos de lotes para quitarlos permanentemente de [!DNL Dynamic Media]. Es decir, ya no se muestran en el [!UICONTROL Ajuste preestablecido de conjunto de lotes] ni se muestran en la variable **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** lista desplegable del **[!UICONTROL Procesamiento de Dynamic Media]** de la carpeta **[!UICONTROL Propiedades]** página. Como tal, el ajuste preestablecido no se aplica a los recursos existentes en un reprocesamiento de carpetas ni cuando se cargan nuevos recursos en la carpeta.

Si elimina un ajuste preestablecido que se haya aplicado anteriormente a una o varias carpetas, cualquier conjunto de imágenes o conjunto de giros que se hayan creado a partir de recursos de esas carpetas seguirá mostrándose tal cual.

Si desea *remove* ajustes preestablecidos de carpetas, consulte [Quitar los ajustes preestablecidos de conjuntos de lotes de las carpetas](#remove-bsp-from-folder).

**Para eliminar los ajustes preestablecidos de conjuntos de lotes:**

1. Seleccione el logotipo del Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**.
1. En el **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** a la izquierda del **[!UICONTROL Nombre de ajuste preestablecido]** , active la casilla de verificación de uno o varios ajustes preestablecidos de conjuntos de lotes que desee eliminar.
1. En la barra de herramientas, seleccione **[!UICONTROL Eliminar ajustes preestablecidos de conjunto de lotes]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. En el **[!UICONTROL Eliminar ajustes preestablecidos de conjunto de lotes]** cuadro de diálogo, seleccione **[!UICONTROL Eliminar]**.

   Si una carpeta de recursos hace referencia al ajuste preestablecido que está eliminando, seleccione **[!UICONTROL Forzar eliminación]** en su lugar.

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [Conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md)
>* [Conjuntos de giros](/help/assets/dynamic-media/spin-sets.md)
>* [Configurar la publicación selectiva en el nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder) - Consulte &quot;Modo de sincronización&quot; en el tema si desea obtener más información sobre la sincronización de una sola carpeta en [!DNL Dynamic Media].
>* [Crear una configuración de Dynamic Media en Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) - Consulte &quot;Modo de sincronización de Dynamic Media&quot; en el tema si desea obtener más información sobre la sincronización de todas las carpetas en [!DNL Dynamic Media].

