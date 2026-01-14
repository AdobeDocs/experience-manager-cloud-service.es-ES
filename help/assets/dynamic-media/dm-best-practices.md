---
title: Prácticas recomendadas de Dynamic Media
description: Conozca las prácticas recomendadas en Dynamic Media a la hora de trabajar con imágenes y vídeo, y las prácticas recomendadas para los visualizadores de Dynamic Media.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Adaptive Streaming, Best Practices, Smart Imaging, Image Profiles, Rulesets, Viewers, Smart Crop, SEO Optimization, Publishing, Video, Renditions, Asset Management
role: User, Admin
mini-toc-levels: 4
exl-id: 39e491bb-367d-4c72-b4ca-aab38d513ac5
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '4048'
ht-degree: 0%

---

# Prácticas recomendadas de Dynamic Media{#about-dm-best-practices}

<!--**Organizations today must connect with their customers through an ever-growing array of channels and devices.** The customer experience spans physical stores, websites, mobile apps, social media, email, and e-commerce platforms. This diversity requires organizations to create many more versions of each piece of content. Personalization adds complexity by increasing the number of variations needed for each item. Despite budget constraints for content creation, there's still a need to produce more campaigns in the same timeframe, on a global scale. AEM Dynamic Media offers a comprehensive set of tools to meet these challenges, providing consistent, personalized, high-performance, and optimized brand experiences across all channels and devices. 

Key Features of AEM Dynamic Media:

* **Single File Approach:** Save on storage costs by storing just one master file. AEM Dynamic Media generates all size variations and visual effects on-demand, at the time of delivery, eliminating workflow complexity and last-minute creative changes.
* **Global Reach:** With Smart Imaging, images are automatically optimized during delivery, significantly reducing file size and page weight without sacrificing visual quality. This optimization is tailored for network bandwidth and device pixel ratio.
* **AI-Powered Efficiency:** Smart Crop uses AI to automate the cropping of images and videos, focusing on points of interest. This feature saves countless hours of manual editing and is designed for large-scale enterprise production.
* **Video Made Simple:** Upload a master video file and AEM Dynamic Media will adaptively stream it in multiple languages and with descriptive audio, ensuring a broad reach.
* **Customizable Experience Viewer:** Select, customize, and brand the experience viewers for images and videos with ease. These viewers can be seamlessly integrated into any digital experience.
* **Support for Emerging Formats:** AEM Dynamic Media is also your solution for delivering immersive 3D and panoramic experiences.

In the accompanying guide, you'll find a comprehensive list of best practices for maximizing the benefits of AEM Dynamic Media. As you embark on your Dynamic Media journey, make sure to consult these expert recommendations and resources.

Stage Business Problem Best Practice Recommendation: This section will outline specific business challenges and provide targeted best practices and recommendations to address them effectively. -->

{{see-also-dm}}

Las organizaciones se enfrentan a una explosión de canales y dispositivos para interactuar con los usuarios. El recorrido del cliente abarca tiendas físicas, web, móviles, medios sociales, correos electrónicos y comercio. Para satisfacer esta demanda, Dynamic Media en Adobe Experience Manager (AEM) ofrece una solución completa. Optimiza la entrega de recursos, gestiona la personalización y garantiza experiencias coherentes, de rendimiento y alineadas con la marca en todos los canales y dispositivos.

Algunos de los principios clave de Dynamic Media son los siguientes:

* **Enfoque de un solo archivo:** Con Dynamic Media, almacena un archivo de origen principal, y todas las variaciones de tamaño y los efectos visuales se crean y optimizan dinámicamente en el momento de la entrega. Este enfoque ahorra costes de almacenamiento y elimina la complejidad del flujo de trabajo.
* **Imágenes inteligentes totalmente globales:** Las imágenes inteligentes aplicadas durante la entrega de contenido reducen significativamente el tamaño de la imagen y el peso de la página sin poner en riesgo la calidad visual. Está optimizado para ancho de banda de red y proporción de píxeles del dispositivo.
* **Con tecnología de IA:** Recorte inteligente, una característica impulsada por IA, automatiza el recorte de imágenes y puntos de interés de vídeo. Elimina el esfuerzo manual y se adapta de forma eficaz para el uso empresarial.
* **Vídeo fácil:** Cargue vídeos de origen principal en Dynamic Media y envíelos en secuencias de forma adaptativa en varios idiomas con audio descriptivo.
* **Biblioteca de visualizadores de experiencias:** Personalice y convierta en marca los visualizadores de experiencias para imágenes y vídeos. Estos visores se integran perfectamente en sus experiencias digitales.
* **Compatibilidad con formatos emergentes:** Dynamic Media permite la entrega de experiencias 3D y panorámicas.

A medida que explora el [Recorrido de Dynamic Media](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dm-journey/dm-journey-part1), revisar la lista consolidada de prácticas recomendadas a continuación puede ayudarle a aprovechar al máximo sus capacidades. Adapte estas prácticas recomendadas de Dynamic Media a los requisitos específicos de su contexto y proyecto para poder optimizar sus experiencias en varios canales y dispositivos.

