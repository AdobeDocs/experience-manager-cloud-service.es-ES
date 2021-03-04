---
title: Conexión a Microsoft Translator
description: Obtenga información sobre cómo conectar AEM a Microsoft Translator de forma predeterminada para automatizar el flujo de trabajo de traducción.
translation-type: tm+mt
source-git-commit: 5902e026c47aac0c1ea62a2b74be6109b216fb74
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 2%

---


# Conexión a Microsoft Translator {#connecting-to-microsoft-translator}

Cree una configuración para el servicio en la nube [Microsoft Translator](https://hub.microsofttranslator.com) para utilizar su cuenta de Microsoft Translation para traducir contenido o recursos de páginas de AEM.

>[!NOTE]
>
>AEM proporciona una cuenta de Microsoft Translation de prueba que permite un máximo de 2 000 000 caracteres traducidos gratuitos al mes. Para obtener una suscripción de cuenta adecuada para los sistemas de producción, consulte [Actualización de la configuración de la licencia de prueba del traductor de Microsoft](#upgrading-the-microsoft-translator-trial-license-configuration).

| Propiedad | Descripción |
|---|---|
| Etiqueta de traducción | El nombre para mostrar del servicio de traducción |
| Atribución de traducción | (Opcional) Para el contenido generado por el usuario, la atribución que aparece junto al texto traducido, por ejemplo `Translations by Microsoft` |
| ID del espacio de trabajo | (Opcional) El ID del motor de Microsoft Translator personalizado para usar |
| Clave de suscripción | La clave de suscripción de Microsoft para Microsoft Translator |

Después de crear la configuración, debe [activarla](#activating-the-translator-service-configurations).

El siguiente procedimiento crea una configuración de Microsoft Translator.

1. En el panel de navegación [,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) toque o haga clic en **Herramientas** -> **Cloud Services** -> **Servicios de nube de traducción**.
1. Vaya a donde desea crear la configuración. Normalmente, esto se encuentra en la raíz del sitio o puede ser una configuración global predeterminada.
1. Toque o haga clic en el botón **Create**.
1. Defina la configuración.
   1. Seleccione **Microsoft Translator** en la lista desplegable.
   1. Escriba un título para la configuración. El título identifica la configuración en la consola de Cloud Services, así como en las listas desplegables de propiedades de página.
   1. Opcionalmente, escriba un nombre para usar para el nodo del repositorio que almacena la configuración.

   ![Crear configuración de traducción](../assets/create-translation-config.png)

1. Haga clic en **Crear**.
1. En la ventana **Edit Configuration**, proporcione los valores para el servicio de traducción descrito en la tabla anterior.

   ![Editar configuración de traducción](../assets/edit-translation-config.png)

1. Toque o haga clic en **Connect** para verificar la conexión.
1. Toque o haga clic en **Guardar y cerrar**.

## Actualización de la configuración de licencia de prueba de Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Las páginas de configuración de Microsoft Translation proporcionan un práctico vínculo al sitio web de Microsoft para obtener una suscripción de cuenta adecuada para los sistemas de producción.

1. En el panel de navegación [,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) toque o haga clic en **Herramientas** -> **Cloud Services** -> **Servicios de nube de traducción**.
1. Toque o haga clic en la configuración existente de Microsoft Translator.
1. Toque o haga clic en **Editar**.
1. En la ventana **Editar configuración**, pulse o haga clic en **Actualizar suscripción**. Se abre una página web de Microsoft con más detalles sobre el servicio.

## Personalización del motor de traducción de Microsoft {#customizing-your-microsoft-translator-engine}

Las páginas de configuración de Microsoft Translation proporcionan un práctico vínculo al sitio web de Microsoft para personalizar el motor de Microsoft Translator.

1. En el panel de navegación [,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) toque o haga clic en **Herramientas** -> **Cloud Services** -> **Servicios de nube de traducción**.
1. Toque o haga clic en la configuración existente de Microsoft Translator.
1. Toque o haga clic en **Editar**.
1. En la ventana **Editar configuración**, pulse o haga clic en **Personalizar traductor**. Utilice la página web de Microsoft que se abre para personalizar el servicio.

## Activación de las configuraciones del servicio de traducción {#activating-the-translator-service-configurations}

Debe activar las configuraciones del servicio en la nube para que admitan el contenido traducido que se replica en la instancia de publicación. Utilice el método de [publicación de un árbol](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree) para activar los nodos del repositorio que almacenan las configuraciones de Microsoft Translator. Los nodos se encuentran debajo de los siguientes nodos principales:

* `/libs/settings/cloudconfigs/translation/msft-translation`
