---
title: Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar Perfiles de imagen o Perfiles de vídeo de Dynamic Media
description: '"Sugerencias y prácticas recomendadas para nombrar, organizar y administrar archivos de imagen y archivos de recursos de vídeo de Dynamic Media".'
contentOwner: Rick Brough
feature: Administración de recursos,Perfiles de imagen,Perfiles de vídeo
role: Administrator,Business Practitioner
exl-id: 82ab5432-088c-4442-a9db-9f4e0184febf
translation-type: tm+mt
source-git-commit: 1fe6ce1259972c1805d934327aa2f24cdcdc0bc8
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# Prácticas recomendadas para organizar los recursos digitales con el fin de utilizar perfiles de imagen o perfiles de vídeo{#best-practices-for-organizing-your-digital-assets-for-using-profiles}

Un concepto importante con respecto al uso de Perfiles de imagen o Perfiles de vídeo de Dynamic Media es que se les asigna a carpetas. Dentro de un perfil hay ajustes para una imagen o un vídeo. Esta configuración procesa el contenido de una carpeta junto con cualquiera de sus subcarpetas. Por lo tanto, la forma en que se asignan nombres a archivos y carpetas, se organizan subcarpetas y se gestionan los archivos de estas carpetas afecta a la forma en que el perfil procesa esos recursos.

Al utilizar estrategias de asignación de nombres de archivos y carpetas coherentes y adecuadas, junto con prácticas recomendadas en materia de metadatos, aproveche al máximo la recopilación de recursos digitales y asegúrese de que el perfil correcto procesa los archivos adecuados.

Consulte [Acerca del perfil de imagen de Dynamic Media y los perfiles de vídeo](about-image-video-profiles.md).

A continuación se indican las prácticas recomendadas para organizar los archivos de recursos digitales.

* Organice los archivos en función de los metadatos que les agregue en lugar de hacerlo en las carpetas en las que residan. Puede realizar esta práctica añadiendo perfiles de metadatos.

   * Consulte [Perfiles de metadatos](/help/assets/metadata-profiles.md).
   * Consulte [Metadatos para Digital Asset Management](/help/assets/manage-metadata.md).

* Normalmente, su colección de recursos digitales siempre está creciendo. Por lo tanto, es importante (anteriormente) formalizar el uso de los metadatos, la estructura de carpetas y la asignación de nombres a los archivos entre todos los recursos cargados. La estandarización en estos elementos garantiza que, a medida que crezca su grupo de recursos digitales, puede aplicar perfiles de procesamiento a las carpetas con buena precisión y coherencia.
* Utilice carpetas solo para imponer una estructura de almacenamiento coherente para sus recursos digitales. Por ejemplo, las estructuras de carpetas que pueden ayudarle a refinar qué perfiles asignar pueden incluir lo siguiente:

   * **Carpetas de desarrollo** : contiene recursos digitales en los que está trabajando.
   * **Carpetas de cliente** : contiene recursos digitales basados en clientes o nombres de proyecto.
   * **Carpetas de origen principales** : contiene recursos digitales de origen originales.
   * **Carpetas de representación** : contiene representaciones y copias de los recursos digitales originales.
   * **Carpetas de tamaño de archivo** : contiene recursos digitales basados en tamaños de archivo pequeños, medios o grandes.
   * **Carpetas de ensayo** : contiene recursos digitales que están listos para publicarse en el sitio web.
   * **Carpetas de tipo Mime** : contiene recursos digitales específicos de tipos MIME, como imágenes, documentos y multimedia.
   * **Carpetas de archivo** : contiene recursos digitales retirados.
   * **Carpetas basadas en datos** : contiene recursos digitales basados en una fecha de creación o en una fecha de última modificación.

* Cree un directorio de carpetas que no es probable que cambien para que no se rompan los perfiles asignados.
* Supongamos que un recurso ya está publicado y, a continuación, utiliza Adobe Experience Manager para mover el recurso a otra carpeta y volver a publicarlo desde su nueva ubicación. La ubicación del recurso publicado originalmente aún está disponible, junto con el recurso recién republicado. Sin embargo, el recurso publicado original se &quot;pierde&quot; para el Experience Manager y no se puede cancelar su publicación. Por lo tanto, se recomienda cancelar la publicación de los recursos primero antes de moverlos a una carpeta diferente.
