---
title: Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar Perfiles de imagen o Perfiles de vídeo de Dynamic Media
description: Sugerencias y prácticas recomendadas para nombrar, organizar y administrar archivos de recursos de imagen y vídeo de Dynamic Media.
contentOwner: Rick Brough
translation-type: tm+mt
source-git-commit: 58aa2f416aac6fa6b260e846fc5265bdf62a1949
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar perfiles de imagen o perfiles de vídeo{#best-practices-for-organizing-your-digital-assets-for-using-profiles}

Un concepto importante con respecto al uso de Perfiles de imagen o Perfiles de vídeo de Dynamic Media es que están asignados a las carpetas. Dentro de un perfil hay ajustes para una imagen o un vídeo. Esta configuración procesa el contenido de una carpeta junto con cualquiera de sus subcarpetas. Por lo tanto, la forma en que se asignan nombres a los archivos y las carpetas, la forma en que se organizan las subcarpetas y la forma en que se gestionan los archivos de estas carpetas influye considerablemente en la forma en que el perfil procesa los recursos.

Al utilizar estrategias de asignación de nombres de archivos y carpetas coherentes y adecuadas, junto con una buena práctica de metadatos, puede sacar el máximo partido de la colección de recursos digitales y asegurarse de que el perfil correcto procesa los archivos adecuados.

Consulte [Acerca del Perfil de imágenes y los Perfiles de vídeo de Dynamic Media](about-image-video-profiles.md).

A continuación se ofrecen consejos sobre prácticas recomendadas para organizar los archivos de recursos digitales.

* Organice los archivos en función de los metadatos que les agregue en lugar de hacerlo en las carpetas en las que residan. Esto se puede lograr agregando perfiles de metadatos.

   * Consulte [Perfiles de metadatos.](/help/assets/metadata-profiles.md)
   * Consulte [Metadatos para administración de activos digitales](/help/assets/manage-metadata.md).

* En la mayoría de los casos, la colección de recursos digitales siempre está creciendo. Por lo tanto, es importante (antes) formalizar el uso de metadatos, la estructura de carpetas y la nominación de archivos entre todos los recursos cargados. La estandarización de estos elementos garantiza que, a medida que crezca su grupo de recursos digitales, podrá aplicar perfiles de procesamiento a las carpetas con buena precisión y coherencia.
* Utilice las carpetas únicamente para imponer una estructura de almacenamiento uniforme a los recursos digitales. Por ejemplo, las estructuras de carpetas que pueden ayudarle a refinar qué perfiles asignar pueden incluir lo siguiente:

   * **Carpetas**  de desarrollo: contiene recursos digitales en los que está trabajando.
   * **Carpetas**  de cliente: contiene recursos digitales basados en nombres de clientes o proyectos.
   * **Carpetas**  de origen principales: contiene recursos digitales originales.
   * **Carpetas**  de representación: contiene representaciones y copias de los recursos digitales originales.
   * **Carpetas**  de tamaño de archivo: contiene recursos digitales basados en tamaños de archivo pequeños, medios o grandes.
   * **Carpetas**  de ensayo: contiene recursos digitales que están listos para publicarse en directo en el sitio web.
   * **Carpetas**  de tipos de MIME: contiene recursos digitales específicos de tipos de MIME, como imágenes, documentos y multimedia.
   * **Carpetas**  de archivo: contiene recursos digitales retirados.
   * **Carpetas**  basadas en fechas: contiene recursos digitales basados en una fecha de creación o en una fecha de última modificación.

* Cree un directorio de carpetas que no es probable que cambien para que los perfiles asignados no se rompan.
* Si un recurso ya está publicado, utilice AEM para moverlo a otra carpeta y volver a publicarlo desde su nueva ubicación, la ubicación del recurso publicado original seguirá estando disponible, junto con el recurso recién republicado. Sin embargo, el recurso publicado original se &quot;pierde&quot; por AEM y no se puede cancelar su publicación. Por lo tanto, se recomienda cancelar la publicación de los recursos antes de moverlos a una carpeta diferente.

