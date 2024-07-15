---
title: Imágenes inteligentes
description: Descubra cómo Imágenes inteligentes con Adobe Sensei AI aplica las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes adecuadas y optimizadas para su experiencia, lo que resulta en un mejor rendimiento y participación.
contentOwner: Rick Brough
feature: Asset Management,Renditions,Best Practices
role: User
mini-toc-levels: 2
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
source-git-commit: 35f31c95e92148ff5f3472f26ea9c40fa5a17947
workflow-type: tm+mt
source-wordcount: '3454'
ht-degree: 1%

---

# Imágenes inteligentes {#smart-imaging}

## Acerca de las imágenes inteligentes{#about-smart-imaging}

La tecnología de imágenes inteligentes aplica las capacidades de IA de Adobe Sensei y funciona con los &quot;ajustes preestablecidos de imagen&quot; existentes. Funciona para mejorar el rendimiento de la entrega de imágenes al optimizar automáticamente el formato, el tamaño y la calidad de la imagen en función de las capacidades del explorador del cliente.

Y ahora, obtenga una mejor puntuación de Google Core Web Vital para LCP (Pintado de contenido más grande) con imágenes inteligentes mejoradas que ahora vienen con soporte para AVIF y WebP.

>[!IMPORTANT]
>
>Imágenes inteligentes requiere el uso de la CDN (red de distribución de contenido) predeterminada incluida en Adobe Experience Manager - Dynamic Media. Esta función no admite ninguna otra CDN personalizada.

