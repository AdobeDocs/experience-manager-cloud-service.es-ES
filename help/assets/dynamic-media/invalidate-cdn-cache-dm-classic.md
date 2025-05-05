---
title: Invalidación de la caché de la CDN (red de distribución de contenido) mediante Dynamic Media Classic
description: Obtenga información sobre cómo invalidar el contenido en caché de la CDN (red de distribución de contenido) para permitirle actualizar rápidamente los recursos que entrega Dynamic Media, en lugar de esperar a que la caché caduque.
contentOwner: Rick Brough
feature: Asset Management,Dynamic Media Classic
role: Admin,User
exl-id: 7e488699-5633-437f-9e2e-58c98aa13145
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 15%

---

# Invalidación de la caché de CDN mediante Dynamic Media Classic {#invalidating-your-cdn-cached-content}

La CDN (red de distribución de contenido) almacena en caché los recursos de Dynamic Media para agilizar la entrega. Sin embargo, cuando realiza actualizaciones en un recurso, desea que los cambios surtan efecto inmediatamente. La invalidación del contenido en caché de la CDN le permite actualizar rápidamente los recursos que entrega Dynamic Media, en lugar de esperar a que la caché caduque.

>[!NOTE]
>
>Esta función requiere que utilice la CDN predeterminada que está integrada en Adobe Experience Manager Dynamic Media. Esta función no admite ninguna otra CDN personalizada.

>[!IMPORTANT]
>
>Estos pasos solo se aplican a Dynamic Media en Adobe Experience Manager 6.5, Service Pack 5 o versiones anteriores. <!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Para invalidar su caché de CDN mediante Dynamic Media Classic:**

1. Abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=es#getting-started) y luego inicie sesión en su cuenta.

   Adobe proporcionó sus credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con Atención al cliente.

1. Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**.
1. En la página Configuración general de la aplicación, en el encabezado del grupo Servidores, busque el cuadro de texto **[!UICONTROL Plantilla de invalidación de CDN]**.

1. Especifique la plantilla que se utiliza para invalidar la caché de la CDN (red de distribución de contenido).

   Por ejemplo, suponga que introduce una URL de imagen (incluidos los ajustes preestablecidos o modificadores de imagen) que hace referencia a `<ID>`, en lugar de un ID de imagen específico como en el siguiente ejemplo:

   `https://server.com/is/image/Company/<ID>?$product$`

   Si la plantilla solo contiene `<ID>`, Dynamic Media rellena `https://<server>/is/image`, donde `<server>` es el nombre del servidor de publicación definido en Configuración general y &lt;ID> son los recursos seleccionados para invalidar.

1. En la esquina inferior derecha de la página, seleccione **[!UICONTROL Cerrar]**.
1. En la interfaz de usuario de Dynamic Media Classic (Scene7), seleccione uno o varios recursos y vaya a **[!UICONTROL Archivo]** > **[!UICONTROL Invalidar CDN]**. Verá una lista de una o más direcciones URL generadas a partir de la plantilla que creó y los recursos seleccionados. Utiliza la URL del servidor que aparece en &quot;Nombre de servidor publicado&quot; en la Configuración general de la aplicación.

   Por ejemplo, con la plantilla de invalidación de CDN establecida en el paso anterior, suponga que seleccionó una sola imagen de recurso de imagen denominada `Backpack_B`. Si va a **[!UICONTROL Archivo]** > **[!UICONTROL Invalidar CDN]**, se generará la siguiente URL en la interfaz de usuario de invalidación de CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. En el cuadro de lista Dirección URL, seleccione **[!UICONTROL Continuar]** para borrar la caché de cada dirección URL específica. Puede editar una dirección URL o puede agregarla escribiéndola o pegándola en el cuadro de lista URL; no necesita establecer previamente una plantilla de invalidación de CDN.

   Después de seleccionar **[!UICONTROL Continuar]**, aparece un indicador que le proporciona una estimación del tiempo que tardará en borrar la caché.

   Si seleccionó varios recursos y luego fue a **[!UICONTROL Archivo]** > **[!UICONTROL Invalidar CDN]**, se hace referencia a cada recurso en la **[!UICONTROL URL de plantilla]** guardada. Por lo tanto, puede definir una **[!UICONTROL plantilla de invalidación de CDN]** que haga referencia a cada ajuste preestablecido de imagen de URL al que se hace referencia en el sitio web, como detalles del producto y resultados de búsqueda. A continuación, al seleccionar una o varias imágenes para la invalidación desde la caché, las direcciones URL rellenan automáticamente la interfaz.

   >[!NOTE]
   >
   >Al seleccionar recursos y, a continuación, ir a **[!UICONTROL Archivo]** > **[!UICONTROL Invalidar CDN]**, Dynamic Media utiliza una plantilla de CDN no válida para crear automáticamente direcciones URL que se van a invalidar desde la CDN. Si no hay nada en el cuadro de texto **[!UICONTROL Plantilla de invalidación de CDN]**, aparecerá una lista de URL en blanco. El almacenamiento en caché en la CDN no está basado en recursos; se basa en la URL. Por lo tanto, es necesario conocer las direcciones URL completas que se encuentran en el sitio web. Después de establecer dichas direcciones URL, puede agregarlas al cuadro de texto **[!UICONTROL Invalidar plantilla CDN]** en los pasos anteriores. A continuación, puede seleccionar esos recursos e invalidar las direcciones URL en un solo paso.
   >
   >Otra opción es agregar direcciones URL completas a la lista **[!UICONTROL Invalidar CDN]**. Si sigue este enfoque, no es necesario seleccionar los recursos en Dynamic Media Classic antes de ir a la opción **[!UICONTROL Archivo]** > **[!UICONTROL Invalidar CDN]**.
