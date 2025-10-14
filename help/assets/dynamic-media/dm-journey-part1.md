---
title: Recorrido de Dynamic Media, parte I
description: El Recorrido de Dynamic Media cubre los conceptos básicos de Dynamic Media, cómo funciona, qué puede hacer por usted y qué valor aporta a su trabajo y a sus clientes.
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles,Best Practices
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
exl-id: f3472006-d5ae-4f70-af3e-44e73aee85cc
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '3615'
ht-degree: 0%

---

# Recorrido de Dynamic Media: Conceptos básicos, parte I {#dm-journey-part1}

{{see-also-dm}}

Bienvenido al Recorrido de Dynamic Media.

Este recorrido cubre los conceptos básicos de Dynamic Media, cómo funciona, qué puede hacer por usted y qué valor aporta a su trabajo y a sus clientes.

**_Requisitos previos_**

* Comprensión básica de los formatos de imagen y vídeo
* Comprensión básica de HTML y CSS
* Comprensión básica de las herramientas de diseño como Adobe Illustrator, Adobe Photoshop y Adobe XD
* El acceso a Dynamic Media en Experience Manager es útil, pero no obligatorio

**_Lo que puede esperar aprender_**

_Parte I_

* ¿Qué es Dynamic Media y cómo puede ayudarle?
* Casos de uso para Dynamic Media
* Flujo de recursos a través del sistema de Dynamic Media

_Parte II_

* Estructura de una URL de Dynamic Media y cómo Dynamic Media entrega contenido
* Aspectos básicos de la creación de ajustes preestablecidos de imagen para procesar recursos
* Conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos

**_Audiencia_**
La audiencia que mejor se adapta a los lectores de este recorrido son los siguientes usuarios que son nuevos en Dynamic Media en Experience Manager:

* Administrador
* Analista empresarial
* Arquitecto de contenido
* Autor de contenido
* Designer
* Desarrollador
* Marketing
* Product Manager/Owner

>[!TIP]
>
>Para obtener los mejores resultados, Adobe recomienda leer y ver este Recorrido de Dynamic Media en un equipo de escritorio.

## ¿Qué es Dynamic Media y cómo puede ayudarle? {#dm-journey-a}

Dynamic Media le ayuda a ofrecer recursos de marketing y comercialización visuales enriquecidos bajo demanda. También le ayuda a crear y ofrecer experiencias de visualización interactivas, como zoom, giro de 360 grados y vídeo. Los recursos se escalan dinámicamente para su consumo en sitios web, móviles y sociales. Al utilizar un conjunto de recursos de origen principales, como imágenes, vídeo y 3D, Dynamic Media genera y ofrece varias variaciones de este contenido enriquecido, en tiempo real a través de su CDN (red de distribución de contenido) global, escalable y optimizada para el rendimiento.

Dynamic Media incorpora los flujos de trabajo de la solución de administración de recursos digitales de Adobe Experience Manager Assets para simplificar y optimizar el proceso de administración de campañas digitales.

### Un archivo con infinitas posibilidades

Uno de los puntos principales para entender Dynamic Media es el concepto de _un archivo de recursos principal con un sinfín de posibilidades_.

Para comprender mejor este concepto, piense en la forma en que trabaja tradicionalmente con un solo recurso, como una imagen o un vídeo. Normalmente, se crea un recurso principal. A continuación, cree manualmente versiones de ese mismo recurso para cada experiencia, cada dispositivo que se necesite, cada página web y cada propiedad donde se utilice. Con el tiempo, ese recurso único puede crecer hasta 20, 30 o más versiones, sin que se les adjunte un historial de versiones. Ahora, imaginen hacer eso para cada imagen o video que tengan. El número de versiones de recursos se convertiría rápidamente en abrumador para mantener y actualizar, sin mencionar el aumento en los costes de almacenamiento.

