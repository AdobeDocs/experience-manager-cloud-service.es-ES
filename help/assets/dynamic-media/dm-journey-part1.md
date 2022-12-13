---
title: recorrido Dynamic Media, parte I
description: El Recorrido de Dynamic Media cubre los conceptos básicos de Dynamic Media, cómo funciona, qué puede hacer por usted y qué valor aporta a su trabajo y a sus clientes.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: f3472006-d5ae-4f70-af3e-44e73aee85cc
source-git-commit: 803c4dc44189d58ddbd2669b00dd8107b2a926ae
workflow-type: tm+mt
source-wordcount: '3712'
ht-degree: 1%

---

# recorrido de Dynamic Media: Conceptos básicos, parte I {#dm-journey-part1}

Bienvenido al Recorrido de Dynamic Media.

Este recorrido cubre los conceptos básicos de Dynamic Media, cómo funciona, qué puede hacer por usted y qué valor aporta a su trabajo y a sus clientes.

**_Requisitos previos_**

* Comprensión básica de los formatos de imagen y vídeo
* Comprensión básica del HTML y la CSS
* Comprensión básica de herramientas de diseño como Adobe Illustrator, Adobe Photoshop o Adobe XD
* El acceso a Dynamic Media en Experience Manager es útil, pero no obligatorio

**_Qué puede esperar aprender_**

_Parte I_

* ¿Qué es Dynamic Media y cómo puede ayudarle?
* Ejemplos de uso de Dynamic Media
* Cómo fluye un recurso a través del sistema Dynamic Media

_Parte II_

* Anatomía de una URL de Dynamic Media y cómo Dynamic Media ofrece contenido
* Aspectos básicos de la creación de ajustes preestablecidos de imagen para procesar recursos
* Conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos

**_Audiencia_**
La audiencia que mejor se adapta a los lectores de este recorrido es la siguiente, que es nueva en Dynamic Media on Experience Manager:

* Administrador
* Analista empresarial
* Arquitecto de contenido
* Autor de contenido
* Designer
* Desarrollador
* Marketing
* Administrador de productos/Propietario

>[!TIP]
>
>Para obtener mejores resultados, Adobe recomienda leer y ver este Recorrido de Dynamic Media en un equipo de escritorio.

## ¿Qué es Dynamic Media y cómo puede ayudarle? {#dm-journey-a}

Dynamic Media le ayuda a distribuir recursos de marketing y comercialización de contenido visual enriquecido bajo demanda. También le ayuda a crear y ofrecer experiencias de visualización interactivas, como zoom, giro de 360 grados y vídeo. Los recursos se escalan de forma dinámica para su consumo en sitios web, móviles y sociales. Con un conjunto de recursos de origen principales, como imágenes, vídeos y 3D, Dynamic Media genera y ofrece varias variaciones de este contenido enriquecido, en tiempo real a través de su CDN (red de distribución de contenido) global, escalable y optimizada para el rendimiento.

Dynamic Media incorpora los flujos de trabajo de la solución de administración de recursos digitales de Adobe Experience Manager Assets para simplificar y optimizar el proceso de administración de campañas digitales.

### Un archivo con infinitas posibilidades

Uno de los principales puntos a comprender sobre Dynamic Media es el concepto de _Un archivo de recursos principal con infinitas posibilidades_.

Para comprender mejor este concepto, piense en la forma en que tradicionalmente trabaja con un solo recurso, como una imagen o un vídeo. Normalmente, se crea un recurso principal. A continuación, cree manualmente versiones de ese mismo recurso para cada experiencia, cada dispositivo que se necesite, cada página web y cada propiedad donde se utilice. Con el tiempo, ese recurso individual puede aumentar a 20, 30 o más versiones, sin tener asociado el historial de versiones. Ahora, imaginen hacer eso por cada imagen o video que tengan. La cantidad de versiones de activos rápidamente sería abrumadora para mantener y actualizar, sin mencionar el aumento en los costos de almacenamiento de información.