<!-- In Dynamic Media on AEM, there are sets of methods, techniques, and guidelines that can help you maximize the potential of your rich media content. These best practices can lead to optimal results and increase efficiency in your use of Dynamic Media. They represent the most efficient and effective courses of action in a particular situation. They also unlock high value for your audience and deliver high-quality, engaging content. -->

>[!IMPORTANT]
>
>Las prácticas recomendadas sobre Dynamic Media de este artículo pueden evolucionar con el tiempo a medida que surjan nuevas tecnologías en Dynamic Media. La información siguiente es actual para la última versión de Dynamic Media.


## Ingesta de recursos en Dynamic Media

**Caso comercial:** *Administre de manera eficiente grandes volúmenes de recursos y asegúrese de que solo el contenido relevante y aprobado se entregue a los usuarios finales.*

Optimice la administración de grandes cantidades de recursos de forma eficaz. Asegúrese de que solo el contenido autorizado y apropiado llegue a los usuarios finales mediante las características de **Sincronización selectiva** y **Publicación selectiva** de Dynamic Media.

* **Sincronización selectiva:**
Característica proactiva que le permite elegir qué recursos sincronizar con Dynamic Media. Por ejemplo, puede decidir sincronizar solo las carpetas que contienen recursos que han recibido la aprobación final. Este flujo de trabajo le ayuda a mantener el control sobre los recursos que se están preparando para su entrega a los clientes.

* **Publicación selectiva:**
Después de sincronizar los recursos, la publicación selectiva le permite controlar qué recursos son visibles para sus clientes. Esta capacidad significa que puede controlar qué recursos aprobados se entregan realmente a través de sus canales, lo que garantiza que sus clientes solo vean el contenido mejor y más relevante.

Estas dos prácticas recomendadas le ayudan a lograr un mejor control, control y productividad sobre el contenido con medios enriquecidos.

¿Desea obtener más información? Vaya a [Configurar publicación selectiva en el nivel de carpeta en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).


## Visores de Dynamic Media

Las prácticas recomendadas del visualizador de Dynamic Media son directrices esenciales diseñadas para optimizar el rendimiento, la funcionalidad y la experiencia del usuario de los recursos de Dynamic Media en AEM. Estas prácticas garantizan que los recursos se sincronicen, publiquen y configuren correctamente para utilizar todas las capacidades de Dynamic Media.

Si sigue estas prácticas recomendadas, podrá lograr una integración optimizada, una administración eficiente de los recursos y unas interacciones mejoradas con el visualizador. La sincronización de recursos, el uso del recorte inteligente y la adherencia a las directrices de inclusión de archivos de JavaScript son prácticas importantes. Estas recomendaciones ayudan a mantener la integridad y fiabilidad de la entrega de medios en varias plataformas y dispositivos.

