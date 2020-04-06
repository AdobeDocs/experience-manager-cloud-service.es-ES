---
title: Compartir recursos, carpetas y colecciones como vínculo
description: En este artículo se describe cómo compartir recursos, carpetas y colecciones dentro de Experience Manager Assets como un hipervínculo.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Configuración del uso compartido de vínculos de recursos {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Para generar la URL de los recursos que desea compartir con los usuarios, utilice el cuadro de diálogo Uso compartido de vínculos. Los usuarios con privilegios de administrador o con permisos de lectura en la `/var/dam/share` ubicación pueden realizar la vista de los vínculos compartidos con ellos. El uso compartido de recursos a través de un vínculo es una forma práctica de poner los recursos a disposición de terceros externos sin que estos tengan que iniciar sesión en Recursos AEM en primer lugar.

>[!NOTE]
>
>Si desea compartir vínculos de la instancia de AEM Author con entidades externas, asegúrese de que solo muestra las siguientes URL para `GET` solicitudes. Bloquee otras direcciones URL para asegurarse de que la instancia de AEM Author es segura.
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


## Configurar el servicio de correo de CQ Day {#configmailservice}

Para poder compartir recursos como vínculos, configure el servicio de correo electrónico.

1. Pulse o haga clic en el logotipo de AEM y, a continuación, vaya a **[!UICONTROL Herramientas]** > **[!UICONTROL Operaciones]** > **[!UICONTROL Consola web]**.
1. En la lista de servicios, localice **[!UICONTROL Day CQ Mail Service]**.
1. Haga clic en el icono **[!UICONTROL Editar]** al lado del servicio y configure los siguientes parámetros para el **servicio de correo de CQ Day** con los detalles mencionados en relación con sus nombres:

   * Nombre de host del servidor SMTP: nombre de host del servidor de correo electrónico
   * Puerto del servidor SMTP: puerto del servidor de correo electrónico
   * Usuario SMTP: nombre de usuario del servidor de correo electrónico
   * Contraseña SMTP: contraseña del servidor de correo electrónico

1. Click/tap **Save**.

## Configurar el tamaño máximo de datos {#maxdatasize}

Al descargar recursos del vínculo compartido mediante la función de uso compartido de vínculos, AEM comprime la jerarquía de recursos del repositorio y, a continuación, devuelve el recurso en un archivo ZIP. Sin embargo, a falta de límites a la cantidad de datos que se pueden comprimir en un archivo ZIP, grandes cantidades de datos están sujetas a compresión, lo que causa errores de memoria insuficiente en JVM. Para proteger el sistema de un posible ataque de denegación de servicio debido a esta situación, configure el tamaño máximo usando el parámetro Tamaño de contenido **máximo (sin comprimir)** para el servlet proxy de uso compartido de recursos ad hoc CQ DAM de Day en Configuration Manager. Si el tamaño sin comprimir del recurso supera el valor configurado, se rechazan las solicitudes de descarga de recursos. El valor predeterminado es 100 MB.

1. Haga clic o pulse el logotipo de AEM y, a continuación, vaya a **Herramientas** > **Operaciones** > **Consola web**.
1. Desde la consola web, busque la configuración del servlet proxy **Day CQ DAM Adhoc Asset Share** .
1. Abra la configuración del servlet proxy **Day CQ DAM Adhoc Asset Share** en modo de edición y modifique el valor del parámetro **Tamaño de contenido máximo (sin comprimir)**.
1. Guarde los cambios.

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->
