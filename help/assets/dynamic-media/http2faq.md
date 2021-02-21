---
title: Preguntas frecuentes sobre la entrega de contenido HTTP2
description: Obtenga información sobre el envío de contenido HTTP2.
translation-type: tm+mt
source-git-commit: 193201670e5e78235025885f52215cca730ce556
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 3%

---


# Preguntas frecuentes sobre la entrega de contenido HTTP2{#http-delivery-of-content-faq}

Adobe está emocionado de anunciar la disponibilidad del envío HTTP/2 del contenido. Al utilizar HTTP/2, se produce un aumento general del rendimiento.

## ¿Qué es HTTP/2? {#what-is-http}

HTTP/2 mejora la forma en que se comunican los exploradores y los servidores, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.

El siguiente sitio web describe HTTP/2 y sus ventajas de una manera breve y sencilla:

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## ¿Cuáles son las ventajas clave del cambio a HTTP/2 para el envío de contenido? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

La mejora del rendimiento varía ampliamente porque se basa en diversos factores. Por ejemplo, el código de su sitio web, la forma en que utiliza Dynamic Media, el dispositivo, la pantalla y la ubicación del consumidor.

Las propias pruebas de Adobe dieron los siguientes resultados:

* En el caso de las imágenes, el tiempo de respuesta mejoró entre un 7% y un 28% en función del dispositivo y el explorador. Las mejoras de rendimiento más notables se produjeron en dispositivos iOS.
* Para los visores, el rendimiento del tiempo de carga ha mejorado un 15 %.

La siguiente demostración ilustra la diferencia entre la carga HTTP/1 y la carga HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## ¿Puedo cambiar a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para utilizar HTTP/2, debe cumplir los siguientes requisitos:

* Utilice HTTPS seguro para sus solicitudes de medios enriquecidos.
* Utilice la CDN (red de envío de contenido) incluida en el Adobe como parte de su licencia de Dynamic Media Classic.
* Utilice un dominio dedicado (es decir, `images.company.com` o `mycompany.scene7.com`), no un dominio Dynamic Media genérico (es decir, `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

   Para encontrar sus dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en su cuenta.

   Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuracióngeneral]**. Busque el campo etiquetado **Nombre del servidor publicado**. Si actualmente está utilizando un dominio de Dynamic Media genérico, puede solicitar el traslado a su propio dominio personalizado como parte de esta transición.

## ¿Cuál es el proceso para habilitar HTTP/2 en mi cuenta de Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dm-account}

[Utilice el Admin Console para crear un ](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html) caso de asistencia y solicitar cambiar a HTTP/2; no se hace automáticamente por usted.

1. Proporcione la siguiente información en su caso de asistencia:

   * Nombre de contacto principal, correo electrónico y número de teléfono.
   * Todos los dominios que se van a transferir a HTTP2. Es decir, `images.company.com` o `mycompany.scene7.com`.

   Para encontrar sus dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en su cuenta.

   Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuracióngeneral]**. Busque el campo etiquetado **[!UICONTROL Nombre del servidor publicado]**.

   * Compruebe que utiliza HTTPS seguro para solicitudes de medios enriquecidos.
   * Compruebe que está utilizando la CDN mediante Adobe y que no se administra con una relación directa.
   * Compruebe que está utilizando un dominio dedicado. Es decir, `images.company.com` o `mycompany.scene7.com`, no es un dominio de Dynamic Media genérico como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

   Para encontrar sus dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) y luego inicie sesión en su cuenta.

   Haga clic en **[!UICONTROL Ajustes > Ajustes de aplicación > Configuracióngeneral]**. Busque el campo etiquetado **[!UICONTROL Nombre del servidor publicado]**. Si actualmente está utilizando un dominio de Dynamic Media genérico, puede solicitar el traslado a su propio dominio personalizado como parte de esta transición.

   1. La asistencia técnica le agrega a la lista de espera de clientes HTTP/2 en función del orden en que se enviaron las solicitudes.
   1. Cuando Adobe está listo para gestionar su solicitud, el Servicio de atención al cliente se pone en contacto con usted para coordinar la transición y establecer una fecha de destinatario.
   1. Se le notificará una vez finalizada la operación y podrá comprobar que la transición a HTTP2 se ha realizado correctamente.



## ¿Cuándo puedo esperar que se realice la transición a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Las solicitudes se procesan en el orden en que son recibidas por la asistencia técnica.

>[!NOTE]
>
>Hay un largo tiempo de espera porque la transición a HTTP/2 implica borrar la caché. Por lo tanto, sólo se pueden gestionar unas pocas transiciones de clientes a la vez.

## ¿Cuáles son los riesgos de pasar a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transición a HTTP/2 borra la caché en la CDN porque implica pasar a una nueva configuración de CDN.

El contenido no almacenado en caché entra directamente en los servidores origen del Adobe hasta que se vuelve a crear la caché. Debido a esta acción, Adobe planea gestionar algunas transiciones de clientes a la vez. Este método garantiza que se mantenga un rendimiento aceptable al extraer solicitudes del origen.

## ¿Cómo puede verificar si una dirección URL o un sitio web está activado con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Descargue una extensión para utilizarla con el explorador Web. Para Firefox y Chrome, existe una extensión denominada **[!UICONTROL HTTP/2 e Indicador SPDY]**. Los navegadores solo admiten HTTP/2 de forma segura, por lo que es necesario llamar a una URL con HTTPS para verificarla. Si se admite HTTP/2, se indica con la extensión en forma de símbolo de Flash azul y con el encabezado &quot;X-Firefox-Spdy&quot;: &quot;h2&quot;.
