---
title: Preguntas frecuentes sobre la entrega de contenido HTTP2
description: Obtenga información sobre la entrega de contenido HTTP2.
contentOwner: Rick Brough
role: Admin,User
exl-id: 0a8a5fd8-a341-4e7f-84a5-409e2de97efe
source-git-commit: 35caac30887f17077d82f3370f1948e33d7f1530
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# Preguntas frecuentes sobre la entrega de contenido HTTP2{#http-delivery-of-content-faq}

Adobe se complace en anunciar la disponibilidad de la entrega HTTP/2 de contenido. Al utilizar HTTP/2, se produce un aumento general del rendimiento.

>[!NOTE]
>
>Esta función requiere que utilice la red de entrega de contenido lista para usar que está incluida con Adobe Experience Manager - Dynamic Media. Esta función no admite ninguna otra red de distribución de contenido personalizada.

## ¿Qué es HTTP/2? {#what-is-http}

HTTP/2 mejora la forma en que se comunican los exploradores y los servidores, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.

El artículo del sitio web [Qué debe saber sobre HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html) describe HTTP/2 y sus ventajas de una manera breve y sencilla.

## ¿Cuáles son las ventajas clave del paso a HTTP/2 para la entrega de contenido? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

La mejora del rendimiento varía ampliamente porque se basa en diversos factores. Por ejemplo, el código de su sitio web, cómo utiliza Dynamic Media, el dispositivo, la pantalla y la ubicación del consumidor.

Las propias pruebas de Adobe dieron los siguientes resultados:

* En el caso de las imágenes, el tiempo de respuesta mejoró del 7 % al 28 % en función del dispositivo y el navegador. Las mejoras de rendimiento más notables se produjeron en dispositivos iOS.
* Para los visores, el rendimiento del tiempo de carga ha mejorado un 15%.

La siguiente demostración ilustra la diferencia entre la carga HTTP/1 y HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## ¿Puedo cambiar a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para utilizar HTTP/2, debe cumplir los siguientes requisitos:

* Utilice HTTPS seguro para sus solicitudes de medios enriquecidos.
* Utilice la CDN (red de distribución de contenido) incluida en la Adobe como parte de su licencia de Dynamic Media Classic.
* Usar un dominio dedicado (es decir, `images.company.com` o `mycompany.scene7.com`), no un dominio Dynamic Media genérico (es decir, `s7d1.scene7.com`, `s7d2.scene7.com`o `s7d13.scene7.com`).

   Para encontrar los dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en su cuenta.

   Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo etiquetado **Nombre del servidor publicado**. Si está utilizando un dominio genérico de Dynamic Media, puede solicitar pasar a su propio dominio personalizado como parte de esta transición.

## ¿Cuál es el proceso para habilitar HTTP/2 para mi cuenta de Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dm-account}

[Utilice el Admin Console para crear un caso de asistencia](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) y solicitar cambiar a HTTP/2; no se realiza automáticamente.

1. Proporcione la siguiente información en su caso de asistencia:

   * Nombre de contacto principal, correo electrónico y número de teléfono.
   * Todos los dominios que se van a transferir a HTTP2. Es decir, `images.company.com` o `mycompany.scene7.com`.

   Para encontrar los dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en su cuenta.

   Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo etiquetado **[!UICONTROL Nombre del servidor publicado]**.

   * Compruebe que utiliza HTTPS seguro para solicitudes de medios enriquecidos.
   * Compruebe que está utilizando la CDN a través de la Adobe y que no se administra con una relación directa.
   * Compruebe que está utilizando un dominio dedicado. Es decir, `images.company.com` o `mycompany.scene7.com`, no un dominio genérico de Dynamic Media como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

   Para encontrar los dominios, abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started), luego inicie sesión en su cuenta.

   Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo etiquetado **[!UICONTROL Nombre del servidor publicado]**. Si está utilizando un dominio genérico de Dynamic Media, puede solicitar pasar a su propio dominio personalizado como parte de esta transición.

   1. La asistencia al cliente le agrega a la lista de espera de clientes HTTP/2 en función del orden en que se enviaron las solicitudes.
   1. Cuando el Adobe esté listo para gestionar su solicitud, el Servicio de atención al cliente se pondrá en contacto con usted para coordinar la transición y establecer una fecha objetivo.
   1. Se le notificará una vez finalizada y podrá verificar que la transición a HTTP2 se ha realizado correctamente.



## ¿Cuándo puedo esperar que se pase a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Las solicitudes se procesan en el orden en que reciben la asistencia al cliente.

>[!NOTE]
>
>Hay un largo tiempo de espera porque la transición a HTTP/2 implica borrar la caché. Por lo tanto, solo se pueden gestionar algunas transiciones de cliente a la vez.

## ¿Cuáles son los riesgos de pasar a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transición a HTTP/2 borra la caché en la CDN porque implica pasar a una nueva configuración de CDN.

El contenido no almacenado en caché llega directamente a los servidores de origen del Adobe hasta que se vuelve a crear la caché. Debido a esta acción, Adobe planea gestionar algunas transiciones de clientes a la vez. Este método garantiza que se mantenga un rendimiento aceptable al extraer solicitudes del origen.

## ¿Cómo se puede verificar si una URL o un sitio web está activado con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Descargue una extensión para utilizarla con el explorador web. Para Firefox y Chrome, hay una extensión llamada **[!UICONTROL Indicador HTTP/2 y SPDY]**. Los navegadores solo admiten HTTP/2 de forma segura, por lo que es necesario llamar a una dirección URL con HTTPS para verificarlo. Si se admite HTTP/2, se indica con la extensión en forma de símbolo de Flash azul y con el encabezado &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.
