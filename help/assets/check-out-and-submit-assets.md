---
title: Insertar y desproteger archivos [!DNL Assets]
description: Obtenga información sobre cómo extraer recursos para editarlos y volver a protegerlos una vez completados los cambios.
contentOwner: AG
feature: Asset Management
role: User
exl-id: adb94a31-d949-4f4a-89bc-44f1b4f67e14
source-git-commit: 8bdd89f0be5fe7c9d4f6ba891d7d108286f823bb
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 6%

---

# Archivos de desprotección y registro en [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] permite extraer recursos para editarlos y volver a protegerlos después de completar los cambios. Después de retirar un recurso, solo puede editarlo, anotarlo, publicarlo, moverlo o eliminarlo. Si se retira un recurso, este se bloquea. Otros usuarios no pueden realizar ninguna de estas operaciones en el recurso hasta que vuelva a proteger el recurso en [!DNL Assets]. Sin embargo, aún pueden cambiar los metadatos del recurso bloqueado.

Para poder extraer o incorporar recursos, debe disponer de acceso de escritura.

Esta función ayuda a evitar que otros usuarios anulen los cambios realizados por un autor en los que varios usuarios colaboran en la edición de flujos de trabajo entre equipos.

## Comprobar recursos {#checking-out-assets}

1. En el [!DNL Assets] interfaz de usuario de , seleccione el recurso que desee desproteger. También puede seleccionar varios recursos para desproteger.

1. En la barra de herramientas, haga clic en **[!UICONTROL Cierre de compra]**. La variable **[!UICONTROL Cierre de compra]** la opción cambia a **[!UICONTROL Proteger]**.
Para verificar si otros usuarios pueden editar el recurso que ha desprotegido, inicie sesión como un usuario diferente. El icono ![icono de bloqueo de cierre de compra](assets/do-not-localize/checkout_lock.png) se muestra en la miniatura del recurso que ha extraído.

   ![icono de cierre de compra en la vista de tarjeta](assets/checkout-icon-card-view.png)

   Seleccione el recurso. Observe que la barra de herramientas no muestra ninguna opción que le permita editar, anotar, publicar o eliminar el recurso.

   ![chlimage_1-472](assets/checkout-asset-toolbar-options.png)

   Para editar los metadatos del recurso bloqueado, haga clic en **[!UICONTROL Ver propiedades]**.

1. Haga clic en **[!UICONTROL Editar]** para abrir el recurso en modo de edición.

1. Edite el recurso y guarde los cambios. Por ejemplo, recorte la imagen y guárdela. También puede elegir anotar o publicar el recurso.

1. Seleccione el recurso editado en el [!DNL Assets] y haga clic en **[!UICONTROL Proteger]** en la barra de herramientas. El recurso modificado está registrado en [!DNL Assets] y está disponible para otros usuarios para su edición.

## Registro forzado {#forced-check-in}

Los administradores pueden proteger los recursos que han extraído otros usuarios.

1. Inicie sesión en [!DNL Assets] como administrador.
1. En el [!DNL Assets] interfaz de usuario de seleccione uno o varios recursos que otros usuarios hayan extraído.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. En la barra de herramientas, haga clic en **[!UICONTROL Bloqueo de la versión]**. El recurso se vuelve a registrar y se puede editar para otros usuarios.

## Prácticas recomendadas y limitaciones {#tips-limitations}

* Es posible eliminar un *carpeta* que contiene archivos de recursos extraídos. Antes de eliminar una carpeta, asegúrese de que los usuarios no hayan extraído ningún recurso digital.

**Consulte también**

* [Traducir recursos](translate-assets.md)
* [API HTTP de Recursos](mac-api-assets.md)
* [Formatos de archivo compatibles con Assets](file-format-support.md)
* [Buscar recursos](search-assets.md)
* [Recursos conectados](use-assets-across-connected-assets-instances.md)
* [Informes de Asset](asset-reports.md)
* [Esquemas de metadatos](metadata-schemas.md)
* [Descarga de recursos](download-assets-from-aem.md)
* [Administración de metadatos](manage-metadata.md)
* [Facetas de búsqueda](search-facets.md)
* [Administrar colecciones](manage-collections.md)
* [Importación masiva de metadatos](metadata-import-export.md)

>[!MORELIKETHIS]
>
>* [Comprender la entrada y la salida [!DNL Experience Manager] aplicación de escritorio](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [Tutorial de vídeo para comprender cómo registrar y registrar [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