>[!TIP]
>
>Pruebe y descubra las ventajas de los modificadores de imagen de Dynamic Media y de las imágenes inteligentes con Dynamic Media [_Snapshot_](https://snapshot.scene7.com/).
>
> Snapshot es una herramienta de demostración visual diseñada para ilustrar la potencia de Dynamic Media para la entrega de imágenes optimizadas y dinámicas. Experimente con imágenes de prueba o direcciones URL de Dynamic Media para observar visualmente la salida de varios modificadores de imagen de Dynamic Media y optimizaciones de imágenes inteligentes para lo siguiente:
>* Tamaño de archivo (con envío WebP y AVIF)
>* Ancho de banda de red
>* DPR (proporción de píxeles del dispositivo)
>
>Para aprender lo fácil que es usar Snapshot, reproduzca el [vídeo de entrenamiento Snapshot](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot.html?lang=en) (3 minutos y 17 segundos).

Imágenes inteligentes se beneficia del aumento de rendimiento añadido de estar totalmente integrado con el mejor servicio de CDN (red de distribución de contenido) premium de Adobe. Este servicio encuentra la ruta de Internet óptima entre servidores, redes y puntos de intercambio entre iguales. Encuentra una ruta que tiene la latencia más baja y la tasa de pérdida de paquetes más baja en lugar de utilizar la ruta predeterminada de Internet.

Los siguientes ejemplos de recursos de imagen ilustran la optimización de imágenes inteligentes agregada:

| Imagen (URL) | Miniatura    | Tamaño (JPEG) | Tamaño (WebP) con imágenes inteligentes | Tamaño (AVIF) con imágenes inteligentes | % de reducción con WebP | % de reducción con AVIF |
|---|---|---|---|---|---|---|
| [Imagen 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![imagen1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90,2 KB | 26,89 % | 37,79 % |
| [Imagen 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![imagen2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16,01 % | 72,57 % |
| [Imagen 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&amp;fmt=jpg&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![imagen3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87,1 KB | 14,47 % | 60,58 % |
| [Imagen 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&amp;qlt=85&amp;resmode=bisharp&amp;op_usm=5,0.125,5,0) | ![imagen4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8,25 % | 51,85 % |

De forma similar a lo anterior, Adobe también ejecutó una prueba con un conjunto de muestras más grande. El formato AVIF proporciona una reducción de tamaño adicional del 20 % con respecto a WebP, lo que supone una reducción del 27 % con respecto al JPEG. Todos con la misma calidad visual. En total, AVIF proporciona una reducción de tamaño promedio de hasta el 41 % con respecto al JPEG.

Si comparamos WebP y AVIF con PNG, podemos observar una reducción del tamaño del 84% con WebP y del 87% con AVIF. Además, como los formatos WebP y AVIF admiten transparencias y múltiples animaciones de imagen, es un buen sustituto de los archivos PNG y GIF transparentes.

Vea también [Optimización de imágenes con formatos de imagen de próxima generación (WebP y AVIF)](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

**Ventajas de las imágenes inteligentes**

Imágenes inteligentes proporciona un mejor rendimiento de entrega de imágenes al optimizar automáticamente el tamaño del archivo de imagen en función del explorador del cliente en uso, la visualización del dispositivo y las condiciones de red. Dado que las imágenes constituyen la mayor parte del tiempo de carga de una página, cualquier mejora de rendimiento puede tener un profundo impacto en los KPI empresariales, como tasas de conversión más altas, tiempo invertido en un sitio y tasas de devolución del sitio más bajas.

Las ventajas clave más recientes de las imágenes inteligentes son las siguientes:

* Ahora admite el formato AVIF de próxima generación.
* Ahora, PNG a WebP y AVIF admiten la conversión con pérdidas. Como PNG es un formato sin pérdidas, las entregas anteriores de WebP y AVIF no sufrieron pérdidas.
* [Conversión de formato del explorador](#bfc)
* [Proporción de píxeles del dispositivo](#dpr)
* [Ancho de banda de red](#bandwidth)

### Acerca de la conversión de formato de navegador {#bfc}

Activar la conversión de formato del explorador adjuntando `bfc=on` a la dirección URL de la imagen convierte automáticamente JPEG y PNG en AVIF con pérdida, WebP con pérdida, JPEGXR con pérdida y JPEG con pérdida para diferentes exploradores. Para los navegadores que no admiten estos formatos, Smart Imaging sigue sirviendo al JPEG o PNG. Junto con el formato, Smart Imaging vuelve a calcular la calidad del nuevo formato.

Las imágenes inteligentes también se pueden desactivar adjuntando `bfc=off` a la dirección URL de la imagen.

Consulte también [bfc](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc.html?lang=en) en la API de servicio y procesamiento de imágenes de Dynamic Media.

### Acerca de la optimización de proporción de píxeles de dispositivo {#dpr}

La proporción de píxeles del dispositivo (DPR), también conocida como proporción de píxeles CSS, es la relación entre los píxeles físicos de un dispositivo y los píxeles lógicos. Especialmente con la llegada de las pantallas de retina, la resolución de píxeles de los dispositivos móviles modernos está creciendo a un ritmo rápido.

Al habilitar la optimización de la proporción de píxeles del dispositivo, la imagen se procesa con la resolución nativa de la pantalla, lo que la hace nítida.

Actualmente, la densidad de píxeles de la visualización proviene de los valores del encabezado CDN de Akamai.

| Valores permitidos en la dirección URL de una imagen | Descripción |
|---|---|
| `dpr=off` | Desactive la optimización del RGPD en un nivel de URL de imagen individual. |
| `dpr=on,dprValue` | Anule el valor del DPR detectado por Imágenes inteligentes, con un valor personalizado (tal y como lo detecta cualquier lógica del lado del cliente u otro medio). El valor permitido para `dprValue` es cualquier número mayor que 0. |

>[!NOTE]
>
>* Puede usar `dpr=on,dprValue` incluso si la configuración del DPR a nivel de compañía está desactivada.
>* Debido a la optimización del RGPD, cuando la imagen resultante es mayor que la configuración de MaxPix Dynamic Media, la anchura de MaxPix siempre se reconoce manteniendo la proporción de aspecto de la imagen. -->

| Tamaño de imagen solicitado | Valor de proporción de píxeles del dispositivo (dpr) | Tamaño de imagen entregado |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

Vea también [Al trabajar con imágenes](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) y [Al trabajar con recorte inteligente](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### Acerca de la optimización del ancho de banda {#bandwidth}

Al activar Ancho de banda de red, se ajusta automáticamente la calidad de imagen que se proporciona en función del ancho de banda real de la red. Para un ancho de banda de red deficiente, la optimización de la RGPD (proporción de píxeles del dispositivo) se desactiva automáticamente, incluso si ya está activada.

Si lo desea, su empresa puede excluirse de la optimización del ancho de banda de la red en el nivel de imagen individual adjuntando `network=off` a la dirección URL de la imagen.

| Valor permitido en la dirección URL de una imagen | Descripción |
|---|---|
| `network=off` | Desactiva la optimización de red en un nivel de URL de imagen individual. |

Los valores de RGPD y ancho de banda de red se basan en los valores detectados del lado del cliente de la CDN agrupada. Estos valores a veces son inexactos. Por ejemplo, iPhone5 con DPR=2 y iPhone12 con `dpr=3`, ambos muestran `dpr=2`. Sin embargo, para los dispositivos de alta resolución, es mejor enviar `dpr=2` que enviar `dpr=1`. Sin embargo, la mejor manera de superar esta inexactitud es utilizar la DPR del lado del cliente para ofrecerle valores 100% precisos. Y funciona para cualquier dispositivo, ya sea Apple o cualquier otro dispositivo que se haya iniciado. Consulte [Usar imágenes inteligentes con proporción de píxeles de dispositivo del lado del cliente](/help/assets/dynamic-media/client-side-dpr.md).

**Ventajas clave adicionales de imágenes inteligentes**

* Se ha mejorado la clasificación SEO de Google para las páginas web que utilizan las últimas imágenes inteligentes.
* Ofrece contenido optimizado inmediatamente (durante la ejecución).
* Utiliza la tecnología Adobe Sensei para realizar conversiones de acuerdo con la calidad (`qlt`) especificada en la solicitud de imagen.
* TTL (Tiempo de vida) independiente. Anteriormente, era obligatorio un TTL mínimo de 12 horas para que las imágenes inteligentes funcionaran.
* Anteriormente, tanto las imágenes originales como las derivadas se almacenaban en caché y se trataba de un proceso de 2 pasos para invalidar la caché. En las últimas imágenes inteligentes, solo se almacenan en caché los derivados, lo que permite un proceso de invalidación de la caché de un solo paso.
* Los clientes que utilizan encabezados personalizados en su conjunto de reglas se benefician de la última versión de imágenes inteligentes, ya que estos encabezados no están bloqueados, a diferencia de la versión anterior de imágenes inteligentes. Por ejemplo, &quot;Tiempo permitido para el origen&quot;, &quot;X-Robot&quot; como se sugiere en [Agregar un valor de encabezado personalizado a las respuestas de imágenes|Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/scene7-rulesets/add-custom-header-val-image.html).

## Funcionamiento de las imágenes inteligentes{#how-smart-imaging-works}

Cuando un consumidor solicita una imagen, Smart Imaging comprueba las características del usuario y la convierte al formato de imagen adecuado en función del explorador en uso. Estas conversiones de formato se realizan de una manera que no degrada la fidelidad visual. Las imágenes inteligentes convierten automáticamente las imágenes a diferentes formatos, según la capacidad del explorador, de la siguiente manera.

* Convertir automáticamente a AVIF si el explorador admite el formato
* Convertir automáticamente a WebP si la conversión AVIF no fue beneficiosa o el explorador no admite AVIF
* Convertir automáticamente a JPEG 2000 si Safari no admite WebP
* Convertir automáticamente a JPEGXR para IE 9+ o si Edge no admite WebP\
  | Formato de imagen | Navegadores admitidos |
|—|—|
| AVIF | [https://caniuse.com/avif](https://caniuse.com/avif) |
| WebP | [https://caniuse.com/webp](https://caniuse.com/webp) |
| JPEG 2000 | [https://caniuse.com/jpeg2000](https://caniuse.com/jpeg2000) |
| JPEGXR | [https://caniuse.com/jpegxr](https://caniuse.com/jpegxr) |
* En los exploradores que no admiten estos formatos, se proporciona el formato de imagen solicitado originalmente.

Si el tamaño de la imagen original es menor que el que produce Smart Imaging, se sirve la imagen original.

## Compatibilidad con formatos de imagen en imágenes inteligentes{#image-format-support}

Se admiten los siguientes formatos de imagen para imágenes inteligentes:

* JPEG
* PNG

Para un formato de archivo de imagen JPEG, Smart Imaging vuelve a calcular la calidad del nuevo formato.

Para formatos de archivo de imagen compatibles con transparencias como PNG, puede configurar Imágenes inteligentes para proporcionar AVIF y WebP con pérdidas. Para la conversión de formato con pérdida, Imágenes inteligentes utiliza la calidad mencionada en la dirección URL de la imagen o, de lo contrario, la calidad configurada en la cuenta de empresa de Dynamic Media.

## Compatibilidad con comandos de Image Serving en Imágenes inteligentes{#imaging-serving-command-support}

No se admiten los comandos del servicio de imágenes `fmt` y `qlt`; se admiten todos los comandos restantes.

## Preguntas más frecuentes sobre imágenes inteligentes{#smart-imaging-faq}

+++**¿Hay costos de licencia asociados con imágenes inteligentes?**

No. Las imágenes inteligentes se incluyen con la licencia existente. Esta regla es verdadera para Dynamic Media Classic o para Experience Manager: Dynamic Media (local, AMS y as a Cloud Service en Experience Manager).

>[!IMPORTANT]
>
>Las imágenes inteligentes no están disponibles para los clientes híbridos de Dynamic Media.

+++

+++**¿Es posible desactivar Imágenes inteligentes para cualquier solicitud?**

Sí. Puede desactivar Imágenes inteligentes si agrega cualquiera de los siguientes modificadores:

* `bfc=off` para desactivar la conversión de formato del explorador. Consulte también [Conversión de formato de explorador](#bfc).
* `dpr=off` para desactivar la proporción de píxeles del dispositivo. Consulte también [Proporción de píxeles del dispositivo](#dpr).
* `network=off` para desactivar el ancho de banda de la red. Consulte también [Ancho de banda de red](#network).

+++

+++**¿Es posible &quot;ajustar&quot; imágenes inteligentes?**

Sí. Imágenes inteligentes tiene tres opciones que puede activar o desactivar.

* [Conversión de formato del explorador](#bfc)
* [Proporción de píxeles del dispositivo](#dpr)
* [Ancho de banda de red](#network)

+++

+++**¿Funcionan las imágenes inteligentes con mis ajustes preestablecidos de imagen existentes?**

Sí. Imágenes inteligentes funciona con los ajustes preestablecidos de imagen existentes y observa todos los ajustes de imagen. Lo que cambia es el formato de imagen, la configuración de calidad o ambos. Para la conversión de formato, Imágenes inteligentes mantiene la fidelidad visual completa tal como se define en los ajustes preestablecidos de la imagen, pero a un tamaño de archivo más pequeño.

Por ejemplo, supongamos que un ajuste preestablecido de imagen se define con formato JPEG, tamaño 500 x 500, calidad=85 y máscara de enfoque=0,1,1,5. Cuando Smart Imaging detecta que un usuario se encuentra en un navegador Chrome, la imagen se convierte al formato WebP, con un tamaño de 500 x 500. Y, unsharp mask=0.1,1,5 tiene una calidad WebP que coincide con una calidad JPEG de 85 tan cerca como sea posible. El espacio de esa conversión WebP se compara con el JPEG y se devuelve el más pequeño de los dos.

+++

+++**¿Tengo que cambiar alguna URL, ajuste preestablecido de imagen o implementar código nuevo en mi sitio?**

No. Imágenes inteligentes funciona perfectamente con las direcciones URL de imagen y ajustes preestablecidos de imagen existentes. Además, Imágenes inteligentes no requiere que agregue código al sitio web para detectar el explorador de un usuario. Toda esta funcionalidad se gestiona automáticamente.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. -->

+++

+++**¿Smart Imaging funciona con HTTPS? ¿Qué tal HTTP/2?**

Sí, a ambas preguntas. Imágenes inteligentes funciona con imágenes entregadas a través de HTTP o HTTPS. Además, también funciona sobre HTTP/2.

+++

+++**¿Cumplo los requisitos para usar imágenes inteligentes?**

Depende de ti. Para utilizar imágenes inteligentes, la cuenta de Experience Manager de Dynamic Media Classic o Dynamic Media de su empresa debe cumplir los siguientes requisitos:

* Utilice la CDN (red de distribución de contenido) empaquetada en Adobe como parte de la licencia.
* Use un dominio dedicado (por ejemplo, `images.company.com` o `mycompany.scene7.com`), no un dominio genérico (por ejemplo, `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

Para encontrar tus dominios, abre la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicia sesión en tu cuenta o cuentas de empresa.

Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo denominado **[!UICONTROL Nombre de servidor publicado]**. Si actualmente utiliza un dominio genérico, puede solicitar pasar a su propio dominio personalizado. Realice esta solicitud de transición cuando envíe un caso de asistencia.

Su primer dominio personalizado no supone ningún coste adicional con una licencia de Dynamic Media.

+++

+++**¿Puedo habilitar imágenes inteligentes para mi cuenta?**

No. Inicia una solicitud para utilizar imágenes inteligentes; no se activa automáticamente.

Cree un caso de soporte como se describe a continuación. En su caso de soporte, asegúrese de mencionar cuál de las siguientes capacidades de imágenes inteligentes (una o más) desea habilitar en su cuenta:

* WebP
* AVIF
* Optimización del ancho de banda de red y DPR
* PNG a AVIF con pérdida o WebP con pérdida

Si ya tiene habilitadas las imágenes inteligentes con WebP, pero desea otras nuevas funcionalidades como las enumeradas anteriormente, debe crear un caso de asistencia.

**Para crear un caso de soporte para habilitar imágenes inteligentes en su cuenta:**

1. [Use el Admin Console para iniciar la creación de un nuevo caso de soporte](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).
1. Proporcione la siguiente información en su caso de asistencia:

   * Nombre del contacto principal, correo electrónico, teléfono.

   * Enumere cuál de las siguientes capacidades de imágenes inteligentes (una o más) desea habilitar en su cuenta:
      * WebP
      * AVIF
      * Optimización del ancho de banda de red y DPR
      * PNG a AVIF con pérdida o WebP con pérdida

   * Se habilitarán todos los dominios para imágenes inteligentes (es decir, `images.company.com` o `mycompany.scene7.com`).

     Para encontrar tus dominios, abre la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicia sesión en tu cuenta o cuentas de empresa.

     Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**.

     Busque el campo denominado **[!UICONTROL Nombre de servidor publicado]**.

   * Compruebe que está utilizando la red de distribución de contenido (CDN) a través del Adobe y que no está gestionada con una relación directa.

   * Compruebe que está usando un dominio dedicado como `images.company.com` o `mycompany.scene7.com`, y no un dominio genérico, como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

     Para encontrar tus dominios, abre la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicia sesión en tu cuenta o cuentas de empresa.

     Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**.

     Busque el campo denominado **[!UICONTROL Nombre de servidor publicado]**. Si está utilizando un dominio de Dynamic Media Classic genérico, puede solicitar pasar a su propio dominio personalizado como parte de esta transición.

   * Indique si desea que funcione sobre HTTP/2.

1. La Asistencia al cliente de Adobe le añade a la Lista de espera de clientes de imágenes inteligentes en función del orden en que se envían las solicitudes.
1. Cuando el Adobe está listo para administrar su solicitud, el Servicio de atención al cliente se pone en contacto con usted para coordinar y establecer una fecha objetivo.
1. **Opcional**: opcionalmente, puede probar las imágenes inteligentes en Ensayo antes de que el Adobe implemente la producción de la nueva característica.
1. Se le notificará una vez que el Servicio de atención al cliente lo haya completado.
1. Para maximizar las mejoras de rendimiento de las imágenes inteligentes, Adobe recomienda establecer el Tiempo de vida (TTL) en 24 horas o más. El TTL define cuánto tiempo la CDN almacena en caché los recursos. Para cambiar esta configuración:

   1. Si usa Dynamic Media Classic, vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de aplicación]** > **[!UICONTROL Configuración de Publish]** > **[!UICONTROL Servidor de imágenes]**. Establezca el valor **[!UICONTROL Tiempo predeterminado de almacenamiento en caché del cliente para activo]** en 24 o más.
   1. Si usa Dynamic Media, siga [estas instrucciones](config-dm.md). Establezca el valor **[!UICONTROL Expiration]** en 24 horas o más.

+++

+++**¿Cuándo se habilita mi cuenta con imágenes inteligentes?**

Las solicitudes se procesan en el orden en que se reciben en Asistencia al cliente, según la Lista de espera.

>[!NOTE]
>
>Puede haber un tiempo de espera largo porque habilitar imágenes inteligentes implica borrar la Adobe de la caché. Por lo tanto, solo se pueden gestionar unas pocas transiciones de clientes en un momento determinado.

+++

+++**¿Hay riesgos con el uso de imágenes inteligentes?**

No hay riesgo para una página web de cliente. Sin embargo, la transición a Imágenes inteligentes borra la caché de CDN. Esta operación implica pasar a una nueva configuración de Dynamic Media Classic o Dynamic Media en Experience Manager.

Durante la transición inicial, las imágenes no almacenadas en caché acceden directamente a los servidores de origen de Adobe hasta que se vuelva a crear la . De este modo, Adobe tiene previsto gestionar varias transiciones de clientes a la vez, de modo que se mantenga un rendimiento aceptable al extraer solicitudes de su origen. Para la mayoría de los clientes, la caché se vuelve a crear por completo en la CDN en un plazo de uno a dos días.

+++

+++**¿Puedo verificar si las imágenes inteligentes funcionan?**

Sí. Puede hacer lo siguiente:

1. Una vez configurada la cuenta con imágenes inteligentes, cargue una URL de imagen de Dynamic Media Classic o Adobe Experience Manager - Dynamic Media en el explorador.
1. Para abrir el panel de desarrolladores de Chrome, ve a **[!UICONTROL Ver]** > **[!UICONTROL Desarrollador]** > **[!UICONTROL Herramientas para desarrolladores]** en el explorador. O bien, elija cualquier herramienta para desarrolladores de navegadores de su elección.

1. Asegúrese de que la caché esté deshabilitada cuando las herramientas para desarrolladores estén abiertas.

   * En Windows®, vaya a la configuración en el panel de herramientas para desarrolladores y, a continuación, active la casilla de verificación **[!UICONTROL Deshabilitar caché (mientras devtools esté abierto)]**.
   * En macOS, en el panel del desarrollador, en la ficha **[!UICONTROL Red]**, seleccione **[!UICONTROL deshabilitar caché]**.

1. Observe cómo el Tipo de contenido se transforma al formato adecuado. La siguiente captura de pantalla muestra una imagen PNG convertida dinámicamente a WebP en Chrome. Si su dominio tiene habilitado AVIF, también puede esperar ver AVIF en el Tipo de contenido.
1. Repita esta prueba en diferentes navegadores y condiciones de usuario.

>[!NOTE]
>
>No todas las imágenes se convierten. Imágenes inteligentes decide si la conversión puede mejorar el rendimiento. En ocasiones, cuando no se espera una ganancia de rendimiento o el formato no es JPEG ni PNG, la imagen no se convierte.

![image2017-11-14_15398](assets/image2017-11-14_15398.png)

+++

+++**¿Hay alguna manera de conocer los beneficios de las imágenes inteligentes?**

Sí. El encabezado de imágenes inteligentes determina las ventajas de las imágenes inteligentes. Cuando se habilita Imágenes inteligentes, después de solicitar una imagen, bajo el encabezado **[!UICONTROL Encabezados de respuesta]**, puede ver `-X-Adobe-Smart-Imaging` como se ve en el siguiente ejemplo resaltado:

![Encabezado de imágenes inteligentes](/help/assets/dynamic-media/assets/smartimagingheader.png)

Este encabezado indica lo siguiente:

* Imágenes inteligentes funciona para la empresa.
* Un valor positivo significa que la conversión se ha realizado correctamente. En este caso, se devuelve una nueva imagen WebP.
* Un valor negativo significa que la conversión no se ha realizado correctamente. En este caso, se devuelve la imagen solicitada original (JPEG de forma predeterminada, si no se especifica).
* Un valor positivo muestra la diferencia en bytes entre la imagen solicitada y la nueva imagen. En el ejemplo anterior, los bytes guardados son `75048` o aproximadamente 75 KB para una imagen.
* Un valor negativo significa que la imagen solicitada es más pequeña que la nueva imagen. Se muestra la diferencia de tamaño negativa, pero la imagen servida solo es la imagen solicitada original.

>[!NOTE]
>
>**X-Adobe-Smart-Imaging = -1 con WebP siendo entregado**
>
>Si el valor de `X-Adobe-Smart-Imaging` es -1 y WebP aún se está entregando, significa que Imágenes inteligentes funciona, pero no se calcularon los beneficios de tamaño debido a la caché antigua. Puede usar `cache=update` (solo una vez) en la dirección URL de la imagen para solucionar este problema.
>Ejemplo de uso del modificador:
>`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`
>Para invalidar toda la caché, debe crear un caso de soporte.

+++

+++**¿Puedo deshabilitar la optimización de AVIF en imágenes inteligentes?**

Sí. Si desea volver a ofrecer WebP de forma predeterminada, cree un caso de soporte para el mismo. Como de costumbre, puede desactivar Imágenes inteligentes agregando el parámetro `bfc=off` a la dirección URL de la imagen. Sin embargo, no puede seleccionar WebP o AVIF en el modificador URL para Imágenes inteligentes. Esta capacidad se mantiene en el nivel de cuenta de la compañía.

+++

+++**¿Por qué falla mi solicitud cuando tengo una URL con fmt=tif en el explorador web Chrome?**

Este error no se produce si Smart Imaging no está habilitado en su cuenta. Imágenes inteligentes funciona solo con formatos JPEG o PNG.

Para evitar este error, puede:

* Especifique JPEG o PNG, o
* No use el modificador `fmt`, o
* Utilice un formato preferido por el explorador definido por Imágenes inteligentes. Por ejemplo, puede utilizar WebP para el explorador web Chrome.

+++

+++**¿Puedo descargar una imagen de TIFF desde la dirección URL de una imagen?**

Sí. Agregue `fmt=tif` y `bfc=off` a la ruta URL de la imagen.

+++

+++**¿Administra Smart Imaging el formato de imagen y la configuración de calidad de imagen?**

Sí. Imágenes inteligentes utiliza formato y calidad. El resto de los parámetros siguen siendo los mismos, si se solicitan en la dirección URL de la imagen.

+++

+++**¿Puedo establecer una configuración de calidad mínima y máxima?**

No. Actualmente no existe ese aprovisionamiento.

+++

+++**¿Smart Imaging ajusta la configuración de salida de calidad porcentual?**

Sí. Imágenes inteligentes ajusta automáticamente el porcentaje de calidad. Este porcentaje de calidad se determina mediante un algoritmo de aprendizaje automático desarrollado por Adobe. Este porcentaje no es específico del intervalo.

+++

+++**¿Solo el JPEG y PNG son reemplazados por Imágenes inteligentes?**

Sí. Esta funcionalidad solo funciona para JPEG y PNG.

+++

+++**¿Por qué a veces se devuelve el JPEG a Chrome en lugar de a WebP?**

Imágenes inteligentes determina si la conversión es beneficiosa o no. Devuelve la nueva imagen solo si la conversión es beneficiosa.

+++

+++**¿Por qué la proporción de píxeles del dispositivo (dpr) no funciona con imágenes compuestas?**

Si una imagen compuesta implica demasiadas capas, la funcionalidad de dpr puede verse afectada al utilizar un modificador de posición. Este problema se conoce y se solucionará en futuras versiones de Imágenes inteligentes. Si otras funcionalidades de imágenes inteligentes no funcionan según lo esperado, puede crear un caso de asistencia para informar del problema.

+++

+++**¿Por qué el PNG de imágenes inteligentes se convierte en WebP/AVIF sin pérdidas?**

Como PNG es un formato sin pérdidas, las entregas anteriores de WebP y AVIF resultaron con pérdidas mayores de lo esperado. Imágenes inteligentes ahora admite la conversión con pérdida. Puede usar el modificador `cache=update` (solo una vez) en una solicitud de imagen para solucionar este problema. Ejemplo de uso de este modificador:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

Para invalidar toda la caché, debe crear un caso de soporte que solicite ese esfuerzo.

+++

+++**¿Puedo seguir usando PNG para convertir sin pérdidas en imágenes inteligentes?**

Sí. Imágenes inteligentes ahora admite la conversión con pérdida en función del nivel de calidad. Para seguir usando la conversión sin pérdidas, puede usar la calidad 100 que se establece mediante la configuración de su compañía o a través de la dirección URL de la imagen usando `qlt=100` en la ruta.

+++



























<!-- ## If Smart Imaging manages the quality settings, are there minimums and maximums I can set? For example, is it possible to set "no lower than 60" and "no greater than 80 quality"? {#minimum-maximum}

There is no such provisioning ability in the current Smart Imaging. -->

<!-- ## Sometimes a JPEG image is returned to Chrome instead of a WebP image. Why does that change happen? {#jpeg-webp}

Smart Imaging determines if the conversion is beneficial or not. It returns the new image only if the conversion results in a smaller file size with comparable quality.

How does Smart Imaging DPR optimization work with Adobe Experience Manager Sites components and Dynamic Media viewers?

* Experience Manager Sites Core Components are configured by default for DPR optimization. To avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Experience Manager Sites Core Components Dynamic Media images.
* Given Dynamic Media Foundation Component is configured by default for DPR optimization, to avoid oversized images owing to server-side Smart Imaging DPR optimization, `dpr=off` is always added to Dynamic Media Foundation Component images. Even if customer deselects DPR optimization in DM Foundation Component, server-side Smart Imaging DPR does not kick in. In summary, in the DM Foundation Component, DPR optimization comes into effect based on DM Foundation Component level setting only.
* Any viewer side DPR optimization works in tandem with server-side Smart Imaging DPR optimization, and does not result in over-sized images. In other words, wherever DPR is handled by the viewer, such as the main view only in a zoom-enabled viewer, the server-side Smart Imaging DPR values are not triggered. Likewise, wherever viewer elements, such as swatches and thumbnails, do not have DPR handling, the server-side Smart Imaging DPR value is triggered.

See also [When working with images](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) and [When working with Smart Crop](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

>[!MORELIKETHIS]
>
>* [Image optimization with next generation image formats WebP and AVIF.](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4) -->
>>
