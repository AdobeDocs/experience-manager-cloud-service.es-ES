---
title: Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar perfiles
description: Sugerencias y prácticas recomendadas para nombrar, organizar y administrar metadatos para archivos de recursos digitales.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Prácticas recomendadas para organizar recursos digitales con el fin de utilizar perfiles {#best-practices-for-organizing-your-digital-assets-for-using-profiles}

Un concepto importante con respecto al uso de perfiles en Recursos AEM es que están asignados a carpetas. Dentro de un perfil hay ajustes en forma de perfiles de metadatos, junto con perfiles de vídeo o perfiles de imagen. Esta configuración procesa el contenido de una carpeta junto con cualquiera de sus subcarpetas. Por lo tanto, la forma en que se asignan nombres a los archivos y carpetas, la forma en que se organizan las subcarpetas y la forma en que se gestionan los archivos dentro de estas carpetas influye considerablemente en la forma en que un perfil procesa esos recursos.

Al utilizar estrategias de asignación de nombres de archivos y carpetas coherentes y adecuadas, junto con prácticas recomendadas en materia de metadatos, puede sacar el máximo partido de la colección de recursos digitales y asegurarse de que el perfil correcto procesa los archivos adecuados.

Consulte [Perfiles para procesar vídeo, metadatos e imágenes](processing-profiles.md).

A continuación se ofrecen consejos sobre prácticas recomendadas para organizar los archivos de recursos digitales.

* Organice los archivos en función de los metadatos que les agregue en lugar de hacerlo en las carpetas en las que residan. Esto se puede lograr añadiendo perfiles de metadatos.

   * Consulte Perfiles [de metadatos.](/help/assets/metadata-profiles.md)
   * Consulte [Metadatos para la administración](/help/assets/manage-metadata.md)de recursos digitales.

* En la mayoría de los casos, la colección de recursos digitales siempre está creciendo. Por lo tanto, es importante (antes) formalizar el uso de metadatos, la estructura de carpetas y la nominación de archivos entre todos los recursos cargados. La estandarización de estos elementos garantiza que, a medida que crezca el grupo de recursos digitales, podrá aplicar perfiles de procesamiento a las carpetas con mayor precisión y coherencia.
* Utilice las carpetas únicamente para imponer una estructura de almacenamiento uniforme para los recursos digitales. Por ejemplo, las estructuras de carpetas que pueden ayudarle a precisar qué perfiles asignar pueden incluir lo siguiente:

   * **Carpetas** de desarrollo: contiene recursos digitales en los que está trabajando.
   * **Carpetas** de cliente: contiene recursos digitales basados en nombres de clientes o proyectos.
   * **Carpetas** maestras: contiene recursos digitales originales.
   * **Carpetas** de representación: contiene representaciones y copias de los recursos digitales originales.
   * **Carpetas** de tamaño de archivo: contiene recursos digitales basados en tamaños de archivo pequeños, medios o grandes.
   * **Carpetas** de ensayo: contiene recursos digitales que están listos para publicarse en directo en el sitio web.
   * **Carpetas** de tipo MIME: contiene recursos digitales específicos de tipos MIME como imágenes, documentos y multimedia.
   * **Carpetas** de archivo: contiene recursos digitales retirados.
   * **Carpetas** basadas en fecha: contiene recursos digitales basados en una fecha de creación o en una fecha de última modificación.

* Cree un directorio de carpetas que no es probable que cambien para que los perfiles asignados no se rompan.
* Si ya se ha publicado un recurso, utilice AEM para moverlo a otra carpeta y volver a publicarlo desde su nueva ubicación, la ubicación original del recurso publicado seguirá estando disponible, junto con el recurso recién republicado. Sin embargo, el recurso publicado original se &quot;pierde&quot; en AEM y no se puede cancelar la publicación. Por lo tanto, se recomienda cancelar la publicación de los recursos antes de moverlos a una carpeta diferente.