Sin embargo, Dynamic Media es fundamentalmente diferente de otros sistemas porque se utiliza para distribuir los medios _dinámicamente_ desde recursos únicos primarios y desde llamadas URL. Las rutas de URL de Dynamic Media que solicita incluyen instrucciones que indican al servidor de publicación de Adobe cómo mostrar el recurso cuando se envía a la pantalla de un cliente. Por ejemplo, si utiliza el mismo recurso principal único, puede que se envíe instantáneamente en representaciones ilimitadas, cambiando el tamaño, el formato, la resolución, el peso, el color, el recorte y efectos, como una vista de zoom.

Este método de envío único garantiza que se envíen experiencias de calidad coherentes a cualquier pantalla, independientemente del tamaño o el ancho de banda. Los vídeos de tamaño completo también están optimizados para todos los tipos de pantalla y se transmiten de forma adaptable para garantizar una experiencia de usuario coherente y de calidad.

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![Adobe Dynamic Media ofrece la misma imagen principal a diferentes medios en diferentes tamaños y formatos.](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_Adobe Dynamic Media garantiza que las experiencias de calidad y consistencia se entreguen a cualquier pantalla, independientemente del tamaño o el ancho de banda._

A medida que siga leyendo, aprenderá más sobre por qué es importante este concepto de &quot;un archivo de recursos principal, posibilidades ilimitadas&quot;.

### La red de distribución de contenido

Cuando esté listo para lanzarse con un recurso de imagen o un recurso de vídeo, la estructura básica de Dynamic Media, que consta de una red de entrega potente y de nivel superior. La red atiende a cientos de clientes de todo el mundo cada día. Los recursos se distribuyen en la red de distribución de contenido (o CDN) alojada en Akamai. La CDN es un sistema de servicios informáticos en red que cooperan de forma transparente para ofrecer contenido, especialmente contenido multimedia enriquecido, a los usuarios finales.

En el sistema CDN, el contenido web se almacena en las cachés web a través de Internet. A continuación, se entrega desde la caché web a los usuarios finales para que su envío sea más rápido. Por lo tanto, la primera vez que alguien descarga una página web, los recursos que ve se envían a una caché de CDN. Se almacenan en el servidor para que la próxima vez que alguien en la misma área acceda a la página web, el mismo contenido de caché se entregue más rápido. El contenido se entrega más rápido porque está más cerca del usuario final. Una CDN permite una visualización más rápida de la página web y, sin embargo, reduce las exigencias de ancho de banda del servidor central, ya que el contenido se entrega desde una red de caché, no desde un servidor central en cada caso. Este flujo optimizado significa una mejor experiencia de usuario, lo que produce un aumento de las ventas.

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

Históricamente, la CDN entrega 3,5 petabytes de tráfico a los clientes, cada mes. El sistema puede entregar 52.000 millones de activos en un solo día. Ese número equivale a 864.000 imágenes y vídeos entregados correctamente a los clientes, _cada segundo_.

### Imágenes inteligentes

Dynamic Media ya realiza una buena tarea de optimizar recursos y garantizar que cada recurso se cargue rápidamente en los sistemas móviles y de escritorio a través de la CDN. Para que esto suceda, los ajustes preestablecidos de imagen se utilizan en Dynamic Media para definir la calidad de la imagen. También definen el tipo de imagen que envía, su nitidez y otras partes de las experiencias o páginas.

Pero para agregar valor a Dynamic Media más allá de los ajustes preestablecidos de imagen, hay _Imágenes inteligentes_.

Las imágenes inteligentes ofrecen un rendimiento de entrega de recursos de imagen aún mejor, ya que optimizan automáticamente el formato y el tamaño de archivo de una imagen en función de la capacidad del explorador del cliente. Funciona con los ajustes preestablecidos de imagen existentes (los ajustes preestablecidos de imagen se tratan en la parte II de este recorrido) y utiliza la inteligencia durante la entrega.

Esta inteligencia reduce aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red y del explorador. Dado que los recursos de imagen constituyen la mayor parte del tiempo de carga de una página, la mejora del rendimiento puede tener un impacto profundo en los indicadores clave del negocio, como:

* Mayor conversión
* Tiempo invertido en el sitio
* Tasa de salida hacia otro sitio inferior

En general, con las imágenes inteligentes, se puede esperar una mejora del rendimiento del 22 % al 47 % en función de los ajustes preestablecidos de imagen existentes y las características específicas del usuario final. Todo mientras se mantiene la calidad de imagen como si nunca se tocara.

![Imágenes inteligentes](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_Las imágenes inteligentes optimizan automáticamente el formato y el tamaño de archivo de una imagen en función de la capacidad del explorador y la velocidad de red del cliente._

Las imágenes inteligentes no están activadas de forma predeterminada, ya que requieren un esfuerzo coordinado entre usted y el soporte técnico de Dynamic Media de Adobe. Además, la activación de imágenes inteligentes requiere una limpieza completa de la caché de CDN, que luego se completa con el tiempo. Si le interesa utilizar imágenes inteligentes, puede trabajar con Adobe para activarlas enviando un ticket de asistencia técnica. El soporte técnico le proporciona un parámetro de URL que le permite probar, de antemano, imágenes inteligentes. Puede probarlo en cualquiera de sus páginas web o imágenes para poder ver el rendimiento que obtiene y los ahorros. Puede activar las imágenes inteligentes para todo el sitio.

### Conjuntos de vídeos adaptables

Cuando hay un vídeo en una página o en una página principal, los clientes tienden a interactuar con ese contenido durante más tiempo y permanecer en la página más tiempo, lo que suele ser bueno. Este comportamiento se ha mostrado a través de análisis que ha realizado el Adobe. Sin embargo, el vídeo puede ser complejo. Por un lado, a menudo tiene un archivo principal grande. Es complicado determinar el tamaño y la distribución del vídeo, todo para garantizar que la experiencia se ejecute sin problemas independientemente del dispositivo en el que se visualice e independientemente del ancho de banda.

Para resolver este problema, Dynamic Media le ofrece la posibilidad de crear _Conjuntos de vídeos adaptables_.

![Conjunto de vídeos adaptables](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_Un conjunto de vídeos adaptables agrupa versiones del mismo vídeo codificadas con diferentes velocidades de bits y formatos._

Comienza con el vídeo principal original, que se carga en el sistema. Tamaño automático de Dynamic Media o _transcodifica_, ese vídeo en varios vídeos. A continuación, en el momento de la entrega, determina de forma inteligente qué pantalla de vídeo, qué calidad y qué formato usar y la envía al teléfono, la tableta o el equipo de escritorio.

Por ejemplo, en un dispositivo móvil iOS, detecta un ancho de banda como 4G, 5G o Wi-Fi. A continuación, selecciona automáticamente el vídeo codificado correcto entre las distintas tasas de bits de vídeo del conjunto de vídeos adaptables. El vídeo se transmite a dispositivos móviles, tabletas o equipos de escritorio.

Además, la calidad de vídeo se cambia de forma dinámica automáticamente si cambian las condiciones de red. Además, si un cliente entra en el modo de pantalla completa en un escritorio, el conjunto de vídeos adaptables responde mediante una mejor resolución, lo que mejora la experiencia de visualización del cliente.

El uso de conjuntos de vídeos adaptables proporciona una reproducción fluida y de alta calidad para los clientes que reproducen vídeo de Dynamic Media en varias pantallas y dispositivos. Realmente elimina la complejidad del vídeo.

## Ejemplos de uso de Dynamic Media {#dm-journey-b}

Los siguientes son problemas comunes de casos de uso y soluciones con las que Dynamic Media puede ayudarlo a impulsar la participación positiva, la lealtad, la conversión y el aumento del ROI de los clientes.

### Caso de uso: Enfoque del archivo principal

Uno de los casos de uso más importantes para Dynamic Media también es uno de los más obvios. Es decir, reducir el peso de las páginas y experiencias, y el tamaño del contenido, ya sea una imagen o un vídeo, que se está entregando.

A continuación se muestra una experiencia o página web típica. Alrededor del 90% de una página está formada por medios enriquecidos, como imágenes y vídeos, que suelen ser archivos mucho más pesados.

![Ponderación de la página de contenido](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_Ponderación de la página de contenido de una página web típica._

El 10 % restante es HTML, código CSS y etiquetas específicas. Desea optimizar el 90 % de peso de esa página, y Dynamic Media ayuda con ese esfuerzo. Antes, leías sobre el concepto de _un archivo de recursos principal con infinitas posibilidades_. Este método es significativo para reducir el peso general de la página. La capacidad de tomar un recurso principal y utilizarlo en una página de detalles del producto, una página en miniatura, el carro de compras y la cuadrícula de búsqueda es un bueno proveedor de horas. También garantiza la coherencia entre las experiencias.

![Enfoque del archivo principal](/help/assets/dynamic-media/assets/dm-onefile.png)
_El reloj es un archivo de recurso principal, pero con varias representaciones de él (no copias) creadas sobre la marcha._

Analicemos más de cerca los problemas que Dynamic Media está solucionando con el archivo único y algunas de las soluciones para ese enfoque.

| **Problema** | **Solución Dynamic Media** |
|---|---|
| Cree y almacene cada recurso. | Utilice un solo archivo de imagen y cree automáticamente las representaciones necesarias solo en el momento de la entrega. |
| Altos costos de almacenamiento de información. | Elimina la necesidad de crear y almacenar varias copias de un recurso. |
| Dificultad para mantener la cadena de custodia. | Garantiza la entrega de experiencias coherentes y optimizadas para dispositivos. |
| No hay historial de versiones. |  |
| Experiencias de marca incoherentes en todos los dispositivos. |  |
| Coste innecesario de la creación de recursos duplicados. |  |

Cuando piensa en un archivo, está creando un recurso para cada tipo de experiencia. Es posible que tenga una imagen de inicio y luego tenga que crear 20, 30 o 40 variaciones de esa imagen, que en última instancia tiene que almacenar y pagar por ese almacenamiento.

A continuación, debe asegurarse de que se utiliza la imagen correcta y que esto puede afectar a su capacidad de mantener la coherencia en las marcas. Y, si no encuentra una imagen, tiene que volver y duplicar esos recursos.

Dynamic Media permite crear variaciones de imágenes, sobre la marcha, a partir de esa imagen inicial. Le permite ser creativo con ese recurso principal y no tener que ir y volver con su artista de diseño gráfico o estudio de fotos para crear contenido adicional. Y eso es dinero y tiempo ahorrado.

Con el enfoque de un archivo, se utiliza un solo archivo principal. A continuación, cree las versiones o representaciones necesarias en los distintos sitios, propiedades y experiencias, solo en el momento en que un cliente las envía o ve. Esta eficacia puede reducir en gran medida la cantidad de almacenamiento necesario para sus activos y la complejidad general del flujo de trabajo. Además, con el sistema de entrega de Dynamic Media, garantiza que todas las imágenes y vídeos se optimizan, se cargan rápidamente y tengan un aspecto bueno en todas las pantallas y dispositivos.

### Caso de uso: Vídeo

Otro caso de uso para el que Dynamic Media resuelve es el vídeo. El vídeo es complejo. Es difícil de manejar. Los archivos de vídeo son difíciles de almacenar y mover debido a sus tamaños de archivo inherentes.

| **Problema** | **Solución Dynamic Media** |
|---|---|
| Es difícil administrar y entregar vídeo optimizado para varios dispositivos. | Utilice un solo vídeo que cambie el tamaño automáticamente para todos los dispositivos. |
| Los vídeos se detienen o reproducen de baja calidad debido al ancho de banda disponible para el usuario final. | Entregue vídeo a través de un reproductor HTML que detecte automáticamente el ancho de banda disponible y adapte la calidad para garantizar una reproducción fluida y de alta fidelidad. |
| No es factible y lleva mucho tiempo crear manualmente todas las versiones de un vídeo solo para garantizar una buena visualización y reproducción entre dispositivos. | Elimine las horas de tedioso trabajo de transcodificación con un flujo de trabajo simplificado. |
|  | Libere tiempo para trabajos de mayor valor. |

Los clientes llegan a Dynamic Media con el siguiente problema que esperan resolver:

&quot;_Tenemos el video, y gastamos mucho dinero creándolo. Pero hemos evitado colocarlo en páginas o entregarlo, porque de nuestras pruebas, realmente no podemos garantizar la calidad del vídeo, o si realmente va a reproducirse. Y, en última instancia, eso afecta a nuestras marcas y potencialmente a nuestro papel hasta en la conversión._&quot;

La solución de Dynamic Media es tomar ese archivo de vídeo principal y dejar que Dynamic Media realice todos los tamaños a través de su proceso de transcodificación. A continuación, empareja esto con el reproductor de vídeo inteligente de Dynamic Media. Este flujo de trabajo garantiza que, tanto si utiliza ese vídeo en la página de aterrizaje principal como en una categoría o página de detalles del producto, será coherente en todo momento y se entregará con alta calidad.

Estos son varios casos de uso más a considerar.

### Caso de uso: Una única fuente de verdad

| **Problema** | **Solución Dynamic Media** |
|---|---|
| Recursos digitales dispersos por toda la organización, aislados en diferentes equipos o unidades de negocio. | Almacene y administre todos los recursos digitales en una ubicación central. |
| Los integrantes del equipo descargan y crean versiones locales. | Los integrantes del equipo utilizan un solo archivo principal para crear _y_ ofrece todas las versiones necesarias en distintos tamaños de pantalla y dispositivos. |
| Recursos de un solo uso creados para cada experiencia y dispositivo. | Elimina los activos de un solo uso, ahorrando tiempo y dinero al crearlos. |

### Caso de uso: Recorte inteligente con tecnología IA para medios enriquecidos

| **Problema** | **Solución Dynamic Media** |
|---|---|
| El tiempo y el trabajo intensivos en dibujar, medir y cortar manualmente imágenes o vídeos para resaltar el punto focal y mostrar adecuadamente en todos los tamaños y dispositivos de pantalla. | Utiliza Recorte inteligente en Dynamic Media, una función de Adobe Sensei AI, para detectar automáticamente el punto focal en cualquier imagen o vídeo y recortar para mantenerlo. |
| Tiempo perdido que se podría invertir mejor en la creación de experiencias de alto impacto. | Captura el punto de interés deseado independientemente del tamaño de la pantalla. |
| Recursos de un solo uso creados para cada experiencia y dispositivo. | Elimina las tediosas tareas manuales y ofrece imágenes y vídeos de alta calidad y de carga rápida que se ven bien en cualquier dispositivo o pantalla. |

### Caso de uso: Creación de contenido interactivo

| **Problema** | **Solución Dynamic Media** |
|---|---|
| Experiencias de cliente planas y estáticas que no atraen, generan lealtad ni impulsan la conversión. | Permite a los usuarios no técnicos agregar fácilmente y sin problemas elementos interactivos como zonas interactivas, carruseles y conjuntos de giros para obtener experiencias más dinámicas y atractivas. |
| Rendimiento limitado de la inversión de activos digitales y experiencias de cliente deslucidas. | Impulsa la conversión y el retorno de la inversión a partir de experiencias de medios enriquecidos. |

## Cómo fluye un recurso a través del sistema Dynamic Media {#dm-journey-c}

A continuación se muestra un flujo de trabajo típico de Dynamic Media.

![Flujo de trabajo de Dynamic Media](/help/assets/dynamic-media/assets/dm-workflow.png)
_Cómo fluye un recurso a través del sistema Dynamic Media._

Empiece con la fase de creación con el objetivo principal de que el recurso principal se encuentre al final. Estos recursos principales podrían provenir de sesiones fotográficas, de proveedores de vídeo o podrían ser algunos archivos de audio que haya creado. Puede utilizar las aplicaciones Creative Suite de Adobe como Adobe InDesign, Adobe Photoshop o Adobe Illustrator para ayudarle a determinar el contenido.

Cuando la parte de creación haya terminado, puede colocar el recurso en la solución de creación cargando el recurso en Dynamic Media. Dentro de Dynamic Media, asegúrese de tener los ajustes preestablecidos de imagen y los visualizadores adecuados alineados para las distintas páginas web del sitio.

Y, finalmente, optimiza todo ese contenido y publíquelo en los servidores de Dynamic Media para que esté disponible para la web, la impresión, el correo electrónico, los escritorios y los dispositivos móviles.

### Carga de recursos en Dynamic Media

Cuando termine de crear un recurso principal, cárguelo en Dynamic Media. El tipo de archivo que carga, el formato y el tamaño del archivo son atributos importantes para Dynamic Media. Es en el momento de la carga que desea asegurarse de que obtiene el máximo valor de la compatibilidad con un archivo.

Por ejemplo, la imagen del reloj que aparece a continuación es de 4560 x 3020 píxeles. Y aunque nunca se use una imagen de ese tamaño, se puede seguir cargando. Cuanto más grande sea la imagen, mejor será la calidad que Dynamic Media puede proporcionar, incluso hasta una representación en miniatura. Recuerde: puede _disminuir_ la resolución de una imagen existente. Pero si tratas de _aumentar_ la resolución de una imagen probablemente no resulte satisfactoria.

![Formatos recomendados para cargar en Dynamic Media](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_Consideraciones sobre la carga de recursos._

Adobe recomienda cargar los recursos en un formato sin pérdidas. Por lo general, es mejor evitar el JPEG, ya que al entregar un JPEG o al seguir guardando un JPEG, se empieza a perder la calidad de la imagen con el paso del tiempo. Desea comenzar con las imágenes de mayor resolución en un formato sin pérdidas con el que puede vivir. Ese formato suele ser un TIFF o un archivo PNG.

En cuanto al espacio de color, cuando piensa en un canal digital o en una vista web, normalmente piensa en el RGB (rojo, verde, azul).

La mayoría nunca pensaría en entregar algo en CMYK o en por qué podría incluso querer entregar en CMYK. El motivo es que ese espacio de color se utiliza con mayor frecuencia para enviar elementos impresos. Sin embargo, Dynamic Media puede ofrecer en ambos espacios de color.

Hay muchos clientes que todavía imprimen, como los clubs de mayoristas de almacenes. Y hay tiendas de comestibles que a menudo imprimen volantes semanalmente. Estos clientes requieren que sus imágenes estén en ambos espacios de color. Tradicionalmente, eso requeriría dos imágenes diferentes: uno en RGB y otro en CMYK. Sin embargo, puede cargar recursos CMYK directamente en Dynamic Media y hacer que Dynamic Media envíe recursos de RGB a través de un ajuste preestablecido de imagen o a través de un perfil de color de forma automática. No es necesario crear varias versiones de un archivo, manteniendo así el concepto de _un archivo de recursos principal con infinitas posibilidades_.

<!-- **The Value of Renditioning??? or Demo portion** -->

### Publicar y previsualizar recursos

Una vez cargados los recursos en Dynamic Media, se recomienda _publicar_ seleccionan los recursos y, a continuación, hacen clic en **[!UICONTROL Publicación]** o **[!UICONTROL Publicación rápida]** en Dynamic Media. La publicación de recursos es necesaria si desea utilizarlos en cualquier experiencia. Una vez publicados los recursos, quedan disponibles para su inclusión en una página web mediante una URL generada por Dynamic Media que copie o mediante la incrustación de código en la página.

Además de publicar recursos manualmente, puede configurar Dynamic Media para que publique los recursos instantáneamente, sin intervención del usuario, en el momento de la carga.

Después de la carga, hay diferentes formas de previsualizar las representaciones de un recurso en Dynamic Media. La vista previa de representaciones puede ayudarle a hacerse una idea de lo que ve un cliente. Un método de vista previa habitual es seleccionar un recurso y, a continuación, ver sus representaciones seleccionando una _ajuste preestablecido de imagen_ tal como se ve a continuación.

![Vista previa de una representación de un recurso en función del ajuste preestablecido de imagen grande](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_Vista previa de una representación de un recurso en función del ajuste preestablecido de imagen &quot;Grande&quot; seleccionado. Se hizo clic en el botón URL . La ruta de URL resultante contiene el nombre de ajuste preestablecido de imagen &quot;Grande&quot; y se puede utilizar en una página web._

¡La URL anterior está activa! [Pruébelo](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$){target=&quot;_blank&quot;}.

Otro método para obtener una vista previa de un recurso es seleccionar un recurso de imagen y, a continuación, seleccionar un _Visualizadores_ preestablecido como se ve en el siguiente.

![Vista previa de un recurso en función del ajuste preestablecido de visor de zoom vertical Light](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_Vista previa de un recurso en función del ajuste preestablecido de visualizador &quot;ZoomVertical_light&quot; seleccionado. El puntero del ratón (`+`) se movió sobre el reloj para acercar. Observe los botones URL e Incrustar ._

¡La representación de arriba está activa! [Pruébelo](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&amp;config=jpearldemo/ZoomVertical_light){target=&quot;_blank&quot;}.

## Opcional: Más información

La parte I de este recorrido abarcaba los conceptos básicos de una variedad de temas de Dynamic Media. Si desea obtener más información sobre lo que acaba de leer, utilice los materiales siguientes para explorar conceptos con buenos detalles. De lo contrario, puede continuar con la parte II de su recorrido. Consulte [Siguientes pasos en este Recorrido de Dynamic Media](#whats-next).

_Temas de ayuda de Dynamic Media_

* [Trabajar con Dynamic Media en Experience Manager](/help/assets/dynamic-media/dynamic-media.md)
* [Acerca de las imágenes inteligentes](/help/assets/dynamic-media/imaging-faq.md)
* [Cómo crear conjuntos de vídeos adaptables](/help/assets/dynamic-media/video.md)
* [Práctica recomendada para optimizar la calidad de las imágenes](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [Cómo cargar recursos](/help/assets/add-assets.md#upload-assets)
* [Cómo previsualizar recursos](/help/assets/dynamic-media/previewing-assets.md)
* [Cómo previsualizar recursos 3D](/help/assets/dynamic-media/previewing-3d-assets.md)
* [Cómo entregar Dynamic Media Assets](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [Cómo publicar recursos](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [Trabajo con Publicación selectiva en Dynamic Media](/help/assets/dynamic-media/selective-publishing.md)

_Tutoriales de Dynamic Media_

* [Uso de Dynamic Media con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=es)
* [Biblioteca de contenido de Adobe Experience Manager](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (busque en _Dynamic Media_)

_Visores de Dynamic Media_

* [Demostraciones en directo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) de cada visor

## Siguientes pasos en este Recorrido de Dynamic Media {#whats-next}

En la parte II de este recorrido, examinará las URL de Dynamic Media un poco más de cerca para comprender mejor qué sucede cuando se entrega un recurso. También obtendrá más información sobre los aspectos básicos de la creación de ajustes preestablecidos de imagen para procesar recursos, y aprenderá sobre los conjuntos de imágenes, los conjuntos de giros y los conjuntos de medios mixtos y cómo se crean.

Llévame a [recorrido de Dynamic Media: Conceptos básicos, parte II](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d).

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->