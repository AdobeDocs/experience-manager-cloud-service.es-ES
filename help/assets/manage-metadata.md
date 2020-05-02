---
title: Administre metadatos de sus recursos digitales en [!DNL Adobe Experience Manager].
description: Obtenga información sobre los tipos de metadatos y cómo [!DNL Adobe Experience Manager Assets] ayuda a administrar los metadatos de los recursos para facilitar la categorización y organización de los recursos. [!DNL Experience Manager] permite organizar y procesar automáticamente recursos en función de sus metadatos.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 07ebe0588944fff40157119e658aca00eaed6ec3

---


# Gestión de metadatos de los recursos digitales {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] guarda los metadatos de cada recurso. Esto permite una clasificación y organización más sencillas de los recursos y ayuda a las personas que buscan un recurso específico. Con la capacidad de extraer metadatos de los archivos cargados en [!DNL Experience Manager Assets], la administración de metadatos se integra con el flujo de trabajo creativo. Gracias a la capacidad de mantener y gestionar metadatos con sus recursos, [!DNL Experience Manager Assets] es posible organizar y procesar automáticamente recursos en función de sus metadatos.

>[!MORELIKETHIS]
>
>* [Metadatos XMP](xmp-metadata.md)
>* [Cómo editar o agregar metadatos](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## Por qué los metadatos {#why-metadata}

Metadatos significa datos sobre los datos. A este respecto, los datos hacen referencia a su recurso digital, por ejemplo una imagen. Los metadatos son fundamentales para una administración eficaz de los recursos.

Los metadatos son la recopilación de todos los datos disponibles para un recurso, pero no necesariamente están contenidos en esa imagen. Algunos ejemplos de metadatos son:

* Nombre del recurso.
* Hora y fecha de la última modificación.
* Tamaño del recurso tal como se almacenó en el repositorio.
* Nombre de la carpeta en la que está contenido.
* Recursos relacionados o etiquetas aplicadas.

Estas son las propiedades básicas de metadatos que [!DNL Experience Manager] pueden administrarse para los recursos, lo que permite a los usuarios ver todos los recursos, por ejemplo, ordenados en la fecha de la última modificación; esto resulta útil cuando se intenta descubrir qué recursos se han agregado recientemente al repositorio.

Puede agregar más datos de alto nivel a recursos digitales, por ejemplo:

* Tipo de recurso (¿es una imagen, un vídeo, un clip de audio o un documento?).
* Propietario del recurso.
* Título del recurso.
* Descripción del recurso.
* Etiquetas asignadas a un recurso.

Más metadatos le ayudan a categorizar los recursos y resulta útil a medida que crece la cantidad de información digital. Es posible administrar unos cientos de archivos basándose únicamente en los nombres de archivo. Sin embargo, este enfoque no es escalable y se queda corto rápidamente cuando aumenta el número de personas involucradas y el número de activos administrados.

Con la adición de metadatos, el valor de un recurso digital aumenta, ya que el recurso se convierte en

* Más accesible: los sistemas y usuarios pueden encontrarlo fácilmente.
* Más fácil de administrar: puede encontrar recursos con el mismo conjunto de propiedades más fácilmente y aplicarles cambios.
* Más completo: cuantos más metadatos haya agregado a un recurso, más información y contexto tendrá.

Por estas razones, [!DNL Assets] le proporciona los medios adecuados para crear, administrar e intercambiar metadatos para sus recursos digitales.

## Tipos de metadatos {#types-of-metadata}

Los dos tipos básicos de metadatos son los metadatos técnicos y los descriptivos.

Los metadatos técnicos son útiles para las aplicaciones de software que se ocupan de activos digitales y no deben mantenerse manualmente. [!DNL Experience Manager Assets] y otro software determina automáticamente los metadatos técnicos y los metadatos pueden cambiar cuando se modifica el recurso. Los metadatos técnicos disponibles de un recurso dependen en gran medida del tipo de archivo del recurso. Algunos ejemplos de metadatos técnicos son:

* Tamaño de un archivo.
* Dimensiones (altura y anchura) de una imagen.
* Velocidad de bits de un archivo de audio o vídeo.
* Resolución (nivel de detalle) de una imagen.

Los metadatos descriptivos son metadatos relacionados con el dominio de la aplicación, por ejemplo, el negocio del que proviene un recurso. Los metadatos descriptivos no se pueden determinar automáticamente. Se crea de forma manual o semiautomática. Por ejemplo, una cámara con GPS puede rastrear automáticamente la latitud y la longitud y añadir la etiqueta geográfica de la imagen.

Debido al elevado costo del trabajo manual necesario para crear información descriptiva sobre metadatos, se han establecido normas para facilitar el intercambio de metadatos entre los sistemas y organizaciones de programas informáticos.

[!DNL Experience Manager Assets] admite todas las normas pertinentes para la gestión de metadatos.

Debido a la importancia de los metadatos y a la gran participación manual necesaria para crear metadatos, se han establecido normas que facilitan el intercambio.

## Normas de codificación {#encoding-standards}

Existen varias formas de incrustar metadatos en los archivos. Se admite una selección de estándares de codificación:

* XMP: utilizado por [!DNL Assets] para almacenar los metadatos extraídos en el repositorio.
* ID3: para archivos de audio y vídeo.
* Exif: para archivos de imagen.
* Otro/Heredado: desde [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], etc.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) es un estándar abierto que se utiliza [!DNL Experience Manager Assets] para toda la administración de metadatos. El estándar oferta la codificación de metadatos universales que puede incrustarse en todos los formatos de archivo. Adobe y otras compañías admiten el estándar XMP, ya que proporciona un modelo de contenido enriquecido. Los usuarios del estándar XMP y de [!DNL Experience Manager Assets] tienen una poderosa plataforma sobre la que construir. For more information, see [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Los datos almacenados en estas etiquetas ID3 se muestran cuando se reproduce un archivo de audio digital en el equipo o en un reproductor portátil MP3.

Las etiquetas ID3 están diseñadas para el formato de archivo MP3. Información adicional sobre los formatos:

* Las etiquetas ID3 funcionan en archivos MP3 y mp3PRO.
* WAV no tiene etiquetas.
* WMA tiene etiquetas de propiedad que no permiten la implementación de código abierto.
* Ogg Vorbis utiliza Comentarios Xiph incrustados en el contenedor Ogg.
* AAC utiliza un formato de etiquetado propio.

### Exif {#exif}

El formato de archivo de imagen intercambiable (Exif) es el formato de metadatos más utilizado en la fotografía digital. Proporciona una forma de incrustar un vocabulario fijo de propiedades de metadatos en muchos formatos de archivo, como JPEG, TIFF, RIFF y WAV. Exif almacena los metadatos como pares de un nombre de metadatos y un valor de metadatos. Estos pares de metadatos nombre-valor-valor también se denominan etiquetas, por lo que no deben confundirse con el etiquetado de [!DNL Experience Manager]. Como Exif se crea automáticamente mediante cámaras digitales modernas y se admite a través de software de gráficos modernos, puede considerarse el denominador común más bajo para la gestión de metadatos.

Una limitación importante de Exif es que algunos formatos de archivo de imagen populares como BMP, GIF o PNG no lo admiten.

Los campos de metadatos definidos normalmente por Exif son de naturaleza técnica y tienen un uso limitado para la administración descriptiva de metadatos. Por este motivo, [!DNL Experience Manager Assets] oferta la asignación de propiedades Exif en esquemas [de metadatos](metadata-schemas.md) comunes y en XMP.

#### Otros metadatos {#other-metadata}

Otros metadatos que se pueden incrustar desde archivos son Microsoft Word, PowerPoint, Excel, etc.

## Gestión de metadatos de los recursos digitales {#manage-assets-metadata}

Recursos de Enterprise Manager le permite editar los metadatos de varios recursos simultáneamente para que pueda propagar rápidamente cambios comunes de metadatos a los recursos de forma masiva. Utilice la página [!UICONTROL Propiedades] para cambiar las propiedades de metadatos a un valor común o para agregar o modificar etiquetas. Para personalizar la página Propiedades de metadatos, incluida la adición, modificación y eliminación de propiedades de metadatos, utilice el editor de Esquema.

>[!NOTE]
>
>Los métodos de edición masiva funcionan para los recursos disponibles en una carpeta o una colección. En el caso de los recursos disponibles en varias carpetas o que cumplen un criterio común, es posible actualizar [masivamente los metadatos después de realizar la búsqueda](/help/assets/search-assets.md#metadataupdates).

1. Navegue a la ubicación de los recursos que desee editar.
1. Seleccione los recursos para los que desea editar propiedades comunes.
1. En la barra de herramientas, toque o haga clic en **[!UICONTROL Propiedades]** para abrir la página [!UICONTROL Propiedades] de los recursos seleccionados.

   >[!NOTE]
   >
   >Cuando se seleccionan varios recursos, se selecciona el formulario principal común más bajo para los recursos. En otras palabras, la página [!UICONTROL Propiedades] solo muestra los campos de metadatos que son comunes en las páginas [!UICONTROL Propiedades] de todos los recursos individuales.

1. Modifique las propiedades de metadatos de los recursos seleccionados en las distintas fichas.
1. Para vista del editor de metadatos de un recurso específico, anule la selección de los recursos restantes de la lista. Los campos del editor de metadatos se rellenan con los metadatos del recurso concreto.

   >[!NOTE]
   >
   >* En la página [!UICONTROL Propiedades] , puede quitar recursos de la lista de recursos anulándolos. La lista de recursos tiene todos los recursos seleccionados de forma predeterminada. Los metadatos de los recursos que se eliminan de la lista no se actualizan.
   >* En la parte superior de la lista de recursos, active la casilla de verificación situada junto a **[!UICONTROL Título]** para alternar entre seleccionar los recursos y borrar la lista.


1. Para seleccionar otro esquema de metadatos para los recursos, toque o haga clic en **[!UICONTROL Configuración]** en la barra de herramientas y seleccione el esquema que desee. Guarde los cambios.
1. Para anexar los nuevos metadatos con los metadatos existentes en los campos que contienen varios valores, seleccione el **[!UICONTROL modo Anexar]**. Si no selecciona esta opción, los metadatos nuevos sustituirán a los metadatos existentes en los campos. Pulse o haga clic en **[!UICONTROL Enviar]**.

   >[!CAUTION]
   >
   >En el caso de los campos de un solo valor, los nuevos metadatos no se anexan al valor existente en el campo aunque seleccione el modo **[!UICONTROL Anexar]**.

## Configurar límite para la actualización masiva de metadatos {#configlimit}

Para evitar una situación similar a DOS, AEM limita el número de parámetros admitidos en una solicitud de Sling. Al actualizar los metadatos de muchos recursos de una sola vez, es posible que se alcance el límite y que los metadatos no se actualicen para más recursos. AEM genera la siguiente advertencia en los registros:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Para cambiar el límite, acceda a la consola web ( **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**) y cambie el valor de **[!UICONTROL Máximo de parámetros POST]** en la configuración OSGi de la **[!UICONTROL administración de parámetros de solicitud Apache Sling]**.

## Esquemas de metadatos {#metadata-schemata}

Los esquemas de metadatos son conjuntos predefinidos de definiciones de propiedades de metadatos que se pueden utilizar en varias aplicaciones. Las propiedades siempre están asociadas a un recurso, lo que significa que las propiedades están &quot;cerca&quot; del recurso.

También puede diseñar sus propios esquemas de metadatos si no existe ninguno que satisfaga sus necesidades. No duplicado la información existente. Dentro de una organización, la separación de esquemas facilita el uso compartido de metadatos. [!DNL Experience Manager] proporciona una lista predeterminada de los esquemas de metadatos más populares. La lista le ayuda a poner en marcha la estrategia de metadatos y a elegir rápidamente las propiedades de metadatos que necesita.

A continuación se enumeran los esquemas de metadatos admitidos.

### Metadatos estándar {#standard-metadata}

* DC - [!DNL Dublin Core] es un conjunto de metadatos importante y ampliamente utilizado.
* DICOM - Imágenes digitales y comunicaciones en medicina.
* Iptc4xmpCore y iptc4xmpExt - International Press Communications Standard contienen muchos metadatos específicos de cada asunto.
* rdf - Marco de descripción de recursos - para metadatos web semánticos genéricos.
* xmp - [!DNL Extensible Metadata Platform].
* xmpBJ - Entradas de trabajo básicas.

### Metadatos específicos de la aplicación {#application-specific-metadata}

Los metadatos específicos de la aplicación incluyen metadatos técnicos y descriptivos. Si utiliza estos metadatos, es posible que otras aplicaciones no puedan utilizarlos. Por ejemplo, si tiene un recurso con [!DNL Adobe Photoshop] metadatos y otra aplicación de procesamiento de imágenes intenta acceder a los metadatos, es posible que no pueda acceder a ellos. Si encuentra que tiene muchos metadatos específicos de la aplicación en los recursos, puede crear un paso de flujo de trabajo que cambie una propiedad específica de la aplicación a una propiedad estándar.

* ACDSee: metadatos administrados por el [!DNL ACDSee] programa. Consulte [www.acdsee.com/](https://www.acdsee.com/).
* Álbum - [!DNL Adobe Photoshop Album].
* CQ - Utilizado por [!DNL Experience Manager Assets].
* DAM - Utilizado por [!DNL Experience Manager Assets].
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html) es una colección de herramientas para la administración de metadatos y archivos para sistemas operativos Windows.
* CRS: [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto y MP - Microsoft Photo.
* PDF y PDF/X.
* Photoshop y psAux - [!DNL Adobe Photoshop].

### Metadatos de Digital Rights Management {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - Sistema [universal de licencias de](https://www.useplus.com)imágenes.
* PRISM: requisitos de [publicación para metadatos](https://www.idealliance.org/prism-metadata)estándar del sector.
* PRL - lenguaje de derechos PRISM.
* PUR - Derechos de uso de PRISM.
* `xmpPlus` - Integración de PLUS con XMP.

### Metadatos específicos de la fotografía {#photography-specific-metadata}

* Exif - Información técnica de la cámara, incluyendo la posición GPS.
* CRS - [!DNL Camera Raw] esquema.
* `iptc4xmpCore` y `iptc4xmpExt`.
* TIFF: metadatos de imagen (no solo para imágenes TIFF).

### Metadatos específicos de impresión {#print-specific-metadata}

* PDF y PDF/X: Adobe PDF y aplicaciones de terceros.
* PRISM: [www.prismstandard.org](https://www.prismstandard.org) de publicación compatibles con los metadatos estándar del sector.
* XMP.
* `xmpPG` - Metadatos XMP para texto paginado.

### Metadatos específicos de multimedia {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Administración de medios.

## flujos de trabajo impulsados por metadatos {#metadata-driven-workflows}

La creación de flujos de trabajo basados en metadatos ayuda a automatizar algunos procesos, lo que mejora la eficacia. En un flujo de trabajo basado en metadatos, el sistema de administración de flujo de trabajo lee el flujo de trabajo y, como resultado, realiza alguna acción predefinida. Por ejemplo, algunas de las formas en que puede utilizar flujos de trabajo basados en metadatos:

* El flujo de trabajo puede comprobar si una imagen tiene un título o no. Si no lo hace, el sistema notifica que se debe agregar un título.
* El flujo de trabajo puede comprobar si un aviso de copyright de un recurso permite la distribución o no. En consecuencia, el sistema envía el recurso a un servidor o al otro.
* Un flujo de trabajo puede buscar recursos sin metadatos predefinidos y obligatorios ni recursos con metadatos *no válidos* .
