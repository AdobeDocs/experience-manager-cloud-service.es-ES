---
title: Recorrido en Dynamic Media, parte II
description: El Recorrido de Dynamic Media cubre los conceptos básicos de Dynamic Media, su funcionamiento, lo que puede hacer por usted y el valor que aporta a su trabajo y a sus clientes.
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
source-git-commit: f0e9fe0bdf35cc001860974be1fa2a7d90f7a3a9
workflow-type: tm+mt
source-wordcount: '2875'
ht-degree: 0%

---

# Recorrido de Dynamic Media: Conceptos básicos, parte II  {#dm-journey-part2}

Bienvenido al Recorrido de Dynamic Media: Conceptos básicos, parte II, donde aprenderá lo siguiente:

* Estructura de una URL de Dynamic Media y cómo Dynamic Media entrega el contenido
* Aspectos básicos de la creación de ajustes preestablecidos de imagen para procesar recursos
* Conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos

Consulte también [Recorrido de Dynamic Media; Conceptos básicos, parte I](/help/assets/dynamic-media/dm-journey-part1.md).

>[!TIP]
>
>Para obtener los mejores resultados, Adobe recomienda leer y ver este Recorrido de Dynamic Media en un equipo de escritorio.

## Estructura de una URL de Dynamic Media y cómo Dynamic Media entrega el contenido {#dm-journey-d}

Una vez cargados y publicados los recursos de Dynamic Media, puede copiar la URL generada de un recurso y pegarla en el explorador para ver cómo aparecerá el recurso para un cliente. La siguiente URL copiada para una imagen de reloj se desglosa por color para facilitar su lectura y comprensión.

![Estructura de una URL de Dynamic Media](/help/assets/dynamic-media/assets/dm-colored-url.png)
_Estructura de una URL de Dynamic Media._

La primera parte de la dirección URL en rojo hace referencia al propio dominio del servidor. En este caso, Dynamic Media se está ejecutando en un dominio de servidor genérico, que es `https://s7d1.scene7.com/is/image/`. Es fácil poder ver un conjunto de imágenes y comprender si Dynamic Media las proporciona simplemente mirando el dominio del servidor. La dirección URL va a ser bastante coherente. Sin embargo, hay algunos clientes de Dynamic Media que han cambiado a un dominio de servidor específico en el que podría estar `name-of-your-company.scene7.com`. Se requiere un dominio de servidor dedicado para imágenes inteligentes.

El nombre de la cuenta es la porción en morado. En este caso, se llama a la cuenta `jpearldemo`.

El nombre o ID del recurso, `AdobeStock_28563982` está en verde. Observe que el recurso tiene _no_ extensión de archivo como `.png` o `.jpg`. Cuando los recursos se incorporan en Dynamic Media, la extensión de archivo se elimina y se crea un tipo diferente de archivo: un archivo TIFF piramidal. El TIFF pirámico permite a Dynamic Media crear rápidamente representaciones sobre la marcha.

Y finalmente, hay algunos parámetros de procesamiento de imágenes, `?wid=1000&fmt=jpeg&qlt=85`, se muestra en amarillo al final.

La ruta de URL completa está activa. [Pruébelo.](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?wid=1000&amp;fmt=jpeg&amp;qlt=85){target="_blank"}.

Con la ventana del explorador aún abierta a la URL de Dynamic Media y a la imagen del reloj, veamos más de cerca cómo puede crear representaciones de la imagen solo cambiando la URL.

### Representar la imagen del reloj mediante la dirección URL

Comience eliminando manualmente solo las reglas de procesamiento de imágenes en la ruta URL; deje el nombre del servidor, el nombre de cuenta y el ID del recurso o el nombre de la imagen. [Pruébelo.](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982){target="_blank"}.

Ahora añada un parámetro de procesamiento de imagen al final de la dirección URL. En el campo URL, a la derecha del nombre de la imagen, escriba `?wid=500`y luego pulse **[!UICONTROL Entrar]**. [Pruébelo.](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=500){target="_blank"}.

Observe que se genera una nueva representación del reloj. Una clave para entender de este sencillo ejercicio de cambiar el ancho de la imagen, es que la imagen vista se genera 100% dinámicamente.

