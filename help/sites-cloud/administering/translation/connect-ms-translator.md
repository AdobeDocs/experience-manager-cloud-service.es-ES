---
title: Volver a conectar con Microsoft Translator
description: Obtenga información sobre cómo conectar AEM a Microsoft Translator de forma predeterminada para automatizar el flujo de trabajo de traducción.
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
solution: Experience Manager Sites
source-git-commit: 2314ad30ea31b49d832ce0fdf729420e0ee70e0c
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 65%

---

# Volver a conectar con Microsoft Translator {#connecting-to-microsoft-translator}

AEM un conector integrado para [Microsoft Translator](https://www.microsoft.com/es-es/translator/business/) para traducir contenido o recursos de la página. Después de obtener una licencia de Microsoft para utilizar Microsoft Translator, configure el conector siguiendo las instrucciones de esta página.

>[!TIP]
>
>Si acaba de empezar a traducir contenido, consulte el [Recorrido de traducción de Sites,](/help/journey-sites/translation/overview.md) que es una ruta guiada a través de la traducción del contenido de AEM Sites mediante las poderosas herramientas de traducción de AEM, ideal para aquellos que no tengan experiencia con la traducción o con AEM.

| Propiedad | Descripción |
|---|---|
| Etiqueta de traducción | El nombre para mostrar del servicio de traducción |
| Atribución de traducción | (Opcional) Para el contenido generado por el usuario, la atribución que aparece junto al texto traducido, por ejemplo, `Translations by Microsoft` |
| ID del espacio de trabajo | (Opcional) El ID del motor personalizado de Microsoft Translator que debe utilizar |
| Clave de suscripción | La clave de suscripción de Microsoft para Microsoft Translator |

El siguiente procedimiento crea una configuración de Microsoft Translator.

1. En el panel de navegación [seleccione ](/help/sites-cloud/authoring/basic-handling.md#first-steps) **Herramientas** > **Cloud Service** > **Cloud Service de traducción**.
1. Desplácese hasta donde desee crear la configuración. Normalmente, se encuentra en la raíz del sitio o puede ser una configuración global predeterminada.
1. Seleccione el botón **Crear**.
1. Defina la configuración.
   1. Seleccione **Microsoft Translator** en la lista desplegable.
   1. Escriba un título para la configuración. El título identifica la configuración en la consola Cloud Services y en las listas desplegables de propiedades de página.
   1. De forma opcional, escriba un nombre para usar para el nodo del repositorio que almacena la configuración.

   ![Creación de configuración de traducción](../assets/create-translation-config.png)

1. Haga clic en **Crear**.
1. En la ventana **Editar configuración**, proporcione los valores para el servicio de traducción descrito en la tabla anterior.

   ![Edición de la configuración de traducción](../assets/msft-config-ui.png)

1. Seleccione **Conectar** para verificar la conexión.
1. Seleccione **Guardar y cerrar**.

## Publicación de las configuraciones del servicio de traducción {#publishing-the-translator-service-configurations}

Como último paso, publique las configuraciones de Microsoft Translator para que admitan el contenido traducido publicado, mediante la acción [publicar un árbol](/help/sites-cloud/authoring/sites-console/publishing-pages.md#publishing-and-unpublishing-a-tree).
