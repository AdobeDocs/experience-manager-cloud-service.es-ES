---
title: Valores preestablecidos de conjunto por lotes
description: Descubra cómo automatizar la creación de conjuntos de imágenes y conjuntos de giros mediante valores preestablecidos de conjunto por lotes en Dynamic Media.
contentOwner: Rick Brough
feature: Ajustes preestablecidos de imagen, Ajustes preestablecidos de visor
role: Business Practitioner
exl-id: 022ee347-54ec-4cec-b808-9eb3a9e51424
translation-type: tm+mt
source-git-commit: 1fe6ce1259972c1805d934327aa2f24cdcdc0bc8
workflow-type: tm+mt
source-wordcount: '3435'
ht-degree: 1%

---

# Acerca de los ajustes preestablecidos de conjuntos de lotes {#about-bsp}

Utilice **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** para crear y organizar varios recursos en un conjunto de imágenes o conjunto de giros en el momento de cargar archivos de recursos en una carpeta, ya sea de forma individual o mediante ingesta masiva. Puede hacer que el ajuste preestablecido se ejecute junto con los trabajos de importación de recursos que programe en [!DNL Dynamic Media]. Cada ajuste preestablecido es un conjunto de instrucciones con un nombre único e independiente que define cómo construir el conjunto de imágenes o el conjunto de giros utilizando imágenes que coinciden con las convenciones de nomenclatura definidas en la fórmula preestablecida.

>[!IMPORTANT]
>
>Si ha utilizado ajustes preestablecidos de conjuntos de lotes en [!DNL Dynamic Media Classic] y está migrando de [!DNL Dynamic Media Classic] a Adobe Experience Manager como Cloud Service, vuelva a crear manualmente las definiciones de los ajustes preestablecidos de conjuntos de lotes en [!DNL Adobe Experience Manager as a Cloud Service].

**Práctica recomendada** : Al trabajar con ajustes preestablecidos de conjuntos de lotes, el Adobe recomienda el siguiente flujo de trabajo:

1. Cree un ajuste preestablecido de conjunto de lotes. Consulte [Creación de un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp).
1. Cree una carpeta de recursos o utilice una carpeta de recursos existente y asegúrese de que está sincronizada con [!DNL Dynamic Media]. Consulte [Creación de carpetas](/help/assets/manage-digital-assets.md#creating-folders).
1. Aplique el ajuste preestablecido de conjunto de lotes a la carpeta de recursos. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjuntos de lotes a las carpetas](#apply-bsp).
1. Cargar imágenes a la carpeta de recursos. Consulte [Carga de recursos para conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [Carga de recursos para conjuntos de giros](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets) o [Adición de recursos digitales a Adobe Experience Manager](/help/assets/add-assets.md#add-assets-to-experience-manager).
1. El conjunto de imágenes o el conjunto de giros se generan automáticamente en la carpeta deseada.
1. Publique el conjunto de imágenes o el conjunto de giros. Consulte [Publicación de recursos de Dynamic Media](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Creación de un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros {#creating-bsp}

Para crear ajustes preestablecidos de conjuntos de lotes, es deseable que tenga cierta familiaridad y comprensión de las expresiones regulares.

Lo ideal es que su empresa ya haya definido una convención de nomenclatura para saber cómo se agrupan los recursos en un conjunto.
Para ayudarle a comprender la importancia de utilizar una convención de nombres, supongamos que la convención de nombres definida por su empresa es `<style>-<color>-<view>`. Además, el nombre base del conjunto siempre debe ser `<style>-<color>` y la extensión del nombre del conjunto debe ser `-SET`. Si carga una imagen con el nombre `0123-RED-01`, se creará un conjunto con el nombre `0123-RED-SET`. Si más adelante carga imágenes `0123-RED-03` y `0123-BLUE-01`, la imagen `RED-03` se agregará al conjunto en la segunda posición porque está ordenada por debajo de `01`. Sin embargo, la imagen `BLUE-01` formaría parte de un nuevo conjunto denominado `0123-BLUE-SET`. Para la siguiente carga de recursos, agregue archivos `0123-RED-02` y `0123-BLUE-02`. Cada recurso se agregaría a su conjunto respectivo. La imagen `RED-02` se ordenaría automáticamente entre las imágenes `01` y `03` existentes debido al orden de clasificación.

La página **[!UICONTROL Ajuste preestablecido de conjunto de lotes]** de [!DNL Dynamic Media] permite crear, editar o eliminar ajustes preestablecidos de conjuntos de lotes y aplicar o quitar ajustes preestablecidos de conjuntos de lotes de las carpetas de recursos. Puede utilizar las listas desplegables de campos de formulario para definir un ajuste preestablecido de conjunto de lotes o el campo **[!UICONTROL Raw Code]**, que permite escribir la sintaxis de las expresiones regulares.

Puede crear muchos ajustes preestablecidos de conjuntos de lotes para cubrir todos los trabajos de ingesta de recursos que necesite.

### Acerca de la Convención de nomenclatura de recursos

El área **[!UICONTROL Convención de nombres de recursos]** de la página **[!UICONTROL Ajuste preestablecido de conjunto de lotes]** tiene dos elementos que puede utilizar para definir el ajuste preestablecido de conjunto de lotes: **[!UICONTROL Coincidir]** y **[!UICONTROL Nombre base]**. Estos elementos permiten definir una convención de nombres e identificar la parte de la convención utilizada para asignar un nombre al conjunto en el que están contenidos. <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

La convención de nombres individual de una empresa a menudo utiliza una o más líneas de definición de cada uno de estos dos elementos. Puede utilizar tantas líneas para su definición única y agruparlas en elementos distintos, como Imagen principal, Elemento de color, Elemento de vista alternativa y Elemento de muestra.

Por ejemplo, la sintaxis de una expresión regular de coincidencia literal podría ser similar a la siguiente:

`(\w+)-\w+-\w+`

### Acerca del orden de secuencias

Si lo desea, puede definir el orden en que se muestran las imágenes después de agrupar el conjunto de imágenes o el conjunto de giros en [!DNL Dynamic Media]. De forma predeterminada, los recursos se ordenan alfanuméricamente. Sin embargo, puede utilizar una lista de expresiones regulares separadas por coma para definir el orden.

En cuanto a la automatización de la ordenación de secuencias, se especifican reglas para forzar la ordenación de los recursos de una determinada manera, si es necesario. Por ejemplo, supongamos que el primer recurso siempre se llama `_main` y desea que siga con `_alt1`, `_alt2`, `_alt3`, etc. En estos casos, puede crear una regla de orden de secuencia con la siguiente sintaxis:

`.*_main,.*_alt[0-9]`

Aunque es posible ordenar una secuencia a fuerza, lo mejor es utilizar la numeración alfanumérica para ordenar secuencias en la medida de lo posible. Además, puede utilizar el conjunto de imágenes o las herramientas del editor de conjuntos de giros en [!DNL Dynamic Media] para reorganizar el orden de secuencia de los recursos, o agregar y eliminar nuevos recursos en el conjunto mediante una operación de arrastrar y soltar.

Cuando termine de crear un ajuste preestablecido de conjunto de lotes, debe aplicarlo a una o varias carpetas que haya creado. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjuntos de lotes a las carpetas](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**Para crear un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros:**

1. Pulse el logotipo del Experience Manager y vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. En la página **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, cerca de la esquina superior derecha, pulse **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Crear ajuste preestablecido de conjunto de lotes]**, en el campo de texto **[!UICONTROL Nombre de ajuste preestablecido]**, introduzca un nombre descriptivo. El nombre del ajuste preestablecido no se puede editar si más adelante decide cambiarlo.

1. En la lista desplegable **[!UICONTROL Tipo de ajuste preestablecido]**, seleccione **[!UICONTROL Conjunto de imágenes]** o **[!UICONTROL Conjunto de giros]**. Asegúrese de elegir el tipo de ajuste preestablecido correcto; no se puede editar más tarde.
1. Toque **[!UICONTROL Crear]**.
1. A la derecha de la página **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]**, defina las opciones editables que desee en los encabezados **[!UICONTROL Detalles del ajuste preestablecido]** y **[!UICONTROL Convención de nomenclatura de conjuntos]**.
Para obtener más información sobre las opciones editables que están disponibles, consulte [Detalles de ajustes preestablecidos, Convenciones de nombres establecidos y Resultados de reglas: Opciones de RegX](#features-options-bsp).

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. Cree uno o más grupos de expresiones regulares.

   * A la izquierda de la página **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]**, en **[!UICONTROL Coincidencia]**, **[!UICONTROL Nombre base]** o **[!UICONTROL Orden de secuencia]**, pulse **[!UICONTROL Agregar grupo]**.
   * El campo **[!UICONTROL Match]** es obligatorio. **[!UICONTROL El]** nombre base es obligatorio solo si el campo  **** Coincidencia no especifica todavía un nombre base mediante una agrupación de corchetes. **[!UICONTROL El]** orden de secuencia es opcional.
   * Mediante las listas desplegables y los cuadros de texto del formulario del grupo, especifique un grupo de expresiones que desee utilizar para definir los criterios de nomenclatura para el conjunto de imágenes o los miembros del recurso de conjuntos de giros.
      * Al seleccionar y especificar expresiones para un grupo, observe que la sintaxis real de la expresión regular se refleja cerca de la parte inferior derecha de la página, en el encabezado **[!UICONTROL Resultados de regla - RegX]**. Para ver la cadena de expresión regular actualizada en la parte inferior derecha, pulse cualquier lugar fuera del área del formulario. Estas cadenas de expresión regular representan el patrón que desea que coincida en una búsqueda de [!DNL Dynamic Media] recursos para crear el conjunto de imágenes o el conjunto de giros.
      * Para eliminar un grupo que haya agregado, pulse **[!UICONTROL X]**.
   * Cuando agregue dos o más grupos, en la lista desplegable **[!UICONTROL And]**, seleccione **[!UICONTROL And]** para unir un grupo recién agregado con cualquier grupo de expresiones anterior que haya agregado. O bien, seleccione **[!UICONTROL Or]** para añadir una alternativa entre el grupo de expresiones anterior y el nuevo grupo que cree. El operando **[!UICONTROL Or]** se define mediante el uso de un carácter de línea vertical `|` en la propia sintaxis de la expresión regular.

1. Realice una de las acciones siguientes:

   * Para agregar otro grupo nuevo, en **[!UICONTROL Coincidencia]**, **[!UICONTROL Nombre base]** o **[!UICONTROL Orden de secuenciación]**, pulse **[!UICONTROL Agregar grupo]**. Cree otro grupo de expresiones regulares como en el paso anterior.
   * Revise la sintaxis de la expresión regular en el área **[!UICONTROL Resultados de regla - RegX]**. Si debe cambiar la sintaxis, realice las ediciones en el grupo correspondiente de la izquierda de la página.
   * Si ha terminado de crear grupos de expresiones, continúe con el siguiente paso.

1. En la esquina superior derecha de la página, toque **[!UICONTROL Guardar]**.

Ya está listo para aplicar el ajuste preestablecido de conjunto de lotes a una carpeta de recursos. A continuación, cargue los recursos en esa carpeta. Este flujo de trabajo genera automáticamente el conjunto de imágenes o el conjunto de giros. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjuntos de lotes a carpetas de recursos](#apply-bsp).

### Detalles de ajustes preestablecidos, Convención de asignación de nombres y Resultados de reglas: opciones de RegX {#features-options-bsp}

Estas opciones están disponibles en la página **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]** al crear o editar un ajuste preestablecido de conjunto de lotes.

Consulte [Creación de un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp) o [Edición de un ajuste preestablecido de conjunto de lotes](#edit-bsp).

| **[!UICONTROL Detalles del ajuste preestablecido]** | Descripción |
| --- | --- |
| Nombre de ajuste preestablecido  | Solo lectura. El nombre especificado al crear el conjunto de lotes por primera vez. Si debe cambiar el nombre del ajuste preestablecido, puede copiar el ajuste preestablecido de conjunto de lotes existente y especificar un nuevo nombre. Consulte [Copia de un ajuste preestablecido de conjunto de lotes existente](#copy-bsp). |
| Tipo | Solo lectura. El tipo se especificó la primera vez que creó el conjunto de lotes. La copia de un ajuste preestablecido de conjunto de lotes existente no permite cambiar su [!UICONTROL Tipo]; en su lugar, debe crear un ajuste preestablecido. |
| Incluir recursos derivados | Opcional. Para que el IPS de [!DNL Dynamic Media] (Image Production System) incluya imágenes generadas o &quot;derivadas&quot; con su conjunto de giros o conjunto de imágenes, seleccione **[!UICONTROL Yes]** (predeterminado). Un recurso derivado es una imagen que un usuario no ha cargado directamente. En su lugar, IPS produjo el recurso cuando se cargó un recurso maestro. Por ejemplo, un recurso de imagen que IPS generó a partir de una página en un PDF, en el momento en que el PDF se cargó en [!DNL Dynamic Media], se considera un recurso derivado. |
| Carpeta de destino | Opcional. Si define un gran número de conjuntos de imágenes o conjuntos de giros, Adobe recomienda mantener estos conjuntos separados de las carpetas que contienen los propios recursos. Como tal, considere la posibilidad de crear una carpeta Conjuntos de imágenes o Conjuntos de giros y redirija la aplicación para colocar conjuntos de lotes generados aquí.<br>En este caso, especifique qué carpeta dentro de la estructura de carpetas de recursos de Experience Manager (`/content/dam`) tiene activo el ajuste preestablecido de conjunto de lotes. Asegúrese de que la carpeta está habilitada para la sincronización [!DNL Dynamic Media] para permitirla como carpeta de destino. Consulte [Configuración de la publicación selectiva a nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>Si se aplica el ajuste preestablecido mediante las  **[!UICONTROL Propiedades]** de la carpeta, puede asignarse a más de una carpeta un conjunto de lotes determinado preestablecido. Consulte [Aplicación de ajustes preestablecidos de conjuntos de lotes desde la página Propiedades](#apply-bsp-to-folders-via-properties) de una carpeta de recursos.<br>Si no especifica ninguna carpeta, el conjunto de lotes preestablecido de conjunto de imágenes generado o el conjunto de giros se crea en la misma carpeta que la carpeta de recursos cargada en. |
| **[!UICONTROL Establezca la convención de asignación de nombres]** |  |
| Prefijo<br>o<br>Sufijo | Opcional. Introduzca un prefijo, un sufijo o ambos en los campos correspondientes.<br>Los campos prefijo y sufijo permiten crear muchos ajustes preestablecidos de conjuntos de lotes utilizando una convención de nombres de archivo personalizada y alternativa para un conjunto de contenido determinado. Este método es especialmente útil en casos en los que hay una excepción al esquema de nombres predeterminado definido por la empresa.<br>El prefijo o el sufijo se añaden al  **[!UICONTROL nombre]** base definido en el área  **[!UICONTROL Convenciones de nombres de]** recursos. Al agregar un prefijo o sufijo, se asegura de que el conjunto de imágenes o el conjunto de giros se creen de forma exclusiva e independiente de otros recursos. También puede servir para ayudar a otros a identificar tipos de archivos. Por ejemplo, para determinar un modo de color utilizado, puede agregar como prefijo o sufijo `rgb` o `cmyk`.<br>Aunque no es necesario especificar una convención de nombres de conjuntos para utilizar la funcionalidad preestablecida de conjuntos de lotes, se recomienda utilizar la convención de nombres de conjuntos. Esta práctica permite definir tantos elementos de la convención de nombres como desee agrupar en un conjunto para ayudar a optimizar la creación de conjuntos de lotes. |
| **[!UICONTROL Resultados de la regla - RegX]** |  |
| Convención de nomenclatura de recursos - Coincidencia | Solo lectura. Muestra la sintaxis de la expresión regular en función de las opciones de formulario de coincidencia que haya elegido o del código sin procesar que haya introducido. |
| Convención de nombres de recursos - Nombre base | Solo lectura. Muestra la sintaxis de la expresión regular en función de las opciones de formulario Nombre base que haya elegido o del código sin procesar que haya introducido. |
| Orden de secuencias: Coincidencia | Solo lectura. Muestra la sintaxis de la expresión regular en función de las opciones de formulario que haya elegido o el código sin procesar que haya introducido. |

## Acerca de la aplicación de ajustes preestablecidos de conjuntos de lotes a carpetas de recursos {#apply-bsp}

Cuando asigna ajustes preestablecidos de conjuntos de lotes a una o varias carpetas de recursos, las subcarpetas heredan automáticamente los ajustes preestablecidos de su carpeta principal.

Puede aplicar varios ajustes preestablecidos de conjuntos de lotes a una carpeta de recursos.

Las carpetas que tienen un ajuste preestablecido de lote asignado se indican en la interfaz de usuario con el nombre del ajuste preestablecido que aparece en la carpeta, en la vista **[!UICONTROL Card]**.

Para aplicar ajustes preestablecidos de conjuntos de lotes a carpetas de recursos, utilice uno de los dos métodos siguientes:

* [Aplicar ajustes preestablecidos de conjuntos de lotes a carpetas de recursos desde la página](#apply-bsp-to-folders-via-bsp-page)  Ajuste preestablecido de conjuntos de lotes: este método le ofrece la mayor flexibilidad. Puede aplicar uno o varios ajustes preestablecidos a una o varias carpetas.
* [Aplicar ajustes preestablecidos de conjuntos de lotes desde la página Propiedades de una carpeta de recursos](#apply-bsp-to-folders-via-properties) : este método permite aplicar uno o más ajustes preestablecidos de conjuntos de lotes a una única carpeta.

Como práctica recomendada, asegúrese de que las carpetas de recursos estén sincronizadas [!DNL Dynamic Media] y, a continuación, aplique los ajustes preestablecidos que desee.

Volver a procesar los recursos en una carpeta si se da alguna de las dos situaciones siguientes:

* Desea ejecutar un ajuste preestablecido de conjunto de lotes en una carpeta de recursos existente que ya tenga activos cargados en ella.
* Posteriormente, edita un ajuste preestablecido de conjunto de lotes existente que se aplicaba anteriormente a una carpeta de recursos.

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### Aplicación de ajustes preestablecidos de conjuntos de lotes a carpetas de recursos desde la página Ajustes preestablecidos de conjuntos de lotes {#apply-bsp-to-folders-via-bsp-page}

1. Pulse el logotipo del Experience Manager y vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.
1. En la página **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, active la casilla de verificación de cada ajuste preestablecido de conjunto de lotes que desee aplicar a las carpetas.
1. En la barra de herramientas, pulse **[!UICONTROL Aplicar ajuste preestablecido de lote a las carpetas]**.
1. En la página **[!UICONTROL Seleccionar carpetas]**, active la casilla de verificación de cada carpeta a la que desee aplicar los ajustes preestablecidos de conjuntos de lotes.
1. En la esquina superior derecha de la página **[!UICONTROL Seleccionar carpetas]**, pulse **[!UICONTROL Aplicar]**.

### Aplicación de ajustes preestablecidos de conjuntos de lotes desde la página Propiedades de una carpeta de recursos {#apply-bsp-to-folders-via-properties}

1. Pulse el logotipo del Experience Manager y vaya a **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Desplácese a la carpeta a la que desee aplicar uno o varios ajustes preestablecidos de conjuntos de lotes.
1. En la página, a la izquierda de la columna **[!UICONTROL Name]**, seleccione la casilla de verificación de una carpeta.
1. En la barra de herramientas, pulse **[!UICONTROL Propiedades]**.
1. En la página Propiedades de la carpeta, pulse la pestaña **[!UICONTROL Dynamic Media Processing]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. En **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, en el cuadro de lista desplegable **[!UICONTROL Nombre de ajuste preestablecido]**, seleccione el nombre de un ajuste preestablecido de conjunto de lotes que desea aplicar. La captura de pantalla anterior muestra dos ajustes preestablecidos de conjuntos de lotes seleccionados que se aplican a la carpeta de recursos.

   Si no existen nombres de ajustes preestablecidos de conjuntos de lotes en el cuadro de lista desplegable **[!UICONTROL Nombre de ajustes preestablecidos]**, significa que aún no se ha creado ningún ajuste preestablecido de conjuntos de lotes. Consulte [Creación de un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp).

   Para quitar un ajuste preestablecido de conjunto de lotes aplicado, pulse **[!UICONTROL X]** a la derecha del tipo preestablecido.

1. En la esquina superior derecha de la página, pulse **[!UICONTROL Guardar y cerrar]**.

## Edición de un ajuste preestablecido de conjunto de lotes {#edit-bsp}

Puede editar un ajuste preestablecido de conjunto de lotes existente que haya creado. Puede cambiar cualquiera de los grupos de expresiones creados para la convención de nombres de recursos o el orden de secuencia. Si es necesario, también puede actualizar la carpeta de destino y establecer las convenciones de nomenclatura.

Sin embargo, no se puede cambiar el nombre o tipo de ajuste preestablecido (conjunto de imágenes o conjunto de giros). Si es necesario cambiar el nombre de un ajuste preestablecido, copie el ajuste preestablecido existente y especifique un nuevo nombre. Consulte [Copia de un ajuste preestablecido de conjunto de lotes](#copy-bsp).

Si edita un ajuste preestablecido de conjunto de lotes que se haya aplicado anteriormente a una carpeta, el ajuste preestablecido de conjunto de lotes recién editado se aplicará únicamente a los nuevos recursos cargados en esa carpeta.

Si desea que el ajuste preestablecido recién editado se vuelva a aplicar a los recursos existentes en la carpeta, debe volver a procesar la carpeta. <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->De este modo, los recursos existentes ahora cumplirían los requisitos para formar parte de un conjunto de imágenes o un conjunto de giros y se añadirían. Además, los activos existentes que ya estaban incluidos en el conjunto de imágenes o el conjunto de giros (según el conjunto de lotes preestablecido utilizado) no se eliminan ni se muestran tal cual. En este escenario se supone que ya no cumplen los requisitos según el ajuste preestablecido recién editado.

**Para editar un ajuste preestablecido de conjunto de lotes:**

1. Pulse el logotipo del Experience Manager y vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.
1. En la página **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, compruebe el ajuste preestablecido de conjunto de lotes que desea cambiar.
1. En la barra de herramientas, pulse **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]**.
1. Edite el ajuste preestablecido según sea necesario.
1. En la esquina superior derecha de la página **[!UICONTROL Ajuste preestablecido de conjunto de lotes]**, pulse **[!UICONTROL Guardar]**.

## Copia de un ajuste preestablecido de conjunto de lotes existente {#copy-bsp}

Puede copiar un ajuste preestablecido de conjunto de lotes existente para evitar tener que volver a crear manualmente un ajuste preestablecido complejo, o si simplemente desea cambiar el nombre de un ajuste preestablecido. Sin embargo, no se puede cambiar el tipo de ajuste preestablecido utilizado (conjunto de imágenes o conjunto de giros).

Si copia un ajuste preestablecido existente al que hacen referencia las carpetas de recursos, estas carpetas no se verán afectadas.

**Para copiar un ajuste preestablecido de conjunto de lotes existente:**

1. Pulse el logotipo del Experience Manager y vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.
1. En la página **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, seleccione la casilla de verificación del ajuste preestablecido de conjunto de lotes que desea copiar.
1. En la barra de herramientas, pulse **[!UICONTROL Copiar]**.
1. En el cuadro de diálogo **[!UICONTROL Copiar ajuste preestablecido de conjunto de lotes]**, en el cuadro de texto **[!UICONTROL Título]**, escriba un nuevo nombre para el ajuste preestablecido.

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. Pulse **[!UICONTROL Copiar]**.

## Acerca de la eliminación de los ajustes preestablecidos de conjuntos de lotes de las carpetas {#remove-bsp-from-folder}

Al quitar los ajustes preestablecidos de conjuntos de lotes de las carpetas, los recursos nuevos que cargue en estas carpetas no tendrán el ajuste preestablecido de conjuntos de lotes aplicado. Los recursos existentes en la carpeta que ya se habían agregado al conjunto de imágenes o al conjunto de giros basado en el ajuste preestablecido de conjunto de lotes que se aplicó a la carpeta siguen mostrándose tal cual.

Si desea *eliminar* ajustes preestablecidos de carpetas, consulte [Eliminación de ajustes preestablecidos de conjuntos de lotes](#delete-bsp).

Existen dos métodos que puede utilizar para eliminar los ajustes preestablecidos de conjuntos de lotes de las carpetas.

* [Eliminación de los ajustes preestablecidos de conjuntos de lotes de las carpetas mediante la página Ajuste preestablecido de conjuntos de lotes](#remove-bsp-from-folders-via-bsp-page) : este método ofrece la mayor flexibilidad. Puede quitar uno o varios ajustes preestablecidos de una carpeta o carpetas únicas.
* [Eliminación de los ajustes preestablecidos de conjuntos de lotes de la página Propiedades de una carpeta](#remove-bsp-from-folders-via-properties) : este método permite eliminar uno o varios ajustes preestablecidos de conjuntos de lotes solo de una carpeta.

### Eliminación de los ajustes preestablecidos de conjuntos de lotes de las carpetas mediante la página Ajustes preestablecidos de conjuntos de lotes {#remove-bsp-from-folders-via-bsp-page}

1. Pulse el logotipo del Experience Manager y vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.
1. En la página **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, active la casilla de verificación de uno o varios ajustes preestablecidos de conjunto de lotes que desee eliminar de una o varias carpetas.
1. En la barra de herramientas, pulse **[!UICONTROL Quitar ajuste preestablecido de lote de las carpetas]**.

1. En la página **[!UICONTROL Seleccionar carpetas]**, seleccione una o varias carpetas en las que desee quitar los ajustes preestablecidos de conjuntos de lotes.
1. En la esquina superior derecha de la página **[!UICONTROL Seleccionar carpetas]**, pulse **[!UICONTROL Quitar]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. En el cuadro de diálogo **[!UICONTROL Quitar perfil]**, pulse **[!UICONTROL Quitar]**.

### Eliminación de los ajustes preestablecidos de conjuntos de lotes de la página Propiedades {#remove-bsp-from-folders-via-properties} de una carpeta

1. Pulse el logotipo del Experience Manager y vaya a **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Desplácese a la carpeta en la que desee eliminar uno o varios ajustes preestablecidos de conjuntos de lotes.
1. En la página, a la izquierda de la columna **[!UICONTROL Name]**, seleccione la casilla de verificación de una carpeta.
1. En la barra de herramientas, pulse **[!UICONTROL Propiedades]**.
1. En la página Propiedades de la carpeta, pulse **[!UICONTROL Procesamiento de Dynamic Media]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. En **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, pulse **[!UICONTROL X]** a la derecha del tipo de ajuste preestablecido.

1. En la esquina superior derecha de la página, pulse **[!UICONTROL Guardar y cerrar]**.

## Eliminación de ajustes preestablecidos de conjuntos de lotes {#delete-bsp}

Puede eliminar los ajustes preestablecidos de conjuntos de lotes para eliminarlos permanentemente de [!DNL Dynamic Media]. Es decir, ya no aparecen en la página [!UICONTROL Ajuste preestablecido de conjunto de lotes] ni en la lista desplegable **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]** de la pestaña **[!UICONTROL Procesamiento de Dynamic Media]** en la página **[!UICONTROL Propiedades]** de la carpeta. Como tal, el ajuste preestablecido no se aplica a los recursos existentes en un reprocesamiento de carpetas ni cuando se cargan nuevos recursos en la carpeta.

Si elimina un ajuste preestablecido que se haya aplicado anteriormente a una o varias carpetas, cualquier conjunto de imágenes o conjunto de giros que se hayan creado a partir de recursos de esas carpetas seguirá mostrándose tal cual.

Si desea *quitar los ajustes preestablecidos* de las carpetas, consulte [Eliminación de los ajustes preestablecidos de conjuntos de lotes de las carpetas](#remove-bsp-from-folder).

**Para eliminar los ajustes preestablecidos de conjuntos de lotes:**

1. Pulse el logotipo del Experience Manager y vaya a **[!UICONTROL Tools]** > **[!UICONTROL Assets]** > **[!UICONTROL Batch Set Presets]**.
1. En la página **[!UICONTROL Ajustes preestablecidos de conjunto de lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, active la casilla de verificación de uno o varios ajustes preestablecidos de conjunto de lotes que desee eliminar.
1. En la barra de herramientas, pulse **[!UICONTROL Eliminar ajustes preestablecidos de conjunto de lotes]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. En el cuadro de diálogo **[!UICONTROL Eliminar ajustes preestablecidos de conjunto de lotes]**, pulse **[!UICONTROL Eliminar]**.

   Si la carpeta de recursos hace referencia al ajuste preestablecido que está eliminando, pulse **[!UICONTROL Forzar eliminación]** en su lugar.

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [Conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md)
>* [Conjuntos de giros](/help/assets/dynamic-media/spin-sets.md)
>* [Configuración de una publicación selectiva a nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder) : consulte &quot;Modo de sincronización&quot; en el tema para obtener más información sobre la sincronización de una sola carpeta en  [!DNL Dynamic Media].
>* [Creación de una configuración de Dynamic Media en Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) : consulte &quot;Modo de sincronización de Dynamic Media&quot; en el tema para obtener más información sobre la sincronización de todas las carpetas en  [!DNL Dynamic Media].

