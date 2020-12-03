---
title: Valores preestablecidos de conjunto por lotes
description: Descubra cómo automatizar la creación de conjuntos de imágenes y conjuntos de giros mediante ajustes preestablecidos de conjuntos de lotes en Dynamic Media.
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: b10ad95e0e8b87eaaf6a0a99ce82d6b317660b12
workflow-type: tm+mt
source-wordcount: '3521'
ht-degree: 1%

---


# Acerca de los ajustes preestablecidos de conjunto por lotes {#about-bsp}

Utilice **[!UICONTROL Valores preestablecidos de conjunto por lotes]** para facilitar la creación y organización de varios recursos en un conjunto de imágenes o conjunto de giros en el momento de cargar los archivos de recursos en una carpeta, ya sea individualmente o mediante ingestión masiva. El ajuste preestablecido se puede ejecutar junto con los trabajos de importación de recursos programados en [!DNL Dynamic Media]. Cada ajuste preestablecido tiene un nombre exclusivo y un conjunto de instrucciones independiente que define cómo construir el conjunto de imágenes o el conjunto de giros con imágenes que coinciden con las convenciones de nombre definidas en la fórmula preestablecida.

>[!IMPORTANT]
>
>Si ha utilizado ajustes preestablecidos de conjunto de lotes en [!DNL Dynamic Media Classic] y está migrando de [!DNL Dynamic Media Classic] a Adobe Experience Manager como Cloud Service, deberá volver a crear manualmente las definiciones de los ajustes preestablecidos de conjunto de lotes en [!DNL Adobe Experience Manager as a Cloud Service].

**Práctica**  recomendada: al trabajar con ajustes preestablecidos de conjunto de lotes, Adobe recomienda el siguiente flujo de trabajo:

1. Cree un ajuste preestablecido de conjunto de lotes. Consulte [Creación de un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp).
1. Cree una nueva carpeta de recursos o utilice una carpeta de recursos existente y asegúrese de sincronizarla con [!DNL Dynamic Media]. Consulte [Creación de carpetas](/help/assets/manage-digital-assets.md#creating-folders).
1. Aplique el ajuste preestablecido de conjunto de lotes a la carpeta de recursos. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjunto de lotes a carpetas](#apply-bsp).
1. Cargue imágenes en la carpeta de recursos. Consulte [Carga de recursos para conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md#uploading-assets-in-image-sets), [Carga de recursos para conjuntos de giros](/help/assets/dynamic-media/spin-sets.md#uploading-assets-for-spin-sets) o [Añadir recursos digitales a Adobe Experience Manager](#add-assets-to-experience-manager).
1. Cree el conjunto de imágenes o giros. Consulte [Conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md) o [Conjuntos de giros](/help/assets/dynamic-media/spin-sets.md).
1. Publique el conjunto de imágenes o giros. Consulte [Publicación de recursos de medios dinámicos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

## Creación de un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros {#creating-bsp}

Para crear ajustes preestablecidos de conjunto por lotes, es aconsejable que esté familiarizado con las expresiones normales y que lo comprenda.

Lo ideal es que la compañía también tenga una convención de nombres definida para determinar cómo se deben agrupar los recursos en un conjunto.
Para ayudarle a comprender la importancia de utilizar una convención de nombres, supongamos que la convención de nombres definida por la compañía es `<style>-<color>-<view>`. Además, el nombre base del conjunto siempre debe ser `<style>-<color>` y la extensión del nombre del conjunto debe ser `-SET`. Si carga una imagen con el nombre `0123-RED-01`, se creará un conjunto con el nombre `0123-RED-SET`. Si posteriormente carga imágenes `0123-RED-03` y `0123-BLUE-01`, la imagen `RED-03` se agregará al conjunto en la segunda posición porque está ordenada por debajo de `01`. Sin embargo, la imagen `BLUE-01` formaría parte de un nuevo conjunto denominado `0123-BLUE-SET`. Para la siguiente carga de recursos, agregue archivos `0123-RED-02` y `0123-BLUE-02`. Cada recurso se agregaría a su conjunto respectivo. La imagen `RED-02` se ordenaría automáticamente entre las imágenes `01` y `03` existentes, debido al orden de clasificación.

La página **[!UICONTROL Valor preestablecido de conjunto por lotes]** de [!DNL Dynamic Media] permite crear, editar o eliminar ajustes preestablecidos de conjunto por lotes y aplicar o quitar ajustes preestablecidos de conjunto por lotes de carpetas de recursos. Puede utilizar las listas desplegables del campo de formulario para definir un ajuste preestablecido de conjunto de lotes o el campo **[!UICONTROL Código sin procesar]**, que le permite escribir la sintaxis de expresión normal.

Puede crear tantos ajustes preestablecidos de conjunto de lotes como sea necesario para cubrir todos los trabajos de ingesta de recursos que necesite.

**Acerca de la convención de nombres de recursos**

El área **[!UICONTROL Conjuntos de nombres de recursos]** de la página **[!UICONTROL Valores preestablecidos de conjuntos de lotes]** tiene dos elementos que puede utilizar para definir el valor preestablecido de conjunto de lotes: **[!UICONTROL Coincidencia]** y **[!UICONTROL Nombre base]**. Estos elementos le permiten definir una convención de nombre e identificar la parte de la convención utilizada para asignar un nombre al conjunto en el que están contenidos. <!-- While **[!UICONTROL Match]** is required, **[!UICONTROL Base Name]** is mandatory only if the **[!UICONTROL Match]** field does not already specify a base name through the use of a bracket grouping. -->

La convención de nombre individual de una compañía suele utilizar una o varias líneas de definición de cada uno de estos dos elementos. Puede utilizar tantas líneas como desee para su definición única y agruparlas en elementos distintos, como imagen principal, elemento de color, elemento de Vista alternativa y elemento de muestra.

Por ejemplo, la sintaxis de una expresión regular de coincidencia literal puede tener el siguiente aspecto:

`(\w+)-\w+-\w+`

**Acerca del orden de secuencia**

Opcionalmente, puede definir el orden en que se muestran las imágenes después de que el conjunto de imágenes o de giros se agrupe en [!DNL Dynamic Media]. De forma predeterminada, los recursos se ordenan de forma alfanumérica. Sin embargo, puede utilizar una lista separada por comas de expresiones regulares para definir el orden.

Con respecto a la automatización de pedidos de secuencia, se especifican reglas para forzar la ordenación de recursos de una determinada manera, si es necesario. Por ejemplo, supongamos que el primer recurso se denomina siempre `_main` y que desea que le siga `_alt1`, `_alt2`, `_alt3`, etc. En estos casos, puede crear una regla de orden de secuencia con la siguiente sintaxis:

`.*_main,.*_alt[0-9]`

Si bien es posible una secuencia de orden de fuerza, generalmente es mejor basarse en la numeración alfanumérica para el orden de secuencias, en la medida de lo posible. Además, puede utilizar el conjunto de imágenes o las herramientas del editor de conjuntos de giros de [!DNL Dynamic Media] para reorganizar fácilmente el orden de secuencia de los recursos, o bien, agregar y eliminar nuevos recursos del conjunto mediante una operación de arrastrar y soltar.

Cuando termine de crear un ajuste preestablecido de conjunto de lotes, se aplicará a una o varias carpetas que haya creado. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjunto de lotes a carpetas](#apply-bsp).

<!-- See also [Creating a batch set preset for the auto generation of a 2D Spin Set](application-setup.md#creating_a_batch_set_preset_for_the_auto_generation_of_a_2d_spin_set). -->

**Para crear un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros:**

1. Toque el logotipo de Adobe Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Valores preestablecidos de conjunto por lotes]**.

   ![bsp-create1.png](/help/assets/assets-dm/bsp-create1.png)

1. En la página **[!UICONTROL Valores preestablecidos de conjunto por lotes]**, cerca de la esquina superior derecha, toque **[!UICONTROL Crear]**.
1. En el cuadro de diálogo **[!UICONTROL Crear ajuste preestablecido de conjunto de lotes]**, en el campo de texto **[!UICONTROL Nombre de ajuste preestablecido]**, introduzca un nombre descriptivo. Tenga en cuenta que el nombre del ajuste preestablecido no se puede editar si posteriormente decide cambiarlo.

1. En la lista desplegable **[!UICONTROL Tipo de ajuste preestablecido]**, seleccione **[!UICONTROL Conjunto de imágenes]** o **[!UICONTROL Conjunto de giros]**. Asegúrese de elegir el tipo de ajuste preestablecido correcto; no se puede editar más tarde.
1. Toque **[!UICONTROL Crear]**.
1. En la parte derecha de la página **[!UICONTROL Editar ajuste preestablecido de conjunto de lotes]**, establezca las opciones editables que desee en los encabezados **[!UICONTROL Detalles de ajustes preestablecidos]** y **[!UICONTROL Definir convención de nombres]**.
Consulte [Detalles de ajustes preestablecidos, Definir convención de nombres y Resultados de reglas: opciones de RegX](#features-options-bsp) para obtener más información sobre las opciones editables que tiene a su disposición.

   ![bsp-create4.png](/help/assets/assets-dm/bsp-create4.png)

1. Cree uno o varios grupos de expresiones normales.

   * En la parte izquierda de la página **[!UICONTROL Editar ajuste preestablecido de conjunto por lotes]**, en **[!UICONTROL Coincidencia]**, **[!UICONTROL Nombre base]** o **[!UICONTROL Orden de secuencia]**, toque **[!UICONTROL Añadir grupo]**.
   * Se requiere el campo **[!UICONTROL Coincidencia]**. **[!UICONTROL El]** nombre base es obligatorio solo si el campo  **** Coincidencia no especifica ya un nombre base mediante el uso de una agrupación de corchetes. **[!UICONTROL El]** pedido de secuencia es opcional.
   * Mediante las listas desplegables y los cuadros de texto del formulario del grupo, especifique un grupo de expresiones que desee utilizar para definir los criterios de nomenclatura para el conjunto de imágenes o los miembros del recurso del conjunto de giros.
      * Al seleccionar y especificar expresiones para un grupo, observará que la sintaxis de la expresión regular real se refleja cerca del lado inferior derecho de la página, bajo el encabezado **[!UICONTROL Resultados de la regla - RegX]** (es posible que tenga que tocar en cualquier parte fuera del área del formulario para ver la cadena de expresión normal actualizada en la parte inferior derecha). Estas cadenas de expresión normales representan el patrón que desea que coincida en una búsqueda de [!DNL Dynamic Media] recursos para crear el conjunto de imágenes o de giros.
      * Para eliminar un grupo que haya agregado, toque **[!UICONTROL X]**.
   * Cuando agregue dos o más grupos, en la lista desplegable **[!UICONTROL And]**, seleccione **[!UICONTROL And]** para unir un grupo recién agregado con cualquier grupo de expresiones anterior que haya agregado. O bien, seleccione **[!UICONTROL O]** para agregar una alternancia entre el grupo de expresiones anterior y el nuevo grupo que cree. El operando **[!UICONTROL O]** se define mediante el uso de un carácter de línea vertical `|` en la propia sintaxis de expresión normal.

1. Realice una de las acciones siguientes:

   * Para agregar otro nuevo grupo, en **[!UICONTROL Coincidencia]**, **[!UICONTROL Nombre base]** o **[!UICONTROL Orden de secuencia]**, toque **[!UICONTROL Añadir grupo]**. Cree otro grupo de expresiones normal como lo hizo en el paso anterior.
   * Revise la sintaxis de expresión regular en el área **[!UICONTROL Resultados de regla - RegX]**. Si necesita realizar cambios en la sintaxis, realice los cambios en el grupo correspondiente en el lado izquierdo de la página.
   * Si ha terminado de crear grupos de expresiones, continúe con el paso siguiente.

1. En la esquina superior derecha de la página, toque **[!UICONTROL Guardar]**.

Ahora puede leer para aplicar el ajuste preestablecido de conjunto de lotes a una o varias carpetas de recursos, cargar recursos en la carpeta y, a continuación, crear el conjunto de imágenes o el conjunto de giros. Consulte [Acerca de la aplicación de ajustes preestablecidos de conjunto de lotes a carpetas](#apply-bsp).

### Detalles de ajustes preestablecidos, Definir convención de nombres y Resultados de reglas: opciones de RegX {#features-options-bsp}

Estas opciones están disponibles en la página **[!UICONTROL Editar ajuste preestablecido de conjunto por lotes]** al crear o editar un ajuste preestablecido de conjunto de lotes.

Consulte [Creación de un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp) o [Edición de un ajuste preestablecido de conjunto de lotes](#edit-bsp).

| **[!UICONTROL Detalles del ajuste preestablecido]** | Descripción |
| --- | --- |
| Nombre de ajuste preestablecido  | Solo lectura. El nombre especificado al crear el conjunto de lotes por primera vez. Si necesita cambiar el nombre del ajuste preestablecido, puede copiar el ajuste preestablecido de conjunto de lotes existente y especificar un nuevo nombre. Consulte [Copia de un ajuste preestablecido de conjunto de lotes existente](#copy-bsp). |
| Tipo | Solo lectura. El tipo se especificó la primera vez que creó el conjunto de lotes. La copia de un ajuste preestablecido de conjunto de lotes existente no permite cambiar su [!UICONTROL Tipo]; debe crear un nuevo ajuste preestablecido. |
| Incluir recursos derivados | Opcional. Seleccione **[!UICONTROL Sí]** (predeterminado) para que el IPS de [!DNL Dynamic Media] (Image Production System) incluya imágenes generadas o &quot;derivadas&quot; con el conjunto de giros o el conjunto de imágenes. Un recurso derivado es una imagen que un usuario no ha cargado directamente. En su lugar, IPS produjo el recurso cuando se cargó un recurso principal. Por ejemplo, un recurso de imagen que IPS generó a partir de una página en un PDF, en el momento en que se cargó el PDF en [!DNL Dynamic Media], se considera un recurso derivado. |
| Carpeta de destino | Opcional.  Si define un gran número de conjuntos de imágenes o conjuntos de giros, es posible que prefiera mantener estos conjuntos separados de las carpetas que contienen los propios recursos. Como tal, es posible que desee considerar la posibilidad de crear una carpeta Conjuntos de imágenes o Conjuntos de giros y redirigir la aplicación para colocar aquí los conjuntos de lotes generados.<br>En ese caso, especifique qué carpeta de la estructura de carpetas (`/content/dam`) de Adobe Experience Manager Assets debe tener activo el ajuste preestablecido de conjunto de lotes. Asegúrese de que la carpeta está habilitada para la sincronización [!DNL Dynamic Media] para permitirla como carpeta de destino. Consulte [Configuración de la publicación selectiva a nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder).<br>Tenga en cuenta que más de una carpeta puede tener asignado un ajuste preestablecido de conjunto de lotes determinado, si aplica el ajuste preestablecido mediante las  **[!UICONTROL Propiedades]** de la carpeta. Consulte [Aplicación de ajustes preestablecidos de conjunto de lotes desde la página Propiedades de una carpeta de recursos](#apply-bsp-to-folders-via-properties).<br>Si no especifica una carpeta, el ajuste preestablecido de conjunto de lotes se crea en la misma carpeta que la carpeta de carga de recursos. |
| **[!UICONTROL Establezca la convención de asignación de nombres]** |  |
| Prefijo<br>o<br>Sufijo | Opcional. Introduzca un prefijo, un sufijo o ambos en los campos correspondientes.<br>Los campos de prefijo y sufijo permiten crear tantos ajustes preestablecidos de conjunto de lotes mediante una convención de nombre de archivo personalizada alternativa que puede ser necesaria para un conjunto de contenido determinado. Este método resulta especialmente útil en casos en los que existe una excepción al esquema de nombres predeterminado definido por una compañía.<br>El prefijo o sufijo se agrega al nombre  **[!UICONTROL base que]** defina en el área de  **[!UICONTROL convención de nombres de]** recursos. Al agregar un prefijo o sufijo, se asegura de que el conjunto de imágenes o de giros se cree de forma exclusiva e independiente de otros recursos. También puede servir para ayudar a otros usuarios a identificar los tipos de archivos. Por ejemplo, para determinar un modo de color utilizado, puede agregar como prefijo o sufijo `rgb` o `cmyk`.<br>Aunque no es necesario especificar una convención de nombre de conjunto para utilizar la funcionalidad de ajuste preestablecido de conjunto de lotes, la práctica recomendada es utilizar la convención de nombre de conjunto para definir tantos elementos de la convención de nombre que desee agrupar en un conjunto para ayudar a agilizar la creación de conjuntos de lotes. |
| **[!UICONTROL Resultados de la regla - RegX]** |  |
| Convención de nombres de recursos: coincidencia | Solo lectura. Muestra la sintaxis de expresión normal en función de las opciones de formulario de coincidencia que haya seleccionado o del código sin procesar que haya introducido. |
| Convención de nombres de recursos - Nombre base | Solo lectura. Muestra la sintaxis de la expresión normal en función de las opciones de formulario Nombre base que haya elegido o del código sin procesar que haya introducido. |
| Orden de secuencia: Coincidencia | Solo lectura. Muestra la sintaxis de la expresión normal en función de las opciones de formulario elegidas o del código sin procesar introducido. |

## Acerca de la aplicación de ajustes preestablecidos de conjunto de lotes a carpetas {#apply-bsp}

Cuando se asignan ajustes preestablecidos de conjunto de lotes a una o varias carpetas, las subcarpetas heredan automáticamente los ajustes preestablecidos de su carpeta principal.

Puede aplicar varios valores preestablecidos de conjunto de lotes a una carpeta.

Las carpetas que tienen un ajuste preestablecido de lote asignado se indican en la interfaz de usuario por el nombre del ajuste preestablecido que aparece en la carpeta, en la vista **[!UICONTROL Card]**.

Utilice uno de los dos métodos siguientes para aplicar ajustes preestablecidos de conjunto de lotes a las carpetas:

* [Aplique ajustes preestablecidos de conjunto de lotes a las carpetas de recursos desde la página](#apply-bsp-to-folders-via-bsp-page)  Valores preestablecidos de conjunto de lotes: este método le oferta la mayor flexibilidad. Puede aplicar uno o varios ajustes preestablecidos a una o varias carpetas.
* [Aplicar ajustes preestablecidos de conjunto de lotes desde la página](#apply-bsp-to-folders-via-properties)  Propiedades de una carpeta de recursos: Este método permite aplicar uno o varios ajustes preestablecidos de conjunto de lotes a una sola carpeta.

La práctica recomendada es asegurarse de que las carpetas de recursos se sincronizan [!DNL Dynamic Media] y, a continuación, aplicar los ajustes preestablecidos que desee.

Es posible que sea necesario volver a procesar los recursos de una carpeta si se da alguna de las dos situaciones siguientes:

* Desea ejecutar un ajuste preestablecido de conjunto de lotes en una carpeta de recursos existente que ya tenga recursos cargados en ella.
* Posteriormente editará un ajuste preestablecido de conjunto de lotes existente que se aplicó anteriormente a una carpeta de recursos.

<!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). -->

### Aplicación de ajustes preestablecidos de conjunto de lotes a carpetas de recursos desde la página Valores preestablecidos de conjunto de lotes {#apply-bsp-to-folders-via-bsp-page}

1. Toque el logotipo de Adobe Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Valores preestablecidos de conjunto por lotes]**.
1. En la página **[!UICONTROL Valores preestablecidos de conjunto por lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, active la casilla de verificación de cada ajuste preestablecido de conjunto de lotes que desee aplicar a las carpetas.
1. En la barra de herramientas, toque **[!UICONTROL Aplicar ajuste preestablecido de lote a carpetas]**.
1. En la página **[!UICONTROL Seleccionar carpetas]**, active la casilla de verificación de cada carpeta a la que desee aplicar los ajustes preestablecidos de conjunto de lotes.
1. En la esquina superior derecha de la página **[!UICONTROL Seleccionar carpetas]**, toque **[!UICONTROL Aplicar]**.

### Aplicación de ajustes preestablecidos de conjunto de lotes desde la página Propiedades de una carpeta de recursos {#apply-bsp-to-folders-via-properties}

1. Toque el logotipo de Adobe Experience Manager y vaya a **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Vaya a la carpeta a la que desee aplicar uno o varios valores preestablecidos de conjunto de lotes.
1. En la página, a la izquierda de la columna **[!UICONTROL Nombre]**, seleccione la casilla de verificación de la.
1. En la barra de herramientas, toque **[!UICONTROL Propiedades]**.
1. En la página Propiedades de la carpeta, toque la ficha **[!UICONTROL Procesamiento de medios dinámicos]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-apply-via-properties2a.png)

1. En **[!UICONTROL Valores preestablecidos de conjunto por lotes]**, en el cuadro de lista desplegable **[!UICONTROL Nombre de ajuste preestablecido]**, seleccione el nombre de un ajuste preestablecido de conjunto de lotes que desee aplicar. La captura de pantalla de arriba muestra que se han aplicado dos ajustes preestablecidos de conjunto de lotes a la carpeta.

   Si no hay nombres de ajustes preestablecidos de conjunto de lotes en el cuadro de lista desplegable **[!UICONTROL Nombre de ajuste preestablecido]**, significa que aún no ha creado ningún ajuste preestablecido de conjunto de lotes. Consulte [Creación de un ajuste preestablecido de conjunto de lotes para un conjunto de imágenes o un conjunto de giros](#creating-bsp).

   Para quitar un ajuste preestablecido de conjunto de lotes aplicado, toque **[!UICONTROL X]** a la derecha del tipo de ajuste preestablecido.

1. En la esquina superior derecha de la página, toque **[!UICONTROL Guardar y cerrar]**.

## Edición de un ajuste preestablecido de conjunto de lotes {#edit-bsp}

Puede editar un ajuste preestablecido de conjunto de lotes existente que haya creado. Puede cambiar cualquiera de los grupos de expresiones creados para la convención de nombres de recursos o el orden de secuencias. Si es necesario, también puede actualizar la carpeta de destino y establecer las convenciones de nomenclatura.

Sin embargo, no puede cambiar el nombre o el tipo de ajuste preestablecido (Conjunto de imágenes o Conjunto de giros). Si es necesario cambiar el nombre de un ajuste preestablecido, puede simplemente copiar el ajuste preestablecido existente y especificar un nuevo nombre. Consulte [Copia de un ajuste preestablecido de conjunto de lotes](#copy-bsp).

Si edita un ajuste preestablecido de conjunto de lotes que se haya aplicado anteriormente a una carpeta, el ajuste preestablecido recién editado se aplicará solo a los recursos nuevos que se carguen en la carpeta.

Si desea que el ajuste preestablecido recién editado se vuelva a aplicar a los recursos existentes en la carpeta, debe volver a procesar la carpeta. <!-- See [Reprocessing assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). --> De este modo, los recursos existentes ahora podrían formar parte de un conjunto de imágenes o de giros y añadirse. Además, los recursos existentes que ya estaban incluidos en el conjunto de imágenes o el conjunto de giros, según el ajuste preestablecido de conjunto de lotes anterior utilizado, no se eliminan (suponiendo que ya no cumplen los requisitos según el ajuste preestablecido recientemente editado) y se mostrarán tal cual.

**Para editar un ajuste preestablecido de conjunto de lotes:**

1. Toque el logotipo de Adobe Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Valores preestablecidos de conjunto por lotes.]**
1. En la página **[!UICONTROL Valores preestablecidos de conjunto por lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, compruebe el valor preestablecido de conjunto de lotes que desea cambiar.
1. En la barra de herramientas, toque **[!UICONTROL Editar ajuste preestablecido de conjunto por lotes.]**
1. Edite el ajuste preestablecido según sea necesario.
1. En la esquina superior derecha de la página **[!UICONTROL Valor preestablecido de conjunto de lotes]**, toque **[!UICONTROL Guardar.]**

## Copia de un ajuste preestablecido de conjunto de lotes existente {#copy-bsp}

Puede copiar un ajuste preestablecido de conjunto de lotes existente para evitar tener que volver a crear manualmente un ajuste preestablecido complejo o simplemente cambiar el nombre de un ajuste preestablecido. Sin embargo, no se puede cambiar el tipo de ajuste preestablecido utilizado (Conjunto de imágenes o Conjunto de giros).

Si copia un ajuste preestablecido existente al que hacen referencia las carpetas de recursos, estas carpetas no se verán afectadas.

**Para copiar un ajuste preestablecido de conjunto de lotes existente:**

1. Toque el logotipo de Adobe Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Valores preestablecidos de conjunto por lotes.]**
1. En la página **[!UICONTROL Valores preestablecidos de conjunto por lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, active la casilla de verificación del ajuste preestablecido de conjunto de lotes que desee copiar.
1. En la barra de herramientas, toque **[!UICONTROL Copiar]**.
1. En el cuadro de diálogo **[!UICONTROL Copiar ajuste preestablecido de conjunto de lotes]**, en el cuadro de texto **[!UICONTROL Título]**, escriba un nuevo nombre para el ajuste preestablecido.

   ![bsp-copy2.png](/help/assets/assets-dm/bsp-copy2.png)

1. Pulse **[!UICONTROL Copiar]**.

## Acerca de la eliminación de ajustes preestablecidos de conjunto de lotes de carpetas {#remove-bsp-from-folder}

Al eliminar los ajustes preestablecidos de conjunto de lotes de las carpetas, los recursos nuevos que cargue en estas carpetas no tendrán el ajuste preestablecido de conjunto de lotes aplicado a ellos. Los recursos existentes en la carpeta que ya se han agregado al conjunto de imágenes o al conjunto de giros, según el ajuste preestablecido de conjunto de lotes aplicado a la carpeta, seguirán mostrándose tal cual.

Si desea *eliminar* ajustes preestablecidos de carpetas, consulte [Eliminación de ajustes preestablecidos de conjunto de lotes](#delete-bsp).

Existen dos métodos que puede utilizar para quitar los ajustes preestablecidos de conjunto de lotes de las carpetas.

* [Eliminación de ajustes preestablecidos de conjunto de lotes de las carpetas mediante la página](#remove-bsp-from-folders-via-bsp-page)  Valores preestablecidos de conjunto por lotes: este método le oferta la mayor flexibilidad. Puede quitar uno o varios ajustes preestablecidos de una o varias carpetas.
* [Eliminación de ajustes preestablecidos de conjunto de lotes de la página](#remove-bsp-from-folders-via-properties)  Propiedades de una carpeta: Este método permite quitar uno o varios ajustes preestablecidos de conjunto de lotes de una sola carpeta.

### Eliminación de ajustes preestablecidos de conjunto de lotes de carpetas mediante la página Valores preestablecidos de conjunto de lotes {#remove-bsp-from-folders-via-bsp-page}

1. Toque el logotipo de Adobe Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Valores preestablecidos de conjunto por lotes]**.
1. En la página **[!UICONTROL Valores preestablecidos de conjunto por lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, active la casilla de verificación de uno o varios valores preestablecidos de conjunto de lotes que desee eliminar de una o varias carpetas.
1. En la barra de herramientas, toque **[!UICONTROL Quitar ajuste preestablecido de lote de carpetas]**.

1. En la página **[!UICONTROL Seleccionar carpetas]**, seleccione una o varias carpetas en las que desee eliminar los ajustes preestablecidos de conjunto de lotes. La captura de pantalla de arriba muestra una carpeta seleccionada con los nombres de dos ajustes preestablecidos de conjunto de lotes ya aplicados que se eliminarán.
1. En la esquina superior derecha de la página **[!UICONTROL Seleccionar carpetas]**, toque **[!UICONTROL Eliminar]**.

   ![bsp-remove-from-folders3.png](/help/assets/assets-dm/bsp-remove-from-folders3.png)

1. En el cuadro de diálogo **[!UICONTROL Eliminar perfil]**, toque **[!UICONTROL Eliminar]**.

### Eliminación de ajustes preestablecidos de conjunto de lotes de la página Propiedades de una carpeta {#remove-bsp-from-folders-via-properties}

1. Toque el logotipo de Adobe Experience Manager y vaya a **[!UICONTROL Assets]** > **[!UICONTROL Files]**.
1. Vaya a la carpeta en la que desee quitar uno o varios valores preestablecidos de conjunto de lotes.
1. En la página, a la izquierda de la columna **[!UICONTROL Nombre]**, active la casilla de verificación de una carpeta.
1. En la barra de herramientas, toque **[!UICONTROL Propiedades]**.
1. En la página Propiedades de la carpeta, toque **[!UICONTROL Procesamiento de medios dinámicos]**.

   ![bsp-apply-via-properties2.png](/help/assets/assets-dm/bsp-remove-via-properties2.png)

1. En **[!UICONTROL Valores preestablecidos de conjunto por lotes]**, toque **[!UICONTROL X]** a la derecha del tipo de ajuste preestablecido.

1. En la esquina superior derecha de la página, toque **[!UICONTROL Guardar y cerrar]**.

## Eliminando ajustes preestablecidos de conjunto de lotes {#delete-bsp}

Puede eliminar los ajustes preestablecidos de conjunto de lotes para quitarlos de forma permanente de [!DNL Dynamic Media]. Es decir, ya no se mostrarán en la página [!UICONTROL Valor preestablecido de conjunto por lotes] ni se mostrarán en la lista desplegable **[!UICONTROL Valores preestablecidos de conjunto por lotes]** de la ficha **[!UICONTROL Procesamiento de medios dinámicos]** de la página **[!UICONTROL Propiedades]** de la carpeta. Como tal, el ajuste preestablecido no se aplicará a los recursos existentes en un proceso de reprocesamiento de carpetas ni cuando se carguen nuevos recursos en la carpeta.

Si elimina un ajuste preestablecido aplicado anteriormente a una o varias carpetas, los conjuntos de imágenes o conjuntos de giros creados a partir de recursos de esas carpetas seguirán mostrándose tal cual.

Si sólo desea *quitar* ajustes preestablecidos de carpetas, consulte [Eliminación de ajustes preestablecidos de conjunto de lotes de carpetas](#remove-bsp-from-folder).

**Para eliminar ajustes preestablecidos de conjunto de lotes:**

1. Toque el logotipo de Adobe Experience Manager y vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Recursos]** > **[!UICONTROL Valores preestablecidos de conjunto por lotes]**.
1. En la página **[!UICONTROL Valores preestablecidos de conjunto por lotes]**, a la izquierda de la columna **[!UICONTROL Nombre de ajuste preestablecido]**, active la casilla de verificación de uno o varios valores preestablecidos de conjunto por lotes que desee eliminar.
1. En la barra de herramientas, toque **[!UICONTROL Eliminar valores preestablecidos de conjunto por lotes]**.

   ![bsp-delete2.png](/help/assets/assets-dm/bsp-delete2.png)

1. En el cuadro de diálogo **[!UICONTROL Eliminar ajustes preestablecidos de conjunto por lotes]**, toque **[!UICONTROL Eliminar]**.

   Si la carpeta de recursos hace referencia al ajuste preestablecido que está eliminando, es posible que tenga que tocar **[!UICONTROL Forzar eliminación]** en su lugar.

   ![bsp-delete3.png](/help/assets/assets-dm/bsp-delete3.png)

>[!MORELIKETHIS]
>
>* [Conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md)
>* [Conjuntos de giros](/help/assets/dynamic-media/spin-sets.md)
>* [Configuración de la publicación selectiva a nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md#selective-publish-configure-folder) : consulte &quot;Modo de sincronización&quot; en el tema para obtener más información sobre la sincronización de una sola carpeta a  [!DNL Dynamic Media].
>* [Creación de una nueva configuración de Dynamic Media en Cloud Services](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) : consulte &quot;Modo de sincronización de Dynamic Media&quot; en el tema para obtener más información sobre la sincronización de todas las carpetas en  [!DNL Dynamic Media].