Dynamic Media, sin embargo, es fundamentalmente diferente de otros sistemas porque lo usa para entregar sus medios _dinámicamente_ desde recursos únicos, principales y desde llamadas a URL. Las rutas de URL de Dynamic Media que solicita incluyen instrucciones que indican al servidor de publicación de Adobe cómo mostrar el recurso cuando se envía a la pantalla de un cliente. Por ejemplo, con el mismo recurso principal, puede entregarlo instantáneamente en representaciones ilimitadas, cambiando el tamaño, el formato, la resolución, el peso, el color, el recorte y los efectos como una vista de zoom.

Este método de entrega único garantiza que las experiencias de calidad coherentes se envíen a cualquier pantalla, independientemente del tamaño o el ancho de banda. Los vídeos de tamaño completo también están optimizados para todos los tipos de pantalla y se transmiten de forma adaptativa para garantizar una experiencia de usuario uniforme y de calidad.

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![Adobe Dynamic Media entrega la misma imagen principal a diferentes medios en diferentes tamaños y formatos](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)
_Adobe Dynamic Media garantiza que las experiencias coherentes y de calidad se entreguen a cualquier pantalla, independientemente del tamaño o el ancho de banda._

A medida que siga leyendo, aprenderá más sobre por qué este concepto de &quot;un archivo de recursos principal, posibilidades ilimitadas&quot; es importante.

### La red de distribución de contenido

Cuando esté listo para su lanzamiento con un recurso de imagen o de vídeo, la red troncal de Dynamic Media, que consta de una potente red de entrega de nivel superior, lo admite. La red atiende a cientos de clientes en todo el mundo todos los días. Los recursos se distribuyen en la red de entrega de contenido (o CDN) alojada en Akamai. La red de distribución de contenido (CDN) es un sistema de servicios informáticos conectados en red que cooperan de forma transparente para ofrecer contenido, especialmente contenido multimedia enriquecido de gran tamaño, a los usuarios finales.

En el sistema CDN, el contenido web se almacena en cachés web a través de Internet. A continuación, se envía desde la caché web a los usuarios finales para realizar una entrega más rápida. Por lo tanto, la primera vez que alguien descarga una página web, los recursos que ve se envían a una caché de CDN. Se almacenan en el servidor para que la próxima vez que alguien en la misma área acceda a la página web, el mismo contenido en caché se envíe más rápido. El contenido se entrega más rápido porque se encuentra más cerca del usuario. Una CDN hace que la página web se muestre más rápido y, sin embargo, reduce la demanda de ancho de banda en el servidor central porque el contenido se entrega desde una red de caché, no desde un servidor central en cada caso. Este flujo optimizado significa una mejor experiencia de usuario, lo que conduce a mayores ventas.

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

Históricamente, la CDN entrega 3,5 petabytes de tráfico a los clientes cada mes. El sistema puede entregar 52.000 millones de activos en un solo día. Ese número equivale a 864.000 imágenes y vídeos que se entregaron correctamente a los clientes, _cada segundo_.

### Imágenes inteligentes

Dynamic Media ya realiza un buen trabajo para optimizar recursos y garantizar que cada recurso se cargue rápidamente en sistemas móviles y de escritorio, a través de la red de distribución de contenido (CDN). Para que esto suceda, se utilizan ajustes preestablecidos de imagen en Dynamic Media para definir la calidad de la imagen. También definen el tipo de imagen que está enviando, su nitidez y otras piezas para diversas partes de sus experiencias o páginas.

Pero para agregar valor a Dynamic Media más allá de los ajustes preestablecidos de imagen, hay _Imágenes inteligentes_.

Imágenes inteligentes proporciona un rendimiento de entrega de recursos de imagen aún mejor al optimizar automáticamente el formato y el tamaño de archivo de una imagen en función de la capacidad del explorador del cliente. Funciona con los ajustes preestablecidos de imagen existentes (los ajustes preestablecidos de imagen se tratan en la parte II de este recorrido) y utiliza inteligencia en la entrega.

