---
title: Vídeo en Dynamic Media
description: Aprenda a trabajar con vídeo en Dynamic Media. Revise las prácticas recomendadas para codificar vídeos, publicar vídeos en YouTube, ver informes de vídeo y añadir subtítulos o marcadores de capítulo a los vídeos.
contentOwner: Rick Brough
feature: Video Profiles,Best Practices
role: User
exl-id: 0d5fbb3e-b763-415f-8c69-ea36445f882b
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '10063'
ht-degree: 2%

---

# Vídeo {#video}

En esta sección se describe el trabajo con vídeo en Dynamic Media.

## Inicio rápido: vídeos {#quick-start-videos}

La siguiente descripción paso a paso del flujo de trabajo se ha diseñado para ayudarle a ponerse en marcha rápidamente con los conjuntos de vídeos adaptables en Dynamic Media. Después de cada paso, hay referencias cruzadas a encabezados de temas donde puede encontrar más información.

>[!NOTE]
>
>Antes de trabajar con vídeo en Dynamic Media, asegúrese de que su administrador de Adobe Experience Manager ya haya habilitado y configurado los servicios en la nube de Dynamic Media.
>
>* Consulte [Configurar servicios de nube de Dynamic Media](/help/assets/dynamic-media/config-dm.md#configuring-dynamic-media-cloud-services) en Configuración de Dynamic Media y [Solucionar problemas de Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md).
>

1. **Cargue sus vídeos de Dynamic Media** haciendo lo siguiente:

   * Cree su propio perfil de codificación de vídeo. O bien, puede usar el perfil predefinido _Codificación de vídeo adaptable_ que se incluye con Dynamic Media.

      * [Crear un perfil de codificación de vídeo](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming).
      * La resolución de codificación de vídeo de salida máxima es de 8.192 × 4.320 o 4.320 × 8.192,md.
      * Más información sobre [Prácticas recomendadas para la codificación de vídeo](#best-practices-for-encoding-videos).

   * Asocie el perfil de procesamiento de vídeo a una o varias carpetas en las que va a cargar los vídeos de origen principales.

      * [Aplicar un perfil de vídeo a las carpetas](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
      * Más información sobre [Organizar recursos digitales](/help/assets/organize-assets.md).

   * Cargue los vídeos de origen principales en las carpetas designadas. Una vez añadidos, los vídeos se codifican según el perfil de procesamiento de vídeo asignado a la carpeta.

      * Dynamic Media admite principalmente vídeos de formato corto con una duración máxima de 30 minutos y una resolución mínima superior a 25 × 25.
      * La resolución de entrada de vídeo máxima admitida es de 16.384 × 16.384.
      * Puede cargar archivos de vídeo de hasta 15 GB cada uno.
      * [Cargue sus vídeos](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).
      * Más información sobre [Formatos de archivo de entrada compatibles](/help/assets/file-format-support.md).

   * Supervise el progreso de la codificación de vídeo [1} desde la vista de recursos o de flujo de trabajo.](#monitoring-video-encoding-and-youtube-publishing-progress)

1. **Administre sus vídeos de Dynamic Media** mediante cualquiera de las siguientes acciones:

   * Organizar, examinar y buscar recursos de vídeo

      * [Organizar recursos digitales](/help/assets/organize-assets.md)
      * [Buscar recursos de vídeo](/help/assets/search-assets.md#custompredicates) o [Buscando recursos](/help/assets/manage-digital-assets.md#search-assets)

   * Previsualización y publicación de recursos de vídeo

      * Vea el vídeo de origen y las representaciones codificadas del vídeo junto con sus miniaturas asociadas:
        [Previsualizar vídeos](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) o [Previsualizar recursos](/help/assets/dynamic-media/previewing-assets.md)
        [Administrar representaciones de vídeo](/help/assets/manage-digital-assets.md#managing-renditions)

      * [Administrar ajustes preestablecidos de visor](/help/assets/dynamic-media/managing-viewer-presets.md)
      * [Publicación de recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)

   * Trabajo con metadatos de vídeo

      * Edite las propiedades del vídeo, como el título, la descripción y las etiquetas, y campos de metadatos personalizados:
        [Editar propiedades de vídeo](/help/assets/manage-digital-assets.md#editing-properties)

      * [Administración de metadatos para recursos digitales](/help/assets/manage-metadata.md)
      * [Esquemas de metadatos](/help/assets/metadata-schemas.md)

   * Revise, apruebe y anote vídeos, y mantenga un control total de las versiones

      * [Anotar vídeos](/help/assets/manage-video-assets.md#annotate-video-assets) o [Anotar recursos](/help/assets/manage-digital-assets.md#annotating)

      * [Crear una versión](/help/assets/manage-digital-assets.md#asset-versioning)
      * [Iniciar un flujo de trabajo en un recurso](/help/assets/manage-digital-assets.md#starting-a-workflow-on-an-asset)

      * [Revisar recursos de carpeta](/help/assets/bulk-approval.md)
      * [Proyectos](/help/sites-cloud/authoring/projects/overview.md)

1. **Publique sus vídeos de Dynamic Media** mediante uno de los procedimientos siguientes:

   * Si utiliza Experience Manager como sistema WCM (Web Content Management), puede añadir vídeos directamente a las páginas web.

      * [Agregar vídeos a sus páginas web](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

   * Si utiliza un sistema WCM de terceros, puede vincular o incrustar vídeos a sus páginas web.

      * Integrar vídeo con URL:
        [Vincular URL a su aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md).

      * Integración de vídeo mediante código incrustado en una página web:
        [Incrustar el visor de vídeo en una página web](/help/assets/dynamic-media/embed-code.md).

   * [Generar informes de vídeo](#viewing-video-reports).

   * [Agregar varios subtítulos y pistas de audio a un vídeo](#about-msma).

## Trabajo con vídeo en Dynamic Media {#working-with-video-in-dynamic-media}

El vídeo en Dynamic Media es una solución completa que facilita la publicación de vídeo adaptable de alta calidad para su streaming en varias pantallas, incluidas escritorios, tabletas y dispositivos móviles. Un conjunto de vídeos adaptable agrupa versiones del mismo vídeo que se codifican a diferentes velocidades de bits y formatos, como 400 kbps, 800 kbps y 1000 kbps. El equipo de escritorio o dispositivo móvil detecta el ancho de banda disponible.

Por ejemplo, en un dispositivo móvil iOS, detecta un ancho de banda, como 3G, 4G o Wi-Fi. A continuación, selecciona automáticamente el vídeo codificado correcto entre las distintas velocidades de bits de vídeo dentro del conjunto de vídeos adaptables. El vídeo se transmite a equipos de escritorio, dispositivos móviles o tabletas.

Además, la calidad de vídeo cambia automáticamente si las condiciones de red cambian en el escritorio o en el dispositivo móvil. Además, si un cliente entra en modo de pantalla completa en un equipo de escritorio, el conjunto de vídeos adaptable responde con una mejor resolución, lo que mejora la experiencia de visualización del cliente. El uso de conjuntos de vídeos adaptables le ofrece la mejor experiencia de visualización posible para los clientes que reproducen vídeo de Dynamic Media en varias pantallas y dispositivos.

La lógica que utiliza un reproductor de vídeo para determinar qué vídeo codificado se reproducirá o seleccionará durante la reproducción se basa en el siguiente algoritmo:

1. El reproductor de vídeo carga el fragmento de vídeo inicial en función de la velocidad de bits más cercana al valor establecido para &quot;velocidad de bits inicial&quot; en el propio reproductor.
1. El reproductor de vídeo cambia según los cambios en la velocidad del ancho de banda según los siguientes criterios:

   1. El reproductor elige el flujo de ancho de banda más alto por debajo o igual al ancho de banda estimado.
   1. El reproductor considera solo el 80% del ancho de banda disponible. Sin embargo, si está subiendo, es más conservador en solo el 70% para evitar la sobreestimación y volver inmediatamente.

Para obtener información técnica detallada sobre el algoritmo, consulte [https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp](https://android.googlesource.com/platform/frameworks/av/+/master/media/libstagefright/httplive/LiveSession.cpp)

Al administrar un solo vídeo y conjuntos de vídeos adaptables, se admiten los siguientes elementos:

* Carga de vídeo desde numerosos formatos de vídeo y audio compatibles. Codificación de vídeo en formato MP4 H.264 para su reproducción en varias pantallas. Puede utilizar ajustes preestablecidos de vídeo adaptables predefinidos, ajustes preestablecidos de codificación de vídeo únicos o personalizar su propia codificación para controlar la calidad y el tamaño del vídeo.

   * Cuando se genera un conjunto de vídeos adaptable, incluye vídeos MP4.
   * **Nota**: Los vídeos principales/de origen no se agregan a un conjunto de vídeos adaptable.

* Subtítulos de vídeo en todos los visores de vídeo de HTML5.
* Organice, examine y busque vídeos con compatibilidad total con metadatos para una administración eficaz de los recursos de vídeo.
* Ofrezca conjuntos de vídeos adaptables a la web y a equipos de escritorio, tabletas y dispositivos móviles.

La transmisión de vídeo adaptable es compatible con varias plataformas de iOS. Consulte la [Guía de referencia de visores de Dynamic Media](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/video/c-html5-video-reference).

<!-- OUTDATED 2/28/22 BASED ON CQDOC-18692 Dynamic Media supports mobile video playback for MP4 H.264 video. You can find BlackBerry&reg; devices that support this video format at the following: [Supported video formats on BlackBerry&reg;](https://support.blackberry.com/kb/articleDetail?ArticleNumber=000005482).

OUTDATED 2/28/22 BASED ON CQDOC-18692 You can find Windows&reg; devices that support this video format at the following [Supported video formats on Windows&reg; Phone](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/supported-codecs). -->

* Reproduzca el vídeo con los ajustes preestablecidos del visualizador de vídeos de Dynamic Media, incluidos los siguientes:

   * Visores de vídeo únicos.
   * Visores de medios mixtos que combinan contenido de vídeo e imagen.

* Configure reproductores de vídeo para satisfacer sus necesidades de marca.
* Integre vídeo en su sitio web, sitio móvil o aplicación móvil con una URL simple o código incrustado.

<!-- GIVES a 404 See [Dynamic video playback](https://s7d9.scene7.com/s7/uvideo.jsp?asset=GeoRetail/Mop_AVS&config=GeoRetail/Universal_Video1&stageSize=640,480) sample. -->

Consulte también [Visualizadores solo para Experience Manager Assets y Dynamic Media Classic](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers#viewers-aem-assets-dmc) y [Visualizadores solo para Experience Manager Assets](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only) en la [Guía de referencia de visualizadores de Dynamic Media](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources).

## Práctica recomendada: Uso del visualizador de vídeo HTML5 {#best-practice-using-the-html-video-viewer}

Los ajustes preestablecidos del visualizador de vídeo Dynamic Media HTML5 son reproductores de vídeo sólidos. Puede utilizarlas para evitar muchos problemas comunes asociados con la reproducción de vídeo de HTML5 y problemas asociados con dispositivos móviles. Por ejemplo, una falta de entrega de flujo de bits adaptable y un alcance limitado del explorador de escritorio.

En el lado del diseño del reproductor, puede diseñar la funcionalidad del reproductor de vídeo con herramientas de desarrollo web estándar. Por ejemplo, puede diseñar los botones, los controles y el fondo de imagen de póster personalizado con HTML5 y CSS para ayudarle a llegar a sus clientes con una apariencia personalizada.

En la parte de reproducción del visor, detecta automáticamente la capacidad de vídeo del explorador. A continuación, sirve el vídeo mediante HLS o DASH, también conocidos como flujo de vídeo adaptable. O bien, si estos métodos de envío no están presentes, se utiliza HTML5 progressive en su lugar.

Puede combinar en un solo reproductor la capacidad de diseñar los componentes de reproducción mediante HTML5 y CSS. Puede tener reproducción integrada y utilizar flujo adaptable y progresivo según la capacidad del explorador. Toda esta funcionalidad significa que puede ampliar el alcance del contenido multimedia enriquecido tanto para usuarios de escritorio como móviles, así como garantizar una experiencia de vídeo optimizada.

Consulte también [Solo visores para Experience Manager Assets](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/c-html5-aem-asset-viewers#viewers-for-aem-assets-only) en la [Guía de referencia de visores de Dynamic Media](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources).


### Reproducción de vídeo en equipos de escritorio y dispositivos móviles mediante el visualizador de vídeo HTML5 {#playback-of-video-on-desktop-computers-and-mobile-devices-using-the-html-video-viewer}

En el caso de la transmisión de vídeo adaptable de escritorio y móvil, los vídeos utilizados para la conmutación de velocidad de bits se basan en todos los vídeos MP4 del conjunto de vídeos adaptable.

La reproducción de vídeo se produce mediante HLS o DASH, o descarga de vídeo progresivo. En versiones anteriores de Experience Manager, como 6.0, 6.1 y 6.2, los vídeos se transmitían por HTTP.

Sin embargo, en Experience Manager 6.3 y versiones posteriores, los vídeos ahora se transmiten por HTTPS (es decir, HLS o DASH) porque la URL del servicio de puerta de enlace DM siempre utiliza HTTPS. Este comportamiento predeterminado no afecta a los clientes. La transmisión de vídeo siempre se produce a través de HTTPS si el explorador es compatible. Consulte la siguiente tabla.

Por lo tanto,

* Si tiene un sitio web HTTPS con flujo de vídeo HTTPS, el flujo está bien.
* Si tiene un sitio web HTTP con flujo de vídeo HTTPS, el flujo está bien y no hay problemas de contenido mixto desde el explorador web.

DASH es el estándar internacional y HLS es un estándar de Apple. Ambos se utilizan para la transmisión de vídeo adaptable. Además, ambas tecnologías ajustan automáticamente la reproducción según la capacidad del ancho de banda de la red. También permite al cliente &quot;buscar&quot; cualquier punto del vídeo sin necesidad de esperar a que se descargue el resto del vídeo.

El vídeo progresivo se proporciona descargando y almacenando el vídeo localmente en el sistema de escritorio o el dispositivo móvil de un usuario.

En la tabla siguiente se describe el dispositivo, el explorador y el método de reproducción de vídeos en equipos de escritorio y dispositivos móviles que utilizan el [Visor de vídeo HTML5 de Dynamic Media](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-for-aem-assets-only/interactive-video/c-html5-aem-int-video#interactive-video).

<table>
 <tbody>
  <tr>
   <td><strong>Dispositivo</strong></td>
   <td><strong>Explorador</strong></td>
   <td><strong>Modo de reproducción de vídeo</strong></td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Internet Explorer 9 y 10</td>
   <td>Descarga progresiva.</td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Internet Explorer 11+</td>
   <td>En Windows® 8 y Windows® 10: forzar el uso de HTTPS cada vez que se solicite DASH o HLS. Limitación conocida: HTTP en DASH o HLS no funciona en esta combinación de explorador/sistema operativo <br /> <br /> En Windows® 7: descarga progresiva. Utiliza la lógica estándar para el protocolo HTTP frente al protocolo HTTPS.</td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Firefox 23-44</td>
   <td>Descarga progresiva.</td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Firefox 45 o posterior</td>
   <td>Flujo de velocidad de bits adaptable HLS o DASH*</td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Chrome</td>
   <td>Flujo de velocidad de bits adaptable HLS o DASH*</td>
  </tr>
  <tr>
   <td>Escritorio</td>
   <td>Safari (Mac)</td>
   <td>Flujo de velocidad de bits adaptable HLS</td>
  </tr>
  <tr>
   <td>Dispositivo móvil</td>
   <td>Chrome (Android™ 6 o anterior)</td>
   <td>Descarga progresiva.</td>
  </tr>
  <tr>
   <td>Dispositivo móvil</td>
   <td>Chrome (Android™ 7 o posterior)</td>
   <td>HLS o DASH* adaptive bitrate streaming/td&gt;
  </tr>
  <tr>
   <td>Dispositivo móvil</td>
   <td>Android™ (explorador predeterminado)</td>
   <td>Descarga progresiva.</td>
  </tr>
  <tr>
   <td>Dispositivo móvil</td>
   <td>Safari (iOS)</td>
   <td>Flujo de velocidad de bits adaptable HLS</td>
  </tr>
  <tr>
   <td>Dispositivo móvil</td>
   <td>Chrome (iOS)</td>
   <td>Flujo de velocidad de bits adaptable HLS</td>
  </tr>
 </tbody>
</table>

<!--  THIS LINE WAS REMOVED FROM THE TABLE ABOVE ON FEB 28, 2022 BASED ON CQDOC 18692 -RSB <tr>
   <td>Mobile</td>
   <td>BlackBerry&reg;</td>
   <td>HLS or DASH</td>
  </tr>
 -->

## Arquitectura de la solución de vídeo Dynamic Media {#architecture-of-dynamic-media-video-solution}

El siguiente gráfico muestra el flujo de trabajo general de creación de vídeos que se cargan y codifican a través de DMGateway (en modo híbrido de Dynamic Media) y que se ponen a disposición del público.

![chlimage_1-427](assets/chlimage_1-427.png)

## Arquitectura de publicación híbrida para vídeos {#hybrid-publishing-architecture-for-videos}

![chlimage_1-428](assets/chlimage_1-428.png)

## Prácticas recomendadas para codificar vídeos {#best-practices-for-encoding-videos}

El flujo de trabajo **Dynamic Media Encode Video** codifica el vídeo si ha activado Dynamic Media y ha configurado los servicios de Video Cloud. Este flujo de trabajo captura el historial de procesos de flujo de trabajo y la información de errores. Si ha habilitado Dynamic Media y ha configurado los servicios de Video Cloud, el flujo de trabajo de **[!UICONTROL codificación de vídeo de Dynamic Media]** surte efecto automáticamente al cargar un vídeo. (Si no usa Dynamic Media, el flujo de trabajo **[!UICONTROL DAM Update Asset]** surte efecto).

Las siguientes son sugerencias recomendadas para codificar archivos de vídeo de origen.

<!-- For advice about video encoding, see the following:

* [Streaming 101: The Basics — Codecs, Bandwidth, Data Rate, and Resolution](https://www.adobe.com/go/learn_s7_streaming101_en).
* [Video Encoding Basics](https://www.adobe.com/go/learn_s7_encoding_en). -->

### Archivos de vídeo de Source {#source-video-files}

Cuando codifique un archivo de vídeo, utilice un archivo de vídeo de origen de la máxima calidad posible. Evite utilizar archivos de vídeo codificados anteriormente porque estos archivos ya están comprimidos y una codificación posterior crea un vídeo de calidad inferior.

* Dynamic Media admite principalmente vídeos de formato corto con una duración máxima de 30 minutos y una resolución mínima superior a 25 × 25.
* Puede cargar archivos de vídeo de origen principales de hasta 15 GB cada uno.

En la tabla siguiente se describe el tamaño recomendado, la relación de aspecto y la velocidad de bits mínima que deben tener los archivos de vídeo de origen antes de codificarlos:

| Tamaño | Proporción de aspecto | Velocidad de bits mínima |
|--- |--- |--- |
| 1024 × 768 | 4:3 | 4500 Kbps para la mayoría de los vídeos. |
| 1280 × 720 | 16:9 | 3000 - 6000 kbps, dependiendo de la cantidad de movimiento en el vídeo. |
| 1920 × 1080 | 16:9 | 6.000 a 8.000 kbps, en función de la cantidad de movimiento del vídeo. |

### Obtener los metadatos de un archivo {#obtaining-a-file-s-metadata}

Puede obtener los metadatos de un archivo visualizando sus metadatos mediante una herramienta de edición para vídeos o utilizando una aplicación diseñada para obtener metadatos. A continuación se indican instrucciones para utilizar MediaInfo, una aplicación de terceros, para obtener los metadatos de un archivo de vídeo:

1. Ir a [Descarga de MediaInfo](https://mediaarea.net/en/MediaInfo/Download).
1. Seleccione y descargue el instalador para la versión GUI y siga las instrucciones de instalación.
1. Después de la instalación, haga clic con el botón derecho en el archivo de vídeo (solo Windows®) y seleccione MediaInfo o abra MediaInfo y arrastre el archivo de vídeo a la aplicación. Verá todos los metadatos asociados con el archivo de vídeo, incluidos el ancho, el alto y los fps.

### Proporción de aspecto {#aspect-ratio}

Cuando seleccione o cree un ajuste preestablecido de codificación de vídeo para el archivo de vídeo de origen principal, asegúrese de que el ajuste preestablecido tenga la misma proporción de aspecto. Este enfoque garantiza la coherencia con el archivo de vídeo de origen principal. La relación de aspecto es la relación entre la anchura y la altura del vídeo.

Para determinar la proporción de aspecto de un archivo de vídeo, obtenga los metadatos del archivo. Observe la anchura y altura del archivo (consulte Obtención de metadatos de un archivo más arriba). A continuación, utilice esta fórmula para determinar la relación de aspecto:

anchura/altura = proporción de aspecto

En la tabla siguiente se describe cómo se traducen los resultados de la fórmula en opciones de relación de aspecto comunes:

| Resultado de fórmula | Proporción de aspecto |
|--- |--- |
| 1,33 | 4:3 |
| 0,75 | 3:4 |
| 1,78 | 16:9 |
| 0,56 | 9:16 |

Por ejemplo, un vídeo de 1440 de anchura × 1080 de altura tiene una relación de aspecto de 1440/1080 o 1,33. En este caso, elija un ajuste preestablecido de codificación de vídeo con una relación de aspecto de 4:3 para codificar el archivo de vídeo.

### Velocidad de bits {#bitrate}

La velocidad de bits es la cantidad de datos codificados para formar un segundo de reproducción de vídeo. La velocidad de bits se mide en kilobits por segundo (Kbps).

>[!NOTE]
>
>Como todos los códecs utilizan compresión con pérdida, la velocidad de bits es el factor más importante en la calidad del vídeo. Con la compresión con pérdida, cuanto más comprime un archivo de vídeo, más se degrada la calidad. Por este motivo, si todas las demás características son iguales (resolución, velocidad de fotogramas y códec), cuanto menor sea la velocidad de bits, menor será la calidad del archivo comprimido.

Al seleccionar una codificación de velocidad de bits, puede elegir entre dos tipos:

* **[!UICONTROL Codificación de velocidad de bits constante]** (CBR): durante la codificación CBR, la velocidad de bits, o el número de bits por segundo, se mantiene igual durante todo el proceso de codificación. La codificación CBR conserva la velocidad de datos establecida en su configuración durante todo el vídeo. Además, la codificación CBR no optimiza los archivos multimedia para la calidad, pero ahorra espacio de almacenamiento.
Utilice CBR si el vídeo contiene un nivel de movimiento similar en todo el vídeo. CBR se utiliza comúnmente para el contenido de vídeo de streaming. Consulte también [Usar parámetros personalizados de codificación de vídeo](/help/assets/dynamic-media/video-profiles.md#using-custom-added-video-encoding-parameters).

* **[!UICONTROL Codificación de velocidad de bits variable]** (VBR): la codificación VBR ajusta la velocidad de datos hacia abajo y hasta el límite superior establecido, según los datos requeridos por el compresor. Esta funcionalidad significa que durante un proceso de codificación VBR la velocidad de bits del archivo multimedia aumenta o disminuye dinámicamente según las necesidades de velocidad de bits del archivo multimedia.
VBR tarda más en codificarse, pero produce los resultados más favorables; la calidad del archivo multimedia es superior. VBR se utiliza comúnmente para la entrega progresiva de contenido de vídeo http.

¿Cuándo se utiliza VBR o CRB?
Al seleccionar VBR en comparación con CBR, casi siempre se recomienda utilizar VBR para los archivos multimedia. VBR proporciona archivos de mayor calidad a velocidades de bits competitivas. Cuando utilice VBR, asegúrese de utilizar con codificación de dos pasos y establezca la velocidad de bits máxima en 1,5 veces la velocidad de bits de vídeo de destino.

Al elegir un ajuste preestablecido de codificación de vídeo, asegúrese de tener en cuenta la velocidad de conexión del usuario de destino. Elija un ajuste preestablecido con una velocidad de datos del 80 % de esa velocidad. Por ejemplo, si la velocidad de conexión del usuario de destino es de 1000 Kbps, el mejor ajuste preestablecido es uno con una velocidad de datos de vídeo de 800 Kbps.

En esta tabla se describe la velocidad de datos de las velocidades de conexión típicas.

| Velocidad (Kbps) | Tipo de conexión |
|--- |--- |
| 256 | Conexión de acceso telefónico. |
| 800 | Conexión móvil típica. Para esta conexión, establezca como objetivo una velocidad de datos en el rango de 400 a un máximo de 800 para experiencias 3G. |
| 2000 | Conexión de escritorio de banda ancha típica. Para esta conexión, establezca como objetivo una velocidad de datos en el rango de 800-2000 Kbps, con un promedio de la mayoría de los objetivos de 1200-1500 Kbps. |
| 5000 | Conexión típica de banda ancha alta. No se recomienda la codificación en este rango superior porque la mayoría de los consumidores no pueden acceder a la entrega de vídeo a esta velocidad. |

### Resolución {#resolution}

**Resolución** describe la altura y anchura de un archivo de vídeo en píxeles. La mayor parte del vídeo de origen se almacena en alta resolución (por ejemplo, 1920 × 1080). Para fines de streaming, el vídeo de origen se comprime con una resolución más pequeña (640 × 480 o menor).

La resolución y la velocidad de datos son dos factores integrados que determinan la calidad del vídeo. Para mantener la misma calidad de vídeo, cuanto mayor sea el número de píxeles de un archivo de vídeo (mayor será la resolución), mayor deberá ser la velocidad de datos. Por ejemplo, considere el número de píxeles por fotograma en una resolución de 320 × 240 y un archivo de vídeo de resolución de 640 × 480:

| Resolución | Píxeles por cuadro |
|--- |--- |
| 320 × 240 | 76.800 |
| 640 × 480 | 307.200 |

El archivo de 640 × 480 tiene cuatro veces más píxeles por fotograma. Para lograr la misma velocidad de datos para estas dos resoluciones de ejemplo, se aplica cuatro veces la compresión al archivo de 640 × 480, lo que puede reducir la calidad del vídeo. Por lo tanto, una velocidad de datos de vídeo de 250 Kbps produce una visualización de alta calidad con una resolución de 320 × 240, pero no con una resolución de 640 × 480.

En general, cuanto mayor sea la velocidad de datos que utilice, mejor aparecerá el vídeo y, cuanto mayor sea la resolución que utilice, mayor será la velocidad de datos que deberá mantener con calidad de visualización (en comparación con resoluciones más bajas).

Como la resolución y la velocidad de datos están vinculadas, tiene dos opciones al codificar vídeo:

* Elija una velocidad de datos y, a continuación, codifique con la resolución más alta que parezca buena a la velocidad de datos elegida.
* Elija una resolución y codifique a la velocidad de datos necesaria para conseguir vídeo de alta calidad con la resolución que elija.

Cuando elija (o cree) un ajuste preestablecido de codificación de vídeo para el archivo de vídeo de origen principal, utilice esta tabla para seleccionar la resolución correcta:

| Resolución | Altura (píxeles) | Tamaño de pantalla |
|--- |--- |--- |
| 240p | 240 | Pantalla pequeña |
| 300p | 300 | Pantalla pequeña normalmente para dispositivos móviles |
| 360p | 360 | Pantalla pequeña |
| 480p | 480 | pantalla de Medium |
| 720p | 720 | Pantalla grande |
| 1080p | 1080 | Pantalla grande de alta definición |

La resolución de entrada de vídeo máxima admitida es de 16.384 × 16.384. La resolución máxima de codificación de vídeo de salida es de 8.192 × 4.320 o 4.320 × 8.192.

### Fps (fotogramas por segundo) {#fps-frames-per-second}

En Estados Unidos y Japón, la mayor parte del vídeo se graba a 29,97 fps; en Europa, la mayor parte del vídeo se graba a 25 fps. Se filma una película a 24 fps.

Elija un ajuste preestablecido de codificación de vídeo que coincida con la velocidad de fps del archivo de vídeo de origen principal. Por ejemplo, si el vídeo de origen principal es de 25 fps, elija un ajuste preestablecido de codificación con 25 fps. De forma predeterminada, toda la codificación personalizada utiliza el fps del archivo de vídeo de origen principal. Por este motivo, no es necesario especificar la configuración de fps explícitamente al crear un ajuste preestablecido de codificación de vídeo.

### Dimensiones de codificación de vídeo {#video-encoding-dimensions}

Para obtener resultados óptimos, seleccione dimensiones de codificación de modo que el vídeo de origen sea un múltiplo completo de todos los vídeos codificados.

Para calcular esta proporción, se divide el ancho de origen por el ancho codificado para obtener la proporción de ancho. A continuación, se divide la altura de origen por la altura codificada para obtener la relación de altura.

Si la proporción resultante es un entero, significa que el vídeo se escala de forma óptima. Si la proporción resultante no es un entero, afecta a la calidad del vídeo al dejar artefactos de píxeles sobrantes en la pantalla. Este efecto es más evidente cuando el vídeo tiene texto.

Por ejemplo, supongamos que el vídeo de origen es 1920 × 1080. En la tabla siguiente, los tres vídeos codificados proporcionan la configuración de codificación óptima para utilizar.

| Tipo de vídeo | Anchura × altura | Proporción de anchura | Proporción de altura |
|--- |--- |--- |--- |
| Origen | 1920 × 1080 | 1 | 1 |
| Codificado | 960 × 540 | 2 | 2 |
| Codificado | 640 × 360 | 3 | 3 |
| Codificado | 480 × 270 | 4 | 4 |

### Formato de archivo de vídeo codificado {#encoded-video-file-format}

Dynamic Media recomienda utilizar ajustes preestablecidos de codificación de vídeo MP4 H.264. Como los archivos MP4 utilizan el códec de vídeo H.264, proporciona vídeo de alta calidad pero en un tamaño de archivo comprimido.

## Ver informes de vídeo {#viewing-video-reports}

>[!NOTE]
>
>Los informes de vídeo solo están disponibles cuando se ejecuta Dynamic Media (modo híbrido).

Los informes de vídeo muestran varias métricas agregadas durante un período especificado para ayudarle a supervisar que los vídeos individuales y agregados de *publicados* funcionan según lo esperado. Los siguientes datos de métricas principales se agregan para todos los vídeos publicados en todo el sitio web:

* Inicios de vídeo
* Tasa de finalización
* Promedio de tiempo en vídeo
* Tiempo total en vídeo
* Vídeos por visita

También se muestra una tabla con todos los *vídeos publicados* para que puedas rastrear los vídeos más vistos en tu sitio web en función del total de inicios de vídeo.

Al seleccionar un nombre de vídeo en la lista, se muestra el informe de retención de audiencia (menú desplegable) del vídeo en forma de gráfico de líneas. El gráfico muestra el número de vistas durante un momento determinado de la reproducción de vídeo. Cuando reproduce el vídeo, la barra vertical rastrea en sincronización con el indicador de tiempo del reproductor. Las caídas en los datos del gráfico de líneas indican dónde cae la audiencia debido al desinterés.

Si el vídeo se ha codificado fuera de Adobe Experience Manager Dynamic Media, el gráfico de retención de audiencia (entrega) y los datos del porcentaje de reproducción de la tabla no están disponibles.

>[!NOTE]
>
>Los datos de seguimiento y creación de informes se basan exclusivamente en el uso del reproductor de vídeo propio de Dynamic Media y del ajuste preestablecido del reproductor de vídeo asociado. Como tal, no puede rastrear vídeos que reproducen otros reproductores de vídeo e informar sobre ellos.

De forma predeterminada, la primera vez que se acceden a Informes de vídeo, el informe muestra los datos de vídeo a partir del primer día del mes en curso y termina con la fecha del mes actual. Sin embargo, puede anular el intervalo de fechas predeterminado especificando su propio intervalo de fechas. La próxima vez que lo haga en los informes de vídeo, se utilizará el intervalo de fechas que haya especificado.

Para que los informes de vídeo funcionen correctamente, se crea automáticamente un ID de grupo de informes cuando se configura Dynamic Media Cloud Services. Al mismo tiempo, el ID del grupo de informes se inserta en el servidor de publicación para que esté disponible para la función Copiar URL al obtener una vista previa de los recursos. Sin embargo, esta funcionalidad requiere que el servidor de publicación ya esté configurado. Si el servidor de publicación no está configurado, aún puede publicar para ver el informe de vídeo. Sin embargo, debe volver a la configuración de nube de Dynamic Media y seleccionar **[!UICONTROL Aceptar]**.

**Para ver informes de vídeo:**

1. En la esquina superior izquierda de Experience Manager, seleccione el logotipo de Experience Manager. En el carril izquierdo, haga clic en ![Icono de martillo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Hammer_18_N.svg) > **[!UICONTROL Assets]** > **[!UICONTROL Informes de vídeo]**.
1. En la página Informes de vídeo, realice una de las siguientes acciones:

   * Cerca de la esquina superior derecha, selecciona el icono **[!UICONTROL Actualizar informe de vídeo]**.
Sólo puede usar Actualizar si la fecha de finalización del informe es el día actual. Esta función garantiza que pueda ver el seguimiento de vídeo que se ha producido desde la última vez que ejecutó el informe.

   * Cerca de la esquina superior derecha, seleccione el icono **[!UICONTROL Selector de fecha]**.
Especifique el intervalo de fechas inicial y final para el que desea obtener datos de vídeo y, a continuación, seleccione **[!UICONTROL Ejecutar informe]**.

   El cuadro de grupo Métricas principales identifica varias mediciones agregadas de todos los *vídeos publicados* en el sitio.

1. En la tabla que muestra los vídeos más publicados, seleccione un nombre de vídeo para reproducir el vídeo y también consulte el informe de retención de audiencia (lista desplegable) del vídeo.

<!-- OBSOLETE CONTENT OBSOLETE CONTENT - SDK ONLY AVAILABLE INTERNALLY NOW 
### Viewing video reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK {#viewing-video-reports-based-on-a-video-viewer-that-you-created-using-the-scene-hmtl-viewer-sdk}

If you are using an out-of-box video viewer provided by Dynamic Media, or if you created a custom viewer preset based off of an out-of-box video viewer, then no additional steps are required to view video reports. However, if you have created your own video viewer based off the Dynamic Media HTML5 Viewer SDK, then use the following steps to ensure the your video viewer is sending tracking events to Dynamic Media Video Reports.

Use the Dynamic Media Viewers Reference and the Dynamic Media HTML5 Viewers SDK to create your own video viewers.

See [Dynamic Media Viewers Reference Guide](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/library/home.html).

Download the Scene7 HTML Viewer SDK from Adobe Developer Connection.

See [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).

**To view Video Reports based on a video viewer that you created using the Dynamic Media HTML5 Viewer SDK:**

1. Navigate to any published video asset.
1. Near the upper-left corner of the asset's page, from the drop-down list, select **[!UICONTROL Viewers]**.
1. Select any video viewer preset and copy the embed code.
1. In the embed code, find the line with the following:

   `videoViewer.setParam("config2", "<value>");`

   The `config2` parameter enables tracking in HTML5 Viewers. It is also a company-specific preset that contains the configuration information for Video Reporting, and for customer-specific Adobe Analytics configurations.

   The correct value for the config2 parameter is found in both the **[!UICONTROL Embed Code]** and in the copy **[!UICONTROL URL]** function. In the URL from the copy **[!UICONTROL URL]** command, the parameter to look for is `&config2=<value>` . The value is almost always `companypreset`, but in some instances it can also be `companypreset-1`, `companypreset-2`, and so forth.

1. In your custom video viewer code, add AppMeasurementBridge .jsp to the viewer page by doing the following:

    * First, determine if you need the `&preset` parameter.
      If the `config2` parameter is `companypreset`, you do *not *need `&preset=parameter`.
      If `config2` is anything else, set the preset parameter the same as the `config2` parameter. For example, if `config2=companypreset-2`, add `&param2=companypreset-2` to the AppMeasurmentBridge.jsp URL.

    * Then, add the AppMeasurementBridge.jsp script:
      `<script language="javascript" type="text/javascript" src="https://s7d1.scene7.com/s7viewers/AppMeasurementBridge.jsp?company=robindallas&preset=companypreset-2"></script>`

1. Create the TrackingManager component by doing the following:

    * After calling `s7sdk.Utils.init();` create a TrackingManager instance to track events by adding the following:
      `var trackingManager = new s7sdk.TrackingManager();`

    * Connect components to TrackingManager by doing the following:
      In the `s7sdk.Event.SDK_READY` event handler, attach the component you want to track to the TrackingManager.
      For example, if the component is `videoPlayer`, add
      `trackingManager.attach(videoPlayer);`
      to attach the component to the trackingManager. To track multiple viewers on a page, use multiple tracking mangaer components.

    * Create the AppMeasurementBridge object by adding the following:

      ```
      var appMeasurementBridge = new AppMeasurementBridge(); appMeasurementBridge.setVideoPlayer(videoPlayer);
      ```

    * Add the tracking function by adding the following:

      ```
      trackingManager.setCallback(appMeasurementBridge.track,
       appMeasurementBridge);
      ```

   The appMeasurementBridge object has a built-in track function. OBSOLETE However, you can provide your own to support multiple tracking systems or other functionality.

   For more information, see *Using the TrackingManager Component* in the *Scene7 HTML5 Viewer SDK User Guide* available for download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html).
 -->

## Acerca de la compatibilidad con varios subtítulos y pistas de audio para vídeos en Dynamic Media{#about-msma}

Gracias a la capacidad de incluir varios subtítulos y pistas de audio en Dynamic Media, puede añadir fácilmente varias pistas de audio. También puede agregar varios archivos de subtítulos utilizando sus propios archivos de `.vtt` (Pista de texto de vídeo) o archivos de subtítulos generados por IA. Los subtítulos generados por IA en Dynamic Media están diseñados para mejorar la accesibilidad y la participación de los vídeos mediante la generación automática de subtítulos precisos y sincronizados. Esta tecnología utiliza algoritmos de IA avanzados para transcribir el contenido hablado en texto, que luego se muestra como subtítulos en el vídeo. Algunas características clave de esta tecnología son las siguientes:

* **Transcripción automática:** El sistema de IA transcribe las palabras habladas en texto en tiempo real, lo que garantiza que los subtítulos se generen de forma rápida y precisa.
* **Soporte multilingüe:** Los subtítulos se pueden entregar automáticamente en más de 60 idiomas, lo que facilita el acceso a una audiencia global.
* **Accesibilidad mejorada:** Al proporcionar subtítulos, los videos se vuelven más accesibles para los espectadores sordos o con dificultades auditivas, o para las personas que prefieren ver videos con el sonido apagado.
* **Participación mejorada:** Los subtítulos pueden ayudar a conservar la atención del usuario y mejorar la comprensión, especialmente en entornos ruidosos o cuando el idioma nativo del usuario es diferente del idioma del vídeo.

Estas funciones hacen que los subtítulos con tecnología de IA sean una herramienta valiosa para los creadores de contenido que buscan mejorar la accesibilidad y la participación de su contenido de vídeo.

![Pestaña Subtítulos y pistas de audio en Dynamic Media junto con una tabla que muestra los archivos de subtítulos .VTT cargados y los archivos de pista de audio .MP3 cargados para un vídeo.](/help/assets/dynamic-media/assets/msma-caption-audiotracks-tab2.png)

Algunos de los casos de uso que se deben tener en cuenta para agregar varios subtítulos y pistas de audio al vídeo principal son los siguientes:

| Tipo | Caso de uso |
|--- |--- |
| **Subtítulos** | Compatibilidad con varios idiomas |
|  | Texto descriptivo para accesibilidad |
| **Pistas de audio** | Compatibilidad con varios idiomas |
|  | Pistas de comentarios |
|  | Audio descriptivo |

Todos los [formatos de vídeo admitidos en Dynamic Media](/help/assets/file-format-support.md) y todos los visores de vídeo de Dynamic Media, excepto el visor de *Video_360* de Dynamic Media, son compatibles para su uso con varios subtítulos y pistas de audio.

### Agregue varios subtítulos y pistas de audio al vídeo {#add-msma}

Antes de agregar varias pistas de subtítulos y audio al vídeo, asegúrese de que ya dispone de lo siguiente:

* Dynamic Media está configurado en un entorno de AEM.
* Se ha aplicado un perfil de vídeo de [Dynamic Media a la carpeta en la que se han introducido los vídeos](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

Los subtítulos añadidos son compatibles con los formatos WebVTT y Adobe VTT. Además, los archivos de pista de audio añadidos son compatibles con el formato MP3.

>[!IMPORTANT]
>
>Para los vídeos cargados *antes de* que habilitan la compatibilidad con múltiples subtítulos/pistas de audio o subtítulos generados por IA en su cuenta de Dynamic Media, [debe volver a procesarlos](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). Este paso de reprocesamiento garantiza que estos vídeos puedan utilizar varios subtítulos/pistas de audio y subtítulos generados por IA. Después del reprocesamiento, las direcciones URL del vídeo siguen funcionando y reproduciéndose como de costumbre.

**Para agregar varios subtítulos y pistas de audio al vídeo:**

1. [Cargue el vídeo principal en una carpeta](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) que ya tenga un perfil de vídeo asignado.
1. Desplácese hasta el recurso de vídeo cargado al que desee agregar varias pistas de subtítulos y audio.
1. En el modo de selección de recursos, en ![Ver icono de tarjeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista de tarjeta) o en ![Ver icono de lista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista de lista), seleccione el recurso de vídeo.
1. En la barra de herramientas, haga clic en ![Icono de información](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Propiedades.
   ![Recurso de vídeo seleccionado con marca de verificación sobre la imagen en miniatura de vídeo y Propiedades de vista resaltadas en la barra de herramientas.](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*Recurso de vídeo seleccionado en la vista de tarjeta.*
1. En la página Propiedades del vídeo, seleccione la ficha **[!UICONTROL Pistas de subtítulos y audio]**.

   >[!TIP]
   >Si no ve la ficha **[!UICONTROL Pistas de subtítulos y audio]**, significa una de estas dos cosas:
   >
   >* La carpeta en la que reside el vídeo seleccionado no tiene asignado un perfil de vídeo. En cuyo caso, consulte [Aplicar un perfil de vídeo a la carpeta](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)
   >* O bien, Dynamic Media debe volver a procesar el vídeo. En cuyo caso, consulte [Volver a procesar los recursos de Dynamic Media en una carpeta](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).
   >
   >Cuando haya completado cualquiera de las tareas anteriores, vuelva a estos pasos.

   ![Ficha Pistas de subtítulos y audio en la página Propiedades.](/help/assets/dynamic-media/assets/msma-audiotracks.png)
   *Ficha Pistas de subtítulos y audio en la página Propiedades del vídeo.*

1. Para agregar una o más pistas de audio a un vídeo, haga lo siguiente:
   1. Seleccione **[!UICONTROL Cargar pistas de audio]**.
   1. Desplácese hasta uno o varios archivos .mp3, ábralos y selecciónelos.
   1. Para que las pistas de audio estén visibles en la lista emergente **[!UICONTROL Seleccionar audio o subtítulo]** del reproductor multimedia, debe agregar los detalles necesarios sobre cada archivo de pista de audio. Al hacerlo, se asegura de que todas las pistas de audio estén correctamente enumeradas y accesibles. Haga clic en ![Icono Dibujar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) a la derecha del nombre de un archivo de pista de audio. En el cuadro de diálogo **Editar pista de audio**, escriba los siguientes detalles necesarios:

      | Metadatos de pista de audio | Descripción |
      |--- |--- |
      | Nombre de archivo | El nombre de archivo predeterminado se deriva del nombre de archivo original. El nombre de archivo solo se puede cambiar durante la carga y no se puede cambiar más adelante. Los requisitos de caracteres de nombre de archivo son los mismos que para los AEM Assets.<br>No se puede usar el mismo nombre de archivo para archivos de pista de audio o de rótulo adicionales. |
      | Idioma | Seleccione el idioma correcto de la pista de audio. |
      | Tipo | Seleccione el tipo de pista de audio que está utilizando.<br>**Original**: la pista de audio adjuntada originalmente al vídeo y representada como `[Original]` en la etiqueta con el idioma `English` seleccionado de forma predeterminada. Aunque **[!UICONTROL Label]** y **[!UICONTROL Language]** se pueden cambiar en el cuadro de diálogo **[!UICONTROL Editar pista de audio]**, el valor predeterminado son los valores originales si se vuelve a procesar el vídeo principal.<br>**Estándar**: pista de audio de complemento para un idioma distinto del original.<br>**Descripción del audio**: pista de audio que también incluye una narración descriptiva de gestos y acciones no verbales en el vídeo, lo que hace que el contenido sea más accesible para las personas con problemas de visión. |
      | Etiqueta | El texto que se muestra como nombre de la pista de audio en la lista emergente **[!UICONTROL Seleccionar audio o rótulo]** del reproductor multimedia. La etiqueta es lo que ve un cliente y que corresponde a una pista de audio. Por ejemplo, `English [Original]`. La etiqueta de audio adjunto a un vídeo está establecida en `[Original]` de forma predeterminada. |

      Si es necesario, puede cambiar o editar los metadatos de la pista de audio más adelante. Cuando se publica el vídeo, estos detalles se reflejan en las direcciones URL públicas de los vídeos publicados.

   1. Cerca de la esquina superior derecha de la página, en el menú desplegable **[!UICONTROL Guardar y cerrar]**, haga clic en **[!UICONTROL Guardar]**.
   1. Realice una de las siguientes acciones:
      * Repita este proceso para cada archivo de pista de audio que cargue.
      * Continúe con el paso siguiente para agregar subtítulos a un vídeo.

1. Para añadir uno o más archivos de subtítulos a un vídeo, elija cuál de los siguientes casos de uso se adapta mejor a su escenario:

   |  | Caso de uso | Opción Crear pie de ilustración para utilizar |
   | --- | --- | --- |
   | **Opción 1** | Tengo mis propios archivos de subtítulos preexistentes en los idiomas que quiero usar.<br>Ver **Opción 1** a continuación. | **[!UICONTROL Cargar archivos]** |
   | **Opción 2** | Quiero que AI genere mis archivos de subtítulos en varios idiomas.<br>Ver **Opción 2** a continuación. | **[!UICONTROL Convertir pistas de audio]** |
   | **Opción 3** | Es necesario corregir el texto de un archivo de subtítulos (`.vtt`), volver a cargarlo para reemplazar el archivo `.vtt` antiguo y, a continuación, hacer que AI traduzca el archivo corregido.<br>Ver **Opción 3** a continuación. | **[!UICONTROL Traducir pie de ilustración]** |

   ![Opciones para crear subtítulos.](/help/assets/dynamic-media/assets/msma-createcaption.png)
   *El menú desplegable Crear pie de ilustración le ofrece tres opciones: Cargar archivos, Convertir pistas de audio y Traducir pie de ilustración.*

   +++**Opción 1:** *Tengo mis propios archivos de subtítulos preexistentes en los idiomas que deseo usar* (opción **[!UICONTROL Cargar archivos]**)

   1. Cerca de la parte superior derecha de la página, haz clic en **[!UICONTROL Crear pie de ilustración]** > **[!UICONTROL Cargar archivos]**.
   1. Vaya a uno o varios de los `.vtt` archivos preexistentes y selecciónelos, y ábralos.
   1. Para que los subtítulos estén visibles en el reproductor multimedia, *debe* agregar los detalles necesarios sobre *cada* archivo de subtítulos que cargue. Haga clic en ![Dibujar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) a la derecha del nombre de archivo de rótulo. En el cuadro de diálogo **Editar pie de ilustración**, escriba los siguientes detalles necesarios sobre el archivo:

      | Metadatos de rótulo | Descripción |
      |--- |--- |
      | Nombre de archivo | El nombre de archivo predeterminado se deriva del nombre de archivo original. El nombre de archivo solo se puede cambiar durante la carga y no se puede cambiar más adelante. Los requisitos de caracteres de nombre de archivo son los mismos que para los AEM Assets.<br>No se puede usar el mismo nombre de archivo para archivos de subtítulos y de pistas de audio adicionales. |
      | Idioma | Seleccione el idioma del pie de ilustración. Después de procesar un archivo de rótulo, este campo de idioma deja de poder editarse (aparece atenuado) |
      | Tipo | Seleccione el tipo de rótulo que está utilizando.<br>**Subtítulo**: el texto del título que se muestra con el vídeo que traduce o transcribe el cuadro de diálogo.<br>**Pie de ilustración**: el texto del pie de ilustración incluye ruidos de fondo, diferenciación del altavoz y otros detalles relevantes, junto con la traducción o transcripción del cuadro de diálogo, lo que mejora la accesibilidad para las personas sordas o con dificultades auditivas. |
      | Etiqueta | Texto que se muestra para el nombre del pie de ilustración en la lista emergente **[!UICONTROL Seleccionar audio o pie de ilustración]** del reproductor multimedia. La etiqueta es lo que ve un cliente y que corresponde a un subtítulo o pista de rótulo. Por ejemplo, `English (CC)`. |

      Si es necesario, puede cambiar o editar los metadatos de los subtítulos más adelante. Cuando se publica el vídeo, estos detalles se reflejan en las direcciones URL públicas de los vídeos publicados.

   1. Cerca de la esquina superior derecha de la página, en el menú desplegable **[!UICONTROL Guardar y cerrar]**, haga clic en **[!UICONTROL Guardar]**. Los archivos se cargan y comienza el procesamiento de metadatos, tal como se ve en la columna **Estado** de la interfaz.

      >[!NOTE]
      >
      >En función de la configuración de almacenamiento en caché de la instancia, el procesamiento de metadatos puede tardar varios minutos en reflejarse en la vista previa y en las direcciones URL publicadas.

   1. Si seleccionaste **[!UICONTROL Guardar y cerrar]** en el paso anterior, en lugar de seleccionar **[!UICONTROL Guardar]**, aún puedes ver el estado de procesamiento de los archivos cargados. Ver [Ver el estado del ciclo de vida de los archivos de subtítulos y pistas de audio cargados](#lifecycle-status-video).
   1. Continúe con el paso 8.

   +++

   +++**Opción 2:** *Quiero que AI genere mis archivos de subtítulos en varios idiomas* (**[!UICONTROL Opción Convertir pistas de audio]**)

   1. Cerca de la esquina superior derecha de la página, haga clic en **[!UICONTROL Crear pie de ilustración]** > **[!UICONTROL Convertir pistas de audio]**.

      ![Cuadro de diálogo Convertir pistas de audio.](/help/assets/dynamic-media/assets/msma-convertaudiotracks.png)
      *El cuadro de diálogo Convertir pistas de audio usa IA para generar archivos de subtítulos en varios idiomas.*

   1. En el cuadro de diálogo **Convertir pistas de audio**, defina las siguientes opciones:

      | Opción | Descripción |
      |--- |--- |
      | Pista de audio a convertir | Haga clic en ![Icono de cheurón descendente](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) y, a continuación, elija el archivo de pista de audio cargado desde el que desea que se generen subtítulos mediante IA. |
      | Idiomas de salida | Haga clic en ![Icono de cheurón descendente](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) y, a continuación, seleccione uno o varios idiomas en los que desee que aparezca el archivo de rótulo.<br>Para quitar un idioma seleccionado, haga clic en ![Cerrar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg).<br>Durante la reproducción del vídeo, la lista de idiomas aparecerá en el reproductor de contenidos en el orden en que los seleccione aquí. |

   1. Haga clic en **[!UICONTROL Listo]**.
   1. Cerca de la esquina superior derecha de la página, en el menú desplegable **[!UICONTROL Guardar y cerrar]**, haga clic en **[!UICONTROL Guardar]**.
   1. Vuelva a hacer clic en la ficha **[!UICONTROL Pistas de subtítulos y audio]**. Se crean uno o más archivos de subtítulos y comienza el procesamiento, tal como se ve en la columna **Status** de la interfaz. Ver también [Ver el estado del ciclo de vida de los archivos de subtítulos y pistas de audio cargados](#lifecycle-status-video).

      >[!NOTE]
      >
      >En función de la configuración de almacenamiento en caché de la instancia, el procesamiento de metadatos puede tardar varios minutos en reflejarse en la vista previa y en las direcciones URL publicadas.

   1. (Opcional) Haga clic en ![Dibujar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) a la derecha del nombre de un archivo de rótulo. En el cuadro de diálogo **Editar pie de ilustración**, puede editar los siguientes detalles sobre el archivo:

      | Metadatos de rótulo | Descripción |
      | --- | --- |
      | Tipo | Seleccione el tipo de rótulo que está utilizando.<br>**Subtítulo**: el texto del título que se muestra con el vídeo que traduce o transcribe el cuadro de diálogo.<br>**Pie de ilustración**: el texto del pie de ilustración incluye ruidos de fondo y diferenciación de altavoz. También incluye otra información relevante, junto con la traducción o transcripción del diálogo. Este enfoque hace que el contenido sea más accesible para las personas sordas o con dificultades auditivas. |
      | Etiqueta | Texto que se muestra para el nombre del pie de ilustración en la lista emergente **[!UICONTROL Seleccionar audio o pie de ilustración]** del reproductor multimedia. La etiqueta es lo que ve un cliente y que corresponde a un subtítulo o pista de rótulo. Por ejemplo, `English (CC)`. |

      Puede cambiar o editar ciertos metadatos de subtítulos más adelante, si es necesario. Cuando se publica el vídeo, los detalles de estos metadatos se reflejan en las direcciones URL públicas de los vídeos publicados.
   1. Continúe con el paso 8.

   +++

   +++**Opción 3:** *El texto de un archivo de subtítulos (`.vtt`) debe corregirse, volver a cargarse para reemplazar el archivo `.vtt` antiguo y, a continuación, hacer que AI traduzca el archivo corregido* (**[!UICONTROL Opción Traducir subtítulos]**)

   1. Haga clic en **[!UICONTROL Crear subtítulo]** > **[!UICONTROL Traducir subtítulos]**. Esta opción está disponible si ya se han agregado y procesado uno o más archivos de rótulo.

      ![Cuadro de diálogo Traducir subtítulos.](/help/assets/dynamic-media/assets/msma-translate-captions.png)
      *El cuadro de diálogo Traducir subtítulos le permite utilizar un archivo de subtítulos existente para que AI genere nuevos archivos de subtítulos en varios idiomas.*

   1. En el cuadro de diálogo **Traducir subtítulos**, defina las siguientes opciones:

      | Opción | Descripción |
      |--- |--- |
      | Pie de ilustración para traducir | Haga clic en ![Icono de cheurón hacia abajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) y, a continuación, elija un archivo de rótulo del que desee que se generen los rótulos mediante IA. |
      | Idiomas de salida | Haga clic en ![Icono de cheurón descendente](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) y, a continuación, seleccione uno o varios idiomas en los que desee que aparezca el archivo de rótulo.<br>Para quitar un idioma seleccionado, haga clic en ![Cerrar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg).<br>Durante la reproducción del vídeo, la lista de idiomas aparecerá en el reproductor de contenidos en el orden en que los seleccione aquí. |

   1. Haga clic en **[!UICONTROL Listo]**.
   1. Cerca de la esquina superior derecha de la página, en el menú desplegable **[!UICONTROL Guardar y cerrar]**, haga clic en **[!UICONTROL Guardar]**.
   1. Vuelva a hacer clic en la ficha **[!UICONTROL Pistas de subtítulos y audio]**. Se crean uno o más archivos de subtítulos y comienza el procesamiento, tal como se ve en la columna **Status** de la interfaz. Ver también [Ver el estado del ciclo de vida de los archivos de subtítulos y pistas de audio cargados](#lifecycle-status-video).

      >[!NOTE]
      >
      >En función de la configuración de almacenamiento en caché de la instancia, el procesamiento de metadatos puede tardar varios minutos en reflejarse en la vista previa y en las direcciones URL publicadas.

   1. (Opcional) Haga clic en ![Dibujar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Draw_18_N.svg) a la derecha del nombre de un archivo de rótulo. En el cuadro de diálogo **Editar pie de ilustración**, puede editar los siguientes detalles sobre el archivo:

      | Metadatos de rótulo | Descripción |
      | --- | --- |
      | Tipo | Seleccione el tipo de rótulo que está utilizando.<br>**Subtítulo**: el texto del título que se muestra con el vídeo que traduce o transcribe el cuadro de diálogo.<br>**Pie de ilustración**: el texto del pie de ilustración también incluye ruidos de fondo y diferenciación del altavoz. También incluye otra información relevante, junto con la traducción o transcripción del diálogo. Este enfoque hace que el contenido sea más accesible para las personas sordas o con dificultades auditivas. |
      | Etiqueta | Texto que se muestra para el nombre del pie de ilustración en la lista emergente **[!UICONTROL Seleccionar audio o pie de ilustración]** del reproductor multimedia. La etiqueta es lo que ve un cliente y que corresponde a un subtítulo o pista de rótulo. Por ejemplo, `English (CC)`. |

      Puede cambiar o editar ciertos metadatos de subtítulos más adelante, si es necesario. Cuando se publica el vídeo, los detalles de estos metadatos se reflejan en las direcciones URL públicas de los vídeos publicados.

   1. Continúe con el paso 8.

   +++

1. (Opcional) Previsualice el vídeo antes de publicarlo para garantizar que los subtítulos y el audio funcionan según lo esperado. Ver [Vista previa de un vídeo con varios subtítulos y pistas de audio](#preview-video-audio-subtitle).
1. Publique el vídeo. Consulte [Publicar recursos](publishing-dynamicmedia-assets.md).

#### Agregar archivos de rótulo y de pista de audio a un vídeo ya publicado

Después de cargar archivos adicionales de subtítulos o pistas de audio en un vídeo publicado, estos archivos tienen un estado de `Processed` una vez que se han preparado. A continuación, puede obtener una vista previa del vídeo en Dynamic Media para ver o escuchar los nuevos archivos.

Sin embargo, tras la vista previa, debe *publicar* el vídeo de nuevo para que también se publiquen los archivos de subtítulos o pistas de audio que acaba de agregar. Después de la publicación, los subtítulos o el audio estarán disponibles con la URL pública de Dynamic Media.

>[!NOTE]
>
>En función de la configuración de almacenamiento en caché de la instancia, las actualizaciones de metadatos pueden tardar varios minutos en reflejarse en la vista previa y en las direcciones URL publicadas.

En el caso de que haya configurado Dynamic Media para la publicación inmediata, la carga de archivos de audio o subtítulos adicionales déclencheur inmediatamente la publicación del vídeo después de la carga de archivos de audio o subtítulos.

>[!CAUTION]
>
>Cuando subes archivos de subtítulos o archivos de audio a un vídeo que se ha publicado o cancelado la publicación, los archivos se eliminarán si [*vuelve a procesar*](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets) el vídeo. Solo el audio original del vídeo permanece intacto. En estos casos, debe volver a cargar los archivos de rótulo y de pista de audio en el vídeo.

#### Añada varios subtítulos a un vídeo que tenga una URL existente con el modificador caption

Dynamic Media admite la adición de un solo pie de ilustración con vídeo mediante un modificador de URL. Ver [Agregar subtítulos al vídeo](#adding-captions-to-video).

Los cambios de varios subtítulos tienen prioridad sobre los subtítulos añadidos mediante un modificador URL para los vídeos publicados.

**Para agregar varios subtítulos a un vídeo que ya tiene una dirección URL con el modificador de subtítulos:**

1. Cargue el archivo de rótulo que ya se haya añadido como modificador al vídeo para que pueda administrar el archivo explícitamente.
1. Cargue los archivos de subtítulos adicionales que sean necesarios.
1. Publique el vídeo como de costumbre.
La URL existente con el modificador caption ahora puede cargar varios subtítulos.


### Editar subtítulos de vídeo

Puede editar subtítulos (subtítulos) para recursos de vídeo directamente en la interfaz de usuario de Dynamic Media. Esta función le permite editar `.vtt` archivos de subtítulos, previsualizar actualizaciones y publicar cambios sin problemas.

* Cuando se publican subtítulos, los cambios se sincronizan y publican automáticamente.
* Si se producen errores de edición y necesita volver a generar los subtítulos:
   * Elimine el archivo de subtítulos existente.
   * Use la opción 2 (Convertir pistas de audio) en el paso 7 de [Agregue varios subtítulos y pistas de audio al vídeo](#add-msma).
   * Haga clic en **Guardar** o **Guardar y cerrar** para generar un nuevo archivo de subtítulos.
* La vista previa de subtítulos dentro del editor es solo para edición y no refleja cómo aparecen los subtítulos en la interfaz de usuario final de reproducción de vídeo.

**Para editar subtítulos de vídeo:**

1. Vaya al recurso de vídeo cuyos subtítulos desee editar.
1. En el modo de selección de recursos, en ![Ver icono de tarjeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista de tarjeta) o en ![Ver icono de lista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista de lista), seleccione el recurso de vídeo.
1. En la barra de herramientas, haga clic en ![Icono de información](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Propiedades.
1. En la página Propiedades, seleccione la ficha **[!UICONTROL Pistas de subtítulos y audio]**.
1. Bajo el encabezado **Subtítulos**, haga clic en ![icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ProjectEdit_18_N.svg) a la derecha del nombre de archivo de un subtítulo.

   ![El icono Editar subtítulo bajo el encabezado de Subtítulos](/help/assets/dynamic-media/assets/msma-editcaption.png)

1. En el cuadro de diálogo **Editar subtítulo**, edite el texto del archivo WebVTT según sea necesario.

   ![Cuadro de diálogo Editar subtítulo](/help/assets/dynamic-media/assets/msma-editsubtitle-dialogbox.png)

1. En la esquina inferior derecha del cuadro de diálogo, haga clic en **Guardar**.


### Ver el estado del ciclo de vida de los archivos de subtítulos y pistas de audio cargados {#lifecycle-status-video}

Puede observar el estado del ciclo vital de cualquier subtítulo o archivo de pista de audio cargado en el vídeo principal. Puede hacerlo desde la pestaña **Subtítulos y pistas de audio** de **Propiedades**.

**Para ver el estado del ciclo de vida de un vídeo:**

1. Vaya al recurso de vídeo cuyo estado de ciclo vital desee ver.
1. En el modo de selección de recursos, en ![Ver icono de tarjeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista de tarjeta) o en ![Ver icono de lista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista de lista), seleccione el recurso de vídeo.
1. En la barra de herramientas, haga clic en ![Icono de información](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Propiedades.
1. En la página **Propiedades**, seleccione la pestaña **[!UICONTROL Pistas de subtítulos y audio]**.
1. En la columna **[!UICONTROL Estado]**, anote el estado de cada título o archivo de audio.

| Estado de los subtítulos y las pistas de audio | Descripción |
| --- | --- |
| Procesamiento | Cuando se añade y se guarda un nuevo pie de ilustración o archivo de pista de audio, pasa al estado &quot;Procesando&quot;. Dynamic Media procesa el archivo adjuntando el manifiesto de flujo continuo al vídeo principal. |
| Procesado | Una vez completado el procesamiento, el pie de ilustración o el archivo de pista de audio, o la pista de audio original asociada al vídeo principal, aparecen en estado &quot;Procesado&quot;. Puede obtener una vista previa de los archivos de subtítulos y pistas de audio que aparecen como &quot;Procesado&quot; *antes de* publicar el vídeo en directo. |
| Publicado | El estado &quot;Publicado&quot; representa un estado similar al estado &quot;Publicado&quot; de un vídeo principal. Assets se publican cuando se publica el vídeo principal y están disponibles en la URL pública de Dynamic Media. |
| Error | El estado &quot;failed&quot; significa que no se ha completado el procesamiento de un subtítulo o archivo de pista de audio. Elimine el pie de ilustración o el archivo de pista de audio y vuelva a cargarlo. |
| Una página sin publicar   | Cuando se cancela la publicación explícita de un vídeo principal publicado, también se cancela la publicación de cualquier subtítulo o archivo de pista de audio que haya agregado al vídeo. |


### Establecer el audio predeterminado para un vídeo que tiene varias pistas de audio

De forma predeterminada, el audio original de un vídeo se establece como el audio predeterminado que se va a reproducir.

Sin embargo, cualquier archivo de pista de audio cargado puede establecerse como audio predeterminado para que se reproduzca después de cargar un vídeo en el visualizador. En la interfaz de usuario Propiedades, en la ficha **Pistas de subtítulos y audio**, la etiqueta `Default` se aplica a la derecha del archivo de pista de audio para la reproducción de vídeo.

>[!NOTE]
>
>La reproducción del audio predeterminado también puede depender de lo que se establezca en los siguientes exploradores:
>
>* Chrome: se reproduce el audio predeterminado definido en el vídeo.
>* Safari: si el idioma predeterminado se establece en Safari, el audio se reproduce con el idioma predeterminado establecido, si está disponible con el manifiesto del vídeo. De lo contrario, se reproduce el audio predeterminado que se establece como parte de las propiedades de un vídeo.

**Para establecer el audio predeterminado de un vídeo que tiene varias pistas de audio:**

1. Vaya al recurso de vídeo cuya pista de audio predeterminada desee establecer.
1. En el modo de selección de recursos, en ![Ver icono de tarjeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista de tarjeta) o en ![Ver icono de lista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista de lista), seleccione el recurso de vídeo.
1. En la barra de herramientas, haga clic en ![Icono de información](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Propiedades.
1. En la página Propiedades, seleccione la ficha **[!UICONTROL Pistas de subtítulos y audio]**.
1. Bajo el encabezado **Pistas de audio**, seleccione el archivo de pista de audio que desee establecer como predeterminado para el vídeo.
1. Haga clic en ![Icono de audio](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Audio_18_N.svg) **[!UICONTROL Establecer como predeterminado]**.
1. En el cuadro de diálogo **Establecer como predeterminado**, haga clic en **[!UICONTROL Reemplazar]**.

   ![El encabezado Pistas de audio tiene un nombre de archivo de pista de audio seleccionado y se resaltó el botón &quot;Establecer como predeterminado&quot;.](/help/assets/dynamic-media/assets/msma-defaultaudiotrack.png)*Estableciendo la pista de audio predeterminada para un vídeo.*

1. En la esquina superior derecha, haz clic en **[!UICONTROL Guardar y cerrar]**.
1. Publique el vídeo. Consulte [Publicar recursos](publishing-dynamicmedia-assets.md).

### Vista previa de un vídeo con varios subtítulos y pistas de audio {#preview-video-audio-subtitle}

Una vez que los archivos de subtítulos y de pistas de audio se hayan cargado a un vídeo y procesado, puede utilizar el visualizador de vídeo de Dynamic Media para previsualizar todas las pistas. Al hacerlo, puede ver el aspecto y el sonido que tiene el vídeo para los clientes y garantizar que se comporte según lo esperado.

Cuando esté satisfecho con el vídeo, puede [publicarlo](publishing-dynamicmedia-assets.md) mediante cualquiera de los métodos siguientes.

Ver [Incrustar el visor de vídeo o de imágenes en una página web](/help/assets/dynamic-media/embed-code.md).
Ver [URL de vínculo a su aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md). El método de vinculación basado en URL no es posible si el contenido interactivo tiene vínculos con direcciones URL relativas, especialmente vínculos a páginas de Experience Manager Sites.
Consulte [Agregar Dynamic Media Assets a las páginas](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md).

>[!NOTE]
>
>La pestaña Vista previa de Experience Manager predeterminada no muestra varias pistas de subtítulos y audio. El motivo es que esas pistas están asociadas con Dynamic Media y solo se pueden ver con la previsualización del visualizador de Dynamic Media.

**Para obtener una vista previa de un vídeo que tiene varios subtítulos y pistas de audio:**

1. En **[!UICONTROL Assets]**, desplácese a un vídeo existente en el que haya agregado varios subtítulos y pistas de audio.
1. Haga clic en el recurso de vídeo para abrirlo en el modo de vista previa.
1. En la página de vista previa, cerca de la esquina superior izquierda de la página, haz clic en ![Icono de carril izquierdo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) ![Icono de cheurón abajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) y, a continuación, selecciona **[!UICONTROL Visualizadores]**.

   ![Lista desplegable que muestra la opción Visualizadores.](/help/assets/dynamic-media/assets/msma-selectviewers.png)

1. Cerca de la esquina superior izquierda de la página, haga clic en ![Icono de carril izquierdo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RailLeft_18_N.svg) Visualizadores ![Icono de cheurón hacia abajo](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) y, a continuación, seleccione el visualizador que desee utilizar para la vista previa del vídeo.

1. Cerca de la esquina inferior derecha de la página, haga clic en el icono de la burbuja de voz y, a continuación, seleccione el audio o subtítulo/pie de ilustración que desee oír, ver o ambos.

   ![La lista emergente Audio y subtítulos en el visor de vídeo.](/help/assets/dynamic-media/assets/msma-selectaudiosubtitle.png)*Simulación de un usuario que selecciona el audio y el pie de ilustración para la reproducción de vídeo.*

1. Para comenzar la reproducción, haga clic en ![icono PLay](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PlayCircle_22_N.svg).
Si lo desea, haga clic en ![Maximizar icono](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Maximize_22_N.svg) para maximizar la ventana de visualización.
Observe los botones **[!UICONTROL URL]** e **[!UICONTROL Incrustar]** cerca de la esquina inferior izquierda de la página. Use estos botones para [vincular la URL del vídeo a su aplicación web](/help/assets/dynamic-media/linking-urls-to-yourwebapplication.md) o para [incrustar el vídeo en una página web](/help/assets/dynamic-media/embed-code.md), respectivamente.
1. Cerca de la esquina superior derecha de la página de vista previa, haga clic en **[!UICONTROL Cerrar]**.

### Eliminar archivos de subtítulos o pistas de audio de un vídeo

Puede eliminar archivos de subtítulos o pistas de audio de un vídeo. La eliminación de archivos de subtítulos o pistas de audio publicados se refleja automáticamente en la dirección URL publicada del vídeo.

La pista de audio original extraída de un vídeo principal no se puede eliminar.

**Para eliminar archivos de subtítulos o pistas de audio de un vídeo:**

1. Vaya al recurso de vídeo cuya pista de audio predeterminada desee establecer.
1. En el modo de selección de recursos, en ![Ver icono de tarjeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista de tarjeta) o en ![Ver icono de lista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista de lista), seleccione el recurso de vídeo.
1. En la barra de herramientas, haga clic en ![Icono de información](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Propiedades.
1. En la página Propiedades, seleccione la ficha **[!UICONTROL Pistas de subtítulos y audio]**.
1. Realice una de las siguientes acciones:

   * Subtítulos: bajo el encabezado **Subtítulos**, seleccione uno o más archivos de subtítulos que desee eliminar del vídeo y, a continuación, haga clic en ![Eliminar icono](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Delete_22_N.svg) **[!UICONTROL Eliminar]**.
   * Pistas de audio: en el encabezado **Pistas de audio**, seleccione uno o más archivos de pista de audio que desee eliminar del vídeo y, a continuación, haga clic en ![Eliminar icono](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Delete_22_N.svg) **[!UICONTROL Eliminar]**.

1. En el cuadro de diálogo Eliminar, haga clic en **[!UICONTROL Aceptar]**.
1. Publique el vídeo.

### Descargar archivos de subtítulos o pistas de audio cargados en un vídeo

Puede descargar cualquier subtítulo o archivo de pista de audio que haya cargado para un vídeo. Tiene la opción de descargar todos los archivos seleccionados como un `.zip` o de crear una carpeta de descarga independiente para cada archivo.

No se puede descargar la pista de audio original extraída de un archivo de vídeo principal.

**Caso de uso:** La descarga de un archivo de subtítulos podría ser necesaria si encuentra un error en un archivo de `.vtt`. Simplemente descargue el archivo `.vtt` incorrecto, ábralo en un editor de texto sin formato y realice las correcciones pertinentes. Después de guardar el archivo de `.vtt`, cárguelo de nuevo. A continuación, use la opción **[!UICONTROL Traducir subtítulos]** para volver a traducir el archivo `.vtt` corregido.

**Para descargar los archivos de subtítulos o de pistas de audio que se cargaron en un vídeo:**

1. Vaya al recurso de vídeo cuya pista de audio predeterminada desee establecer.
1. En el modo de selección de recursos, en ![Ver icono de tarjeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista de tarjeta) o en ![Ver icono de lista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista de lista), seleccione el recurso de vídeo.
1. En la barra de herramientas, haga clic en ![Icono de información](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Propiedades.
1. En la página **Propiedades**, seleccione la pestaña **[!UICONTROL Pistas de subtítulos y audio]**.
1. Realice una de las siguientes acciones:

   * Subtítulos - Bajo el encabezado **Subtítulos**, seleccione uno o más archivos de subtítulos que desee descargar del vídeo y, a continuación, haga clic en ![Icono de descarga](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Download_22_N.svg) **[!UICONTROL Descargar]**.
   * Pistas de audio: en el encabezado **Pistas de audio**, seleccione uno o más archivos de pista de audio que desee descargar del vídeo y, a continuación, haga clic en ![Icono de descarga](https://spectrum.adobe.com/static/icons/workflow_22/Smock_Download_22_N.svg) **[!UICONTROL Descargar]**.

1. En el cuadro de diálogo Descargar, defina las siguientes opciones:

   | Opción Descargar | Descripción |
   |--- |--- |
   | Guardar como | Utilice el nombre de archivo predeterminado especificado en el campo de texto Guardar como o especifique su propio nombre. |
   | Cree una carpeta independiente para cada recurso | Cree una carpeta para cada archivo de rótulo o de pista de audio que haya seleccionado para la descarga. |
   | Correo electrónico | Utilice su programa de correo electrónico predeterminado para enviar el archivo .zip a una dirección de correo electrónico especificada. |
   | Recursos | Especifica el número de archivos que está descargando y el tamaño total combinado de todos los archivos seleccionados. Al anular la selección de esta opción, se atenúa (desactiva) el botón **[!UICONTROL Descargar]**, lo que impide que se descargue ningún archivo. |
   | Representaciones | Una representación hace referencia a una versión alternativa o a una vista previa del archivo original, normalmente una versión más pequeña o de menor resolución. Si se muestra como 0 B, es probable que signifique que no hay ninguna versión alternativa disponible o que es demasiado pequeño para registrar un tamaño. |

1. Seleccione **[!UICONTROL Descargar]**.
1. Publique el vídeo. Consulte [Publicar recursos](publishing-dynamicmedia-assets.md).

<!-- ## About AI-generated captions for videos in Dynamic Media

AI-powered captions in Dynamic Media are designed to enhance video accessibility and engagement by automatically generating accurate and synchronized subtitles. This technology uses advanced AI algorithms to transcribe spoken content into text, which is then displayed as captions on the video. Here are some key features.

* **Automatic Transcription:** The AI system transcribes spoken words from an existing audio file into text in real-time, ensuring that captions are generated quickly and accurately.
* **Multilingual Support:** It supports more than 60 languages, making it easier to reach a global audience. You can even translate your existing captions to different languages.
* **Enhanced Accessibility:** By providing captions, videos become more accessible to viewers who are deaf or hard of hearing, as well as those who prefer to watch videos with the sound off.
* **Improved Engagement:** Captions can help retain viewer attention and improve comprehension, especially in noisy environments or when the viewer's native language is different from the video's language.

These features in Dynamic Media make AI-powered video aptions a valuable tool for content creators looking to enhance their video content's accessibility and engagement. -->

## Añadir subtítulos opcionales a un vídeo {#adding-captions-to-video}

Puede ampliar el alcance de sus vídeos a los mercados globales añadiendo subtítulos a vídeos únicos o a conjuntos de vídeos adaptables. Al añadir subtítulos opcionales, evitará la necesidad de doblar el audio o la necesidad de utilizar hablantes nativos para volver a grabar el audio para cada idioma diferente. El vídeo se reproduce en el idioma en que se grabó. Los subtítulos en idiomas extranjeros aparecen para que las personas de diferentes idiomas puedan entender la parte de audio.

Los subtítulos opcionales también proporcionan una mayor accesibilidad para las personas sordas o con dificultades auditivas.

>[!NOTE]
>
>El reproductor de vídeo que utilice debe admitir la visualización de subtítulos.

Consulte también [Accesibilidad en Dynamic Media](/help/assets/dynamic-media/accessibility-dm.md).

Dynamic Media puede convertir archivos de rótulo al formato JSON (JavaScript Object Notation). Esta conversión significa que puede incrustar el texto JSON en una página web como una transcripción oculta pero completa del vídeo. Los motores de búsqueda pueden rastrear/indexar el contenido para que los vídeos sean más fáciles de descubrir y dar a los clientes más detalles sobre el contenido del vídeo.

Consulte [Servicio de contenido estático (que no es de imagen)](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/c-serving-static-nonimage-contents#image-serving-api) para obtener más información sobre el uso de la función JSON en una dirección URL.

**Para agregar subtítulos a un vídeo:**

1. Utilice una aplicación o un servicio de terceros para crear el archivo de rótulo de vídeo.

   Asegúrese de que el archivo que crea sigue el estándar WebVTT (Web Video Text Track). La extensión de nombre de archivo de subtítulos es `.vtt`. Puede obtener más información sobre el estándar de subtítulos WebVTT.

   Ver [WebVTT: el formato de seguimiento de texto de vídeo web](https://w3c.github.io/webvtt/).

   Hay muchos sitios web que ofrecen herramientas y servicios gratuitos y de primera calidad que puede utilizar para crear archivos de subtítulos WebVTT fuera de Dynamic Media.

Siga las instrucciones en pantalla de un sitio para crear y guardar el archivo WebVTT. Cuando haya terminado, copie el contenido del archivo de rótulo y péguelo en un editor de texto sin formato y guárdelo con la extensión de nombre de archivo VTT.

>[!NOTE]
>
>Para ofrecer compatibilidad global con subtítulos de vídeo en varios idiomas, el estándar WebVTT requiere que cree `.vtt` archivos y llamadas independientes para cada idioma que desee admitir.

Por lo general, desea asignar el mismo nombre al archivo de rótulo `.vtt` que al archivo de vídeo y anexarlo con la configuración regional de idioma, como -EN, -FR o -DE. Al hacerlo, puede ayudarle con la automatización de la generación de las direcciones URL de vídeo mediante el sistema WCM existente.

1. En Experience Manager, cargue el archivo de subtítulos WebVTT en DAM.
1. Vaya al recurso de vídeo *publicado* para asociarlo al archivo de subtítulos que ha cargado.

   Recuerde que las direcciones URL solo están disponibles para copiarse *después* de *publicar* los recursos por primera vez.

   Consulte [Publicar recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md).

1. Realice una de las siguientes acciones:

   * Para obtener una experiencia de visor de vídeo emergente, haga clic en el botón **[!UICONTROL URL]**. En el cuadro de diálogo URL, seleccione y copie la URL en el Portapapeles y, a continuación, pegue la URL en un editor de texto simple. Anexe la URL copiada del vídeo con la siguiente sintaxis:

     `&caption=<server_path>/is/content/<path_to_caption.vtt_file,1>`

     Observe `,1` al final de la ruta de acceso del título. Inmediatamente después de la extensión de nombre de archivo VTT en la ruta, opcionalmente puede habilitar (activar) o deshabilitar (desactivar) el botón de subtítulos opcionales en la barra del reproductor de vídeo estableciendo en `,1` o `,0`, respectivamente.

   * Para obtener una experiencia de visor de vídeo integrada, haga clic en **[!UICONTROL Código incrustado]**. En el cuadro de diálogo Código incrustado, seleccione, copie el código incrustado en el Portapapeles y, a continuación, pegue el código en un editor de texto simple. Anexe el código incrustado copiado con la siguiente sintaxis:

     `videoViewer.setParam("caption","<path_to_caption.vtt_file,1>");`

     Observe `,1` al final de la ruta de acceso del título. Inmediatamente después de la extensión de nombre de archivo VTT en la ruta, opcionalmente puede habilitar (activar) o deshabilitar (desactivar) el botón de subtítulos opcionales en la barra del reproductor de vídeo estableciendo en `,1` o `,0`, respectivamente.

## Añadir marcadores de capítulo al vídeo {#adding-chapter-markers-to-video}

Puede facilitar la visualización y navegación de los vídeos de formato largo añadiendo marcadores de capítulo a vídeos únicos o a conjuntos de vídeos adaptables. Cuando un usuario reproduce el vídeo, puede seleccionar los marcadores de capítulo en la cronología del vídeo (también conocida como selección manual de vídeo). Pueden desplazarse fácilmente a su punto de interés o ir inmediatamente a nuevos contenidos, formación y demostraciones.

>[!NOTE]
>
>El reproductor de vídeo utilizado debe admitir el uso de marcadores de capítulo. Los reproductores de vídeo de Dynamic Media no admiten marcadores de capítulo, pero es posible que el uso de reproductores de vídeo de terceros no los admita.

<!-- OBSOLETE CONTENT OBSOLETE CONTENT If desired, you can create and brand your own custom video viewer with chapters instead of using a video viewer preset. For instructions on creating your own HTML5 viewer with chapter navigation, in the Adobe Scene7 Viewer SDK for HTML5 guide, reference the heading "Customizing Behavior Using Modifiers" under the classes `s7sdk.video.VideoPlayer` and `s7sdk.video.VideoScrubber`. The Adobe Scene7 Viewer SDK is available as a download from [Adobe Developer Connection](https://help.adobe.com/en_US/scene7/using/WSef8d5860223939e2-43dedf7012b792fc1d5-8000.html). -->

Puede crear una lista de capítulos para el vídeo de la misma manera que crea subtítulos. Es decir, se crea un archivo WebVTT. Sin embargo, tenga en cuenta que este archivo debe ser independiente de cualquier archivo de subtítulos WebVTT. No se pueden combinar subtítulos y capítulos en un archivo WebVTT.

Puede utilizar el siguiente ejemplo como ejemplo del formato que utiliza para crear un archivo WebVTT con navegación por capítulos:

### Archivo WebVTT con navegación por capítulos de vídeo {#webvtt-file-with-video-chapter-navigation}

```xml {.line-numbers}
WEBVTT
Chapter 1
00:00.000 --> 01:04.364
The bicycle store behind it all.
Chapter 2
01:04.364 --> 02:00.944
Creative Cloud.
Chapter 3
02:00.944 --> 03:02.937
Ease of management for a working solution.
Chapter 4
03:02.937 --> 03:35.000
Cost-efficient access to rapidly evolving technology.
```

En el ejemplo anterior, `Chapter 1` es el identificador de referencia y es opcional. La hora de referencia de `00:00:000 --> 01:04:364` especifica la hora de inicio y finalización del capítulo, en formato `00:00:000`. Los tres últimos dígitos son milisegundos y pueden dejarse como `000`, si se prefiere. El título de capítulo de `The bicycle store behind it all` es la descripción real del contenido del capítulo. El identificador de referencia, el tiempo de referencia inicial y el título del capítulo aparecen en una ventana emergente del reproductor de vídeo cuando un usuario pasa el puntero del ratón sobre un punto de referencia visual en la cronología.

Como está utilizando un visor de vídeo HTML5, asegúrese de que el archivo de capítulo que cree sigue el estándar WebVTT (Web Video Text Tracks). La extensión del nombre de archivo del capítulo es `.vtt`. Puede obtener más información sobre el estándar de subtítulos WebVTT.

Ver [WebVTT: el formato de seguimiento de texto de vídeo web](https://w3c.github.io/webvtt/).

**Para agregar marcadores de capítulo a un vídeo:**

1. Guarde el archivo `.vtt` con la codificación UTF8 para evitar problemas con la representación de caracteres en el texto del título del capítulo.

   Por lo general, desea asignar al archivo VTT del capítulo el mismo nombre que al archivo de vídeo y anexarlo con capítulos. Al hacerlo, puede ayudarle con la automatización de la generación de las direcciones URL de vídeo mediante el sistema WCM existente.
1. En Experience Manager, cargue el archivo de capítulo WebVTT.

   Consulte [Cargar recursos](/help/assets/manage-digital-assets.md#uploading-assets).

1. Realice una de las siguientes acciones:

   <table>
     <tbody>
      <tr>
       <td>Para obtener una experiencia de visor de vídeo emergente,</td>
       <td>
       <ol>
       <li>Vaya al recurso de vídeo <i>publicado </i>para asociarlo al archivo de capítulo que ha cargado. Recuerde que las direcciones URL solo están disponibles para copiarse <i>después</i> de <i>publicar</i> los recursos por primera vez. Ver <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Publicación de Assets.</a></li>
       <li>En el menú desplegable, seleccione <strong>Visualizadores</strong>.</li>
       <li>En el carril izquierdo, seleccione el nombre del ajuste preestablecido de visualizador de vídeo. Se abrirá una vista previa del vídeo en una página independiente.</li>
       <li>En el carril izquierdo, al final, haga clic en el botón <strong>URL</strong>.</li>
       <li>En el cuadro de diálogo URL, seleccione y copie la URL en el Portapapeles, después pegue la URL en un editor de texto simple.</li>
       <li>Anexe la URL copiada del vídeo con la siguiente sintaxis para que pueda asociarla con la URL copiada al archivo de capítulo:<br /> <br /> <code>&navigation=<<i>full_copied_URL_path_to_chapter_file</i>.vtt></code><br /> </li>
       </ol> </td>
      </tr>
      <tr>
       <td>Para una experiencia de visor de vídeo incrustado,<br /> </td>
       <td>
       <ol>
       <li>Vaya al recurso de vídeo <i>publicado </i>para asociarlo al archivo de capítulo que ha cargado. Recuerde que las direcciones URL solo están disponibles para copiarse <i>después</i> de <i>publicar</i> los recursos por primera vez. Ver <a href="/help/assets/dynamic-media/publishing-dynamicmedia-assets.md">Publicación de Assets.</a></li>
       <li>En el menú desplegable, seleccione <strong>Visualizadores</strong>.</li>
       <li>En el carril izquierdo, seleccione el nombre del ajuste preestablecido de visualizador de vídeo. Se abrirá una vista previa del vídeo en una página independiente.</li>
       <li>En el carril izquierdo, en la parte inferior, seleccione <strong>Insertar</strong>.</li>
       <li>En el cuadro de diálogo Código incrustado, seleccione, copie todo el código en el Portapapeles y péguelo en un editor de texto simple.</li>
       <li>Anexe el código incrustado del vídeo con la siguiente sintaxis para que pueda asociarlo a la dirección URL copiada del archivo de capítulo:<br /> <br /> <code>videoViewer.setParam("navigation","&lt;<i>full_copied_URL_path_to_chapter_file</i>.vtt>"</code></li>
       </ol> </td>
      </tr>
     </tbody>
   </table>


## Acerca de las miniaturas {#about-video-thumbnails}

Una miniatura de vídeo es una versión de tamaño reducido de un fotograma de vídeo o un recurso de imagen que representa el vídeo para el cliente. La miniatura debe servir para animar a un cliente a seleccionar el vídeo.

Todos los vídeos de Experience Manager deben tener una miniatura asociada. De forma predeterminada, al cargar un vídeo en Experience Manager, se utiliza el primer fotograma como miniatura. Sin embargo, puede personalizar la miniatura para fines de personalización de marca o búsqueda visual. Al personalizar una miniatura de vídeo, puede reproducir el vídeo y pausar el fotograma que desee utilizar. O bien, puede seleccionar un recurso de imagen que ya ha cargado y *publicado* en su administrador de recursos digitales.

Cuando se cambia la miniatura de un vídeo, se omite la generación de miniaturas mediante el servicio Asset Compute al reprocesar el vídeo.

La capacidad de personalizar una miniatura de vídeo solo está disponible después de haber aplicado un perfil de vídeo a la carpeta en la que se encuentra el vídeo.

### Añadir una miniatura de vídeo personalizada {#adding-a-custom-video-thumbnail}

1. Asegúrese de haber realizado ya lo siguiente:

   * Se ha creado una carpeta para los recursos de vídeo.
   * [Se aplicó un perfil de vídeo a la carpeta](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).

   * [Cargó sus vídeos en la carpeta](/help/assets/manage-video-assets.md#upload-and-preview-video-assets).


1. Vaya a un recurso de vídeo cargado cuya imagen en miniatura desee cambiar.
1. En el modo de selección de recursos, en ![Ver icono de tarjeta](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewCard_18_N.svg) (Vista de tarjeta) o en ![Ver icono de lista](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) (Vista de lista), seleccione el recurso de vídeo.
1. En la barra de herramientas, haga clic en ![Icono de información](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) Propiedades.
1. En la página Propiedades del vídeo, haga clic en **[!UICONTROL Cambiar miniatura]**.
1. En el cuadro de diálogo Cambiar miniatura, siga uno de estos procedimientos:

   * Para utilizar un fotograma del vídeo como nueva miniatura:

      * En la barra de herramientas, haga clic en la ficha **[!UICONTROL Seleccionar fotograma del vídeo]**.
      * Haga clic en ![icono de reproducción](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PlayCircle_22_N.svg).
      * Haga clic en ![Icono de pausa](https://spectrum.adobe.com/static/icons/workflow_22/Smock_PauseCircle_22_N.svg) en el fotograma que quiera capturar como nueva miniatura del vídeo.

   * Para utilizar un recurso de imagen como nueva miniatura:

      * En la barra de herramientas, haga clic en la ficha **[!UICONTROL Seleccionar miniatura de Assets]**.
      * Haga clic en el botón **[!UICONTROL Seleccionar miniatura]**.
      * Vaya a un recurso de imagen previamente cargado y publicado que desee utilizar. El recurso cambia de tamaño automáticamente para servir como imagen en miniatura del vídeo.
      * Seleccione el recurso de imagen y, a continuación, haga clic en **[!UICONTROL Seleccionar]**.

1. En el cuadro de diálogo Cambiar miniatura, haga clic en **[!UICONTROL Guardar cambio]**.
1. En la página Propiedades del vídeo, en la esquina superior derecha, haz clic en **[!UICONTROL Guardar y cerrar]** o en **[!UICONTROL Guardar]**.



<!--

## About video thumbnails in Dynamic Media Hybrid mode{#about-video-thumbnails-in-dynamic-media-hybrid-mode}

You can choose from one of ten thumbnail images automatically generated by Dynamic Media to add to your video. The video player displays your selected thumbnail when a video asset is used with the Dynamic Media component in the authoring environment of Experience Manager Sites, Experience Manager Mobile, or Experience Manager Screens. The thumbnail serves as a static picture that best represents the contents of your entire video and further encourages users to select the Play button.

Based on the total time of the video, Dynamic Media captures ten (default) thumbnail images at 1%, 11%, 21%, 31%, 41%, 51%, 61%, 71%, 81%, and 91% into the video. The ten thumbnails persist meaning that if you decide to choose a different thumbnail later on, you do not need to regenerate the series. You preview the ten thumbnail images and then select the one you want to use with your video. If you want to change to default you can use CRXDE Lite to configure the time interval that thumbnail images are generated. For example, if you only wanted to generate a series of four evenly spaced thumbnail images from your video, you can configure the interval time at 24%, 49%, 74%, and 99%.

Ideally, you can add a video thumbnail anytime after you upload your video but before you publish the video on your website.

If you prefer, you can choose to upload a custom thumbnail to represent your video instead of using a thumbnail generated by Dynamic Media. For example, you could create a custom thumbnail image that has the title of your video, an eye-catching opening image, or a very specific image captured from your video. The custom video thumbnail image that you upload should have a maximum resolution of 1280 &times; 720 pixels (minimum width of 640 pixels) and be no larger than 2MB.

See also [About video thumbnails](/help/assets/dynamic-media/video.md#about-video-thumbnails-in-dynamic-media-scene-mode).

-->

<!--

### Adding a video thumbnail {#adding-a-video-thumbnail}

1. Navigate to an uploaded video asset that you want to add a video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Select Frame]**.

   Dynamic Media generates a series thumbnail images from your video, based on the default time interval or time interval you customized.

1. Preview the generated thumbnail images, then select the one you want to add to your video.
1. Select **[!UICONTROL Save Change]**.

   The video's thumbnail image is updated to use the thumbnail you selected. If you later decide to change the thumbnail image, you can return to the **[!UICONTROL Change Thumbnail]** page and select a new one.

   If you configured new default time intervals, or you uploaded a new video to replace the existing video, you need to have Dynamic Media regenerate the thumbnails.

   See [Configuring the default time interval that video thumbnails are generated](#configuring-the-default-time-interval-that-video-thumbnails-are-generated).

-->

<!--

#### Configuring the default time interval that video thumbnails are generated {#configuring-the-default-time-interval-that-video-thumbnails-are-generated}

When you configure and save the new default time interval, your change automatically applies only to videos that you upload in the future. It does not automatically apply the new default to videos that you previously uploaded. For existing videos, you must regenerate the thumbnails.

See [Adding a video thumbnail](#adding-a-video-thumbnail).

**To configure the default time interval that video thumbnails are generated,**

1. In Experience Manager, navigate to **[!UICONTROL Tools]** > **[!UICONTROL General]** > **[!UICONTROL CRXDE Lite]**.

1. In the CRXDE Lite page, in the directory panel on the left, navigate t `o etc/dam/imageserver/configuration/jcr:content/settings.`

   if the directory panel is not visible, you may need to select the >> icon to the left of the Home tab.

1. On the lower-right panel, in the Properties tab, double-select `thumbnailtime`.
1. In the Edit thumbnailtime dialog box, use the text fields to enter interval values as percentages.

    * Select the plus sign (+) icon to add one or more interval value fields. You may need to scroll to the bottom of the dialog box to see the icon.
    * Select the minus sign (-) icon to the right of an interval value field to delete it from the list.
    * Select the up arrow icon and the down arrow icon to reorder the interval values.

1. Select **[!UICONTROL OK]** to return to the Properties tab.
1. Near the upper-left corner of the CRXDE Lite page, select **[!UICONTROL Save All]**, then select the Back Home icon in the upper-left corner to return to Experience Manager.

   See [Adding a video thumbnail](#adding-a-video-thumbnail).

-->

<!--

### Adding a custom video thumbnail {#adding-a-custom-video-thumbnail-1}

These steps apply only to Dynamic Media running in Hybrid mode.

T**o add a custom video thumbnail**,

1. Navigate to an uploaded video asset that you want to add a custom video thumbnail.
1. In asset selection mode either from the List View or the Card View, select the video asset.
1. On the toolbar, select the **[!UICONTROL View Properties]** icon (a circle with an "i" in it).
1. On the video's Properties page, select **[!UICONTROL Change Thumbnail]**.
1. On the Change Thumbnail page, on the toolbar, select **[!UICONTROL Upload New Thumbnail]**.
1. Navigate to a thumbnail image you want to use, select it, then select **[!UICONTROL Open]** to begin uploading the image into Experience Manager. Following the upload, be sure you publish the image.
1. After you have successfully uploaded and published the image, in the Change Thumbnail page, select **[!UICONTROL Save Changes]**.

   The custom thumbnail is added to your video.

-->

## Cambio de la URL de Dynamic Media para los recursos de Dynamic Media

Los visualizadores listos para usar pueden reproducir vídeos procesados en Dynamic Media. También puede reproducirlos accediendo directamente a las direcciones URL de manifiesto y utilizando sus propios visores personalizados. A continuación se muestra la API para recuperar las URL de manifiesto de un vídeo.

### Acerca de la API de getVideoManifestURI

La API `getVideoManifestURI`se expone a través de c`q-scene7-api:com.day.cq.dam.scene7.api` y se puede usar para generar las siguientes direcciones URL de manifiesto:

```java
/**   
* Returns the manifest url for videos 
* @param resource video resource 
* @param manifestType type of video streaming manifest being requested 
* @param onlyIfPublished return a manifest only if the video is published 
* @return the manifest url for videos 
* 
* @throws Exception 
*/
@Nullable 
String getVideoManifestURI(Resource resource, ManifestType manifestType, boolean onlyIfPublished) throws Exception;
```

#### Parámetros de API getVideoManifestURI

Esta API emplea los tres parámetros siguientes:

| Parámetro | Descripción |
| --- | --- |
| `resource` | El recurso correspondiente al vídeo que Dynamic Media ha introducido. |
| `manifestType` | Puede ser `ManifestType.DASH` o `ManifestType.HLS` |
| `onlyIfPublished` | Se establece en true en caso de que el URI de manifiesto se genere solo si está publicado y disponible en el nivel de envío. |

Para recuperar las URL de manifiesto de los vídeos mediante el método anterior, añada un [perfil de codificación de vídeo](/help/assets/dynamic-media/video-profiles.md#creating-a-video-encoding-profile-for-adaptive-streaming) a una carpeta &quot;cargar vídeos&quot;. Dynamic Media procesa estos vídeos en función de las codificaciones encontradas en el archivo de codificación de vídeo asignado a la carpeta. Ahora puede invocar la API anterior para recuperar las direcciones URL de manifiesto para los vídeos cargados.

### Escenarios de error

La API devuelve un valor nulo si hay errores. Las excepciones se registran en los registros de errores de Experience Manager. Todos estos errores registrados comienzan con `Could not generate Video Manifest URI`. Los siguientes escenarios pueden provocar estos errores:

* Se registra un(a) `IllegalArgumentException` para cualquiera de los siguientes elementos:

   * El parámetro `resource` pasado es nulo.
   * El parámetro `resource` pasado no es un vídeo.
   * El parámetro `manifestType` pasado es nulo.
   * El parámetro `onlyIfPublished` se pasó como true, pero el vídeo no se publicó.
   * El vídeo no se ha introducido con un conjunto de vídeos adaptable de Dynamic Media.

* `IOException` se registra cuando hay un problema al conectarse a Dynamic Media.
* `UnsupportedOperationException` se registra cuando se pasa un parámetro `manifestType` que es `ManifestType.DASH`, mientras que el vídeo no se ha procesado con el formato DASH.

<!-- THE REMAINING SECTION IS FOR 6.5 ONLY 

The following is an example of the above API using servlets written in *HTTPWhiteBoard* specification. Select each tab for the code syntax.

>[!BEGINTABS]

>[!TAB Add dependency in pom.xml]

+++**Add dependency in pom.xml** 

```java
dependency> 
     <groupId>com.day.cq.dam</groupId> 
     <artifactId>cq-scene7-api</artifactId> 
     <version>5.12.64</version> 
     <scope>provided</scope> 
</dependency> 
```

+++

>[!TAB Sample servlet]

+++**Sample servlet** 

```java
@Component
        service = Servlet.class 
) 
@HttpWhiteboardServletPattern(value = ManifestServlet.SERVLET_PATTERN) 
@HttpWhiteboardContextSelect(value = Constants.SERVLET_CONTEXT_SELECTOR) 
public class ManifestServlet extends HttpServlet { 

   private static final Logger LOGGER = LoggerFactory.getLogger(ManifestServlet.class); 

   private final ObjectMapper objectMapper; 

    @Reference 
    private Scene7Service scene7Service; 

   public static final String SERVLET_PATTERN = Constants.VIDEO_API_PREFIX + "/manifestUrl"; 

   public ManifestServlet() {
         this.objectMapper = new ObjectMapper(); 
         objectMapper.setSerializationInclusion(JsonInclude.Include.NON_NULL); 
   }

   @Override 

   protected void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException {
        final ResourceResolver resolver = getResourceResolver(request); 
        String assetPath = request.getParameter("assetPath"); 
        String manifest = request.getParameter("manifestType"); 
        String onlyIfPublished = request.getParameter("onlyIfPublished"); 
        Resource resource = resolver.getResource(assetPath); 
        response.setCharacterEncoding(StandardCharsets.UTF_8.toString()); 
        response.setContentType("application/json"); 
        if(resource == null) { 
            LOGGER.info("could not retrieve the resource from JCR"); 
            error("could not retrieve the resource from JCR", response); 
            return; 
        }

        String manifestUri = null; 

        try{ 
            ManifestType manifestType =  ManifestType.DASH; 
            if(manifest != null) { 
                manifestType = ManifestType.valueOf(manifest); 
            } 
            manifestUri = scene7Service.getVideoManifestURI(resource, manifestType, onlyIfPublished != null); 
            objectMapper.writeValue(response.getWriter(), new ManifestUrl(manifestUri)); 
            response.setContentType("application/json"); 
        } catch (Exception e) { 
            LOGGER.error(e.getMessage(), e); 
            error(String.format("Unable to get the manifest url for %s. %s", assetPath, e.getMessage()), response); 
        } 
    } 

    private ResourceResolver getResourceResolver(HttpServletRequest request) { 
        Object rr = request.getAttribute(AuthenticationSupport.REQUEST_ATTRIBUTE_RESOLVER); 
        if (!(rr instanceof ResourceResolver)) { 
            throw new IllegalStateException( 
                    "The request does not seem to have been created via Apache Sling's authentication mechanism."); 
        } else { 
            return (ResourceResolver) rr; 
        } 
    } 

    private void error(String errorMessage, HttpServletResponse response) throws IOException { 
        ManifestUrl errorManifest = new ManifestUrl(null); 
        errorManifest.setErrorMessage(errorMessage); 
        response.setStatus(HttpServletResponse.SC_INTERNAL_SERVER_ERROR); 
        objectMapper.writeValue(response.getWriter(), errorManifest); 
    } 
} 
```

+++

>[!TAB Response Class for servlet]

+++**Response Class for servlet** 

```java
public class ManifestUrl extends VideoResponse { 
     String manifestUrl; 
     public ManifestUrl(String manifestUrl) { 
         this.manifestUrl = manifestUrl; 
     } 
     public String getManifestUrl() { 
         return manifestUrl; 
     } 
} 

public abstract class VideoResponse { 
     String errorString; 

     public String getErrorString() { 
         return errorString; 
     } 

     public void setErrorMessage(String errorString) { 
         this.errorString = errorString; 
     } 
} 
```

+++

>[!TAB Constants file referenced in servlet]

+++**Constants file referenced in servlet** 

```java
public final class Constants { 

     private Constants() { 
     } 

     public static final String VIDEO_API_PREFIX = "/dynamicmedia/video"; 
     public static final String SERVLET_CONTEXT_SELECTOR = "(" + HttpWhiteboardConstants.HTTP_WHITEBOARD_CONTEXT_NAME + "=" + 
             DMSampleApiHttpContext.CONTEXT_NAME + ")"; 

 } 
```

+++

>[!TAB ServletContext]

+++**ServletContext** 

Mount the above servlet using a `servletContext`. The following is an example of `servletContext`. 

```java
public class DMSampleApiHttpContext extends ServletContextHelper { 

 public static final String CONTEXT_NAME = "com.adobe.dmSample"; 
 public static final String CONTEXT_PATH = "/dmSample"; 

 private final MimeTypeService mimeTypeService; 

 private final AuthenticationSupport authenticationSupport; 

 /** 
  * Constructs a new context that will use the given dependencies. 
  * 
  * @param mimeTypeService Used when providing mime type of requests. 
  * @param authenticationSupport Used to authenticate requests with sling. 
  */ 
 @Activate 
 public DMSampleApiHttpContext(@Reference final MimeTypeService mimeTypeService, 
                               @Reference final AuthenticationSupport authenticationSupport) { 
     this.mimeTypeService = mimeTypeService; 
     this.authenticationSupport = authenticationSupport; 
 } 

 // ---------- HttpContext interface ---------------------------------------- 
 /** 
  * Returns the MIME type as resolved by the <code>MimeTypeService</code> or 
  * <code>null</code> if the service is not available. 
  */ 
 @Override 
 public String getMimeType(String name) { 
     MimeTypeService mtservice = mimeTypeService; 
     if (mtservice != null) { 
         return mtservice.getMimeType(name); 
     } 
     return null; 
 } 

 /** 
  * Returns the real context path that is used to mount this context. 
  * @param req servlet request 
  * @return the context path 
  */ 
 public static String getRealContextPath(HttpServletRequest req) { 
     final String path = req.getContextPath(); 
     if (path.equals(CONTEXT_PATH)) { 
         return ""; 
     } 
     return path.substring(CONTEXT_PATH.length()); 
 } 

 /** 
  * Returns a request wrapper that transforms the context path back to the original one 
  * @param req request 
  * @return the request wrapper 
  */ 
 public static HttpServletRequest createContextPathAdapterRequest(HttpServletRequest req) { 
     return new HttpServletRequestWrapper(req) { 

         @Override 
         public String getContextPath() { 
             return getRealContextPath((HttpServletRequest) getRequest()); 
         } 

     }; 

 } 

 /** 
  * Always returns <code>null</code> because resources are all provided 
  * through individual endpoint implementations. 
  */ 
 @Override 
 public URL getResource(String name) { 
     return null; 
 } 

 /** 
  * Tries to authenticate the request using the 
  * <code>SlingAuthenticator</code>. If the authenticator or the Repository 
  * is missing this method returns <code>false</code> and sends a 503/SERVICE 
  * UNAVAILABLE status back to the client. 
  */ 
 @Override 
 public boolean handleSecurity(HttpServletRequest request, 
                               HttpServletResponse response) throws IOException { 

     final AuthenticationSupport authenticator = this.authenticationSupport; 
     if (authenticator != null) { 
         return authenticator.handleSecurity(createContextPathAdapterRequest(request), response); 
     } 

     // send 503/SERVICE UNAVAILABLE, flush to ensure delivery 
     response.sendError(HttpServletResponse.SC_SERVICE_UNAVAILABLE, 
             "AuthenticationSupport service missing. Cannot authenticate request."); 
     response.flushBuffer(); 

     // terminate this request now 
     return false; 
 } 
}
```

+++

>[!ENDTABS]



### Use the sample servlet

You invoke the servlet by performing a `GET` operation at `/dmSample/dynamicmedia/video/manifestUrl`. The following query parameters are passed: 

| Query parameter | Description |
| --- | --- |
| `assetPath` | Mandatory. The path to the video for which `manifestUrl` is generated. |
| `manifestType` | Optional. Parameter can be DASH or HLS. If it is not passed, it defaults to DASH. |
| `onlyIfPublished` | Optional. If passed, the `manifestUrl` is returned only if the video is published.  |

In this example, let us assume the following setup: 

* The company is `samplecompany`.
* The authoring instance is `http://sample-aem-author.com`.
* The folder `/content/dam/video-example` has a video encoding profile applied to it. 
* The video `scenery.mp4` is uploaded to the folder `/content/dam/video-example`.

You can invoke the servlet in following ways: 
     
| Type | Description |
| :--- | --- |
| HLS | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=HLS&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8?packagedStreaming=true"}`<br><br>In case DASH delivery is disabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.m3u8"}` |
| DASH | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scenery.mp4`<br><br>In case DASH delivery is enabled:<br>`{"manifestUrl":"https://s7d1.scene7.com/is/content/samplecompany/scenery-AVS.mpd"}`<br><br>In case DASH delivery is disabled:<br>`{}` |
| Error: asset path is wrong | `http://sample-aem-author.com/dmSample/dynamicmedia/video/manifestUrl?manifestType=DASH&assetPath=/content/dam/video-example/scennnnnnery.mp4`<br><br>`{"errorString":"could not retrieve the resource from JCR"}` |

-->


<!-- REMOVED THE FOLLOWING TOPIC AS PER EMAIL FROM RIYA MIDHA, WEDNESDAY, MARCH 5, 2025; TOPIC IS OBSOLETE/NO LONGER NEEDED BECAUSE THE FEATURES IT DESCRIBES ARE NOW GA WITHIN THE SOFTWARE

## Enable DASH, multi-captions and multi-audio tracks, and AI-generated captions support on your Dynamic Media account {#enable-dash}

You can enable support in Dynamic Media for:

* DASH
* Multi-captions and audio tracks
* AI-generated captions (Limited Availability)

By creating and submitting an Adobe Customer Support case. 

Enabling any of the above three capabilities, enables all of them. So, if you only want DASH enabled, you are actually enabling all three capabilities listed above.  

| Capability | Description |
| --- | --- |
| DASH | DASH (Digital Adaptive Streaming over HTTP) is the international standard for video streaming and is widely adopted across different video viewers. When DASH is enabled on your account, you get the option to choose from either DASH or HLS for adaptive video streaming. Or, you can opt for both with automatic switching between players when **[!UICONTROL auto]** is selected as the playback type in the Viewer preset.<br>Some key benefits from enabling DASH on your account include the following:<ul><li>Package DASH stream video for adaptive bitrate streaming. This method leads to higher efficiency of delivery. Adaptive streaming ensures the best viewing experience for your customers.</li><li>Browser optimized streaming with Dynamic Media players switches between HLS and DASH streaming to ensure the best quality of service. The video player auto-switches to HLS when a Safari browser is used.</li><li>You can configure your preferred streaming method (HLS or DASH) by editing the video viewer preset.</li><li>Optimized video encoding ensures that no additional storage is used while enabling DASH capability. A single set of video encodings is created for both HLS and DASH to optimize video storage costs.</li><li>Helps make video delivery more accessible for your customers.</li><li>Get the streaming URL by way of APIs, too.</li></ul>|
| Multi-captions and audio tracks | You can benefit from having multiple caption and audio track support automatically enabled. After enablement, all subsequent videos that you upload are processed with a new backend architecture that includes support for adding multiple caption and audio tracks to your videos. |
| AI-generated captions (Limited Availability) | Create captions for your videos powered by AI. Using AI, it creates the transcript of the video and converts it into captions. Even the timeline is defined, too. |

>[!IMPORTANT]
>
>Any videos that you uploaded *before* enabling multiple caption and audio track support on your Dynamic Media account, [must be reprocessed](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). This video reprocessing step is necessary so that multiple caption and audio track capability is available to them. The video URLs continue to work and play as usual, after reprocessing.

**To enable DASH, multi-captions and multi-audio tracks, and AI-generated captions support on your Dynamic Media account:** 

1. [Use the Admin Console to start the creation of a new support case](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).
1. To create a support case, follow the instructions while ensuring you provide the following information:

    * Primary contact name, email, phone.
    * Your Cloud Services environment (program ID and environment ID).
    * Your Dynamic Media company account name.
    * Your Dynamic Media region: North America (NA), Asia-Pacific (APAC), or Europe-Middle East-Asia (EMEA).
    * Specify that you want DASH, multi-captions and multi-audio tracks, and AI-generated captions (Limited Availability) support enabled on your Dynamic Media account, on AEM as a Cloud Service.
   
1. Adobe Customer Support adds you to the Customer Wait List based on the order in which requests are submitted.
1. When Adobe is ready to handle your request, Customer Support contacts you to coordinate and set a target date for enablement.
1. Adobe Customer Support notifies you after completion.
1. Now, do one or more of the following:

    * Create your [video viewer preset](/help/assets/dynamic-media/managing-viewer-presets.md#creating-a-new-viewer-preset) as usual.
    * Create your [video profile](/help/assets/dynamic-media/video-profiles.md) as usual.
    * [Add multiple captions and audio tracks](#add-msma) to your video. -->


<!-- 
## About multiple caption and audio track support for videos in Dynamic Media{#about-msma}

With multiple caption and audio track capability in Dynamic Media, you can easily add multiple captions and audio tracks to a primary video. This capability means that your videos are accessible to a global audience. You can customize a single, published primary video to a global audience in multiple languages and adhere with accessibility guidelines for different geographical regions. Authors can also manage the captions and audio tracks from a single tab in the user interface.

   ![Captions and audio tracks tab in Dynamic Media along with a table showing uploaded .VTT caption files and uploaded .MP3 audio track files for a video.](/help/assets/dynamic-media/assets/msma-caption-audiotracks-tab2.png)


Some of the use cases to consider for adding multiple captions and audio tracks to your primary video include the following:

| Type | Use case |
| --- | --- |
| Captions | Multiple language support<br>Descriptive text for accessibility |
| Audio tracks | Multiple language support<br>Commentary tracks<br>Descriptive audio |


All [video formats supported in Dynamic Media](/help/assets/file-format-support.md) and all Dynamic Media video viewers-except the Dynamic Media Video_360 viewer-are supported for use with multiple captions and audio tracks.

Multi-caption and multi-audio track capability is available for your Dynamic Media account by way of a feature toggle that must be enabled (turned on) by Adobe Customer Support.

### Add multiple captions and audio tracks to your video {#add-msma}

Before you add multiple caption and audio tracks to your video, be sure you already have the following in-place:

* Dynamic Media is set up in an AEM environment.
* A [Dynamic Media Video profile is applied to the folder where your videos are ingested](/help/assets/dynamic-media/video-profiles.md#applying-a-video-profile-to-folders).
* [Multi-caption, and multi-audio track is enabled on your Dynamic Media account](/help/assets/dynamic-media/video.md#enable-dash).

Added captions and captions are supported with WebVTT and Adobe VTT formats. And, added audio track files are supported with MP3 format.

>[!IMPORTANT]
>
>Any videos that you uploaded before enabling multiple caption and audio track support on your Dynamic Media account, [must be reprocessed](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets). This video reprocessing step is necessary so that multiple caption and audio track capability is available to them. The video URLs continue to work and play as usual, after reprocessing.

**To add multiple captions and audio tracks to your video:**

1. [Upload your primary video to a folder](/help/assets/manage-video-assets.md#upload-and-preview-video-assets) that already has a video profile assigned to it.
1. Navigate to the uploaded video asset that you want to add multiple caption and audio tracks.
1. In asset selection mode, either from the List View or the Card View, select the video asset.
1. On the toolbar, select the Properties icon (a circle with an "i" in it). 

   ![Asset properties button.](/help/assets/dynamic-media/assets/msma-selectedasset-propertiesbutton.png)*Selected video asset in Card View.*

1. On the video's Properties page, select the **[!UICONTROL Captions & Audio tracks]** tab.


   >[!TIP]
   >If you do not see the [!UICONTROL Captions & Audio tracks] tab, it means either one of two things:
   >* The folder in which the selected video resides does not have a video profile assigned to it. In which case, see [Apply a video profile to the folder](/help/assets/dynamic-media/video-profiles.md#applying-video-profiles-to-specific-folders)
   >* Or, Dynamic Media must reprocess the video. In which case, see [Reprocess Dynamic Media assets in a folder](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).

    When you have completed either one of the above tasks, return to these steps.

   ![Asset properties](/help/assets/dynamic-media/assets/msma-audiotracks.png)*Captions and audio tracks tab on the video's Properties page.*

1. (Optional) To add one or more caption files to a video, do the following:

    * Select **[!UICONTROL Upload Captions]**.
    * Navigate to, and select, one or more `.vtt` (Video Text Tracks) files and open them.
    * For captions to be visible on the media player, you must add required details (metadata) about each caption file that you uploaded. Select the pencil icon to the right of a caption file name. In the Edit Caption dialog box, enter the following required details about the file, then select **[!UICONTROL Save]**. Repeat this process for each caption file that you uploaded:


    | Caption metadata | Description | 
    | --- | --- | 
    Filename | The default filename is derived from the original filename. The filename can be changed only while uploading and cannot be changed later. Filename character requirements are the same as for AEM Assets.<br>The same filename cannot be used for additional caption files and audio track files. |
    | Language | Select the language of the caption. |
    | Type | Select the type of caption that you are using.<br>**Subtitle** - The caption text displayed with the video that translates or transcribes the dialogue.<br>**Caption** - The caption text includes background noises and speaker identification. It also includes other relevant details alongside the translation or transcription of dialogue. This functionality makes the content more accessible to individuals who are deaf or hard of hearing. |
    | Label | The text that is displayed for the caption's name in the **[!UICONTROL Select audio or caption]** pop-up list in the media player. The label is what a customer sees that corresponds to a subtitle or caption track. For example, English (CC). |

    You can change or edit caption metadata later, if necessary. When the video is published, these details are reflected on public URLs in published videos.

1. (Optional) To add one or more audio tracks to a video, do the following:

    * Select **[!UICONTROL Upload Audio Tracks]**.
    * Navigate to, and select, one or more .mp3 files and open them.
    * To make audio tracks visible in the **[!UICONTROL Select audio or caption]** pop-up list on the media player, add the required details for each audio track file. Ensure you include all necessary information for proper display. Select the pencil icon to the right of an audio track file name. In the Edit Audio Track dialog box, enter the following required details, then select **[!UICONTROL Save]**. Repeat this process for each audio track file that you uploaded.

    | Audio Track metadata | Description |
    | --- | --- |
    | Filename | The default filename is derived from the original filename. The filename can be changed only while uploading and cannot be changed later. Filename character requirements are the same as for AEM Assets.<br>The same filename cannot be used for additional audio track files or caption files.| 
    | Language | Select the language of the audio track. |
    | Type | Select the type of audio track that you are using.<br>**Original** - The audio track originally attached to the video and represented as `[Original]` in the label with English language selected by default. While **[!UICONTROL Label]** and **[!UICONTROL Language]** can be changed in the **[!UICONTROL Edit Audio Track]** dialog box, it defaults to the original values if the primary video is reprocessed.<br>**Standard** - An add-on audio track for a language other than the original.<br>**Audio description** - An audio track that also includes a descriptive narration of non-verbal actions and gestures in the video, making content more accessible for individuals who are visually impaired. |
    | Label | The text that is displayed as the audio track's name in the **[!UICONTROL Select audio or caption]** pop-up list in the media player. The label is what a customer sees that corresponds to an audio track. For example, `English [Original]`. The label of audio attached to a video is set to `[Original]` by default. |

    You can change or edit this audio track metadata later, if necessary. When the video is published, these details are reflected on public URLs in published videos.

1. In the upper-right corner of the page, from the **[!UICONTROL Save & Close]** drop-down list, select **[!UICONTROL Save]**. The files are uploaded and metadata processing begins, as seen in the Status column of the interface.

    >[!NOTE]
    >
    >Based on the caching settings of your instance, the metadata processing can take several minutes before it is reflected in preview and in published URLs.

1. (Optional) If you selected **[!UICONTROL Save & Close]** in the previous step, instead of selecting **[!UICONTROL Save]**, you can still view the processing status of the uploaded files. See [View the lifecycle status of uploaded caption and audio track files](/help/assets/dynamic-media/video.md#lifecycle-status-video).

1. (Optional) Preview the video before publishing to ensure the captions and audio work as expected. See [Preview a video that has multiple captions and audio tracks](/help/assets/dynamic-media/video.md#preview-video-audio-subtitle).

1. Publish the video. See [Publish assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md). -->






