---
title: Volver a conectar con Microsoft Translator
description: Obtenga información sobre cómo conectar AEM a Microsoft Translator de forma predeterminada para automatizar el flujo de trabajo de traducción.
feature: Language Copy
role: Admin
exl-id: ca3c50f9-005e-4871-8606-0cfd3ed21936
source-git-commit: 04054e04d24b5dde093ed3f14ca5987aa11f5b0e
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 4%

---

# Volver a conectar con Microsoft Translator {#connecting-to-microsoft-translator}

Cree una configuración para el [Traductor de Microsoft](https://hub.microsofttranslator.com) servicio en la nube para usar su cuenta de Microsoft Translation para traducir AEM contenido o recursos de la página.

>[!TIP]
>
>Si es nuevo en traducir contenido, consulte nuestra [Recorrido de traducción de sitios,](/help/journey-sites/translation/overview.md) que es una ruta guiada a través de la traducción del contenido de AEM Sites mediante las poderosas herramientas de traducción de AEM, ideal para aquellos que no tengan experiencia de traducción ni AEM.

>[!NOTE]
>
>AEM proporciona una cuenta de traducción de Microsoft de prueba que permite un máximo de 2 000 000 caracteres traducidos gratuitos al mes. Para obtener una suscripción de cuenta adecuada para los sistemas de producción, consulte [Actualización De La Configuración De Licencias De Prueba De Microsoft Translator](#upgrading-the-microsoft-translator-trial-license-configuration).

| Propiedad | Descripción |
|---|---|
| Etiqueta de traducción | El nombre para mostrar del servicio de traducción |
| Atribución de traducción | (Opcional) Para el contenido generado por el usuario, la atribución que aparece junto al texto traducido, por ejemplo `Translations by Microsoft` |
| ID del espacio de trabajo | (Opcional) El ID del motor de traducción personalizado de Microsoft que debe utilizar |
| Clave de suscripción | La clave de suscripción de Microsoft para Microsoft Translator |

Después de crear la configuración, debe [actívelo](#activating-the-translator-service-configurations).

El siguiente procedimiento crea una configuración de Microsoft Translator.

1. En el [panel de navegación,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) toque o haga clic en **Herramientas** -> **Cloud Services** -> **Cloud Services de traducción**.
1. Vaya a donde desea crear la configuración. Normalmente, esto se encuentra en la raíz del sitio o puede ser una configuración global predeterminada.
1. Toque o haga clic en el botón **Crear** botón.
1. Defina la configuración.
   1. Select **Traductor de Microsoft** en la lista desplegable .
   1. Escriba un título para la configuración. El título identifica la configuración en la consola Cloud Services, así como en las listas desplegables de propiedades de página.
   1. Opcionalmente, escriba un nombre para usar para el nodo del repositorio que almacena la configuración.

   ![Crear configuración de traducción](../assets/create-translation-config.png)

1. Haga clic en **Crear**.
1. En el **Editar configuración** , proporcione los valores para el servicio de traducción descrito en la tabla anterior.

   ![Editar configuración de traducción](../assets/edit-translation-config.png)

1. Toque o haga clic **Connect** para verificar la conexión.
1. Haga clic o pulse en **Guardar y cerrar**.

## Actualización De La Configuración De Licencias De Prueba De Microsoft Translator {#upgrading-the-microsoft-translator-trial-license-configuration}

Las páginas de configuración de traducción de Microsoft proporcionan un práctico vínculo al sitio web de Microsoft para obtener una suscripción de cuenta adecuada para los sistemas de producción.

1. En el [panel de navegación,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) toque o haga clic **Herramientas** -> **Cloud Services** -> **Cloud Services de traducción**.
1. Toque o haga clic en la configuración de Microsoft Translator existente.
1. Toque o haga clic **Editar**.
1. En el **Editar configuración** ventana, toque o haga clic **Actualizar suscripción**. Se abre una página web de Microsoft con más detalles sobre el servicio.

## Personalización del motor de traducción de Microsoft {#customizing-your-microsoft-translator-engine}

Las páginas de configuración de traducción de Microsoft proporcionan un práctico vínculo al sitio web de Microsoft para personalizar el motor de traducción de Microsoft.

1. En el [panel de navegación,](/help/sites-cloud/authoring/getting-started/basic-handling.md#first-steps) toque o haga clic **Herramientas** -> **Cloud Services** -> **Cloud Services de traducción**.
1. Toque o haga clic en la configuración de Microsoft Translator existente.
1. Toque o haga clic **Editar**.
1. En el **Editar configuración** ventana, toque o haga clic **Personalizar traductor**. Utilice la página web de Microsoft que se abre para personalizar el servicio.

## Activación de las configuraciones del servicio de traducción {#activating-the-translator-service-configurations}

Debe activar las configuraciones del servicio en la nube para que admitan el contenido traducido que se replica en la instancia de publicación. Utilice el método de [publicación de un árbol](/help/sites-cloud/authoring/fundamentals/publishing-pages.md#publishing-and-unpublishing-a-tree) para activar los nodos del repositorio que almacenan las configuraciones de Microsoft Translator. Los nodos se encuentran debajo de los siguientes nodos principales:

* `/libs/settings/cloudconfigs/translation/msft-translation`
