---
title: Invalidar la caché de CDN (red de entrega de contenido) mediante Dynamic Media Classic
description: Aprenda a invalidar el contenido almacenado en caché de la CDN (red de distribución de contenido) para permitirle actualizar rápidamente los recursos que Dynamic Media entrega, en lugar de esperar a que caduque la caché.
feature: Administración de recursos,Dynamic Media Classic
role: Admin,User
exl-id: 7e488699-5633-437f-9e2e-58c98aa13145
source-git-commit: 1d42305b6a597dc95bff8b34eee8279eb0e511f3
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 13%

---

# Invalidar la caché de CDN mediante Dynamic Media Classic {#invalidating-your-cdn-cached-content}

La CDN (red de distribución de contenido) almacena en caché los recursos de Dynamic Media para una entrega rápida. Sin embargo, cuando actualice un recurso, desea que esos cambios surtan efecto inmediatamente. La invalidación del contenido en caché de CDN permite actualizar rápidamente los recursos que Dynamic Media entrega, en lugar de esperar a que caduque la caché.

>[!NOTE]
>
>Esta función requiere que utilice la CDN predeterminada incluida con Adobe Experience Manager Dynamic Media. Esta función no admite ninguna otra CDN personalizada.

>[!IMPORTANT]
>
>Estos pasos se aplican únicamente a Dynamic Media en Adobe Experience Manager 6.5, Service Pack 5 o anterior. <!-- If you are using Dynamic Media in AEM as a Cloud Service, [use the new steps found here](/help/assets/invalidate-cdn-cache-dynamic-media.md). -->

Consulte también [Información general de caché en Dynamic Media Classic](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Para invalidar la caché de la CDN mediante Dynamic Media Classic:**

1. Abra la [aplicación de escritorio de Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html#getting-started) e inicie sesión en su cuenta.

   Adobe proporcionó las credenciales y los detalles de inicio de sesión en el momento del aprovisionamiento. Si no dispone de esta información, póngase en contacto con el servicio de asistencia técnica.

1. Vaya a **[!UICONTROL Configuración]** > **[!UICONTROL Configuración de la aplicación]** > **[!UICONTROL Configuración general]**.
1. En la página Configuración general de la aplicación , en el encabezado del grupo Servidores , busque el cuadro de texto **[!UICONTROL Plantilla de invalidación de CDN]**.

1. Especifique la plantilla que se utiliza para invalidar la caché de la CDN (red de entrega de contenido).

   Por ejemplo, supongamos que introduce una URL de imagen (incluidos los ajustes preestablecidos de imagen o modificadores) que hace referencia a `<ID>`, en lugar de un ID de imagen específico, como en el siguiente ejemplo:

   `https://server.com/is/image/Company/<ID>?$product$`

   Si la plantilla solo contiene `<ID>`, Dynamic Media rellena `https://<server>/is/image` donde `<server>` es el nombre del servidor de publicación definido en Configuración general y &lt;ID> es el recurso seleccionado para invalidarse.

1. En la esquina inferior derecha de la página, seleccione **[!UICONTROL Cerrar]**.
1. En la interfaz de usuario de Dynamic Media Classic (Scene7), seleccione uno o varios recursos y vaya a **[!UICONTROL File]** > **[!UICONTROL Invalidate CDN]**. Puede ver una lista de una o más direcciones URL generadas a partir de la plantilla creada y los recursos seleccionados. Utiliza la URL del servidor que aparece en &quot;Nombre del servidor publicado&quot; en Configuración general de la aplicación.

   Por ejemplo, con la plantilla de invalidación de CDN establecida en el paso anterior, supongamos que ha seleccionado una sola imagen de recurso de imagen denominada `Backpack_B`. Cuando vaya a **[!UICONTROL File]** > **[!UICONTROL Invalidate CDN]**, se generará la siguiente URL en la interfaz de usuario de Invalidación de CDN:

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. En el cuadro de lista URL, seleccione **[!UICONTROL Continue]** para borrar la caché de cada URL específica. Puede editar una dirección URL o agregar una dirección URL escribiéndola o pegándola en el cuadro de lista de direcciones URL; no es necesario configurar la plantilla de invalidación de CDN de antemano.

   Después de seleccionar **[!UICONTROL Continue]**, se muestra un indicador que ofrece una estimación del tiempo que se tardará en borrar la caché.

   Si seleccionó varios recursos y accedió a **[!UICONTROL Archivo]** > **[!UICONTROL Invalidar CDN]**, se hace referencia a cada recurso en la **[!UICONTROL URL de plantilla]** guardada. Por lo tanto, puede definir una **[!UICONTROL Plantilla de invalidación de CDN]** que haga referencia a cada ajuste preestablecido de imagen URL al que se hace referencia en el sitio web, como detalles del producto y resultados de búsqueda. A continuación, al seleccionar una o varias imágenes para la invalidación desde la caché, las direcciones URL rellenan automáticamente la interfaz.

   >[!NOTE]
   >
   >Al seleccionar recursos y, a continuación, ir a **[!UICONTROL File]** > **[!UICONTROL Invalidate CDN]**, Dynamic Media utiliza una plantilla de CDN no válida para crear automáticamente direcciones URL que se van a invalidar desde la CDN. Si no hay nada en el cuadro de texto **[!UICONTROL Plantilla de invalidación de CDN]**, aparecerá una lista de URL en blanco. El almacenamiento en caché en la CDN no está basado en recursos; se basa en la URL. Por lo tanto, es necesario conocer las direcciones URL completas que se encuentran en el sitio web. Después de establecer dichas direcciones URL, puede agregarlas al cuadro de texto **[!UICONTROL Invalidar plantilla CDN]** en los pasos anteriores. A continuación, puede seleccionar esos recursos e invalidar las direcciones URL en un solo paso.
   >
   >Otra opción es agregar direcciones URL completas a la lista **[!UICONTROL Invalidar CDN]**. Si sigue este método, no es necesario seleccionar recursos en Dynamic Media Classic antes de ir a la opción **[!UICONTROL File]** > **[!UICONTROL Invalidate CDN]**.
