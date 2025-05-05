---
title: Preguntas frecuentes sobre la entrega de contenido HTTP2
description: Obtenga información sobre la entrega de contenido HTTP2 y cómo mejora la comunicación entre exploradores y servidores para una transferencia de información más rápida.
contentOwner: Rick Brough
feature: Dynamic Media,Configuration,FAQ
role: Admin,User
exl-id: 0a8a5fd8-a341-4e7f-84a5-409e2de97efe
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 1%

---

# Preguntas frecuentes sobre la entrega de contenido HTTP2{#http-delivery-of-content-faq}

Adobe anuncia la disponibilidad de la entrega de contenido HTTP/2. Al utilizar HTTP/2, se experimenta un aumento general del rendimiento.

>[!NOTE]
>
>Esta función requiere que utilice la red de distribución de contenido predeterminada incluida en Adobe Experience Manager - Dynamic Media. Con esta función no se admite ninguna otra red de distribución de contenido personalizada.

## ¿Qué es HTTP/2? {#what-is-http}

HTTP/2 mejora la forma en que los exploradores y servidores se comunican, lo que permite una transferencia de información más rápida y, al mismo tiempo, reduce la cantidad de potencia de procesamiento necesaria.

El artículo del sitio web [Lo que debe saber sobre HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html) describe HTTP/2 y sus ventajas de una manera breve y sencilla.

## ¿Cuáles son las principales ventajas de pasar a HTTP/2 para la entrega de contenido? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

La mejora del rendimiento varía ampliamente porque se basa en varios factores. Por ejemplo, el código de su sitio web, cómo utiliza Dynamic Media, el dispositivo, la pantalla y la ubicación del consumidor.

Las propias pruebas de Adobe arrojaron los siguientes resultados:

* En el caso de las imágenes, el tiempo de respuesta mejoró entre un 7 % y un 28 % en función del dispositivo y el explorador. Las mejoras de rendimiento más notables se obtuvieron en dispositivos iOS.
* Para los espectadores, el rendimiento del tiempo de carga mejoró un 15 %.

La siguiente demostración ilustra la diferencia entre la carga HTTP/1 y HTTP/2:

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## ¿Puedo cambiar a HTTP/2? {#am-i-eligible-to-switch-over-to-http}

Para utilizar HTTP/2, debe cumplir los siguientes requisitos:

* Utilice HTTPS seguro para las solicitudes de medios enriquecidos.
* Utilice la CDN (red de distribución de contenido) incluida en Adobe como parte de la licencia de Dynamic Media Classic.
* Use un dominio dedicado (es decir, `images.company.com` o `mycompany.scene7.com`), no un dominio genérico de Dynamic Media (es decir, `s7d1.scene7.com`, `s7d2.scene7.com` o `s7d13.scene7.com`).

  Para encontrar tus dominios, abre la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=es#getting-started) y luego inicia sesión en tu cuenta.

  Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo denominado **Nombre de servidor publicado**. Si está utilizando un dominio genérico de Dynamic Media, puede solicitar que se traslade a su propio dominio personalizado como parte de esta transición.

## ¿Cuál es el proceso para habilitar HTTP/2 en mi cuenta de Dynamic Media? {#what-is-the-process-for-enabling-http-for-my-dm-account}

[Use Admin Console para crear un caso de soporte](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) y solicite cambiar a HTTP/2; no se hace automáticamente por usted.

1. Proporcione la siguiente información en su caso de asistencia:

   * Nombre del contacto principal, correo electrónico y número de teléfono.
   * Todos los dominios que deben transferirse a HTTP2. Es decir, `images.company.com` o `mycompany.scene7.com`.

   Para encontrar tus dominios, abre la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=es#getting-started) y luego inicia sesión en tu cuenta.

   Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo denominado **[!UICONTROL Nombre de servidor publicado]**.

   * Compruebe que utiliza HTTPS seguro para solicitudes de medios enriquecidos.
   * Compruebe que está utilizando la CDN a través de Adobe y que no está gestionado con una relación directa.
   * Compruebe que está utilizando un dominio dedicado. Es decir, `images.company.com` o `mycompany.scene7.com`, no es un dominio genérico de Dynamic Media como `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

   Para encontrar tus dominios, abre la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=es#getting-started) y luego inicia sesión en tu cuenta.

   Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**. Busque el campo denominado **[!UICONTROL Nombre de servidor publicado]**. Si está utilizando un dominio genérico de Dynamic Media, puede solicitar que se traslade a su propio dominio personalizado como parte de esta transición.

   1. Atención al cliente le añade a la lista de espera de clientes HTTP/2 en función del orden en que se enviaron las solicitudes.
   1. Cuando Adobe esté listo para administrar su solicitud, el Servicio de atención al cliente se pondrá en contacto con usted para coordinar la transición y establecer una fecha objetivo.
   1. Se le notifica una vez finalizada y puede verificar que la transición a HTTP2 se ha realizado correctamente.

## ¿Cuándo puedo esperar que se realice la transición a HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Las solicitudes se procesan en el orden en que se reciben en Asistencia al cliente.

>[!NOTE]
>
>Hay un tiempo de espera largo porque la transición a HTTP/2 implica borrar la caché. Por lo tanto, solo se pueden gestionar unas pocas transiciones de cliente a la vez.

## ¿Cuáles son los riesgos de pasar a HTTP/2? {#what-are-the-risks-with-moving-to-http}

La transición a HTTP/2 borra la caché en la CDN porque implica pasar a una nueva configuración de CDN.

El contenido no almacenado en caché visita directamente los servidores de origen de Adobe hasta que se vuelve a crear la caché. Debido a esta acción, Adobe tiene previsto gestionar algunas transiciones de cliente a la vez. Este método garantiza que se mantenga un rendimiento aceptable al extraer solicitudes del origen.

## ¿Cómo puede verificar si una dirección URL o sitio web está activado con HTTP/2? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Descargue una extensión para utilizarla con el explorador web. Para Firefox y Chrome, hay una extensión llamada **[!UICONTROL HTTP/2 e indicador SPDY]**. Los navegadores solo admiten HTTP/2 de forma segura, por lo que es necesario llamar a una dirección URL con HTTPS para verificarla. Si se admite HTTP/2, se indica con la extensión en forma de símbolo de Flash azul y el encabezado &quot;X-Firefox-Spray&quot; : &quot;h2&quot;.