* **Sincronizar Assets del visor:**
Asegúrese de que todos los recursos del visualizador estén sincronizados con Dynamic Media antes de utilizar el reproductor.

   * Acceda a la página de administrador de muestra en `/libs/dam/gui/content/s7dam/samplemanager/samplemanager`. Esta página permite resincronizar los recursos de un visor, incluidos los iconos, los archivos CSS y los ajustes preestablecidos predeterminados.
   * Si encuentra algún problema con el visor, vaya al artículo [Solucionar problemas de visualizadores de Dynamic Media](/help/assets/dynamic-media/troubleshoot-dm.md#viewers).

* **Publicar Assets:**
Asegúrese de que los recursos se publican antes de verlos en los visores de envío.
* **Vídeos de reproducción automática silenciados:**
Para la funcionalidad de reproducción automática de vídeos, utilice la configuración de vídeo en silencio porque los navegadores restringen la reproducción de vídeos con volumen.
* **Recorte inteligente:**
Utilice el componente Image v3 para el recorte inteligente a fin de mejorar la presentación de los recursos de imagen.
* **Inclusión de archivo JavaScript:**
Incluya solo el archivo JavaScript del visor principal en la página. Evite hacer referencia a archivos JavaScript adicionales que la lógica de tiempo de ejecución del visor pueda descargar. En concreto, no vincule directamente a la biblioteca HTML5 SDK `Utils.js` desde la ruta de contexto `/s7viewers` (conocida como inclusión de SDK consolidada). La lógica del visor administra la ubicación de `Utils.js` o bibliotecas de visor en tiempo de ejecución similares, que pueden cambiar entre versiones. Adobe no conserva versiones anteriores de las inclusiones del visor secundario en el servidor, por lo que la referencia directa a ellas puede interrumpir la funcionalidad del visor en futuras actualizaciones.
* **Directrices de incrustación:**
Utilice la documentación para incrustar directrices específicas para cada visor.
¿Desea obtener más información? Ir a [Visores para AEM Assets](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/viewers-aem-assets-dmc/c-html5-s7-aem-asset-viewers).
* **Tutorial y ejemplos de SDK:**
Consulte el [Tutorial de Viewer SDK](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/library/c-tutorial) y los [ejemplos de aplicaciones de HTML5 SDK](https://s7d9.scene7.com/s7sdk/2024.5/docs/jsdoc/index.html) para obtener información detallada sobre las API de componentes de SDK.


## Preparación de recursos para su entrega

### Organizar los recursos

**Caso comercial:** *Organice los recursos de forma eficaz para optimizar los flujos de trabajo.*

Para una organización de recursos eficiente que optimiza los flujos de trabajo, siga una o más de las siguientes prácticas recomendadas:

* **Organizar recursos en carpetas:**
Para organizar los recursos de forma eficaz, es necesario clasificarlos en carpetas, de forma similar a la organización de archivos de un equipo. La asignación de nombres, la estructuración de subcarpetas y la administración de archivos adecuados dentro de estas carpetas son cruciales para un procesamiento eficaz de los recursos. La implementación de convenciones de nomenclatura sistemática y prácticas de metadatos maximiza la utilidad del repositorio de recursos digitales.
¿Desea obtener más información? Vaya a [Organizar recursos en carpetas](/help/assets/organize-assets.md#organize-using-folders).
* **Organizar recursos con etiquetas:**
El etiquetado de recursos mejora la capacidad de búsqueda, la creación de colecciones y la clasificación de búsqueda. La IA de Adobe emplea un algoritmo de autoaprendizaje para un etiquetado preciso, lo que permite una recuperación rápida de los recursos. Adobe AI también reconoce y asigna etiquetas relevantes, incluidas las personalizadas, a los recursos, lo que simplifica la administración de recursos con un etiquetado automático y descriptivo.
¿Desea obtener más información? Vaya a [Organizar recursos con etiquetas](/help/assets/organize-assets.md#use-tags-to-organize-assets).
* **Organizar recursos como colecciones:**
Dynamic Media junto con Experience Manager Assets permiten la creación, edición y uso compartido eficientes de colecciones de recursos entre los usuarios. Puede establecer varios tipos de colección, incluidas listas estáticas y compilaciones dinámicas basadas en búsquedas. Estos tipos de colecciones se pueden compartir en varias ubicaciones con derechos de edición y acceso personalizables.
¿Desea obtener más información? Vaya a [Organizar recursos como colecciones](/help/assets/manage-collections.md).
* **Organizar recursos mediante perfiles:**
Un perfil de procesamiento automatiza la administración de recursos en carpetas designadas, lo que optimiza la organización. La estandarización de los metadatos, los nombres de archivo y las estructuras de carpetas permite la aplicación coherente y precisa de estos perfiles a medida que se amplía la colección de recursos digitales.
¿Desea obtener más información? Vaya a [Organizar recursos con perfiles](/help/assets/organize-assets.md#organize-to-use-profiles).



### Optimización de la calidad de las imágenes

**Caso comercial:** *Obtenga imágenes de buena calidad de Dynamic Media.*

Para mejorar la calidad de la imagen es necesario tener en cuenta diversos factores. Puede ser un proceso que requiere mucho tiempo. Sin embargo, hay algunas prácticas comprobadas que pueden ayudarle a lograr resultados deseables. Algunas de estas prácticas recomendadas incluyen cómo obtener un tamaño de imagen óptimo, enfoque de imagen y los mejores formatos de imagen que se pueden utilizar.

¿Desea obtener más información? Vaya a [Prácticas recomendadas para optimizar la calidad de las imágenes](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md).

Debido a que la percepción de la calidad de la imagen varía de persona a persona, a veces un enfoque sistemático de la experimentación es esencial para lograr resultados deseables. Adobe Experience Manager facilita este proceso con más de 100 comandos de Dynamic Media para mejorar las imágenes.

¿Desea obtener más información? Ver [instantánea de Dynamic Media](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot) (3 minutos y 17 segundos).

Para evaluar el impacto de estos comandos en la calidad de la imagen, puede cargar una imagen en Dynamic Media, utilizar la interfaz de la herramienta en la dirección URL especificada y aplicar los comandos que desee probar.

¿Quieres probarlo? Iniciar [instantánea de Dynamic Media](https://snapshot.scene7.com/)

### Estandarizar estilos aplicados a imágenes

**Caso comercial:** *Estandarizar de forma eficaz el estilo y la transformación aplicados a mis recursos de imagen.*

Utilice ajustes preestablecidos de imagen con regularidad en Dynamic Media para que pueda ajustar de forma coherente y dinámica los tamaños, formatos y propiedades de la imagen. Considere un ajuste preestablecido de imagen como una macro: es un conjunto con nombre de comandos para cambiar el tamaño y el formato. Por ejemplo, si su sitio necesita imágenes de productos en varios tamaños y formatos, con una compresión específica para equipos de escritorio y dispositivos móviles, los ajustes preestablecidos de imagen automatizan este proceso de forma eficaz.

¿Quieres probarlo? Vaya a [Aspectos básicos de la creación de ajustes preestablecidos de imagen para procesar recursos](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-e)

### Ajustar el enfoque y el marco de imágenes y vídeos

**Caso comercial:** *Asegúrese de que el punto de interés principal de mis imágenes o vídeos permanece enfocado en todos los dispositivos.*

El recorte inteligente es una función de Dynamic Media que utiliza la IA de Adobe, la IA de Adobe y el marco de trabajo de aprendizaje automático, para automatizar el recorte de imágenes y vídeos. Detecta de forma inteligente y se centra en el tema principal o punto de interés de una imagen o vídeo. Esta inteligencia garantiza que el punto focal se mantenga en varios tamaños de pantalla en equipos de escritorio y dispositivos móviles.

Una práctica recomendada es crear un perfil de imagen con recorte inteligente. En el perfil, puede definir varios tamaños de pantalla y permitir que Adobe AI haga el resto, lo que garantiza que las imágenes y los vídeos siempre estén optimizados para el dispositivo del visualizador.

¿Desea obtener más información? Vea [Uso del recorte inteligente con AEM Assets en Dynamic Media](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) (6 minutos, 35 segundos) y [Uso del recorte inteligente de Dynamic Media para el vídeo](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/video/dynamic-media-smart-crop-video) (6 minutos, 22 segundos).

### Mejore las clasificaciones SEO

**Caso comercial:** *Configure Dynamic Media para mejorar las clasificaciones de SEO.*

Utilice las siguientes recomendaciones con regularidad para asegurarse de que las imágenes contribuyen de forma eficaz a su estrategia de SEO general.

* **Nombres de archivos de imagen significativos:**
Utilice nombres de archivo descriptivos que reflejen el contenido de la imagen. Por ejemplo,

   * use `myCompany-Silver-Wrist-Watch`
   * *evitar* `myCompany_Silver_Wrist_Watch` o `myCompanySilverWristWatch`

  Al hacerlo, los motores de búsqueda entienden el contexto de la imagen y mejoran la SEO. Google prefiere guiones en lugar de guiones bajos o espacios en el nombre de un archivo. Además, evite concatenar palabras en un nombre de archivo.
* **Dominio personalizado:**
Implemente un dominio personalizado que incluya su empresa o nombre de marca para reforzar el reconocimiento y la confianza de la marca. Por ejemplo,

   * use `http://images.mycompany.com/is/image/companyname/`
   * *evitar* `https://s7d1.scene7.com/is/image/folder/AdobeStock_28563982`

* **Estructura de carpetas compatible con SEO:**
Organice las imágenes en una estructura de carpetas que incluya el nombre de su empresa o marca para mejorar la indexación, como `http://images.mycompany.com/is/image/companyname/`.
* **Conjuntos de reglas de Dynamic Media:**
Aprenda a transformar de forma condicional las URL en función de varios factores, lo que mejora la SEO y la experiencia del usuario.
¿Desea obtener más información? Vaya a [Use conjuntos de reglas para transformar las direcciones URL](/help/assets/dynamic-media/using-rulesets-to-transform-urls.md).
* **Imágenes inteligentes y recorte inteligente:**
Utilice las funciones de imágenes inteligentes y recorte inteligente de Dynamic Media para ofrecer imágenes optimizadas y adaptables. Al hacerlo, no solo mejora los tiempos de carga de la página, sino que también contribuye positivamente a las clasificaciones de SEO.
¿Desea obtener más información? Vaya a [Imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md) o vea [Uso del recorte inteligente con Dynamic Media de los AEM Assets](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use) (6 minutos, 35 segundos).

Recuerde, estas prácticas recomendadas se alinean bien con las prácticas recomendadas de SEO de imágenes de Google. Estas prácticas enfatizan la importancia de proporcionar contexto y claridad a los motores de búsqueda a través de convenciones de nomenclatura adecuadas, datos estructurados y una entrega de imágenes optimizada.

¿Desea obtener más información? Vaya a [Prácticas recomendadas de estructura de URL para Google](https://developers.google.com/search/docs/crawling-indexing/url-structure) y [Prácticas recomendadas de SEO de imagen de Google](https://developers.google.com/search/docs/appearance/google-images)

### Mejorar dinámicamente las imágenes y crear efectos visuales mediante comandos

**Caso comercial:** *Aplicar efectos visuales enriquecidos a las imágenes.*

Dynamic Media ofrece un conjunto de comandos para mejorar imágenes y crear efectos visuales de forma dinámica, sin necesidad de varios recursos estáticos. A continuación se ofrecen algunas explicaciones breves de algunos de estos procesos y algunos ejemplos que le guiarán:

#### Efectos dentro de la imagen de origen

| Tarea | Qué hacer |
| --- | --- |
| **Cargar y publicar la imagen original** | <ul><li> Comience por cargar la imagen original en Dynamic Media.</li><li> Asegúrese de que se publica y de que se puede acceder a través de una dirección URL.</li><li> En este ejemplo, se carga en Dynamic Media una imagen de stock de un reloj con fondo blanco (llamémoslo &quot;Imagen X&quot;).<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer)</li></ul> |
| **Crear una máscara** | <ul><li> Desarrolle una máscara que defina el sujeto (el área donde desea aplicar los efectos) y el fondo (el área que desea cambiar).<br>[https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps](https://s7g2.scene7.com/is/image/genaibeta/watch-silver-offer-maskps)</li><li> Las máscaras suelen ser imágenes en escala de grises, en las que el blanco representa al sujeto y el negro representa el fondo. Puede crear máscaras con herramientas como Adobe Photoshop.<br>¿Desea obtener más información? Vaya a [Creación y edición de una máscara rápida en Photoshop](https://helpx.adobe.com/in/photoshop/using/create-temporary-quick-mask.html).</li><li> Para &quot;Imagen X&quot;, cree una máscara que describa con precisión el tema que desea mejorar. Por ejemplo, una persona, un objeto, etc.</li></ul> |
| **Aplicar comandos de URL de Dynamic Media para los efectos** | Una vez que tenga la máscara, utilice los comandos de URL para aplicar efectos como un resplandor exterior o cambie el color de fondo a &quot;Imagen X&quot;. Estos son dos ejemplos:<ul><li> **Efecto de resplandor exterior:**<br> Para agregar un efecto de resplandor exterior a lo largo del límite del sujeto, edite la dirección URL de esta manera:<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&maskUse=invert&effect=-1&pos=100,100&op_blur=75&op_grow=1&opac=25](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&maskUse=invert&effect=-1&pos=100,100&op_blur=75&op_grow=1&opac=25)<br>En esta dirección URL, los parámetros `op_blur`, `op_grow` y `opac` crean el efecto de resplandor exterior.</li><li> **Cambio de color de fondo:**<br> Para cambiar el color de fondo, use la dirección URL con un valor de color de fondo diferente:<br>[https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&maskUse=invert&maskUse=invert&color=255,255,0](https://s7g10.scene7.com/is/image/genaibeta/watch-silver-offer?mask=watch-silver-offer-maskps&maskUse=invert&maskUse=invert&color=255,255,0)<br> En este ejemplo, `color=255,255,0` establece el color de fondo en amarillo. Edite el fondo a un color específico para conseguir un impacto visual.</li></ul> |

#### Agregar un borde de imagen

Dynamic Media permite manipular imágenes directamente a través de direcciones URL, lo que lo convierte en una potente herramienta para crear experiencias digitales dinámicas. A continuación se muestran algunos ejemplos. Empecemos con la siguiente URL de imagen original: [https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel).

| Tarea | Qué hacer |
| --- | --- |
| **Borde blanco** | Para agregar un borde blanco, use la siguiente dirección URL:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10)<br>En esta dirección URL, el parámetro `extend=10,10,10,10` especifica el tamaño del borde de diez píxeles en todos los lados. |
| **Desenfocar a lo largo del borde blanco** | Para agregar un efecto de desenfoque a lo largo del borde blanco, puede editar la dirección URL de la siguiente manera:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10&effect=-1&op_blur=60&color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10&effect=-1&op_blur=60&color=0,0,0)<br>En esta dirección URL, el parámetro `effect=-1` aplica el efecto de desenfoque y `op_blur=60` controla la intensidad del desenfoque. |
| **Efecto de sombra paralela a lo largo del límite exterior** | Para agregar un efecto de sombra paralela a lo largo del límite exterior, use esta dirección URL:<br>[https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10&effect=-1&$shadow$&amp;color=0,0,0](https://s7g2.scene7.com/is/image/genaibeta/ocean-facing-hotel?size=400,400&extend=10,10,10,10&effect=-1&$shadow$&color=0,0,0)<br>El parámetro `$shadow$` crea el efecto de sombra y `color=0,0,0` establece el color de sombra en negro. |

Siéntase libre de experimentar con estas URL para lograr los efectos visuales deseados.

#### Creación de superposiciones de imagen

Si desea superponer un logotipo o un icono en una imagen existente, Dynamic Media proporciona una manera directa de conseguirlo mediante comandos de URL. Vamos a desglosar los escalones.

| Paso | Qué hacer |
| --- | --- |
| **Cargar y publicar la imagen base** | En primer lugar, cargue y publique la imagen base sobre la que desee superponer el logotipo o el icono. Puede utilizar cualquier imagen como base.<br>Por ejemplo, aquí hay una imagen base:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa). |
| **Cargar y publicar el logotipo o la imagen del icono** | A continuación, cargue y publique la imagen que desee superponer sobre la imagen base. Esta imagen debe ser un PNG transparente con el logotipo o el icono que desee superponer.<br>Esta es la imagen PNG transparente de un objeto de estrella con efectos de transparencia que se superpondrá:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorate-star](https://s7g2.scene7.com/is/image/genaibeta/decorate-star) |
| **Aplicar la URL de Dynamic Media** | Ahora, cree una URL de Dynamic Media que combine la imagen base y el logotipo o la imagen del icono. Puede utilizar comandos de URL para lograr este efecto.<br>La estructura de la dirección URL tiene este aspecto:<br>[https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&src=decorate-star&scale=1.25&posN=0.33,-.25&fmt=png](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa?layer=1&src=decorate-star&scale=1.25&posN=0.33,-.25&fmt=png)<br>donde el recurso<ul><li> `hotspotRetailBaseImage` es la imagen base.</li><li> `starxp` es la imagen del logotipo/icono.</li><li> `layer=1` especifica que el logotipo o icono se debe colocar en capas sobre la imagen base.</li><li> `scale=1.25` ajusta el tamaño del logotipo/icono.</li><li> `posN=0.33,-.25` determina la posición del logotipo/icono en relación con la imagen base.</li><li> `fmt=png` garantiza que la salida esté en formato PNG.</li></ul> |

¿Qué desea saber más? Vaya a [src](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-src) para obtener más información sobre el comando `src` y otros comandos de URL de Dynamic Media.


#### Superponer texto promocional

A continuación se indican los pasos para superponer un mensaje de texto promocional en una imagen mediante HTML y CSS.

| Paso | Qué hacer |
| --- | --- |
| **Cargar y publicar la imagen base** | En primer lugar, cargue y publique la imagen base sobre la que desee superponer el texto. Puede utilizar cualquier imagen que desee. Por ejemplo, esta es una imagen base de ejemplo:<br>[https://s7g2.scene7.com/is/image/genaibeta/leather-sofa](https://s7g2.scene7.com/is/image/genaibeta/leather-sofa)<br> |
| **Aplicar operadores de texto de Dynamic Media** | Con Dynamic Media, puede aplicar operadores de texto para superponer texto dinámico directamente en la imagen. La siguiente URL de ejemplo muestra esta capacidad:<br>[https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&posN=-0.3,-0.455&text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+New+Collection%7d%7d&amp;size=370,70&amp;textAttr=130&amp;bgcolor=FF333&amp;wid=600&amp;hei=600](https://s7g10.scene7.com/is/image/genaibeta/leather-sofa?layer=1&posN=-0.3,-0.455&text=%7b\rtf1\ansi%7b\fonttbl%7b\f0+Arial;%7d%7d%7b\colortbl+\red255\green255\blue255;%7d\copyfit1000\vertalc\qc%7b\cf0\fs42+Nueva+Colección%7d%7d&size=370,70&textAttr=130&bgcolor=FF333&wid=600&hei=600) |

#### Cambio de tamaño y recorte para varios casos de uso

##### Conceptos básicos de cambio de imagen

El cambio de tamaño de la imagen implica modificar las dimensiones, la resolución y el tamaño de archivo de la imagen. Estos son algunos puntos clave que hay que tener en cuenta:

* **Composición de píxeles:**
Las imágenes digitales constan de puntos diminutos llamados píxeles. Cuando se crea una imagen, tiene un número específico de píxeles. El cambio de tamaño implica añadir o restar píxeles para cambiar las dimensiones, la resolución y el tamaño del archivo de la imagen.
* **Proporción de aspecto:**
El mantenimiento de la relación de aspecto (la relación entre anchura y altura) es crucial para evitar la distorsión. Tanto si desea ampliar una imagen (ampliar) como si lo hace más pequeño (reducir), la preservación de la relación de aspecto garantiza la coherencia visual.
* **Consideraciones de calidad:**
Cambiar el tamaño puede afectar a la calidad de imagen. Evite la ampliación drástica, ya que puede provocar pixelación. Considere la posibilidad de reproducir la imagen a un tamaño y una resolución mayores. Para imágenes más pequeñas, utilice las herramientas adecuadas para mantener la resolución.

##### Recorte o cambio de tamaño

El recorte y el cambio de tamaño son técnicas de Dynamic Media que le permiten transformar imágenes para adaptarlas a varios casos de uso, ya sea creando miniaturas, imágenes de visualización de productos o titulares.

* **Recortando:**
Implica eliminar parte de una imagen para modificar su composición y encuadre. No cambia las dimensiones generales, sino que se centra en un área específica.
* **Cambio de tamaño:**
Ajusta las dimensiones, la resolución y el tamaño de archivo de toda la imagen manteniendo la relación de aspecto.

Exploremos un caso de uso que implica la siguiente imagen de sala de estar:

* **Imagen original de la sala de estar:**
  [https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa](https://s7g2.scene7.com/is/image/genaibeta/decorative-room-sofa)
* **Miniatura (200 px x 200 px):**
Una versión más pequeña adecuada para una carga o visualización rápidas.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&hei=200&fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&hei=200&fit=crop)
* **Miniatura con recorte (200 px x 200 px):**
Recortado para centrarse en el área del sofá.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&hei=200&cropN=.24,.24,.6,.72&fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=200&hei=200&cropN=.24,.24,.6,.72&fit=crop)
* **Imagen de visualización del producto (800 px x 600 px):**
Recortado y redimensionado para mostrar el sofá.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&hei=600&cropN=.24,.24,.6,.72&fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=800&hei=600&cropN=.24,.24,.6,.72&fit=crop)
* **Titular (1720 px x 820 px):**
Derivado de la imagen original, haciendo énfasis en la habitación.
  [https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&hei=820&cropN=0,.1,1,1&fit=crop](https://s7g10.scene7.com/is/image/genaibeta/decorative-room-sofa?wid=1720&hei=820&cropN=0,.1,1,1&fit=crop)

No dude en explorar estas variaciones para sus necesidades específicas.
¿Desea obtener más información sobre los comandos disponibles en una dirección URL? Vaya a [Referencia de comando](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference).

### Distribución de imágenes de GIF

**Caso comercial:** *Transmitir GIF mediante Dynamic Media*

Puede cargar y enviar GIF a través de Dynamic Media. Para procesar un GIF animado, reemplace `is/image` por `is/content` en la dirección URL. Por ejemplo, si subió `abc.gif`, use lo siguiente:

* Esta ruta de URL representa una vista estática de GIF:

  ```
  https://your.domain.com/is/image/yourfolder/abc
  ```

* Esta ruta URL representa la vista de animación de GIF:

  ```
  https://your.domain.com/is/content/yourfolder/abc
  ```

>[!NOTE]
>
>Al usar `is/content` en la ruta de acceso URL, los comandos de transformación de imágenes no se aplican al recurso.

### Publicar un vídeo para mi sitio web

**Caso comercial:** *Publique rápidamente un vídeo para un sitio de marketing.*

* **Seleccionar un perfil de vídeo:**
En primer lugar, en Dynamic Media debe seleccionar un perfil de vídeo adecuado. Puede optar por el perfil *Codificación de vídeo adaptable* disponible en AEM Assets en Perfiles de vídeo. Estos ajustes de codificación predefinidos garantizan que el vídeo esté optimizado para la reproducción en varios dispositivos y condiciones de ancho de banda. También puede crear su propio perfil de vídeo adaptable.
* **Asignar el perfil:**
Asigne el perfil de vídeo seleccionado a las carpetas en las que se va a cargar el vídeo. Este paso garantiza que se aplique la configuración de codificación correcta durante el proceso de carga.
* **Cargar el vídeo original:**
Cargue el archivo de vídeo original. Asegúrese de que sea un vídeo de alta resolución con buena calidad. Cuanto mejor sea el vídeo de origen, mejor será el resultado final.
* **Vista previa y publicación:**
Previsualice el vídeo para asegurarse de que todo tiene el aspecto esperado. Una vez que esté satisfecho, continúe y publíquelo. Este paso hace que el vídeo sea accesible para la audiencia.
* **Vincular o incrustar:**
Después de la publicación, tiene dos opciones.

   * **Vínculo directamente:**
Utilice la dirección URL proporcionada para vincular directamente al vídeo. Conéctelo correctamente a su sitio de marketing.
   * **Incrustar el vídeo:**
Copie el código incrustado proporcionado y péguelo en la HTML de la página web donde desee que aparezca el vídeo. Al hacerlo, el vídeo se reproduce directamente en el sitio.

¿Desea obtener más información? Ir a [Vídeo](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/video).

### Configuración de vídeos para obtener una calidad y una participación óptimas

**Caso comercial:** *Configure vídeos para obtener la mejor calidad y participación.*

Para garantizar la mejor calidad y participación en sus vídeos, considere la posibilidad de implementar una combinación de las siguientes estrategias de prácticas recomendadas:

* **Usar el visor de vídeo HTML5 integrado:**
Los ajustes preestablecidos del visualizador de vídeo HTML5 de Dynamic Media son reproductores de vídeo sólidos. Utilícelos para evitar problemas comunes asociados con la reproducción de vídeo HTML5 y dispositivos móviles.
Estos ajustes preestablecidos afrontan desafíos como la entrega de flujo de bits adaptable y el alcance limitado del explorador de escritorio.
¿Desea obtener más información? Vaya a [Práctica recomendada: usar el visor de vídeo de HTML 5](/help/assets/dynamic-media/video.md#best-practice-using-the-html-video-viewer).

* **Usar perfiles de vídeo de Dynamic Media:**
Los perfiles de vídeo de Dynamic Media ayudan a administrar de forma eficaz el vídeo, a conseguir una calidad uniforme y a utilizar el flujo adaptable.
¿Desea obtener más información? Vaya a [Perfiles de vídeo de Dynamic Media](/help/assets/dynamic-media/video-profiles.md).

* **Seguir prácticas recomendadas para la codificación de vídeo:**
Aplique perfiles de codificación de vídeo que mantengan la calidad de vídeo original sin una reducción excesiva durante la codificación.
¿Desea obtener más información? Vaya a [Prácticas recomendadas para codificar vídeos](/help/assets/dynamic-media/video.md#best-practices-for-encoding-videos).

* **Adoptar flujo adaptable en lugar de flujo progresivo:**
El streaming adaptable ajusta la calidad del vídeo en función de la velocidad de conexión a Internet y las capacidades del dispositivo del visualizador.
Utiliza protocolos como HLS (HTTP Live Streaming) o DASH (`Dynamic Adaptive Streaming over HTTP`) para garantizar una calidad de reproducción óptima.
A diferencia del streaming progresivo, que ofrece vídeos de forma lineal, el streaming adaptable minimiza el almacenamiento en búfer y ofrece una experiencia de visualización perfecta.

### Internacionalización de vídeos para consumo multilingüe

**Caso comercial:** *Prepare los vídeos para el consumo multilingüe.*

La internacionalización de los vídeos para el consumo multilingüe es esencial para llegar a una audiencia global. Dynamic Media proporciona funciones que pueden ayudarle a lograr este objetivo.

* **Cargue sus vídeos:**
   * En primer lugar, cree un perfil de codificación de vídeo. Puede utilizar el perfil predefinido de codificación de vídeo adaptable que viene con Dynamic Media o crear su propio perfil personalizado.
   * Asocie el perfil de procesamiento de vídeo con una o varias carpetas en las que carga los vídeos de origen principales.
   * Cargue los vídeos de origen principales en estas carpetas. Dynamic Media los codifica en función del perfil de procesamiento de vídeo asignado.
   * Dynamic Media admite principalmente vídeos de formato corto (hasta 30 minutos) con una resolución mínima superior a 25 × 25. Se pueden cargar archivos de vídeo de hasta 15 GB1.

* **Administrar los vídeos:**
   * Organice, examine y busque recursos de vídeo en AEM.
   * Previsualización y publicación de recursos de vídeo.
   * Vea el vídeo de origen y sus representaciones codificadas junto con las miniaturas asociadas.
   * Edite propiedades de vídeo, como título, descripción y etiquetas2.

* **Localización:**
   * Para cada geografía/idioma de destino, cree pistas de audio y subtítulos.
   * Añada estas pistas de audio y subtítulos a sus vídeos desde la interfaz de AEM.
   * A medida que los usuarios reproducen los vídeos, pueden seleccionar su idioma preferido para el audio y los subtítulos.

* **Publicación:**
   * Si utiliza AEM como sistema de administración de contenido web (WCM), puede agregar vídeos directamente a las páginas web.
   * Si utiliza un sistema WCM de terceros, puede vincular o incrustar vídeos en las páginas web mediante direcciones URL o códigos incrustados.

¿Desea obtener más información? Vaya a [Acerca de la compatibilidad con múltiples subtítulos y pistas de audio para vídeos en Dynamic Media](/help/assets/dynamic-media/video.md#about-msma).


## Entrega de recursos a los clientes

### Optimizar los tamaños de imagen y minimizar los tiempos de carga de la página

**Caso comercial:** *Optimice el tamaño de las imágenes para cualquier explorador o pantalla y reduzca el tiempo de carga de la página.*

Dynamic Media Smart Imaging es una potente herramienta que mejora el rendimiento de la entrega de imágenes al optimizar automáticamente el formato, el tamaño y la calidad de la imagen en función de las capacidades del explorador del cliente.

Adobe recomienda usar las capacidades de Smart Imaging en lugar de establecer manualmente el formato de imagen en `webp` o `avif`. He aquí la razón:

* **Compatibilidad de explorador:**
Imágenes inteligentes garantiza que el formato de imagen entregado sea compatible con el explorador del usuario.
* **Compresión óptima:**
Selecciona el mejor formato para la compresión en función del navegador, las condiciones de red y la resolución de pantalla específicos.
* **Formatos modernos:**
Aunque `avif` es un formato más reciente que ofrece una mejor compresión, aún no es compatible de forma universal con todos los exploradores.
* **Prácticas recomendadas:**
Para garantizar el mejor formato optimizado para la web, puede confiar en Smart Imaging para que realice la selección del formato en lugar de hacerlo manualmente mediante los comandos `fmt=webp` o `fmt=avif`.

Al utilizar imágenes inteligentes, puede asegurarse de que las imágenes se entreguen de la manera más eficiente posible, adaptadas al entorno de navegación de cada usuario. Este método simplifica el proceso y puede mejorar el rendimiento en términos de tiempos de carga de las imágenes y de la experiencia general del usuario.

¿Desea obtener más información? Vaya a [Imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md).

### Entrega posterior de recursos a los clientes

**Caso comercial:** *Después de publicar contenido nuevo o de sobrescribir contenido existente, ¿cómo se puede garantizar que los cambios aparezcan inmediatamente en la CDN?*

La CDN (red de distribución de contenido) almacena en caché los recursos de Dynamic Media para una entrega rápida a los clientes. Cuando se realizan actualizaciones en estos recursos, es importante que los cambios surtan efecto inmediatamente en el sitio web. Al purgar o invalidar la caché de la CDN, los recursos entregados por Dynamic Media se pueden actualizar rápidamente. Este método elimina la necesidad de esperar a que la caché caduque en función del valor TTL (Tiempo de vida), que normalmente se establece en diez horas. Según el caso de uso específico, puede actualizar la configuración del TTL de CDN (Tiempo de vida) en consecuencia.

¿Desea obtener más información? Vaya a [Invalidar la caché de CDN mediante Dynamic Media](/help/assets/dynamic-media/invalidate-cdn-cache-dynamic-media.md).

