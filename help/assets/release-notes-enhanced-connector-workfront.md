---
title: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
description: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
source-git-commit: 02df53e47d2b8617c9a81f5c438814996af92340
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 5%

---


# Notas de la versión [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

En la siguiente sección se describen las notas de la versión generales de [!DNL Workfront for Experience Manager enhanced connector].

## Fecha de la versión {#release-date}

La fecha de la versión de la última versión de [!DNL Workfront for Experience Manager enhanced connector] es 28 de marzo de 2022.

## Elementos destacados de la versión {#release-highlights}

[!DNL Workfront for Experience Manager enhanced connector] ahora incluye las siguientes actualizaciones:

* Ahora puede crear carpetas vinculadas entre Adobe Workfront y AEM Assets as a Cloud Service incluso si hay varias configuraciones de carpeta vinculadas al proyecto.

* Se ha agregado compatibilidad con la paginación de suscripción de eventos.

* Se ha agregado compatibilidad con AEM 6.4.x.

* Se ha agregado compatibilidad con entornos proxy.

* Varias correcciones de errores basadas en los comentarios de socios y clientes.

## Problemas conocidos {#known-issues}

* Al configurar carpetas de proyecto vinculadas con AEM 6.4, el Experience Manager no guarda los valores de **[!UICONTROL subcarpetas]** y **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]** campos. El valor de la variable **[!UICONTROL subcarpetas]** actualizaciones de campo a **[!UICONTROL undefined]** y el valor de la variable **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]** actualizaciones de campo a **[!UICONTROL Portfolio predeterminado]** automáticamente después de guardar la configuración.

* Cuando utiliza la experiencia clásica de Workfront, la variable **[!UICONTROL Enviar a]** en la **[!UICONTROL Más]** la lista desplegable no permite seleccionar el destino de destino dentro de Experience Manager. La variable **[!UICONTROL Enviar a]** funciona correctamente con la opción **[!UICONTROL Acciones de documento]** lista desplegable. La variable **[!UICONTROL Enviar a]** funciona correctamente para **[!UICONTROL Más]** lista desplegable así como el **[!UICONTROL Acciones de documento]** lista desplegable disponible en la nueva experiencia de Workfront.

>[!MORELIKETHIS]
>
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)


