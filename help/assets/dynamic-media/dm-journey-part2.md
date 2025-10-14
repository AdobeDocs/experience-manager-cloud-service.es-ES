---
title: Recorrido en Dynamic Media, parte II
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
exl-id: cdca41ad-a2cd-4f68-aaa4-5eec33c30f0b
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '2621'
ht-degree: 0%

---

# Recorrido de Dynamic Media: Conceptos básicos, parte II  {#dm-journey-part2}

{{see-also-dm}}

Bienvenido a Recorrido de Dynamic Media: Conceptos básicos, parte II, donde aprenderá lo siguiente:

* Estructura de una URL de Dynamic Media y cómo Dynamic Media entrega contenido.
* Aspectos básicos de la creación de ajustes preestablecidos de imagen para procesar recursos.
* Conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos.

Consulte también [Recorrido de Dynamic Media; Conceptos básicos, parte I](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>Para obtener los mejores resultados, Adobe recomienda leer y ver este Recorrido de Dynamic Media en un equipo de escritorio.

## Estructura de una URL de Dynamic Media y cómo Dynamic Media entrega contenido {#dm-journey-d}

Una vez cargados y publicados los recursos de Dynamic Media, puede copiar la URL generada de un recurso y pegarla en el explorador para ver cómo aparecerá el recurso para un cliente. La siguiente URL copiada para una imagen de reloj se desglosa por color para facilitar su lectura y comprensión.

![Estructura de una URL de Dynamic Media](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Estructura de una URL de Dynamic Media._

La primera parte de la dirección URL en rojo hace referencia al propio dominio del servidor. En este caso, Dynamic Media se está ejecutando en un dominio de servidor genérico, que es `https://s7d1.scene7.com/is/image/`. Es fácil poder ver un conjunto de imágenes y comprender si están siendo proporcionadas por Dynamic Media simplemente mirando el dominio del servidor. La dirección URL va a ser bastante coherente. Sin embargo, hay algunos clientes de Dynamic Media que han cambiado a un dominio de servidor dedicado donde podría ser `name-of-your-company.scene7.com`. Se requiere un dominio de servidor dedicado para imágenes inteligentes.

El nombre de la cuenta es la porción en morado. En este caso, la cuenta se llama `jpearldemo`.

El nombre o ID del recurso `AdobeStock_28563982` está en verde. Observe que el recurso tiene _no_ extensión de archivo, como `.png` o `.jpg`. Cuando los recursos se incorporan en Dynamic Media, la extensión de archivo se elimina y se crea un tipo diferente de archivo: un archivo piramidal de TIFF. El pyramic-TIFF permite a Dynamic Media crear rápidamente representaciones sobre la marcha.

Y finalmente, hay algunos parámetros de procesamiento de imágenes, `?wid=1000&fmt=jpeg&qlt=85`, que se muestran en amarillo al final.

La ruta de URL completa está activa. [Inténtelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&fmt=jpeg&qlt=85){target="_blank"}.

Con la ventana del explorador aún abierta a la URL de Dynamic Media y a la imagen del reloj, veamos más de cerca cómo puede crear representaciones de la imagen solo cambiando la URL.

### Representar la imagen del reloj mediante la dirección URL

Comience eliminando manualmente solo las reglas de procesamiento de imágenes en la ruta URL; deje el nombre del servidor, el nombre de cuenta y el ID del recurso o el nombre de la imagen. [Inténtelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target="_blank"}.

Ahora añada un parámetro de procesamiento de imagen al final de la dirección URL. En el campo URL, a la derecha del nombre de la imagen, escriba `?wid=500` y luego presione **[!UICONTROL Intro]**. [Inténtelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target="_blank"}.

Observe que se genera una nueva representación del reloj. Una clave para entender de este sencillo ejercicio de cambiar el ancho de la imagen, es que la imagen vista se genera 100% dinámicamente.

Ahora cambie el valor de anchura de `500` píxeles a `1000` píxeles y, a continuación, presione **[!UICONTROL Entrar]**. [Inténtelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target="_blank}.
En el momento en que pulse **[!UICONTROL Intro]**, el explorador volverá al servidor de imágenes de Dynamic Media. Genera una representación completamente nueva del reloj, en función del nuevo valor de anchura que acaba de introducir, devuelve la nueva imagen al explorador y la almacena en caché.

Dynamic Media tiene numerosos parámetros de procesamiento de imágenes que puede utilizar para ajustar los recursos de imagen en las páginas web. Puedes [ver una lista de ellos aquí](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=es).

Ahora intente agregar un parámetro de rotación a la imagen del reloj. Y el final de la ruta de la dirección URL, inmediatamente después de `wid=1000`, escriba `&rotate=90` y, a continuación, presione **[!UICONTROL Entrar]**. [Inténtelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&rotate=90){target="_blank"}.

El reloj sigue un poco sesgado hacia la izquierda. Cambie el valor de giro de `90` a `92` y, a continuación, presione **[!UICONTROL Entrar]**. [Inténtelo](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&rotate=9){target="_blank"}.

De nuevo, en el momento en que presiona **[!UICONTROL Enter]**, se genera una nueva representación del reloj de forma casi instantánea. Puede ver el tipo de rendimiento que obtiene, lo que explica por qué Dynamic Media puede entregar más de 800 000 solicitudes de imagen, _por segundo_, en un fin de semana ajetreado o en vacaciones importantes.

Aunque es posible cambiar los parámetros de procesamiento de imágenes en una URL imagen por imagen, no es un método eficiente, especialmente si tiene decenas de miles de imágenes que conforman su sitio web. Un enfoque mucho mejor es el uso de ajustes preestablecidos de imagen.

## Aspectos básicos de la creación de ajustes preestablecidos de imagen para procesar recursos {#dm-journey-e}

Existen varias formas y lugares en los que querrá crear una imagen o en los que una imagen estará disponible. Tradicionalmente, un Creative entra en Adobe Photoshop y guarda cada una de estas diferentes representaciones como imágenes estáticas.

![Imágenes estáticas](/help/assets/dynamic-media/assets/dm-static-images.png)
_Bueno: imágenes estáticas, cada una creada manualmente._

Ahora imaginen que el director de Creative mira las imágenes y dice:

_&quot;Realmente quería esta toma para que la mano grande señale a los cuatro y la mano pequeña señale al 1 para que el dial del reloj sea más fácil de ver.&quot;_

El creativo tendría que volver a rodar todas las nuevas imágenes estáticas.

Sin embargo, con Dynamic Media, si tiene diferentes ajustes preestablecidos de imagen, puede utilizar esas imágenes dondequiera que las necesite. Los ajustes preestablecidos de imagen aplican estándares.

![Método de archivo principal](/help/assets/dynamic-media/assets/dm-onefile.png)
_Mejor: un archivo con varias representaciones creadas sobre la marcha mediante ajustes preestablecidos de imagen, como `Search_Grid` y `Thumbnail`._

| **¿Por qué usar ajustes preestablecidos de imagen?** | |
|---|---|
| Estándares | Los ajustes preestablecidos de imagen aplican un tratamiento de procesamiento de imagen estándar a cualquier imagen con la que se solicite. |
| Administración de cambios | Si debe cambiar el procesamiento de imágenes, simplemente edite el parámetro del ajuste preestablecido de imagen existente. La definición actualizada se propaga automáticamente a todas las solicitudes. |

Cada lugar donde necesite tener un tipo particular de imagen, por ejemplo,

* una página de detalles del producto,
* cuadrícula de búsqueda,
* miniatura,
* tarjeta de compra, o
* imagen a pantalla completa

Desea que la imagen se envíe con los mismos parámetros dondequiera que se vayan a utilizar.

Por un momento, veamos cómo se crea un ajuste preestablecido de imagen en Dynamic Media.

![Creando un ajuste preestablecido de imagen que comienza con la pestaña Básico](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_Creando un ajuste preestablecido de imagen a partir de la ficha Básico._

En el ejemplo anterior, puede ver que se creó un nuevo ajuste preestablecido de imagen con el nombre _Medium_. Dynamic Media utiliza una imagen de ejemplo predeterminada, la mochila, para ayudarle a ver las características del ajuste preestablecido de imagen a medida que lo crea.

El ajuste preestablecido de imagen _Medium_ tiene una anchura de 500 píxeles y una altura de 800 píxeles. En la parte I de este Recorrido, se explica cómo ofrecer recursos en diferentes formatos. En el menú desplegable **[!UICONTROL Formato]**, puede elegir enviar recursos como JPEG, PNG, TIFF o varios otros formatos. Aquí tiene flexibilidad.

Al seleccionar la pestaña **[!UICONTROL Avanzado]**, tiene opciones para el espacio de color del recurso. Según el formato que haya seleccionado en la ficha **[!UICONTROL Básico]** (en el ejemplo anterior, se seleccionó JPEG), puede enviar recursos en RGB, escala de grises o CMYK. En el menú desplegable **[!UICONTROL Perfil de color]**, puede seleccionar cómo desea enviar un recurso de imagen CMYK para utilizarlo en la impresión. Tenga en cuenta también que hay parámetros adicionales que puede aplicar para enfocar las imágenes. En este caso, se aplicó **[!UICONTROL máscara de enfoque]**.

![Creación de un ajuste preestablecido de imagen seleccionando opciones en la pestaña Avanzado](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_Creando un ajuste preestablecido de imagen seleccionando opciones en la pestaña Avanzado._

Recuerda en [Anatomía de una URL de Dynamic Media](#dm-journey-d) anteriormente, que leíste acerca de la URL de Dynamic Media y cómo se genera. En el cuadro de texto **[!UICONTROL Modificador de imagen]** es donde puede escribir cualquier parámetro de procesamiento de imagen adicional que desee. Los parámetros se incluyen en el nombre del ajuste preestablecido de la URL cuando se entregan las imágenes mediante el ajuste preestablecido. En la captura de pantalla anterior, se agregó el parámetro `bgc=451B15`. Es decir, se ha añadido un color de fondo marrón oscuro.

Puede considerar un ajuste preestablecido de imagen como una fórmula para sus imágenes. Entregará todas las imágenes que utilicen el ajuste preestablecido, de forma coherente, cada vez; será el mismo. También se agregó el parámetro `&op_brightness=+10` para aumentar ligeramente el brillo.

Cuando haya terminado, guarde el ajuste preestablecido y ya estará disponible para todas las imágenes que tenga. En este caso, desea aplicar el ajuste preestablecido de imagen _Medium_ a una imagen de un tazón de chocolate líquido.

![Aplicando el ajuste preestablecido de imagen *Medium* para generar una representación de una imagen](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_Aplicando el ajuste preestablecido de imagen Medium para generar una representación de una imagen._

Copie la dirección URL y péguela en el explorador para comprobar el aspecto de la imagen. [Inténtelo](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target="_blank"}.

En el explorador, observe el nombre del ajuste preestablecido de imagen _Medium_ en la ruta de URL completa.

Se puede ver el tipo de claridad que se muestra en la imagen. Esa cualidad se debe en parte a la forma en que el tazón de chocolate fue disparado. Además, se debe en parte a que con Dynamic Media puede almacenar imágenes más grandes que las que se envían a los canales digitales.

Si todo parece satisfactorio para tu tazón de chocolate, pega la URL en tus páginas web donde quieras que aparezca la imagen en tu sitio web.

Si observa de nuevo la siguiente imagen del reloj, verá que hay un ajuste preestablecido de imagen `Cart`, un ajuste preestablecido de `Grid`, un ajuste preestablecido de `Large`, un ajuste preestablecido de `PDP-page` (página de detalles del producto) y varios más.

![Ajustes preestablecidos de imagen estática y dinámica](/help/assets/dynamic-media/assets/dm-image-presets.png)
_Ajustes preestablecidos de imagen estáticos y dinámicos. La imagen del reloj se representó mediante el ajuste preestablecido de imagen `PDP-page`._

Pero, ¿qué sucede si tiene que cambiar una imagen de su sitio web? Por ejemplo, supongamos que ha realizado algunas pruebas y ha detectado que la imagen de 120 x 120 (el ajuste preestablecido de imagen `Cart`) no se recibe como esperaba. Para aumentar el tamaño de la imagen, aumente la anchura a 175 píxeles y la altura a 175 píxeles. Tradicionalmente, tendría que entrar en Adobe Photoshop y volver a crear todas esas imágenes del carro de compras. Sin embargo, con Dynamic Media, solo tiene que editar el ajuste preestablecido de imagen actualizando los valores de Anchura y Altura a 175 y guardar el ajuste preestablecido, como se ve en el ejemplo siguiente.

![Edición de un ajuste preestablecido de imagen](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_Edición de la anchura y altura del ajuste preestablecido de imagen `Cart`._

Después de cambiar el ajuste preestablecido de imagen y vaciar la caché, todas las imágenes se actualizan y todas las direcciones URL que se usan con ese ajuste preestablecido hacen que _no_ cambie en cualquier lugar. Esto significa que no son necesarios vínculos rotos ni redirecciones de páginas web.

## Conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos {#dm-journey-f}

Algunos de los usos más populares de Dynamic Media son la capacidad de crear conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos.

Los conjuntos de imágenes suelen estar formados por una serie de recursos de imagen que se presentan como una sola entidad. Este tipo de conjuntos proporcionan a los usuarios una experiencia de visualización integrada, en la que pueden ver diferentes vistas de un elemento haciendo clic en una imagen en miniatura. Los conjuntos de imágenes permiten presentar vistas alternativas de algo y el visor ofrece herramientas de zoom para examinar las imágenes de cerca. [Ver un conjunto de imágenes llamado &quot;En ejecución&quot; que usa el visor flotante](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

Aquí dentro de Dynamic Media puede ver varias imágenes de zapatillas de running. Es una serie de líneas de productos que las ventas y el marketing desean que los clientes vean como una sola presentación; un conjunto de imágenes.

![Creando un conjunto de imágenes](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_Inicio de la creación de un conjunto de imágenes._

Para crear el conjunto de imágenes, elige **[!UICONTROL Conjunto de imágenes]** en el menú desplegable **[!UICONTROL Crear]**. Observe en el menú que también hay opciones para crear un **[!UICONTROL conjunto de medios mixtos]**, un **[!UICONTROL conjunto de giros]** y un **[!UICONTROL conjunto de carrusel]**. Estos conjuntos se crean de forma muy similar a un conjunto de imágenes.

Un conjunto de medios mixtos puede contener imágenes, conjuntos de muestras, conjuntos de giros, vídeos y conjuntos de vídeos adaptables. [Inténtelo](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). Un conjunto de giros simula el acto del mundo real de girar un objeto para examinarlo. Los conjuntos de giros permiten ver los detalles visuales clave desde cualquier ángulo. [Inténtelo](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&stagesize=500,400){target="_blank"}.

La creación de un conjunto de imágenes es sencilla. Simplemente, agregue los recursos de imagen que desee incluir en el conjunto.

![Creando un conjunto de imágenes](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_El editor de conjuntos de imágenes permite agregar recursos de imagen y reordenar su apariencia en el conjunto._

Debe asignar un nombre al conjunto. Elija el nombre con cuidado porque no puede editarlo más adelante. En el ejemplo anterior, el conjunto se llama `Running`. Cuando haya terminado, guarde el conjunto.

Y aquí está el conjunto de imágenes `Running` en Experience Manager Assets.

![Conjunto de imágenes en ejecución en Experience Manager Assets, vista de tarjeta](/help/assets/dynamic-media/assets/dm-image-set.png)
_El conjunto de imágenes `Running` en Experience Manager Assets, vista de tarjeta._

Tanto si ha creado un conjunto de imágenes, un conjunto de medios mixtos, un conjunto de giros o cualquier otro medio interactivo, después de crear el conjunto, desea ver cómo aparece y se comporta para un cliente. Dynamic Media tiene numerosos visores integrados que le permiten hacer precisamente eso.

Para empezar, seleccione el conjunto de imágenes creado para abrirlo en una vista previa, como se ve en el siguiente ejemplo.

![El conjunto de imágenes en ejecución en la vista previa con la opción Visualizadores seleccionada](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_La imagen `Running` establecida en la vista previa con la opción Visualizadores seleccionada._

Observe en la vista previa que puede seleccionar las muestras de zapatillas de running y acercar y alejar las zapatillas. Para aplicar un visor al conjunto, selecciona **[!UICONTROL Visualizadores]** en el menú desplegable.

![Conjunto de imágenes en ejecución con el visor flotante aplicado](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_El conjunto de imágenes `Running` con el visor flotante aplicado._

En este caso, se seleccionó el visor `Flyout`. En este punto, puede obtener una vista previa del conjunto de imágenes en el visor. Sin embargo, es mejor verlo en su navegador, justo cómo lo ve un cliente. Selecciona **[!UICONTROL URL]** en la esquina inferior izquierda, luego copia la URL y péguela en el navegador. [Inténtelo](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&config=jpearldemo/Flyout){target="_blank"}.

La dirección URL única permite utilizar el conjunto de imágenes y el visor donde los necesite en el sitio web. Es posible que haya notado en el ejemplo anterior que **[!UICONTROL Embed]** está a la derecha del botón URL. Seleccionando **[!UICONTROL Incrustar]**, puede copiar el código para este conjunto/visor de imágenes y añadirlo a una página web o a un componente de Experience Manager Sites.

El visor flotante es un visor predeterminado y listo para usar cuyas propiedades puede editar. O bien, como con la creación de un ajuste preestablecido de imagen, puede crear su propio visor personalizado.

Ahora, supongamos que a su equipo de ventas y marketing no le gusta el visor flotante. Les gusta la función de zoom, pero quieren que los clientes vean el efecto de zoom directamente sobre los zapatos. En tal caso, simplemente aplique el visor InlineZoom al conjunto de imágenes y copie y pegue su URL en el explorador para ver cómo se comporta. [Inténtelo](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&config=jpearldemo/InlineZoom){target="_blank"}.

Cuando mueve el puntero del mouse sobre el zapato, se acerca a esa imagen y puede ver más detalles a medida que mueve el puntero. Y la razón es simplemente el tamaño de la imagen que se cargó inicialmente en Dynamic Media.

Al considerar la posibilidad de vivir como consumidor, o al trabajar en su función diaria, y al visitar diferentes sitios web, ve cosas como esta. Piense en cómo se está haciendo y cómo puede utilizar el poder de Dynamic Media en su propio trabajo y en el sitio web de su compañía.

Acaba de leer acerca de los conjuntos de imágenes y visores. Veamos un par de otros visores y pruébelos en recursos individuales. Para restablecer el visor, haga clic en el botón **[!UICONTROL Actualizar]** en la esquina inferior izquierda.

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` visor aplicado a un recurso de imagen. [Inténtelo](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&config=jpearldemo/ZoomVertical_dark){target="_blank"}.
* `Zoom_light` visor aplicado a una imagen. [Inténtelo](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&config=jpearldemo/Zoom_light){target="_blank"}.

## Opcional: Más información

Si desea obtener más información sobre lo que acaba de leer, utilice los materiales siguientes para explorar los conceptos con mayor detalle. De lo contrario, el Recorrido de Dynamic Media se habrá completado.

<!--
_Dynamic Media Help topics_

* [How to create image presets](/help/assets/dynamic-media/image-presets.md)
* A list of [image processing parameters](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=es) that you can use in the Image Modifier field when you create an image preset
* [How to preview assets](/help/assets/dynamic-media/previewing-assets.md)
* [How to preview 3D assets](/help/assets/dynamic-media/previewing-3d-assets.md)
* [How to create Image sets](/help/assets/dynamic-media/image-sets.md)
* [How to create Spin sets](/help/assets/dynamic-media/spin-sets.md)
* [How to create Mixed Media sets](/help/assets/dynamic-media/mixed-media-sets.md) -->

_Tutoriales de Dynamic Media_

* [Usar Dynamic Media con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=es)
* [Biblioteca de contenido de Adobe Experience Manager](https://experienceleague.adobe.com/es?lang=en#recommended/solutions/experience-manager) (buscar en _Dynamic Media_)

_Visores de Dynamic Media_

* [Demostraciones en directo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) de cada visor

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->