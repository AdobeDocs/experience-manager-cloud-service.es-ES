---
title: Gestión de metadatos para recursos digitales
description: Obtenga información sobre los tipos de metadatos y cómo AEM Assets ayuda a administrar los metadatos de los recursos para facilitar la categorización y organización de los recursos. Con la capacidad de mantener y gestionar metadatos arbitrarios con sus recursos, AEM Assets permite organizar y procesar automáticamente recursos en función de sus metadatos.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Gestión de metadatos de recursos digitales {#managing-metadata-for-digital-assets}

Recursos Adobe Experience Manager (AEM) mantiene los metadatos de cada recurso. Esto permite una clasificación y organización más sencillas de los recursos y ayuda a las personas que buscan un recurso específico. Con la capacidad de extraer metadatos de los archivos cargados en AEM Assets, la gestión de metadatos se integra con el flujo de trabajo creativo. Con la capacidad de mantener y gestionar metadatos arbitrarios con sus recursos, AEM Assets permite organizar y procesar automáticamente recursos en función de sus metadatos.

>[!MORELIKETHIS]
>
>* [Metadatos XMP](xmp-metadata.md)
>* [Cómo editar o agregar metadatos](meta-edit.md)


<!-- 
* [Metadata Schemata Reference](meta-ref.md)
-->

## Por qué los metadatos {#why-metadata}

Metadatos significa datos sobre los datos. A este respecto, los datos hacen referencia al recurso con el que está trabajando, por ejemplo, una imagen. Los metadatos son importantes porque permiten a los usuarios administrar los recursos de forma más eficaz.

Los metadatos son la recopilación de todos los datos disponibles para esta imagen, pero no necesariamente están contenidos en esa imagen, por ejemplo:

* el nombre del recurso
* la hora y la fecha de la última modificación
* el tamaño de la imagen tal como se almacenó en el repositorio
* el nombre de la carpeta en la que se encuentra

Estas son las propiedades básicas de metadatos que AEM puede administrar para los recursos, lo que permite a los usuarios ver todos los recursos, por ejemplo, ordenados en la fecha de la última modificación. Esto resulta útil cuando se intenta descubrir qué recursos se han agregado recientemente al repositorio.

Puede agregar más datos de alto nivel a recursos digitales, por ejemplo:

* el tipo de recurso (¿es una imagen, un vídeo, un clip de audio o un documento?)
* el propietario del activo
* el título del recurso
* la descripción del recurso
* las etiquetas asignadas a un recurso

Más metadatos le ayudan a categorizar los recursos y resulta útil a medida que crece la cantidad de información digital. Si bien una sola persona puede administrar una lista de unos pocos cientos de archivos simplemente basándose en sus nombres de archivo, este enfoque es insuficiente cuando aumenta el número de personas involucradas y el número de activos gestionados.

A medida que se agregan metadatos a los recursos, el valor del recurso crece, ya que el recurso se convierte en

* más accesible - la gente puede encontrarlo mucho más fácil
* más fácil de administrar: puede encontrar recursos con el mismo conjunto de propiedades más fácilmente y aplicarles cambios
* más complejo: cuantos más metadatos haya agregado a un recurso, más importante será administrar los metadatos

Por estos motivos, Recursos AEM le proporciona los medios adecuados para crear, gestionar e intercambiar metadatos para sus recursos digitales.

## Conceptos básicos de metadatos {#metadata-basics}

Los metadatos se extraen de los recursos al importarlos (se ingestan). Además, la adición de metadatos le ayuda a categorizar los recursos aún más.

Esta sección trata los tipos de metadatos y los estándares de codificación.

### Metadatos técnicos {#technical-metadata}

Los metadatos técnicos son útiles para las aplicaciones de software que se ocupan de activos digitales y no deben mantenerse manualmente. Los metadatos técnicos se pueden determinar automáticamente mediante Recursos AEM y otro software y pueden cambiar cuando se modifica el recurso. Los metadatos técnicos disponibles de un recurso dependen en gran medida del tipo de archivo del recurso. A continuación se presentan algunos ejemplos de metadatos técnicos:

* el tamaño de un archivo
* las dimensiones (altura y anchura) de una imagen
* la velocidad de bits de un archivo de audio o vídeo
* la resolución (nivel de detalle) de una imagen

### Metadatos descriptivos {#descriptive-metadata}

Los metadatos descriptivos son metadatos relacionados con el dominio de la aplicación, por ejemplo, el negocio del que proviene un recurso. Los metadatos descriptivos no se pueden determinar automáticamente. Debe crearse manual o semiautomáticamente. Por ejemplo, una cámara con GPS puede rastrear automáticamente la latitud y la longitud en que se tomó una imagen y agregar esta información a los metadatos de la imagen.

Debido al elevado costo del trabajo manual necesario para crear información descriptiva sobre metadatos, se han establecido normas para facilitar el intercambio de metadatos entre los sistemas y organizaciones de programas informáticos.

AEM Assets admite todos los estándares relevantes para la gestión de metadatos.

Debido a la importancia de los metadatos y a la gran participación manual necesaria para crear metadatos, se han establecido normas que facilitan el intercambio.

### Normas de codificación {#encoding-standards}

Existen varias formas de incrustar los metadatos en los archivos. Se admite una selección de estándares de codificación:

* XMP: utilizado por Recursos AEM para almacenar los metadatos extraídos en el repositorio.
* ID3: para archivos de audio y vídeo.
* EXIF: para archivos de imagen.
* Otro/Heredado: desde Microsoft Word, PowerPoint, Excel, etc.

#### XMP {#xmp}

XMP significa Extensible Metadata Platform y es el estándar de metadatos que utiliza AEM Assets para la gestión de todos los metadatos. Además de ofrecer codificación de metadatos universales que se puede incrustar en todos los formatos de archivo, XMP proporciona un modelo de contenido enriquecido y es compatible con Adobe y otras empresas, de modo que los usuarios de XMP en combinación con Recursos AEM tienen una plataforma sólida sobre la que construir.

#### ID3 {#id}

Los datos almacenados en estas etiquetas ID3 se muestran cuando se reproduce un archivo de audio digital en el equipo o en un reproductor portátil MP3.

Las etiquetas ID3 están diseñadas para el formato de archivo MP3. Información adicional sobre los formatos:

* Las etiquetas ID3 funcionan en archivos MP3 y MP3pro.
* WAV no tiene etiquetas.
* WMA tiene etiquetas de propiedad que no permiten la implementación de código abierto.
* Ogg Vorbis utiliza comentarios Xiph incrustados en el contenedor OGG.
* AAC utiliza un formato de etiquetado propio.

#### EXIF {#exif}

EXIF significa formato de archivo de imagen intercambiable y es el formato de metadatos más popular utilizado en fotografía digital. Proporciona una forma de incrustar un vocabulario fijo de propiedades de metadatos en varios formatos de archivo, como

* JPEG
* TIFF
* RIFF
* WAV

Una limitación importante de EXIF es que no se admite en otros formatos de archivo de imagen populares como BMP, GIF o PNG.

EXIF almacena los metadatos como pares de un nombre de metadatos y un valor de metadatos. Estos pares de metadatos nombre-valor-valor también se denominan etiquetas, por lo que no deben confundirse con el etiquetado de AEM.

Dado que EXIF se crea automáticamente mediante cámaras digitales modernas y se admite a través de software de gráficos modernos, puede considerarse el denominador común más bajo para la gestión de metadatos.

La mayoría de los campos de metadatos definidos por EXIF son de carácter muy técnico y de uso limitado para la administración descriptiva de metadatos. Por este motivo, Recursos AEM ofrece la asignación de propiedades EXIF en esquemas [de metadatos](metadata-schemas.md) comunes y en [XMP](xmp-metadata.md), el potente formato de metadatos que AEM Assets utiliza para la gestión de metadatos.

#### Otros metadatos {#other-metadata}

Otros metadatos que se pueden incrustar desde archivos son Microsoft Word, PowerPoint, Excel, etc.

## Gestión de metadatos de los recursos digitales {#manage-assets-metadata}

Recursos de Enterprise Manager le permite editar los metadatos de varios recursos simultáneamente para que pueda propagar rápidamente cambios comunes de metadatos a los recursos de forma masiva. Utilice la página [!UICONTROL Propiedades] para cambiar las propiedades de metadatos a un valor común o para agregar o modificar etiquetas. Para personalizar la página Propiedades de metadatos, incluida la adición, modificación y eliminación de propiedades de metadatos, utilice el editor de esquemas.

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
1. Para ver el editor de metadatos de un recurso específico, anule la selección de los recursos restantes de la lista. Los campos del editor de metadatos se rellenan con los metadatos del recurso concreto.

   >[!NOTE]
   >
   >* En la página [!UICONTROL Propiedades] , puede quitar recursos de la lista de recursos anulándolos. La lista de recursos tiene todos los recursos seleccionados de forma predeterminada. Los metadatos de los recursos que se eliminan de la lista no se actualizan.
   >* En la parte superior de la lista de recursos, active la casilla de verificación situada cerca de **[!UICONTROL Título]** para alternar entre seleccionar los recursos y borrar la lista.


1. Para seleccionar un esquema de metadatos diferente para los recursos, toque o haga clic en **[!UICONTROL Configuración]** en la barra de herramientas y seleccione el esquema deseado. Guarde los cambios.
1. Para anexar los nuevos metadatos con los metadatos existentes en los campos que contienen varios valores, seleccione el modo **** Anexar. Si no selecciona esta opción, los metadatos nuevos sustituirán a los metadatos existentes en los campos. Toque o haga clic en **[!UICONTROL Enviar]**.

   >[!CAUTION]
   >
   >En el caso de los campos de un solo valor, los nuevos metadatos no se anexan al valor existente en el campo aunque seleccione el modo **** Anexar.

## Configurar límite para la actualización masiva de metadatos {#configlimit}

Para evitar una situación similar a DOS, AEM limita el número de parámetros admitidos en una solicitud de Sling. Al actualizar los metadatos de muchos recursos de una sola vez, es posible que se alcance el límite y que los metadatos no se actualicen para más recursos. AEM genera la siguiente advertencia en los registros:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Para cambiar el límite, acceda a la consola web ( **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > Consola **** web) y cambie el valor de **[!UICONTROL Máximo de parámetros]** POST en la configuración OSGi del parámetro de solicitud Sling de **** Apache.

## Esquemas de metadatos {#metadata-schemata}

Los esquemas de metadatos son conjuntos predefinidos de definiciones de propiedades de metadatos que se pueden utilizar en una amplia variedad de aplicaciones. Las propiedades siempre están asociadas a un recurso, lo que significa que las propiedades son &quot;acerca&quot; del recurso.

También puede diseñar sus propios esquemas de metadatos si no hay ninguno que satisfaga sus necesidades (tenga cuidado, sin embargo, de no duplicar algo que ya existe). Dentro de una organización, la separación de esquemas facilita el uso compartido de metadatos entre organizaciones.

AEM le proporciona una lista lista lista lista para usar de los esquemas de metadatos más populares, lo que le permite poner en marcha su estrategia de metadatos y elegir las propiedades de metadatos que necesita de un esquema ya definido.

Los esquemas de metadatos admitidos se enumeran en la siguiente sección.

### Metadatos estándar {#standard-metadata}

* dc - Dublin Core - el conjunto de metadatos más importante y ampliamente utilizado
* DICOM - Imágenes digitales y comunicaciones en medicina
* Iptc4xmpCore y iptc4xmpExt - International Press Communications Standard - muchos metadatos específicos
* rdf - Marco de descripción de recursos - para metadatos web semánticos genéricos
* xmp: Extensible Metadata Platform
* xmpBJ - Entradas de trabajo básicas

### Metadatos específicos de la aplicación {#application-specific-metadata}

>[!NOTE]
>
>Los metadatos específicos de la aplicación incluyen metadatos técnicos y descriptivos. Si utiliza estos metadatos, es posible que otras aplicaciones no puedan utilizarlos. Por ejemplo, si tiene un recurso con metadatos de Adobe Photoshop y otra aplicación de procesamiento de imágenes intenta acceder a los metadatos, es posible que no pueda acceder a ellos.
>
>Si encuentra que tiene muchos metadatos específicos de la aplicación en sus recursos, puede crear un paso de flujo de trabajo que cambie la propiedad específica de la aplicación a una estándar.

* acdsee: metadatos administrados por el programa ACDSee [www.acdsee.com/](https://www.acdsee.com/)
* álbum - Álbum de Adobe Photoshop
* cq: utilizado por Recursos AEM
* dam - utilizado por AEM Assets
* dex - Explorador de descripciones de SC de Optima
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - IView MediaPro
* MicrosoftPhoto y MP - Microsoft Photo
* pdf y pdfx
* photoshop &amp; psAux - Adobe Photoshop

### Metadatos de Digital Rights Management {#digital-rights-management-metadata}

* cc - creative commons
* xmpRights
* plus - Picture Licensing Universal System - https://www.useplus.com/
* prisma: https://www.idealliance.org/prism-metadata de publicación compatibles con metadatos estándar del sector
* prl - Lenguaje de derechos de prisma
* pur: Derechos de uso de Prisma
* xmpPlus: integración de PLUS con XMP

### Metadatos específicos de la fotografía {#photography-specific-metadata}

* exif: mucha información técnica de la cámara, incluida la posición GPS
* crs - cámara fotoshop raw
* Iptc4xmpCore y iptc4xmpExt
* TIFF: metadatos de imagen (no solo para imágenes TIFF)

### Metadatos específicos de impresión {#print-specific-metadata}

* pdf y pdfx: Adobe PDF y aplicaciones de terceros
* prism: [www.prismstandard.org](https://www.prismstandard.org) de publicación para metadatos estándar del sector
* xmp
* xmpPG - xmp para texto paginado

### Metadatos específicos de multimedia {#multimedia-specific-metadata}

* xmpDM - Medios dinámicos
* xmpMM - Administración de medios

## Flujos de trabajo basados en metadatos {#metadata-driven-workflows}

La creación de flujos de trabajo basados en metadatos ayuda a automatizar algunos procesos, lo que mejora la eficacia. En un flujo de trabajo basado en metadatos, el sistema de administración de flujo de trabajo lee el flujo de trabajo y, como resultado, realiza alguna acción predefinida.

Por ejemplo, algunas de las formas de utilizar flujos de trabajo basados en metadatos:

* El flujo de trabajo puede comprobar si una imagen tiene un título. Si no lo hace, el sistema notifica a un usuario concreto para que agregue un título.
* El flujo de trabajo puede comprobar si un aviso de copyright de un recurso permite la distribución. Si lo hace, el sistema envía el recurso a un servidor. Si no lo hace, el sistema envía el recurso a otro servidor.