Ahora cambie el valor de anchura de `500` píxeles a `1000` píxeles y luego presione **[!UICONTROL Entrar]**. [Pruébelo.](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000){target="_blank}.
En el momento en que pulse **[!UICONTROL Entrar]**, el explorador vuelve al servidor de imágenes de Dynamic Media. Genera una representación completamente nueva del reloj, en función del nuevo valor de anchura que acaba de introducir, devuelve la nueva imagen al explorador y la almacena en caché.

Dynamic Media tiene numerosos parámetros de procesamiento de imágenes que puede utilizar para ajustar los recursos de imagen en las páginas web. Puede [consulte la lista aquí.](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html?lang=en).

Ahora intente agregar un parámetro de rotación a la imagen del reloj. Y el final de la ruta URL, inmediatamente después de `wid=1000`, tipo `&rotate=90`y, a continuación, pulse **[!UICONTROL Entrar]**. [Pruébelo.](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=90){target="_blank"}.

El reloj sigue un poco sesgado hacia la izquierda. Cambiar el valor de rotación de `90` hasta `92`y, a continuación, pulse **[!UICONTROL Entrar]**. [Pruébelo.](https://s7d1.scene7.com/is/image/jpearldemo/AdobeStock%5F28563982?wid=1000&amp;rotate=9){target="_blank"}.

De nuevo, en el momento en que presionas **[!UICONTROL Entrar]**, se genera una nueva representación del reloj de forma casi instantánea. Puede ver el tipo de rendimiento que obtiene, lo que explica por qué Dynamic Media puede entregar más de 800 000 solicitudes de imagen, _por segundo_, en un fin de semana ajetreado o en vacaciones importantes.

Aunque es posible cambiar los parámetros de procesamiento de imágenes en una URL imagen por imagen, no es un método eficiente, especialmente si tiene decenas de miles de imágenes que conforman su sitio web. Un enfoque mucho mejor es el uso de ajustes preestablecidos de imagen.

## Aspectos básicos de la creación de ajustes preestablecidos de imagen para procesar recursos {#dm-journey-e}

Existen varias formas y lugares en los que querrá crear una imagen o en los que una imagen estará disponible. Tradicionalmente, un creativo entra en Adobe Photoshop y guarda cada una de estas diferentes representaciones como imágenes estáticas.

![Imágenes estáticas](/help/assets/dynamic-media/assets/dm-static-images.png)
_Bueno: imágenes estáticas, cada una creada manualmente._

Ahora imaginen que Creative Director mira las imágenes y dice:

_&quot;Realmente quería esta toma para que la mano grande señale a los cuatro, y la mano pequeña señale al 1 para que el dial del reloj sea más fácil de ver&quot;._

El creativo tendría que volver a rodar todas estas nuevas imágenes estáticas.

Sin embargo, con Dynamic Media, si tiene diferentes ajustes preestablecidos de imagen, puede utilizar esas imágenes dondequiera que las necesite. Los ajustes preestablecidos de imagen aplican estándares.

![Método del archivo principal](/help/assets/dynamic-media/assets/dm-onefile.png)
_Mejor: un archivo con varias representaciones creadas sobre la marcha utilizando ajustes preestablecidos de imagen, como `Search_Grid` y `Thumbnail`._

| **¿Por qué utilizar ajustes preestablecidos de imagen?** | |
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

![Creación de un ajuste preestablecido de imagen que comience por la pestaña Básico](/help/assets/dynamic-media/assets/dm-image-preset-basictab.png)
_Creación de un ajuste preestablecido de imagen que comience por la pestaña Básico._

En el ejemplo anterior, puede ver que se creó un nuevo ajuste preestablecido de imagen con el nombre _Mediana_. Dynamic Media utiliza un ejemplo de imagen predeterminada (la mochila) para ayudarle a ver las características del ajuste preestablecido de imagen a medida que lo crea.

El _Mediana_ el ajuste preestablecido de imagen tiene una anchura de 500 píxeles y una altura de 800 píxeles. En la parte I de este Recorrido, se explica cómo ofrecer recursos en diferentes formatos. Desde el **[!UICONTROL Formato]** en el menú desplegable, puede elegir enviar recursos como JPEG, PNG, TIFF o varios otros formatos. Aquí tiene flexibilidad.

Selección de la **[!UICONTROL Avanzadas]** le ofrece opciones para el espacio de color del recurso. Según el formato seleccionado en la **[!UICONTROL Básico]** pestaña: en el ejemplo anterior, se seleccionó JPEG . Puede enviar recursos en RGB, escala de grises o CMYK. Desde el **[!UICONTROL Perfil de color]** en el menú desplegable, puede seleccionar cómo enviar un recurso de imagen CMYK para su uso en impresión. Tenga en cuenta también que hay parámetros adicionales que puede aplicar para enfocar las imágenes. En este caso, **[!UICONTROL Máscara de enfoque]** se ha aplicado.

![Creación de un ajuste preestablecido de imagen seleccionando opciones en la pestaña Avanzado](/help/assets/dynamic-media/assets/dm-image-preset-advancedtab.png)
_Creación de un ajuste preestablecido de imagen seleccionando opciones en la pestaña Avanzado._

Lo recuerda en [Estructura de una URL de Dynamic Media](#dm-journey-d) anteriormente, había leído acerca de la URL de Dynamic Media y cómo se crea. El **[!UICONTROL Modificador de imagen]** en el cuadro de texto se puede escribir cualquier parámetro de procesamiento de imagen adicional que desee. Los parámetros se incluyen en el nombre del ajuste preestablecido de la URL cuando se entregan las imágenes mediante el ajuste preestablecido. En la captura de pantalla anterior, el parámetro `bgc=451B15` se ha añadido. Es decir, se ha añadido un color de fondo marrón oscuro.

Puede considerar un ajuste preestablecido de imagen como una fórmula para sus imágenes. Entregará todas las imágenes que utilicen el ajuste preestablecido, de forma consistente, cada vez; será el mismo. El parámetro `&op_brightness=+10` también se ha añadido para aumentar ligeramente el brillo.

Cuando haya terminado, guarde el ajuste preestablecido y ya estará disponible para todas las imágenes que tenga. En este caso, queremos aplicar la variable _Mediana_ imagen preestablecida a una imagen de un tazón de chocolate líquido.

![Aplicación del ajuste preestablecido de imagen *Mediana* para generar una representación de una imagen](/help/assets/dynamic-media/assets/dm-medium-image-preset.png)
_Aplicar el ajuste preestablecido de imagen Medio para generar una representación de una imagen._

Copie la dirección URL y péguela en el explorador para comprobar el aspecto de la imagen. [Pruébelo.](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_74043302?$Medium$){target="_blank"}.

En el explorador, observe el nombre del ajuste preestablecido de imagen _Mediana_ en la ruta de URL completa.

Se puede ver el tipo de claridad que se muestra en la imagen. Esa cualidad se debe en parte a la forma en que el tazón de chocolate fue disparado. Además, esto se debe en parte a que con Dynamic Media puede almacenar imágenes de mayor tamaño que las que se envían a los canales digitales.

Si todo parece satisfactorio para tu tazón de chocolate, pega la URL en tus páginas web donde quieras que aparezca la imagen en tu sitio web.

Si vuelve a ver la imagen del reloj que aparece a continuación, verá que hay un `Cart` ajuste preestablecido de imagen, a `Grid` ajuste preestablecido, a `Large` ajuste preestablecido, a `PDP-page` Ajuste preestablecido de (Página de detalles del producto) y varios más.

![Ajustes preestablecidos de imagen estáticos y dinámicos](/help/assets/dynamic-media/assets/dm-image-presets.png)
_Ajustes preestablecidos de imagen estáticos y dinámicos. La imagen del reloj se procesó con el `PDP-page` ajuste preestablecido de imagen._

Pero, ¿qué sucede si tiene que cambiar una imagen de su sitio web? Por ejemplo, supongamos que ha realizado algunas pruebas y ha encontrado que la imagen de 120 x 120 (la variable `Cart` ajuste preestablecido de imagen) no se recibe tan bien como pensaba. Para aumentar el tamaño de la imagen, aumente la anchura a 175 píxeles y la altura a 175 píxeles. Tradicionalmente, tendría que entrar en Adobe Photoshop y volver a crear todas esas imágenes del carro de compras. Sin embargo, con Dynamic Media, solo tiene que editar el ajuste preestablecido de imagen actualizando los valores de Anchura y Altura a 175 y guardar el ajuste preestablecido, como se ve en el ejemplo siguiente.

![Edición de un ajuste preestablecido de imagen](/help/assets/dynamic-media/assets/dm-edit-image-preset.png)
_Edición de la anchura y la altura de `Cart` ajuste preestablecido de imagen._

Después de cambiar el ajuste preestablecido de imagen y vaciar la caché, todas las imágenes se actualizan y todas las direcciones URL que se utilizan con ese ajuste preestablecido, sí _no_ cambiar en cualquier lugar. Esto significa que no son necesarios vínculos rotos ni redirecciones de páginas web.

## Conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos {#dm-journey-f}

Algunos de los usos más populares de Dynamic Media son la capacidad de crear conjuntos de imágenes, conjuntos de giros y conjuntos de medios mixtos.

Los conjuntos de imágenes suelen estar formados por una serie de recursos de imagen que se presentan como una sola entidad. Este tipo de conjuntos proporcionan a los usuarios una experiencia de visualización integrada, en la que pueden ver diferentes vistas de un elemento haciendo clic en una imagen en miniatura. Los conjuntos de imágenes permiten presentar vistas alternativas de algo y el visor ofrece herramientas de zoom para examinar las imágenes de cerca. [Vea un conjunto de imágenes denominado &quot;En ejecución&quot; que utiliza el visor flotante](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running).

Aquí dentro de Dynamic Media puedes ver varias imágenes de zapatillas de running. Es una serie de líneas de productos que las ventas y el marketing desean que los clientes vean como una sola presentación; un conjunto de imágenes.

![Creación de un conjunto de imágenes](/help/assets/dynamic-media/assets/dm-create-image-set.png)
_Inicio de la creación de un conjunto de imágenes._

Para crear el conjunto de imágenes, elija **[!UICONTROL Conjunto de imágenes]** desde el **[!UICONTROL Crear]** menú desplegable. Observe en el menú que también hay opciones para crear una **[!UICONTROL Conjunto de medios mixtos]**, a **[!UICONTROL Conjunto de giros]**, y a **[!UICONTROL Conjunto de carrusel]**. Estos conjuntos se crean de forma muy similar a un conjunto de imágenes.

Un conjunto de medios mixtos puede contener imágenes, conjuntos de muestras, conjuntos de giros, vídeos y conjuntos de vídeos adaptables. [Pruébelo.](https://s7d9.scene7.com/s7viewers/html5/MixedMediaViewer.html?asset=Scene7SharedAssets/Mixed_Media_Set_Sample). Un conjunto de giros simula el acto del mundo real de girar un objeto para examinarlo. Los conjuntos de giros permiten ver los detalles visuales clave desde cualquier ángulo. [Pruébelo.](https://s7d9.scene7.com/s7viewers/html5/SpinViewer.html?asset=Scene7SharedAssets/SpinSet_Sample&amp;stagesize=500,400){target="_blank"}.

La creación de un conjunto de imágenes es sencilla. Simplemente, agregue los recursos de imagen que desee incluir en el conjunto.

![Creación de un conjunto de imágenes](/help/assets/dynamic-media/assets/dm-create-image-set-add-assets.png)
_El editor de conjuntos de imágenes permite añadir recursos de imagen y reordenar su aspecto en el conjunto._

Debe asignar un nombre al conjunto. Elija el nombre con cuidado porque no puede editarlo más adelante. En el ejemplo anterior, el conjunto se llama `Running`. Cuando haya terminado, guarde el conjunto.

Y aquí está el `Running` Conjunto de imágenes en Experience Manager Assets.

![Conjunto de imágenes en ejecución en Experience Manager Assets, Vista de tarjeta](/help/assets/dynamic-media/assets/dm-image-set.png)
_El `Running` Conjunto de imágenes en Experience Manager Assets, Vista de tarjeta._

Tanto si ha creado un conjunto de imágenes, un conjunto de medios mixtos, un conjunto de giros o cualquier otro medio interactivo, después de crear el conjunto, desea ver cómo aparece y se comporta para un cliente. Dynamic Media tiene numerosos visores integrados que le permiten hacer precisamente eso.

Para empezar, seleccione el conjunto de imágenes creado para abrirlo en una vista previa, como se ve en el siguiente ejemplo.

![El conjunto de imágenes en ejecución en la vista previa con la opción Visualizadores seleccionada](/help/assets/dynamic-media/assets/dm-image-set-viewer.png)
_El `Running` Conjunto de imágenes en vista previa con la opción Visualizadores seleccionada._

Observe en la vista previa que puede seleccionar las muestras de zapatillas de running y acercar y alejar las zapatillas. Para aplicar un visor al conjunto, seleccione **[!UICONTROL Espectadores]** en el menú desplegable.

![Conjunto de imágenes en ejecución con el visor flotante aplicado](/help/assets/dynamic-media/assets/dm-image-set-flyout-viewer.png)
_El `Running` Conjunto de imágenes con el visor flotante aplicado._

En este caso, la variable `Flyout` se seleccionó el visor. En este punto, puede obtener una vista previa del conjunto de imágenes en el visor. Sin embargo, es mejor verlo en su navegador, justo cómo lo ve un cliente. Usted selecciona **[!UICONTROL URL]** en la parte inferior izquierda, copie la dirección URL y péguela en el explorador. [Pruébelo.](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/Flyout){target="_blank"}.

La dirección URL única permite utilizar el conjunto de imágenes y el visor donde los necesite en el sitio web. Es posible que haya observado en el ejemplo anterior que **[!UICONTROL Incrustar]** es a la derecha del botón URL. Al seleccionar **[!UICONTROL Incrustar]** Además, puede copiar el código de este conjunto/visor de imágenes y añadirlo a una página web o a un componente de Experience Manager Sites.

El visor flotante es un visor predeterminado y listo para usar cuyas propiedades puede editar. O bien, como con la creación de un ajuste preestablecido de imagen, puede crear su propio visor personalizado.

Ahora, supongamos que a su equipo de ventas y marketing no le gusta el visor flotante. Les gusta la función de zoom, pero quieren que los clientes vean el efecto de zoom directamente sobre los zapatos. En tal caso, simplemente aplique el visor InlineZoom al conjunto de imágenes y copie y pegue su URL en el explorador para ver cómo se comporta. [Pruébelo.](https://s7d1.scene7.com/s7viewers/html5/FlyoutViewer.html?asset=jpearldemo/Running&amp;config=jpearldemo/InlineZoom){target="_blank"}.

Cuando mueve el puntero del mouse sobre el zapato, se acerca a esa imagen y puede ver más detalles a medida que mueve el puntero. Y la razón de esto es simplemente el tamaño de la imagen que se cargó inicialmente en Dynamic Media.

Al considerar la posibilidad de vivir como consumidor, o al trabajar en su función diaria, y al visitar diferentes sitios web, ve cosas como esta. Piense en cómo se está haciendo y cómo puede utilizar el poder de Dynamic Media en su propio trabajo y en el sitio web de su compañía.

Acaba de leer acerca de los conjuntos de imágenes y visores. Veamos un par de otros visores y pruébelos en recursos individuales. Para restablecer el visor, haga clic en el **[!UICONTROL Actualizar]** en la esquina inferior izquierda.

<!-- LEAVE THIS HIDDEN PATH IN THE DOCUMENTATION FOR DEMO PURPOSES [Flyout viewer with image set](http://www.partycity.com/girls-little-old-lady-costume-P750948.html) -->

* `ZoomVertical_dark` visualizador aplicado a un recurso de imagen. [Pruébelo.](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_96311480&amp;config=jpearldemo/ZoomVertical_dark){target="_blank"}.
* `Zoom_light` visualizador aplicado a una imagen. [Pruébelo.](https://s7d1.scene7.com/s7viewers/html5/BasicZoomViewer.html?asset=jpearldemo/AdobeStock_38827423&amp;config=jpearldemo/Zoom_light){target="_blank"}.

## Opcional: Más información

Si desea obtener más información sobre lo que acaba de leer, utilice los materiales siguientes para explorar conceptos en bueno detalle. De lo contrario, el Recorrido de Dynamic Media se habrá completado.

_Temas de ayuda de Dynamic Media_

* [Cómo crear ajustes preestablecidos de imagen](/help/assets/dynamic-media/image-presets.md)
* Una lista de [parámetros de procesamiento de imagen](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/c-command-reference.html) que se puede utilizar en el campo Modificador de imagen al crear un ajuste preestablecido de imagen
* [Previsualización de recursos](/help/assets/dynamic-media/previewing-assets.md)
* [Previsualización de recursos 3D](/help/assets/dynamic-media/previewing-3d-assets.md)
* [Cómo crear conjuntos de imágenes](/help/assets/dynamic-media/image-sets.md)
* [Cómo crear conjuntos de giros](/help/assets/dynamic-media/spin-sets.md)
* [Cómo crear conjuntos de medios mixtos](/help/assets/dynamic-media/mixed-media-sets.md)

_Tutoriales de Dynamic Media_

* [Uso de Dynamic Media con Experience Manager Assets](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/dynamic-media-overview-feature-video-use.html?lang=es)
* [Biblioteca de contenido de Adobe Experience Manager](https://experienceleague.adobe.com/?lang=en#recommended/solutions/experience-manager) (buscar en _Dynamic Media_)

_Visores de Dynamic Media_

* [Demostraciones en directo](https://landing.adobe.com/en/na/dynamic-media/ctir-2755/live-demos.html) de cada visor

<!-- Live as of April 28 2022. LEAVE IN HERE https://landing.adobe.com/en/na/dynamic-media/ctir-2755/index.html -->