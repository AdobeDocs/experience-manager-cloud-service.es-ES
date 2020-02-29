---
title: Configuración de restricciones al cargar activos
description: Obtenga información sobre cómo configurar Recursos Adobe Experience Manager (AEM) para restringir el tipo de recursos (archivos) que los usuarios pueden cargar.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f2e257ff880ca2009c3ad6c8aadd055f28309289

---


# Configuración de restricciones al cargar activos {#configuring-asset-upload-restrictions}

Puede configurar Recursos Adobe Experience Manager (AEM) para restringir el tipo de recursos (archivos) que los usuarios pueden cargar. Esta función le ayuda a eliminar la posibilidad de que los usuarios carguen recursos en un formato no deseado o carguen archivos maliciosos. El `Day CQ DAM Asset Upload Restriction` servicio le permite controlar el tipo de archivos que los usuarios pueden cargar. De forma predeterminada, Recursos AEM permite a los usuarios cargar recursos de todos los tipos MIME. Sin embargo, puede configurar el servicio para que restrinja a los usuarios la carga de archivos de tipos MIME específicos solamente.

1. Abra la consola web de Configuration Manager. Acceso `https://[aem_server]:[port]/system/console/configMgr`.
1. Abra el servicio **[!UICONTROL Day CQ DAM Asset Upload Restriction]** en modo de edición. De forma predeterminada, está seleccionada la opción **Permitir todo MIME** , que permite a los usuarios cargar archivos de todos los tipos MIME.

   ![chlimage_1-378](assets/chlimage_1-378.png)

1. Para restringir el acceso de los usuarios solo a archivos de ciertos tipos de MIME, desactive la opción **[!UICONTROL Permitir todos los MIME]** y especifique los tipos de MIME permitidos en los campos **[!UICONTROL Recursos de MIME permitidos (regex)]** mediante expresiones regulares.

   ![chlimage_1-379](assets/chlimage_1-379.png)

1. Pulse o haga clic en **[!UICONTROL Guardar]** para almacenar los cambios. Si especifica cadenas MIME para los tipos de MIME permitidos, la operación de carga falla con cualquier recurso que tenga un tipo de MIME que no coincida con las cadenas MIME configuradas en estos campos.
