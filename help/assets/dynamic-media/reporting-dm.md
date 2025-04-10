---
title: Creación de informes en Dynamic Media
description: Obtenga información sobre cómo solicitar un informe de errores para las direcciones URL de entrega de Dynamic Media que fallan.
contentOwner: Rick Brough
feature: Asset Management
role: User
hide: true
hidefromtoc: true
exl-id: 2488f813-df15-4dbb-8747-f827ee5925e1
source-git-commit: 36ab36ba7e14962eba3947865545b8a3f29f6bbc
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Solicitar un informe de errores para las direcciones URL de entrega de Dynamic Media que fallan

Puede solicitar un informe de error que identifique las URL de Dynamic Media que fallaron en el momento de la entrega. El informe es una suma de datos de hasta cinco días y está disponible en formato CSV. El informe de errores incluye la siguiente información:

* URL de envío de Dynamic Media con error: una URL con error es una URL generada por Dynamic Media que no puede producir ningún contenido en el momento de la entrega.
* URL del referente: la URL del referente desde la que se llama a la URL de entrega fallida.
* Recuento de errores: el número de veces que se cargó la dirección URL de envío que resultó en un error.

Cuando solicita el informe de errores, el equipo de Dynamic Media de Adobe le envía por correo electrónico el informe en formato CSV. Cubre un periodo de cinco días a partir del día en que se realizó su solicitud.

Puede solicitar un informe de errores una vez al mes, para una compañía determinada.

**Para solicitar un informe de errores para las direcciones URL de entrega de Dynamic Media que no se completan:**

1. [Envíe un correo electrónico a reports-dynamic-media@adobe.com](mailto:reports-dynamic-media@adobe.com) con el nombre de la empresa asociada a su cuenta de Dynamic Media.

   Si no conoce el nombre de la empresa, consulte la página [Configuración de Dynamic Media](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html?lang=es#configuring-dynamic-media-cloud-services) en **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Herramientas]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Configuración de Dynamic Media]**. En la página Explorador de configuración de Dynamic Media, haga clic en **[!UICONTROL global]**, active la casilla de verificación *[Dynamic_Media_folder_icon]* y, a continuación, seleccione **[!UICONTROL Editar]**. Debe tener derechos de administrador en AEM para acceder a la página de configuración de Dynamic Media.

   ![Accediendo a la página de configuración de Dynamic Media.](/help/assets/dynamic-media/assets/reporting-accessdmconfig.png)
