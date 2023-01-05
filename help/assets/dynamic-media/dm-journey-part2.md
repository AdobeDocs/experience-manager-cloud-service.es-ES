---
title: Recorrido en Dynamic Media, parte II
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
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 9202cf44595070c98ca3d21887dff257bcd88b87
workflow-type: tm+mt
source-wordcount: '2902'
ht-degree: 0%

---

# recorrido de Dynamic Media: Conceptos básicos, parte II  {#dm-journey-part2}

Bienvenido al Recorrido de Dynamic Media: Aspectos básicos, parte II, en la que puede esperar aprender lo siguiente:

* Anatomía de una URL de Dynamic Media y cómo Dynamic Media ofrece contenido
* Aspectos básicos de la creación de ajustes preestablecidos de imagen para procesar recursos
* Conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos

Consulte también [recorrido de Dynamic Media; Conceptos básicos, parte I](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>Para obtener mejores resultados, Adobe recomienda leer y ver este Recorrido de Dynamic Media en un equipo de escritorio.

## Anatomía de una URL de Dynamic Media y cómo Dynamic Media ofrece contenido {#dm-journey-d}

Una vez cargados y publicados los recursos de Dynamic Media, puede copiar la URL generada de un recurso y pegarlo en el navegador para ver cómo aparecerá el recurso para un cliente. La siguiente URL copiada para una imagen de reloj se desglosa por color para facilitar su lectura y comprensión.

![Anatomía de una URL de Dynamic Media](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Anatomía de una URL de Dynamic Media._

La primera parte de la URL en rojo hace referencia al propio dominio del servidor. En este caso, Dynamic Media se ejecuta en un dominio de servidor genérico, que es `https://s7d1.scene7.com/is/image/`. Es fácil ver un conjunto de imágenes y comprender si Dynamic Media las está utilizando solo mirando el dominio del servidor. La URL va a ser bastante coherente. Sin embargo, hay algunos clientes de Dynamic Media que han cambiado a un dominio de servidor dedicado donde podría ser `name-of-your-company.scene7.com`. Se requiere un dominio de servidor dedicado para las imágenes inteligentes.

El nombre de la cuenta es la porción en morado. En este caso, se llama a la cuenta `jpearldemo`.

El ID o nombre del recurso, `AdobeStock_28563982` está en verde. Observe que el recurso tiene _no_ extensión de archivo como `.png` o `.jpg`. Cuando se incorporan recursos en Dynamic Media, la extensión de archivo se elimina y se crea un tipo de archivo diferente: un archivo piramidal-TIFF. El TIFF pirágico permite a Dynamic Media crear rápidamente representaciones sobre la marcha.

Y finalmente, hay algunos parámetros de procesamiento de imágenes, `?wid=1000&fmt=jpeg&qlt=85`, se muestra en amarillo al final.

La ruta de URL completa está activa. [Pruébelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85){target=&quot;_blank&quot;}.

Con la ventana del navegador aún abierta a la URL de Dynamic Media y a la imagen del reloj, vamos a ver cómo puede crear representaciones de la imagen cambiando la URL.

### Representación de la imagen del reloj a través de la URL

Comience eliminando manualmente solo las reglas de procesamiento de imágenes en la ruta URL; deje el nombre del servidor, el nombre de la cuenta y el ID del recurso o el nombre de la imagen. [Pruébelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target=&quot;_blank&quot;}.

Ahora agregue un parámetro de procesamiento de imagen al final de la dirección URL. En el campo URL, a la derecha del nombre de la imagen, escriba `?wid=500`y, a continuación, pulse **[!UICONTROL Entrar]**. [Pruébelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target=&quot;_blank&quot;}.

Observe que se genera una nueva representación del reloj. Una clave para entender de este simple ejercicio de cambiar la anchura de la imagen es que la imagen vista se genera 100% dinámicamente.

Ahora cambie el valor de anchura de `500` píxeles hasta `1000` píxeles y, a continuación, pulse **[!UICONTROL Entrar]**. [Pruébelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target=&quot;_blank}.
El momento en que presionas **[!UICONTROL Entrar]**, el explorador vuelve al servidor de imágenes de Dynamic Media. Genera una nueva representación del reloj, basada en el nuevo valor de anchura que acaba de escribir, luego envía la nueva imagen al explorador y la almacena en caché.

Dynamic Media tiene varios parámetros de procesamiento de imágenes que puede utilizar para ajustar los recursos de imagen en páginas web. Puede [vea una lista de ellos aquí](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en).

Ahora intente agregar un parámetro de rotación a la imagen del reloj. Y el final de la ruta URL, inmediatamente después `wid=1000`, tipo `&rotate=90`y, a continuación, presione **[!UICONTROL Entrar]**. [Pruébelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90){target=&quot;_blank&quot;}.

El reloj sigue ligeramente inclinado a la izquierda. Cambiar el valor de rotación de `90` a `92`y, a continuación, presione **[!UICONTROL Entrar]**. [Pruébelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target=&quot;_blank&quot;}.

Una vez más, el momento en que presionas **[!UICONTROL Entrar]**, se genera casi instantáneamente una nueva representación del reloj. Puede ver el tipo de rendimiento que obtiene, lo que explica por qué Dynamic Media puede entregar más de 800.000 solicitudes de imagen, _por segundo_, en un fin de semana ajetreado o en vacaciones importantes.

Aunque es posible cambiar los parámetros de procesamiento de imágenes en una URL imagen por imagen, no es un método eficiente, especialmente si tiene decenas de miles de imágenes que componen su sitio web. Un enfoque mucho mejor es usar ajustes preestablecidos de imagen.

## Aspectos básicos de la creación de ajustes preestablecidos de imagen para procesar recursos {#dm-journey-e}

Hay varias formas y lugares en los que va a querer crear una imagen o hacer que una imagen esté disponible. Tradicionalmente, un creativo entra en Adobe Photoshop y guarda cada una de estas representaciones como imágenes estáticas.

![Imágenes estáticas](/help/assets/dynamic-media/assets/dm-static-images.png)
_Bueno: imágenes estáticas, cada una creada manualmente._

Ahora imaginen el Creative Director mirando las imágenes y diciendo:

_&quot;Realmente quería esta toma para que la mano grande apunte hacia los cuatro, y la mano pequeña apunte hacia el 1 para hacer el reloj más fácil de ver&quot;._

El creativo tendría que volver a encontrar todas estas nuevas imágenes estáticas.

Pero, con Dynamic Media, si tiene diferentes ajustes preestablecidos de imagen, puede utilizar esas imágenes dondequiera que las necesite. Los ajustes preestablecidos de imagen hacen cumplir los estándares.

![Enfoque del archivo principal](/help/assets/dynamic-media/assets/dm-onefile.png)
_Mejor: un archivo con varias representaciones creadas sobre la marcha mediante ajustes preestablecidos de imagen, como `Search_Grid` y `Thumbnail`._

| **¿Por qué utilizar ajustes preestablecidos de imagen?** |  |
|---|---|
| Estándares | Los ajustes preestablecidos de imagen aplican un tratamiento de procesamiento de imagen estándar en cualquier imagen con la que se solicite. |
| Administración de cambios | Si debe cambiar el procesamiento de la imagen, simplemente edite el parámetro del ajuste preestablecido de imagen existente. La definición actualizada se propaga automáticamente a todas las solicitudes. |

Cada lugar donde necesite tener un tipo de imagen en particular, por ejemplo,

* una página de detalles del producto,
* cuadrícula de búsqueda,
* miniatura,
* tarjeta de compra, o
* imagen a pantalla completa

Desea que la imagen se envíe con los mismos parámetros dondequiera que se vayan a utilizar.

Por un momento, veamos cómo se crea un ajuste preestablecido de imagen en Dynamic Media.

![Creación de un ajuste preestablecido de imagen a partir de la ficha Básico](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_Creación de un ajuste preestablecido de imagen a partir de la ficha Básico ._

En el ejemplo anterior, puede ver que se creó un nuevo ajuste preestablecido de imagen con el nombre _Medio_. Dynamic Media utiliza una imagen predeterminada de ejemplo, la mochila, para ayudarle a ver las características del ajuste preestablecido de imagen a medida que lo crea.

La variable _Medio_ el ajuste preestablecido de imagen tiene una anchura de 500 píxeles y una altura de 800 píxeles. En la parte I de este Recorrido, se lee sobre la entrega de recursos en diferentes formatos. En el **[!UICONTROL Formato]** menú desplegable, puede elegir entregar recursos como JPEG, PNG, TIFF u otros formatos. Aquí tienes flexibilidad.

Al seleccionar la variable **[!UICONTROL Avanzadas]** le ofrece opciones para el espacio de color del recurso. Según el formato que haya seleccionado en la variable **[!UICONTROL Básico]** pestaña : en el ejemplo anterior, se ha seleccionado JPEG , puede enviar recursos en RGB, escala de grises o CMYK. En el **[!UICONTROL Perfil de color]** menú desplegable, puede seleccionar cómo enviar un recurso de imagen CMYK para utilizarlo en la impresión. Tenga en cuenta también que hay parámetros adicionales que puede aplicar para enfocar las imágenes. En este caso, **[!UICONTROL Máscara de enfoque]** se ha aplicado.

![Creación de un ajuste preestablecido de imagen seleccionando opciones en la pestaña Avanzado](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_Creación de un ajuste preestablecido de imagen seleccionando opciones en la pestaña Avanzado ._

Recuerda en [Anatomía de una URL de Dynamic Media](#dm-journey-d) antes, que lea sobre la URL de Dynamic Media y cómo se crea. La variable **[!UICONTROL Modificador de imagen]** es donde puede escribir cualquier parámetro adicional de procesamiento de imagen que desee. Los parámetros se incluyen en el nombre preestablecido de la URL cuando se entregan las imágenes, utilizando el ajuste preestablecido . En la captura de pantalla anterior, el parámetro `bgc=451B15` se ha añadido. Es decir, se añadió un color de fondo marrón oscuro.

Puede considerar un ajuste preestablecido de imagen como una receta para sus imágenes. Va a ofrecer cualquier imagen que utilice el ajuste preestablecido de forma consistente, siempre; va a ser lo mismo. El parámetro `&op_brightness=+10` también se agregó para aumentar ligeramente el brillo.

Cuando haya terminado, guarde el ajuste preestablecido y ahora estará disponible para todas las imágenes que tenga. En este caso, deseamos aplicar la variable _Medio_ imagen preestablecida a una imagen de un recipiente de chocolate líquido.

![Aplicación del ajuste preestablecido de imagen *Medio* para generar una representación de una imagen](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_Aplicar el ajuste preestablecido de imagen Medio para generar una representación de una imagen._

Copie la dirección URL y péguela en el navegador para comprobar el aspecto de la imagen. [Pruébelo](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target=&quot;_blank&quot;}.

En el navegador, observe el nombre del ajuste preestablecido de imagen _Medio_ en la ruta URL completa.

Se puede ver el tipo de claridad que se muestra en la imagen. Esa calidad se debe en parte a la forma en que se disparó el tazón de chocolate. Además, se debe en parte a que con Dynamic Media, se pueden almacenar imágenes más grandes que las que se entregan a los canales digitales.

Si todo parece satisfactorio para su bol de chocolate, pegue la URL en sus páginas web donde desea que la imagen aparezca en su sitio web.

Si mira de nuevo la imagen del reloj que aparece a continuación, puede ver que hay una `Cart` ajuste preestablecido de imagen, un `Grid` preestablecido, un `Large` preestablecido, un `PDP-page` (Página de detalles del producto) y varios otros ajustes preestablecidos.

![Ajustes preestablecidos de imagen estáticos y dinámicos](/help/assets/dynamic-media/assets/dm-image-presets.png)
_Ajustes preestablecidos de imagen estáticos y dinámicos. La imagen del reloj se procesó con la variable `PDP-page` ajuste preestablecido de imagen._

Pero, ¿qué pasa si tienes que cambiar una imagen en tu sitio web? Por ejemplo, supongamos que ha realizado algunas pruebas y ha encontrado que la imagen de 120 x 120 (la variable `Cart` imagen preestablecida) no se está recibiendo tan bien como pensó. Debe aumentar la anchura de la imagen a 175 píxeles y aumentar la altura a 175 píxeles. Tradicionalmente, tendría que entrar en Adobe Photoshop y volver a crear todas esas imágenes del carro de compras. Pero con Dynamic Media, simplemente puede editar el ajuste preestablecido de imagen actualizando los valores de anchura y altura a 175 y guardar el ajuste preestablecido, como se ve en el ejemplo siguiente.

![Edición de un ajuste preestablecido de imagen](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_Edición de la anchura y la altura de la variable `Cart` ajuste preestablecido de imagen._

Después de cambiar el ajuste preestablecido de imagen y vaciar la caché, todas las imágenes se actualizan y todas las URL que se utilizan con ese ajuste preestablecido, sí _not_ cambiar a cualquier lugar. Esto significa que no se necesitan enlaces rotos ni redirecciones de páginas web.

## Conjuntos de imágenes, Conjuntos de giros y Conjuntos de medios mixtos {#dm-journey-f}

Algunos de los usos más populares de Dynamic Media son la capacidad de crear conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos.

Los conjuntos de imágenes suelen estar formados por una serie de recursos de imagen que se presentan como una sola entidad. Este tipo de conjuntos proporcionan a los usuarios una experiencia de visualización integrada, en la que los usuarios pueden ver distintas vistas de un elemento haciendo clic en una imagen en miniatura. Los conjuntos de imágenes le permiten presentar vistas alternativas de algo y el visor ofrece herramientas de zoom para examinar las imágenes de cerca. [Ver un conjunto de imágenes llamado &quot;En ejecución&quot; que utiliza el visor flotante](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

Aquí dentro de Dynamic Media puede ver varias imágenes de zapatillas de correr. Es una serie de líneas de productos que las ventas y el marketing desean que los clientes vean como una única presentación; un conjunto de imágenes.

![Creación de un conjunto de imágenes](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_Inicio de la creación de un conjunto de imágenes._

Para crear el conjunto de imágenes, elija **[!UICONTROL Conjunto de imágenes]** de la variable **[!UICONTROL Crear]** menú desplegable. Observe en el menú que también hay opciones para crear un **[!UICONTROL Conjunto de medios mixtos]**, **[!UICONTROL Conjunto de giros]** y **[!UICONTROL Conjunto de carrusel]**. Estos conjuntos se crean del mismo modo que un conjunto de imágenes.

Un conjunto de medios mixtos puede contener imágenes, conjuntos de muestras, conjuntos de giros, vídeos y conjuntos de vídeos adaptables. [Pruébelo](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). Un conjunto de giros simula el acto real de girar un objeto para examinarlo. Los conjuntos de giros permiten ver detalles visuales clave desde cualquier ángulo. [Pruébelo](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400){target=&quot;_blank&quot;}.

La creación de un conjunto de imágenes es sencilla. Simplemente agregue los recursos de imagen que desee incluir en el conjunto.

![Creación de un conjunto de imágenes](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_El Editor de conjuntos de imágenes permite agregar recursos de imagen y reordenar su aspecto en el conjunto._

Debe asignar un nombre al conjunto. Elija el nombre con cuidado porque no puede editarlo más tarde. En el ejemplo anterior, el conjunto se llama `Running`. Cuando haya terminado, guarde el conjunto.

Y aquí está el `Running` Imagen establecida en Experience Manager Assets.

![El conjunto de imágenes en ejecución en Experience Manager Assets, vista de tarjeta](/help/assets/dynamic-media/assets/dm-image-set.png)
_La variable `Running` Imagen establecida en Experience Manager Assets, vista de tarjeta._

Tanto si ha creado un conjunto de imágenes, un conjunto de medios mixtos, un conjunto de giros o cualquier otro medio interactivo, después de crear el conjunto, desea ver cómo aparece y se comporta para un cliente. Dynamic Media tiene numerosos visores integrados que le permiten hacer exactamente eso.

Para empezar, seleccione el conjunto de imágenes generadas para abrirlo en una previsualización, como se ve en el siguiente ejemplo.

![El conjunto de imágenes en ejecución en la vista previa con la opción Visualizadores seleccionada](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_La variable `Running` Imagen establecida en la vista previa con la opción Visualizadores seleccionada._

Observe en la vista previa que puede seleccionar las muestras de zapato de carrera y acercar y alejar los zapatos. Para aplicar un visor al conjunto, seleccione **[!UICONTROL Visualizadores]** en el menú desplegable.

![El conjunto de imágenes en ejecución con el visor flotante aplicado](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_La variable `Running` Imagen establecida con el visor flotante aplicado._

En este caso, la variable `Flyout` está seleccionado. En este punto, puede obtener una vista previa del conjunto de imágenes en el visor. Pero, es mejor verlo en su navegador, tal como lo ve un cliente. Seleccione **[!UICONTROL URL]** en la parte inferior izquierda, copie la dirección URL y péguela en el explorador. [Pruébelo](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout){target=&quot;_blank&quot;}.

La URL única permite utilizar el conjunto de imágenes y el visor donde los necesita en el sitio web. Puede que haya notado en el ejemplo anterior que **[!UICONTROL Incrustar]** está a la derecha del botón URL . Seleccionando **[!UICONTROL Incrustar]**, puede copiar el código de este conjunto/visor de imágenes y añadirlo a una página web o a un componente de Experience Manager Sites.

El visor flotante es un visor predeterminado y listo para usar cuyas propiedades puede editar. O, al igual que crea un ajuste preestablecido de imagen, puede crear su propio visor personalizado.

Ahora, supongamos que a su equipo de ventas y marketing no le gusta el visor flotante. Les gusta la función de zoom, pero quieren que los clientes vean el efecto de zoom directamente sobre los zapatos. En este caso, simplemente debe aplicar el visor InlineZoom al conjunto de imágenes y copiar y pegar su URL en el navegador para ver cómo se comporta. [Pruébelo](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom){target=&quot;_blank&quot;}.

Cuando mueve el puntero del ratón sobre el zapato, lo amplía y puede ver más detalles a medida que mueve el puntero. Y la razón es simplemente el tamaño de la imagen que se cargó inicialmente en Dynamic Media.

Como uno considera vivir como consumidor, o mientras trabaja en su rol diario, y a medida que va a diferentes sitios web, ve cosas como esta. Piense en cómo se está haciendo esto, y cómo puede usar el poder de Dynamic Media en su propio trabajo y en el sitio web de su empresa.

Sólo lees un poco sobre los conjuntos de imágenes y los espectadores. Veamos un par de otros espectadores y probémoslos en recursos únicos. Para restablecer el visor, haga clic en el botón **[!UICONTROL Actualizar]** en la esquina inferior izquierda.

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` visualizador aplicado a un recurso de imagen. [Pruébelo](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark){target=&quot;_blank&quot;}.
* `Zoom_light` visualizador aplicado a una imagen. [Pruébelo](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light){target=&quot;_blank&quot;}.

## Opcional: Más información

Si desea obtener más información sobre lo que acaba de leer, utilice los materiales siguientes para explorar conceptos con buenos detalles. De lo contrario, el Recorrido de Dynamic Media se habrá completado.

_Temas de ayuda de Dynamic Media_

* [Cómo crear ajustes preestablecidos de imagen](/help/assets/dynamic-media/image-presets.md)
* Una lista de [parámetros de procesamiento de imagen](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) que puede utilizar en el campo Modificador de imagen al crear un ajuste preestablecido de imagen
* [Cómo previsualizar recursos](/help/assets/dynamic-media/previewing-assets.md)
* [Cómo previsualizar recursos 3D](/help/assets/dynamic-media/previewing-3d-assets.md)
* [Cómo crear conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md)
* [Cómo crear conjuntos de giros](/help/assets/dynamic-media/spin-sets.md)
* [Creación de conjuntos de medios mixtos](/help/assets/dynamic-media/mixed-media-sets.md)

_Tutoriales de Dynamic Media_

* [Uso de Dynamic Media con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=es)
* [Biblioteca de contenido de Adobe Experience Manager](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (busque en _Dynamic Media_)

_Visores de Dynamic Media_

* [Demostraciones en directo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) de cada visor

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->