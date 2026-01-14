---
title: Imágenes inteligentes
description: Descubra cómo Imágenes inteligentes con Adobe AI aplica las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes adecuadas optimizadas para su experiencia, lo que resulta en un mejor rendimiento y participación.
contentOwner: Rick Brough
feature: Asset Management,Renditions,Best Practices
role: User
mini-toc-levels: 2
exl-id: 863784d9-0c91-4deb-8edd-1354a21581c3
source-git-commit: 281a8efcd18920dd926d92db9c757c0513d599fd
workflow-type: tm+mt
source-wordcount: '3218'
ht-degree: 1%

---

# Imágenes inteligentes {#smart-imaging}

Descubra cómo Imágenes inteligentes con Adobe AI aplica las características de visualización únicas de cada usuario para ofrecer automáticamente las imágenes adecuadas optimizadas para su experiencia, lo que resulta en un mejor rendimiento y participación.


## Acerca de las imágenes inteligentes {#about-smart-imaging}

La tecnología de imágenes inteligentes aplica las capacidades de IA de Adobe y funciona con los &quot;ajustes preestablecidos de imagen&quot; existentes. Funciona para mejorar el rendimiento de la entrega de imágenes al optimizar automáticamente el formato, el tamaño y la calidad de la imagen en función de las capacidades del explorador del cliente.

Y ahora, obtenga una mejor puntuación de Google Core Web Vital para LCP (Pintado de contenido más grande) con imágenes inteligentes mejoradas, que ahora viene con soporte para AVIF y WebP.

>[!IMPORTANT]
>
>Imágenes inteligentes requiere el uso de la CDN (red de distribución de contenido) integrada en Adobe Experience Manager - Dynamic Media. Esta función no admite ninguna otra CDN personalizada.