Esta inteligencia reduce aún más el tamaño del archivo de imagen en función de la velocidad de conexión de red y del explorador. Dado que los recursos de imagen representan la mayor parte del tiempo de carga de una página, la mejora de rendimiento puede tener un impacto profundo en los indicadores clave de negocio, como:

* Mayor conversión
* Tiempo empleado en el sitio
* Tasa de salida hacia otro sitio inferior

En general, con imágenes inteligentes, se puede esperar una mejora del rendimiento del 22 % al 47 % en función de los ajustes preestablecidos de imagen existentes y las características específicas del usuario final. Todo manteniendo la calidad de imagen como si nunca se tocara.

![Imágenes inteligentes](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
_Imágenes inteligentes optimiza automáticamente el formato y el tamaño de archivo de una imagen en función de la capacidad del explorador y la velocidad de red del cliente._

Las imágenes inteligentes no están activadas de forma predeterminada porque requieren un esfuerzo coordinado entre usted y el servicio de asistencia técnica de Adobe Dynamic Media. Además, para habilitar Imágenes inteligentes es necesario borrar completamente la caché de CDN, que luego se rellenará con el tiempo. Si está interesado en utilizar imágenes inteligentes, puede trabajar con Adobe para activarlo enviando un ticket de asistencia técnica. El soporte técnico le proporciona un parámetro de URL que le permite probar, de antemano, imágenes inteligentes. Puede probarlo en cualquiera de sus páginas web o imágenes para que pueda ver el rendimiento que obtiene y los ahorros. A continuación, puede activar las imágenes inteligentes para todo el sitio.

### Conjuntos de vídeos adaptables

Cuando hay un vídeo en una página o en una página principal, los clientes tienden a interactuar con ese contenido durante más tiempo y a permanecer en la página más tiempo, lo que generalmente es bueno. Este comportamiento se muestra a través de análisis que ha realizado Adobe. Sin embargo, el vídeo puede ser complejo. Por un lado, a menudo tiene un archivo principal grande. Es complicado determinar el tamaño y la entrega del vídeo, todo para garantizar que la experiencia se ejecute sin problemas independientemente del dispositivo en el que se esté viendo e independientemente del ancho de banda.

Para resolver este problema, Dynamic Media le permite crear _conjuntos de vídeos adaptables_.

Un conjunto de vídeos adaptable agrupa versiones del mismo vídeo que se codifican en diferentes velocidades de bits y formatos.

Empiece con el vídeo original principal, que carga en el sistema. Dynamic Media cambia el tamaño automáticamente o _transcodifica_ ese vídeo en varios vídeos. A continuación, en el momento de la entrega, determina de forma inteligente qué pantalla de vídeo, qué calidad y qué formato utilizar, y la envía al teléfono, a la tableta o al equipo de escritorio.

Por ejemplo, en un dispositivo móvil iOS, detecta un ancho de banda como 4G, 5G o Wi-Fi. A continuación, selecciona automáticamente el vídeo codificado correcto entre las distintas velocidades de bits de vídeo dentro del conjunto de vídeos adaptables. El vídeo se transmite a dispositivos móviles, tabletas o equipos de escritorio.

Además, la calidad de vídeo cambia automáticamente si cambian las condiciones de la red. Además, si un cliente entra en modo de pantalla completa en un equipo de escritorio, el conjunto de vídeos adaptable responde con una mejor resolución, lo que mejora la experiencia de visualización del cliente.

El uso de conjuntos de vídeos adaptables proporciona una reproducción suave y de alta calidad para los clientes que reproducen vídeo de Dynamic Media en varias pantallas y dispositivos. Realmente elimina la complejidad del vídeo.

## Casos de uso para Dynamic Media {#dm-journey-b}

Los siguientes son problemas comunes de casos de uso y soluciones con los que Dynamic Media puede ayudarle para impulsar una participación positiva de los clientes, la lealtad, la conversión y un ROI aumentado.

### Caso de uso: enfoque de archivo principal

Uno de los casos de uso más importantes para Dynamic Media también es uno de los más obvios. Es decir, reducir el peso de las páginas y experiencias, y el tamaño del contenido, ya sea una imagen o un vídeo que se está entregando.

A continuación se muestra una experiencia típica o una página web. Alrededor del 90% de una página está formada por medios enriquecidos, como imágenes y vídeos, que suelen ser archivos mucho más pesados.

![Peso de página de contenido](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
_Peso de página de contenido de una página web típica._

El 10 % restante es HTML, código CSS y etiquetas específicas. Desea optimizar el 90 % de peso de esa página y Dynamic Media le ayuda con ese esfuerzo. Anteriormente, leyó acerca del concepto de _un archivo de recurso principal con infinitas posibilidades_. Este enfoque es significativo para reducir el peso total de la página. La capacidad de tomar un recurso principal y utilizarlo en una página de detalles del producto, una página de miniaturas, el carro de compras y la cuadrícula de búsqueda es un gran ahorro de tiempo. Además, garantiza la coherencia en todas las experiencias.

![Método de archivo principal](/help/assets/dynamic-media/assets/dm-onefile.png)
_El reloj es un archivo de recursos principal, pero con varias representaciones (no copias) creadas sobre la marcha._

Veamos más de cerca los problemas que Dynamic Media está resolviendo con el único archivo y algunas de las soluciones a ese enfoque.

| **Problema** | **Solución de Dynamic Media** |
|---|---|
| Cree y almacene cada recurso. | Utilice un solo archivo de imagen, creando automáticamente las representaciones necesarias solo en el momento de la entrega. |
| Costes de almacenamiento elevados. | Elimina la necesidad de crear y almacenar varias copias de un recurso. |
| Dificultad para mantener la cadena de custodia. | Garantiza la entrega de experiencias coherentes y optimizadas para el dispositivo. |
| No hay historial de versiones. | |
| Experiencias de marca incoherentes entre dispositivos. | |
| Coste innecesario de la creación de recursos duplicados. | |

Cuando piensa en un archivo, está creando un recurso para cada tipo de experiencia. Es posible que tenga una imagen inicial y luego tenga que crear 20, 30 o 40 variaciones de esa imagen, que finalmente tiene que almacenar y pagar por ese almacenamiento.

Luego debe asegurarse de que se utiliza la imagen correcta y que esto puede afectar a su capacidad para tener coherencia en todas las marcas. Y, si no encuentra una imagen, debe volver a entrar y duplicar esos recursos.

Dynamic Media le permite crear variaciones de imágenes, sobre la marcha, a partir de esa imagen inicial. Le permite ser creativo con ese recurso principal y no tener que ir y venir con su artista de diseño gráfico o estudio de fotografía para crear contenido adicional. Y eso es dinero y tiempo ahorrado.

Con el enfoque de un solo archivo, se utiliza un solo archivo principal. A continuación, cree las versiones o representaciones necesarias en los sitios, las propiedades y las experiencias solo en el momento en que un cliente las envía o las ve. Esta eficiencia puede disminuir en gran medida la cantidad de almacenamiento necesario para sus recursos y reducir la complejidad general del flujo de trabajo. Además, con el sistema de entrega de Dynamic Media, se garantiza que todas las imágenes y vídeos estén optimizados, se carguen rápidamente y tengan un aspecto impecable en todas las pantallas y dispositivos.

### Caso de uso: vídeo

Otro caso de uso que Dynamic Media resuelve es el vídeo. El vídeo es complejo. Es difícil de manejar. Los archivos de vídeo son difíciles de almacenar y mover debido a sus tamaños de archivo inherentes.

| **Problema** | **Solución de Dynamic Media** |
|---|---|
| Difícil de administrar y ofrecer vídeo optimizado para varios dispositivos. | Utilice un solo vídeo que cambie automáticamente el tamaño de todos los dispositivos. |
| Los vídeos se bloquean o se reproducen en baja calidad debido al ancho de banda disponible del usuario. | Ofrezca vídeo a través de un reproductor HTML que detecta automáticamente el ancho de banda disponible y adapta la calidad para garantizar una alta fidelidad y una reproducción fluida. |
| Crear manualmente todas las versiones de un vídeo no es factible y lleva mucho tiempo, solo para garantizar una buena visualización y reproducción en todos los dispositivos. | Elimine horas de tedioso trabajo de transcodificación con un flujo de trabajo simplificado. |
| | Libere tiempo para un trabajo de mayor valor. |

Los clientes llegan a Dynamic Media con los siguientes problemas que esperan resolver:

&quot;_Mi negocio tiene el video, y el departamento gastó una gran cantidad de dinero creándolo, pero evitó colocarlo en páginas o entregarlo. La razón era que a partir de las pruebas, la calidad del vídeo no podía ser garantizada, o incluso si realmente iba a jugar. Y, en última instancia, esto afecta la marca del negocio y potencialmente su papel en la conversión._&quot;

La solución de Dynamic Media es tomar ese archivo de vídeo principal y permitir que Dynamic Media realice todos los tamaños a través de su proceso de transcodificación. A continuación, vincúlelo con el reproductor de vídeo inteligente de Dynamic Media. Este flujo de trabajo garantiza que, tanto si utiliza ese vídeo en la página de aterrizaje principal, como en una categoría o página de detalles del producto, será coherente en todo y se entregará con una alta calidad.

Estos son varios casos de uso más que hay que tener en cuenta.

### Caso de uso: Una sola fuente de verdad

| **Problema** | **Solución de Dynamic Media** |
|---|---|
| Recursos digitales repartidos por toda la organización, en silos en distintos equipos o unidades empresariales. | Almacene y administre todos los recursos digitales en una ubicación central. |
| Los integrantes del equipo descargan y crean versiones locales. | Los integrantes del equipo utilizan un solo archivo principal para crear _y_ y entregar todas las versiones necesarias en varios dispositivos y tamaños de pantalla. |
| Recursos de un solo uso creados para cada experiencia y dispositivo. | Elimina los activos de un solo uso, lo que ahorra tiempo y dinero al crearlos. |

### Caso de uso: Recorte inteligente con tecnología de IA para medios enriquecidos

| **Problema** | **Solución de Dynamic Media** |
|---|---|
| Dibujar, medir y cortar manualmente imágenes o vídeos que requieren mucho tiempo y trabajo para resaltar el punto focal y mostrarlos correctamente en todos los tamaños y dispositivos de pantalla. | Utiliza Recorte inteligente en Dynamic Media, una capacidad de IA de Adobe Sensei, para detectar automáticamente el punto focal en cualquier imagen o vídeo, y recortar para mantenerlo. |
| Tiempo perdido que podría dedicarse mejor a crear experiencias de alto impacto. | Registra el punto de interés deseado independientemente del tamaño de la pantalla. |
| Recursos de un solo uso creados para cada experiencia y dispositivo. | Elimina las tareas manuales tediosas y ofrece imágenes y vídeo de alta calidad y carga rápida que se ven bien en cualquier dispositivo o pantalla. |

### Caso de uso: Creación de medios interactivos

| **Problema** | **Solución de Dynamic Media** |
|---|---|
| Experiencias de cliente planas y estáticas que no atraigan, generen lealtad ni promuevan la conversión. | Permite a los usuarios no técnicos añadir de forma fácil y sencilla elementos interactivos como puntos interactivos, carruseles y conjuntos de giros para lograr experiencias más dinámicas y atractivas. |
| Rendimiento limitado de la inversión de activos digitales y experiencias de cliente deslucidas. | Impulsa la conversión y el retorno de la inversión de las experiencias con medios enriquecidos. |

## Flujo de recursos a través del sistema de Dynamic Media {#dm-journey-c}

A continuación se muestra un flujo de trabajo típico de Dynamic Media.

![Flujo de trabajo de Dynamic Media](/help/assets/dynamic-media/assets/dm-workflow.png)
_Flujo de recursos a través del sistema Dynamic Media._

Se comienza con la fase de creación con el objetivo principal de que el recurso principal finalice. Estos recursos principales podrían proceder de sesiones fotográficas, de proveedores de vídeo o podrían ser algunos archivos de audio que haya creado. Puede utilizar las aplicaciones de Creative Suite de Adobe, como Adobe InDesign, Adobe Photoshop o Adobe Illustrator, para ayudarle a elaborar el contenido.

Cuando finalice la parte de creación, coloque el recurso en la solución de creación cargándolo en Dynamic Media. En Dynamic Media, asegúrese de tener los ajustes preestablecidos de imagen y los visores adecuados en línea para las distintas páginas web del sitio.

Y, en última instancia, optimiza todo ese contenido y lo publica en servidores de Dynamic Media para que esté disponible para la web, la impresión, el correo electrónico, los escritorios y los dispositivos móviles.

### Carga de recursos en Dynamic Media

Cuando termine de crear un recurso principal, cárguelo en Dynamic Media. El tipo de archivo que carga y el formato y el tamaño del archivo son atributos importantes de Dynamic Media. Es en el momento de la carga que desea asegurarse de obtener el máximo valor de la compatibilidad con un archivo.

Por ejemplo, la imagen del reloj siguiente es de 4560 x 3020 píxeles. Y aunque es posible que nunca use una imagen de ese tamaño, aún puede cargarla. Cuanto mayor sea la imagen, mejor será la calidad que Dynamic Media podrá ofrecer, incluso en una representación de miniaturas. Recuerde: puede _disminuir_ fácilmente la resolución de una imagen existente. Pero si intenta _aumentar_ la resolución de una imagen, es probable que el resultado no sea satisfactorio.

![Formatos recomendados para cargar en Dynamic Media](/help/assets/dynamic-media/assets/dm-upload-formats.png)
_Consideraciones para las cargas de recursos._

Adobe recomienda cargar los recursos en un formato sin pérdidas. En general, es mejor evitar JPEG porque cuando entrega JPEG o cuando sigue guardando JPEG, empieza a perder calidad de imagen con el tiempo. Desea comenzar con las imágenes de mayor resolución en un formato sin pérdidas con el que puede vivir. Dicho formato suele ser un archivo TIFF o PNG.

En cuanto al espacio de color, cuando piensa en un canal digital o una vista web, normalmente piensa en RGB (rojo, verde, azul).

La mayoría nunca pensaría en entregar algo en CMYK o por qué podría incluso querer hacerlo en CMYK. El motivo es que ese espacio de color se utiliza con más frecuencia para enviar artículos impresos. Sin embargo, Dynamic Media puede ofrecer en ambos espacios de color.

Hay muchos clientes que todavía imprimen, como los clubes de venta al por mayor de almacenes. Y hay tiendas de comestibles que a menudo imprimen volantes semanalmente. Estos clientes requieren que sus imágenes estén en ambos espacios de color. Tradicionalmente, esto requería dos imágenes diferentes: una en RGB y otra en CMYK. Sin embargo, puede cargar recursos CMYK directamente en Dynamic Media y hacer que Dynamic Media envíe recursos de RGB a través de un ajuste preestablecido de imagen o a través de un perfil de color automáticamente. No es necesario crear varias versiones de un archivo, manteniendo así el concepto de _un archivo de recurso principal con un sinfín de posibilidades_.

<!-- **The Value of Renditioning??? or Demo portion** -->

### Publicación y previsualización de recursos

Después de cargar recursos en Dynamic Media, se recomienda _publicarlos_; para ello, seleccione los recursos y haga clic en **[!UICONTROL Publicar]** o **[!UICONTROL Publicación rápida]** en Dynamic Media. La publicación de recursos es necesaria si desea utilizarlos en cualquier experiencia. Una vez publicados, los recursos están disponibles para su inclusión en una página web mediante una URL generada por Dynamic Media que copia, o mediante la incrustación de código en la página.

Además de publicar recursos manualmente, puede configurar Dynamic Media para que publique recursos al instante, sin ninguna intervención del usuario, en el momento de la carga.

Después de la carga, hay diferentes formas de previsualizar las representaciones de un recurso en Dynamic Media. La vista previa de representaciones puede ayudarle a hacerse una idea de lo que ve un cliente. Un método común de vista previa es seleccionar un recurso y luego ver sus representaciones seleccionando un _ajuste preestablecido de imagen_, tal como se ve a continuación.

![Vista previa de una representación de un recurso basada en el ajuste preestablecido de imagen grande](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
_Vista previa de una representación de un recurso en función del ajuste preestablecido de imagen &quot;Grande&quot; seleccionado. Se hizo clic en el botón URL. La ruta de URL resultante contiene el nombre del ajuste preestablecido de imagen &quot;Grande&quot; y se puede utilizar en una página web._

La URL anterior está activa. [Inténtelo](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$){target="_blank"}.

Otro método para obtener una vista previa de un recurso es seleccionar el recurso de imagen y, a continuación, seleccionar un ajuste preestablecido de _Visores_, tal como se ve a continuación.

![Vista previa de un recurso basado en el ajuste preestablecido de visor de luz vertical de zoom](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
_Vista previa de un recurso en función del ajuste preestablecido de visualizador &quot;ZoomVertical_light&quot; seleccionado. El puntero del mouse (`+`) se movió sobre el reloj para aumentar la vista. Observe los botones URL e Incrustar._

La representación anterior está activa. [Inténtelo](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&config=jpearldemo/ZoomVertical_light){target="_blank"}.

## Opcional: Más información

La parte I de este recorrido abarcó los conceptos básicos de varios temas relacionados con Dynamic Media. Si desea obtener más información sobre lo que lee, utilice los materiales a continuación para explorar conceptos con mayor detalle. De lo contrario, puede continuar con la Parte II de su recorrido. Ver [Qué sigue en este Recorrido de Dynamic Media](#whats-next).

<!--
_Dynamic Media Help topics_

* [Work with Dynamic Media in Experience Manager](/help/assets/dynamic-media/dynamic-media.md)
* [About Smart Imaging](/help/assets/dynamic-media/imaging-faq.md)
* [How to create Adaptive Video Sets](/help/assets/dynamic-media/video.md)
* [Best practices for optimizing the quality of your images](/help/assets/dynamic-media/best-practices-for-optimizing-the-quality-of-your-images.md)
* [How to upload assets](/help/assets/add-assets.md#upload-assets)
* [How to preview assets](/help/assets/dynamic-media/previewing-assets.md)
* [How to preview 3D assets](/help/assets/dynamic-media/previewing-3d-assets.md)
* [How to deliver Dynamic Media Assets](/help/assets/dynamic-media/delivering-dynamic-media-assets.md)
* [How to publish assets](/help/assets/dynamic-media/publishing-dynamicmedia-assets.md)
* [Work with Selective Publish in Dynamic Media](/help/assets/dynamic-media/selective-publishing.md) -->

_Tutoriales de Dynamic Media_

* [Usar Dynamic Media con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=es)
* [Biblioteca de contenido de Adobe Experience Manager](https://experienceleague.adobe.com/es?lang=en#recommended/solutions/experience-manager) (buscar en _Dynamic Media_)

_Visores de Dynamic Media_

* [Demostraciones en directo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) de cada visor

## Qué sigue en este Recorrido de Dynamic Media {#whats-next}

En la parte II de este recorrido, se examinan detenidamente las URL de Dynamic Media para comprender mejor qué sucede cuando se envía un recurso. También obtendrá más información sobre los aspectos básicos de la creación de ajustes preestablecidos de imagen para procesar recursos, y sobre los conjuntos de imágenes, los conjuntos de giros y los conjuntos de medios mixtos y cómo se crean.

Lléveme a [Recorrido de Dynamic Media: Conceptos básicos, Parte II](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d).

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->