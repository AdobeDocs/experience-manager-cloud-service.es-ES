---
title: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
description: Notas de la versión [!DNL Workfront for Experience Manager enhanced connector]
exl-id: 12de589d-fe5d-4bd6-b96b-48ec8f1ebcb6
source-git-commit: d763bacb0844a438ebea6ef206dfa184a49993fe
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 3%

---

# Notas de la versión [!DNL Workfront for Experience Manager enhanced connector] {#release-notes-enhanced-connector-workfront}

En la siguiente sección se describen las notas de la versión generales de [!DNL Workfront for Experience Manager enhanced connector].

## Fecha de la versión {#release-date}

La fecha de la versión de la última versión 1.9.1 de [!DNL Workfront for Experience Manager enhanced connector] es 1 de julio de 2022.

## Elementos destacados de la versión {#release-highlights}

La última versión de [!DNL Workfront for Experience Manager enhanced connector] incluye las siguientes mejoras y correcciones de errores:

* Se ha agregado compatibilidad con la autenticación entre aplicaciones de Workfront y Experience Manager mediante la clave de API de Workfront para instancias migradas a Adobe IMS.

* Cuando se vinculan archivos o carpetas externos, la aplicación Workfront muestra la variable `SERVER_ERROR` mensaje de error. El mensaje de error hace referencia a una excepción no autorizada debido a una falta de coincidencia en las claves de API.

* Cuando se ejecuta un flujo de trabajo Crear tarea para un recurso, la excepción de puntero nulo aparece en los mensajes de registro.

* Al habilitar la variable `Replace Spaces with DASH` en Configuración avanzada en Experience Manager, resulta en una creación de carpetas duplicadas en Workfront.

>[!IMPORTANT]
>
>Adobe recomienda que [actualizar a la última versión 1.9.1](../assets/update-workfront-enhanced-connector.md) del [!DNL Workfront for Experience Manager enhanced connector].

## Problemas conocidos {#known-issues}

* Al configurar carpetas de proyecto vinculadas con AEM 6.4, el Experience Manager no guarda los valores de **[!UICONTROL subcarpetas]** y **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]** campos. El valor de la variable **[!UICONTROL subcarpetas]** actualizaciones de campo a **[!UICONTROL undefined]** y el valor de la variable **[!UICONTROL Crear carpeta vinculada en proyectos con portafolio]** actualizaciones de campo a **[!UICONTROL Portfolio predeterminado]** automáticamente después de guardar la configuración.

* Cuando utiliza la experiencia clásica de Workfront, la variable **[!UICONTROL Enviar a]** en la **[!UICONTROL Más]** la lista desplegable no permite seleccionar el destino de destino dentro de Experience Manager. La variable **[!UICONTROL Enviar a]** funciona correctamente con la opción **[!UICONTROL Acciones de documento]** lista desplegable. La variable **[!UICONTROL Enviar a]** funciona correctamente para **[!UICONTROL Más]** lista desplegable así como el **[!UICONTROL Acciones de documento]** lista desplegable disponible en la nueva experiencia de Workfront.

## Versiones anteriores {#previous-releases}

### Versión de junio de 2022 {#june-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ahora incluye las siguientes actualizaciones:

* Al cargar a través de una carpeta vinculada o usar la variable `Send To` acción disponible en Workfront para cargar recursos a Experience Manager as a Cloud Service, los recursos se dañan y no se pueden abrir en Adobe Photoshop.

### Versión de marzo de 2022 {#march-2022-release}

[!DNL Workfront for Experience Manager enhanced connector] ahora incluye las siguientes actualizaciones:

* Ahora puede crear carpetas vinculadas entre Adobe Workfront y AEM Assets as a Cloud Service incluso si hay varias configuraciones de carpeta vinculadas al proyecto.

* Se ha agregado compatibilidad con la paginación de suscripción de eventos.

* Se ha agregado compatibilidad con AEM 6.4.x.

* Se ha agregado compatibilidad con entornos proxy.

* Varias correcciones de errores basadas en los comentarios de socios y clientes.

>[!MORELIKETHIS]
>
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/assets/integrations/workfront-integrations.html?lang=en)
>* [Integrar [!DNL Workfront for Experience Manager enhanced connector] con Experience Manager 6.4](https://experienceleague.adobe.com/docs/experience-manager-64/assets/integrations/workfront-integrations.html?lang=en)