>[!TIP]
>
>Pruebe y descubra las ventajas de los modificadores de imagen de Dynamic Media y de las imágenes inteligentes con Dynamic Media [_Snapshot_](https://snapshot.scene7.com/).
>
>Snapshot es una herramienta de demostración visual diseñada para ilustrar la potencia de Dynamic Media para la entrega de imágenes optimizadas y dinámicas. Experimente con imágenes de prueba o URL de Dynamic Media para observar visualmente la salida de varios modificadores de imagen de Dynamic Media y optimizaciones de Imágenes inteligentes para lo siguiente:
>
>* Tamaño de archivo (con envío WebP y AVIF)
>* Ancho de banda de red
>* DPR (proporción de píxeles del dispositivo)
>
>Para aprender lo fácil que es usar Snapshot, reproduzca el [vídeo de entrenamiento Snapshot](https://experienceleague.adobe.com/es/docs/experience-manager-learn/assets/dynamic-media/images/dynamic-media-snapshot) (3 minutos y 17 segundos).

Imágenes inteligentes se beneficia del aumento de rendimiento añadido de estar totalmente integrado con el mejor servicio de CDN (red de distribución de contenido) premium de Adobe. Este servicio encuentra la ruta de Internet óptima entre servidores, redes y puntos de intercambio entre iguales. Encuentra una ruta que tiene la latencia más baja y la tasa de pérdida de paquetes más baja en lugar de utilizar la ruta predeterminada de Internet.

Los siguientes ejemplos de recursos de imagen ilustran la optimización de imágenes inteligentes agregada:

| Imagen (URL) | Miniaturas | Tamaño (JPEG) | Tamaño (WebP) con imágenes inteligentes | Tamaño (AVIF) con imágenes inteligentes | % de reducción con WebP | % de reducción con AVIF |
|---|---|---|---|---|---|---|
| [Imagen 1](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_6?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![imagen1](/help/assets/assets-dm/picture1.png) | 145 KB | 106 KB | 90,2 KB | 26,89 % | 37,79 % |
| [Imagen 2](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_3?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![imagen2](/help/assets/assets-dm/picture2.png) | 412 KB | 346 KB | 113 KB | 16,01 % | 72,57 % |
| [Imagen 3](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_2?hei=500&fmt=jpg&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![imagen3](/help/assets/assets-dm/picture3.png) | 221 KB | 189 KB | 87,1 KB | 14,47 % | 60,58 % |
| [Imagen 4](https://techsupport.scene7.com/is/image/TechSupport/SmartImaging_1?hei=500&qlt=85&resmode=bisharp&op_usm=5,0.125,5,0) | ![imagen4](/help/assets/assets-dm/picture4.png) | 594 KB | 545 KB | 286 KB | 8,25 % | 51,85 % |

De forma similar a lo anterior, Adobe también ejecutó una prueba con un conjunto de muestras más grande. El formato AVIF proporcionó una reducción de tamaño adicional del 20 % con respecto a WebP, que proporcionó una reducción del 27 % con respecto a JPEG. Todos con la misma calidad visual. En total, AVIF proporciona una reducción de tamaño promedio de hasta el 41 % con respecto a JPEG.

Si comparamos WebP y AVIF con PNG, podemos observar una reducción del tamaño del 84% con WebP y del 87% con AVIF. Además, como los formatos WebP y AVIF admiten transparencias y varias animaciones de imagen, es un buen sustituto de los archivos PNG y GIF transparentes.

Vea también [Optimización de imágenes con formatos de imagen de próxima generación (WebP y AVIF)](https://blog.developer.adobe.com/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4)

<!-- HIDDEN ON MAY 19, 2022 BASED ON CQDOC-19280 On the mobile web, the challenges are compounded by two factors:

* Large variety of devices with different form factors and high-resolution displays.
* Constrained network bandwidth.

In terms of images, the goal is to serve the best quality images as efficiently as possible. -->

**Ventajas de las imágenes inteligentes**

Imágenes inteligentes mejora la entrega de imágenes al optimizar automáticamente el tamaño del archivo en función del explorador del usuario, la visualización del dispositivo y las condiciones de la red. Este enfoque garantiza tiempos de carga más rápidos y una mejor experiencia de visualización en diferentes entornos. Dado que las imágenes constituyen la mayor parte del tiempo de carga de una página, cualquier mejora de rendimiento puede tener un profundo impacto en los KPI empresariales, como los siguientes:

* Tasas de conversión más altas.
* Tiempo empleado en un sitio.
* Tasas de devolución del sitio más bajas.

Las ventajas clave más recientes de las imágenes inteligentes son las siguientes:

* Admite el formato AVIF de próxima generación.
* Ahora, PNG a WebP y AVIF admiten la conversión con pérdidas. Como PNG es un formato sin pérdidas, las entregas anteriores de WebP y AVIF no sufrieron pérdidas.
* [Conversión de formato del explorador](#bfc)
* [Proporción de píxeles del dispositivo](#dpr)
* [Ancho de banda de red](#bandwidth)

### Acerca de la conversión de formato {#bfc}

Al activar la conversión de formato del explorador adjuntando `bfc=on` a la dirección URL de la imagen, JPEG y PNG se convierten automáticamente en AVIF con pérdida, WebP con pérdida, JPEGXR con pérdida y JPEG2000 con pérdida para diferentes exploradores. En los exploradores que no admiten estos formatos, Smart Imaging sigue ofreciendo JPEG o PNG. Imágenes inteligentes vuelve a calcular la calidad del nuevo formato junto con el cambio de formato.

Puede desactivar Imágenes inteligentes adjuntando `bfc=off` a la dirección URL de la imagen.

Consulte también [bfc](https://experienceleague.adobe.com/en/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/r-bfc) en la API de servicio y procesamiento de imágenes de Dynamic Media.

### Acerca de la optimización de proporción de píxeles del dispositivo {#dpr}

La proporción de píxeles del dispositivo (DPR), también denominada proporción de píxeles CSS, representa la relación entre los píxeles físicos y los píxeles lógicos de un dispositivo. Con el aumento de las pantallas de retina, la resolución de píxeles de los dispositivos móviles modernos ha ido aumentando rápidamente.

Al habilitar la optimización de la proporción de píxeles del dispositivo, la imagen se procesa con la resolución nativa de la pantalla, lo que la hace nítida.

Actualmente, la densidad de píxeles de la visualización proviene de los valores del encabezado CDN de Akamai.

| Valores permitidos en la dirección URL de una imagen | Descripción |
|---|---|
| `dpr=off` | Desactive la optimización del RGPD en un nivel de URL de imagen individual. |
| `dpr=on,dprValue` | Anule el valor del DPR detectado por Imágenes inteligentes, con un valor personalizado (tal y como lo detecta cualquier lógica del lado del cliente u otro medio). El valor permitido para `dprValue` es cualquier número mayor que 0. |

>[!NOTE]
>
>* Puede usar `dpr=on,dprValue` incluso si la configuración del DPR a nivel de compañía está desactivada.
>* Debido a la optimización del RGPD, cuando la imagen resultante es mayor que la configuración de Dynamic Media de MaxPix, la anchura de MaxPix siempre se reconoce manteniendo la proporción de aspecto de la imagen. -->

| Tamaño de imagen solicitado | Valor de proporción de píxeles del dispositivo (dpr) | Tamaño de imagen entregado |
|---|---|---|
| 816 x 500 | 1 | 816 x 500 |
| 816 x 500 | 2 | 1632 x 1000 |

Vea también [Al trabajar con imágenes](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-images) y [Al trabajar con recorte inteligente](/help/assets/dynamic-media/adding-dynamic-media-assets-to-pages.md#when-working-with-smart-crop).

### Acerca de la optimización del ancho de banda {#bandwidth}

Al activar el ancho de banda de la red, se ajusta automáticamente la calidad de imagen que se proporciona en función del ancho de banda real de la red. Para un ancho de banda de red deficiente, la optimización de la RGPD (proporción de píxeles del dispositivo) se desactiva automáticamente, incluso si ya está activada.

Su compañía puede deshabilitar la optimización del ancho de banda de red para imágenes individuales adjuntando `network=off` a la dirección URL de la imagen.

| Valor permitido en la dirección URL de una imagen | Descripción |
|---|---|
| `network=off` | Desactiva la optimización de red en un nivel de URL de imagen individual. |

Los valores de RGPD y ancho de banda de red se basan en los valores detectados del lado del cliente de la CDN agrupada. Estos valores a veces son inexactos. Por ejemplo, iPhone5 con DPR=2 y iPhone12 con `dpr=3`, ambos muestran `dpr=2`. Sin embargo, para los dispositivos de alta resolución, es mejor enviar `dpr=2` que enviar `dpr=1`. Sin embargo, la mejor manera de superar esta inexactitud es utilizar la DPR del lado del cliente para ofrecerle valores 100% precisos. Y funciona para cualquier dispositivo, ya sea Apple o cualquier otro dispositivo que se haya iniciado. Consulte [Usar imágenes inteligentes con proporción de píxeles de dispositivo del lado del cliente](/help/assets/dynamic-media/client-side-dpr.md).

**Ventajas clave adicionales de imágenes inteligentes**

* Se ha mejorado la clasificación SEO de Google para las páginas web que utilizan las últimas imágenes inteligentes.
* Ofrece contenido optimizado inmediatamente (durante la ejecución).
* Utiliza la tecnología Adobe AI para realizar conversiones de acuerdo con la calidad (`qlt`) especificada en la solicitud de imagen.
* TTL (Tiempo de vida) independiente. Anteriormente, era obligatorio un TTL mínimo de 12 horas para que las imágenes inteligentes funcionaran.
* Anteriormente, tanto las imágenes originales como las derivadas se almacenaban en caché y se realizó un proceso de 2 pasos para invalidar la caché. En la última versión de imágenes inteligentes, solo se almacenan en caché los derivados, lo que permite un proceso de invalidación de la caché de un solo paso.
* Los clientes que utilizan encabezados personalizados en su conjunto de reglas se benefician de la última versión de imágenes inteligentes, ya que estos encabezados no están bloqueados, a diferencia de la versión anterior de imágenes inteligentes.

## Funcionamiento de las imágenes inteligentes{#how-smart-imaging-works}

Cuando un consumidor solicita una imagen, Smart Imaging analiza las características del usuario y la convierte al formato adecuado en función del explorador. Estas conversiones de formato se realizan de una manera que no degrada la fidelidad visual. Las imágenes inteligentes convierten automáticamente las imágenes a diferentes formatos, según la capacidad del explorador, de la siguiente manera.

* Convertir automáticamente a AVIF si el explorador admite el formato
* Convertir automáticamente a WebP si la conversión AVIF no fue beneficiosa o si el explorador no admite AVIF
* Convertir automáticamente a JPEG2000 si Safari no admite WebP
* Convertir automáticamente a JPEGXR para IE 9+ o si Edge no admite WebP

  | Formato de imagen | Navegadores admitidos |
  |---|---|
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

Imágenes inteligentes vuelve a calcular la calidad de los formatos de archivo de imagen de JPEG al convertirlos a un nuevo formato.

Para formatos de archivo de imagen compatibles con transparencias como PNG, puede configurar Imágenes inteligentes para proporcionar AVIF y WebP con pérdidas. Para la conversión de formato con pérdida, Imágenes inteligentes utiliza la calidad mencionada en la dirección URL de la imagen o, de lo contrario, la calidad configurada en la cuenta de empresa de Dynamic Media.

## Compatibilidad con comandos de Image Serving en Imágenes inteligentes{#imaging-serving-command-support}

No se admiten los comandos del servicio de imágenes `fmt` y `qlt`; se admiten todos los comandos restantes.

## Preguntas frecuentes sobre imágenes inteligentes{#smart-imaging-faq}

+++**¿Hay costos de licencia asociados con imágenes inteligentes?**

No. Las imágenes inteligentes se incluyen con la licencia existente. Esta regla es verdadera para Dynamic Media Classic o Experience Manager: Dynamic Media (local, AMS y Experience Manager as a Cloud Service).

>[!IMPORTANT]
>
>Imágenes inteligentes no está disponible para los clientes híbridos de Dynamic Media.

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

Imágenes inteligentes se integra perfectamente con los ajustes preestablecidos de imagen existentes, respetando todos los ajustes de la imagen.

Los únicos ajustes implican el formato de imagen, o la calidad, o ambos. Durante la conversión de formato, Imágenes inteligentes conserva la fidelidad visual completa según los ajustes preestablecidos, pero proporciona un tamaño de archivo más pequeño. Solo tiene que habilitarlo agregando `bfc=on`, `dpr=on,dprValue` o `network=on`, o los tres parámetros de configuración a sus direcciones URL o ajustes preestablecidos existentes.

Por ejemplo, supongamos que un ajuste preestablecido de imagen especifica un formato JPEG de 500 × 500 píxeles, con `quality=85` y `unsharp mask=0.1,1,5`. Imágenes inteligentes detecta si el usuario se encuentra en un navegador Chrome. A continuación, convierte la imagen a WebP con las mismas dimensiones (500 × 500) y una máscara de enfoque que coincide con la configuración de JPEG. A continuación, el sistema compara los tamaños de archivo de las versiones WebP y JPEG y sirve la más pequeña para el usuario.

+++

<!-- OLD VERSION BELOW AS PER CQDOC-22085>
Yes. Smart Imaging works with your existing image presets and observes all your image settings. What changes is the image format, or the quality setting, or both. For format conversion, Smart Imaging maintains full visual fidelity as defined by your image preset settings, but at a smaller file size.

For example, suppose that an image preset is defined with JPEG format, size 500 x 500, quality=85, and unsharp mask=0.1,1,5. When Smart Imaging detects that a user is on a Chrome browser, the image is converted to WebP format, with size 500 x 500. And, unsharp mask=0.1,1,5 is at a WebP quality that matches a JPEG quality of 85 as close as possible. The footprint of that WebP conversion is compared with the JPEG, and the smaller of the two is returned. -->

<!-- QUESTION BELOW WAS REMOVED AS PER CQDOC-22085

+++**Do I have to change any URLs, image presets, or deploy new code on my site?**

No. Smart Imaging works seamlessly with your existing image URLs and image presets. In addition, Smart Imaging does not require you to add code to your website to detect a user's browser. All of this functionality is handled automatically.

<!-- Smart Imaging works seamlessly with your existing image URLs and image presets if you configure Smart Imaging on your existing custom domain. In addition, Smart Imaging does not require you to add any code on your website to detect a user's browser. It is all handled automatically.

In case you must configure a new custom domain to use Smart Imaging, the URLs must be updated to reflect this custom domain.

To understand pre-requisites for Smart Imaging, see [Am I eligible to use Smart Imaging?](#am-i-eligible-to-use-smart-imaging) -->

<!-- OLD As mentioned earlier, Smart Imaging supports only JPEG and PNG image formats. For other formats, you need to append the `bfc=off` modifier to the URL as described earlier. 

-->

+++**¿Smart Imaging funciona con HTTPS? ¿Qué tal HTTP/2?**

Sí, a ambas preguntas. Imágenes inteligentes funciona con imágenes entregadas a través de HTTP o HTTPS. Además, también funciona sobre HTTP/2.
+++

+++**¿Cumplo los requisitos para usar imágenes inteligentes?**

Imágenes inteligentes está listo para su uso inmediato para todos los clientes. Para comenzar a disfrutar de sus ventajas, simplemente agregue `bfc=on`, o `dpr=on,dprValue`, o `network=on`, o los tres parámetros de configuración a las direcciones URL o ajustes preestablecidos existentes.

Para activar Imágenes inteligentes, la cuenta de Dynamic Media Classic o Dynamic Media de su empresa en Experience Manager debe incluir la red de distribución de contenido (CDN) incluida en Adobe como parte de su licencia.

+++

+++**¿Cuál es el proceso para habilitar imágenes inteligentes en una cuenta?**

Para empezar a usar imágenes inteligentes, agregue `bfc=on`, `dpr=on,dprValue` o `network=on`, o los tres parámetros a las direcciones URL o ajustes preestablecidos existentes. Si prefiere no realizar estos cambios manualmente, puede habilitar Imágenes inteligentes de forma predeterminada creando un caso de soporte.

Al crear el caso de soporte, especifique qué funciones de imágenes inteligentes desea activar en su cuenta:

* Conversión de formato del explorador (WebP o AVIF)
* Optimización del ancho de banda de red

>[!NOTE]
>
>El RGPD requiere ajustes del lado del cliente para determinar el `dprValue` correcto. Por lo tanto, Adobe recomienda habilitar el DPR mediante direcciones URL adjuntando `dpr=on,dprValue`.

**Para crear un caso de soporte para habilitar imágenes inteligentes en su cuenta:**

1. [Use Admin Console para iniciar la creación de un nuevo caso de soporte](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html).
1. Proporcione la siguiente información en su caso de asistencia:

   * **Detalles de contacto principal:**

      * Proporcione su nombre, correo electrónico y número de teléfono.

   * **Funciones de imágenes inteligentes para habilitar:**

      * Enumere las funcionalidades que desee para su cuenta:

         * Conversión de formato del explorador: WebP o AVIF
         * Optimización del ancho de banda de red
         * DPR: DPR requiere ajustes del lado del cliente para determinar el `dprValue` correcto. Por lo tanto, Adobe recomienda habilitar el DPR mediante direcciones URL adjuntando `dpr=on,dprValue`.

   * **Dominio para imágenes inteligentes:**

      * Enumerar todos los dominios relevantes, como *`company.com`* o *`mycompany.scene7.com`*
      * Imágenes inteligentes admite dominios genéricos y personalizados.
      * Para identificar sus dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/en/docs/dynamic-media-classic/using/getting-started/signing-out#getting-started) e inicie sesión en su cuenta de empresa.

         1. Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**.
         1. Busque el campo **[!UICONTROL Nombre de servidor publicado]** para confirmar su dominio.
         1. Compruebe que está utilizando la CDN de Adobe en lugar de una administrada por otro proveedor.

   * **Indicar compatibilidad con HTTP/2:**

      * Especifique si necesita imágenes inteligentes para trabajar sobre HTTP/2.

1. La Asistencia al cliente de Adobe habilita las funciones de imágenes inteligentes solicitadas de forma predeterminada, lo que elimina la necesidad de anexar parámetros manualmente a las direcciones URL.
1. Adobe recomienda establecer el Tiempo de vida (TTL) en al menos 24 horas para maximizar el rendimiento mediante el almacenamiento en caché.
Para ajustar el TTL:

   1. **Para Dynamic Media Classic:**
      1. Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de aplicación]** > **[!UICONTROL Configuración de publicación]** > **[!UICONTROL Servidor de imágenes]**.
      1. Establezca el valor de **[!UICONTROL Tiempo de almacenamiento en caché del cliente predeterminado para activo]** en 24 horas o más.
   1. **Para Dynamic Media en Adobe Experience Manager:**
      1. Siga [estas instrucciones](/help/assets/dynamic-media/config-dm.md).
      1. Establezca el valor **[!UICONTROL Expiration]** durante 24 horas o más.

+++

+++**¿Cuándo se habilita una cuenta con imágenes inteligentes?**

La Asistencia al cliente procesa las solicitudes en el orden en que las recibe, según la Lista de espera.

>[!NOTE]
>
>Puede haber un tiempo de espera largo porque habilitar imágenes inteligentes implica que Adobe borre la caché. Por lo tanto, solo se pueden gestionar unas pocas transiciones de clientes en un momento determinado.

+++

+++**¿Hay riesgos con el uso de imágenes inteligentes?**

No hay riesgo para una página web de cliente. Sin embargo, la transición a Imágenes inteligentes borra la caché de CDN. Esta operación implica pasar a una nueva configuración de Dynamic Media Classic o Dynamic Media en Experience Manager.

Durante la transición inicial, las imágenes no almacenadas en caché acceden directamente a los servidores de origen de Adobe hasta que se vuelva a crear la caché. Como tal, Adobe tiene previsto gestionar varias transiciones de clientes a la vez, de modo que se mantenga un rendimiento aceptable al extraer solicitudes del origen. Para la mayoría de los clientes, la caché se vuelve a crear por completo en la CDN en un plazo de uno a dos días.

+++

+++**¿Puedo verificar si las imágenes inteligentes funcionan?**

Sí. Puede hacer lo siguiente:

1. Una vez configurada la cuenta con Imágenes inteligentes, cargue una URL de imagen de Dynamic Media Classic o Adobe Experience Manager - Dynamic Media en el explorador.
1. Para abrir el panel de desarrolladores de Chrome, ve a **[!UICONTROL Ver]** > **[!UICONTROL Desarrollador]** > **[!UICONTROL Herramientas para desarrolladores]** en el explorador. O bien, elija cualquier herramienta para desarrolladores de navegadores de su elección.

1. Asegúrese de que la caché esté deshabilitada cuando las herramientas para desarrolladores estén abiertas.

   * En Windows®, vaya a la configuración en el panel de herramientas para desarrolladores y, a continuación, active la casilla de verificación **[!UICONTROL Deshabilitar caché (mientras devtools esté abierto)]**.
   * En macOS, en el panel Desarrollador, en la ficha **[!UICONTROL Red]**, seleccione **[!UICONTROL deshabilitar caché]**.

1. Observe cómo el Tipo de contenido se transforma al formato adecuado. La siguiente captura de pantalla muestra una imagen PNG convertida dinámicamente a WebP en Chrome. Si su dominio tiene habilitado AVIF, también puede esperar ver AVIF en el Tipo de contenido.
1. Repita esta prueba en diferentes navegadores y condiciones de usuario.

>[!NOTE]
>
>No todas las imágenes se convierten. Imágenes inteligentes decide si la conversión puede mejorar el rendimiento. En ocasiones, cuando no se espera una ganancia de rendimiento o el formato no es JPEG o PNG, la imagen no se convierte.

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
>Si el valor de `X-Adobe-Smart-Imaging` es -1 y WebP aún se está entregando, Imágenes inteligentes estará activo. Sin embargo, las ventajas de tamaño no se calcularon debido a que la caché no está actualizada. Puede usar `cache=update` (solo una vez) en la dirección URL de la imagen para solucionar este problema.
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
* Utilice un formato preferido por el explorador definido por Imágenes inteligentes. Por ejemplo, puede utilizar WebP para el explorador Web Chrome.

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

Sí. Imágenes inteligentes ajusta automáticamente el porcentaje de calidad. Esta calidad se determina mediante un algoritmo de aprendizaje automático desarrollado por Adobe. Este porcentaje no es específico del intervalo.

+++

+++**¿Solo JPEG y PNG son reemplazados por Imágenes inteligentes?**

Sí. Esta funcionalidad solo funciona para JPEG y PNG.

+++

+++**¿Por qué JPEG a veces se devuelve a Chrome en lugar de a WebP?**

Imágenes inteligentes determina si la conversión es beneficiosa o no. Devuelve la nueva imagen solo si la conversión es beneficiosa.

+++

+++**¿Por qué la proporción de píxeles del dispositivo (dpr) no funciona con imágenes compuestas?**

Si una imagen compuesta implica demasiadas capas, la funcionalidad de dpr puede verse afectada al utilizar un modificador de posición. Este problema se conoce y se solucionará en futuras versiones de Imágenes inteligentes. Si otras funcionalidades de imágenes inteligentes no funcionan según lo esperado, puede crear un caso de asistencia para informar del problema.

+++

+++**¿Por qué el PNG de imágenes inteligentes se convierte en WebP/AVIF sin pérdidas?**

Como PNG es un formato sin pérdidas, las entregas anteriores de WebP y AVIF no sufrieron pérdidas, lo que dio como resultado un tamaño mayor del esperado. Imágenes inteligentes ahora admite la conversión con pérdida. Puede usar el modificador `cache=update` (solo una vez) en una solicitud de imagen para solucionar este problema. Ejemplo de uso de este modificador:

`https://smartimaging.scene7.com/is/image/SmartImaging/sample1?cache=update`

Para invalidar toda la caché, debe crear un caso de soporte que solicite ese esfuerzo.

+++

+++**¿Puedo seguir usando PNG para convertir sin pérdidas en imágenes inteligentes?**

Sí. Imágenes inteligentes ahora admite la conversión con pérdida en función del nivel de calidad. Puede seguir utilizando la conversión sin pérdidas estableciendo la calidad en 100, ya sea mediante la configuración de su empresa o agregando `qlt=100` a la ruta de acceso URL de la imagen.

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
>* [Image optimization with next generation image formats WebP and AVIF](https://medium.com/adobetech/image-optimisation-with-next-gen-image-formats-webp-and-avif-248c75afacc4). 
-->
