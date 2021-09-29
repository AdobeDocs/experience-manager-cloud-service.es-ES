---
title: Configuración del marco de integración de traducción
description: Aprenda a configurar el marco de integración de traducción para integrarlo con servicios de traducción de terceros.
feature: Language Copy
role: Admin
exl-id: 6e74cdee-7965-4087-a733-e9d81c4aa7c2
source-git-commit: 917f5790fb36fd1560ba43c67f8072616b605894
workflow-type: tm+mt
source-wordcount: '1419'
ht-degree: 2%

---

# Configuración del marco de integración de traducción {#configuring-the-translation-integration-framework}

El marco de integración de traducción se integra con los servicios de traducción de terceros para organizar la traducción de AEM contenido. Requiere tres pasos básicos.

1. [Conéctese a su proveedor de servicios de traducción.](#connecting-to-a-translation-service-provider)
1. [Cree una configuración del marco de integración de traducción.](#creating-a-translation-integration-configuration)
1. [Asocie las configuraciones de nube con sus páginas.](#configuring-pages-for-translation)

Para obtener una descripción general de las funciones de traducción de contenido de AEM, consulte [Traducción de contenido para sitios multilingües](overview.md).

>[!TIP]
>
>Si es nuevo en traducir contenido, consulte nuestro [Recorrido de traducción de sitios,](/help/journey-sites/translation/overview.md) que es la ruta guiada a través de la traducción del contenido de AEM Sites mediante las poderosas herramientas de traducción de AEM, ideal para aquellos que no tengan experiencia de traducción o AEM.

## Conexión a un proveedor de servicios de traducción {#connecting-to-a-translation-service-provider}

Cree una configuración de nube que se conecte AEM con su proveedor de servicios de traducción. AEM incluye la capacidad de [conectarse a Microsoft Translator](connect-ms-translator.md) de forma predeterminada.

Los siguientes proveedores de traducción proporcionan una implementación de la API de AEM para proyectos de traducción.

* [Microsoft Translator](connect-ms-translator.md)
* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html)  (Adobe Exchange Premier Partner)
* [Tecnologías para tableta de arcilla](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Palabras clave](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM Cloud](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [Smartling](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [SDL](https://exchange.adobe.com/experiencecloud.details.100110.sdl-translation-management.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)

Después de instalar un paquete de conector, puede crear una configuración de nube para el conector. Normalmente, debe proporcionar sus credenciales para autenticarse con el servicio de traducción. Para obtener información sobre cómo agregar una configuración de nube para el conector de Microsoft Translator, consulte [Integración con Microsoft Translator](connect-ms-translator.md).

Si es necesario, puede crear varias configuraciones de nube para el mismo conector. Por ejemplo, cree una configuración para cada una de las cuentas o proyectos que tenga con el mismo proveedor.

Después de configurar una conexión, puede crear la configuración del marco de integración de traducción que la utiliza.

## Creación de una configuración de integración de traducción {#creating-a-translation-integration-configuration}

Cree una configuración del marco de integración de traducción para especificar cómo traducir el contenido. La configuración incluye la siguiente información:

* Qué proveedor de servicios de traducción utilizar
* Si se va a realizar una traducción humana o automática
* Traducción de otro contenido asociado con una página o un recurso, como etiquetas

Después de crear una configuración de marco, asocia la configuración de nube con las páginas que desea traducir según la configuración. Cuando se inicia el proceso de traducción, el flujo de trabajo de traducción se ejecuta según la configuración del marco asociada.

Cuando diferentes secciones del sitio web tengan diferentes requisitos de traducción, cree varias configuraciones de marco según corresponda. Por ejemplo, un sitio web multilingüe puede incluir copias en inglés, español y japonés. El propietario del sitio utiliza dos proveedores de servicios de traducción diferentes para las traducciones al español y al japonés. Por lo tanto, se configuran dos configuraciones del marco. Cada configuración utiliza un proveedor de servicios de traducción diferente.

Después de configurar un marco de integración de traducción, puede [asociarlo a las páginas](preparation.md) que lo utilizan.

>[!TIP]
>
>Para obtener una descripción general de las funciones de traducción de contenido de AEM, consulte [Traducción de contenido para sitios multilingües](overview.md).

Una sola configuración del marco controla cómo traducir el contenido de la página y los recursos.

![Configuración de traducción](../assets/translation-configuration.png)

Para crear una nueva configuración de traducción:

1. En el [menú de navegación global,](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) toque o haga clic en **Herramientas -> Cloud Services -&amp; Cloud Services de traducción**.
1. Desplácese hasta donde desee crear la configuración en la estructura de contenido. A menudo se basa en un sitio en particular o puede ser global.
1. Proporcione la siguiente información en los campos y, a continuación, toque o haga clic en **Crear**:
   1. Seleccione **Tipo de configuración** en la lista desplegable.
   1. Introduzca un **Título** para la configuración. El **Título** identifica la configuración en la consola **Cloud Services**, así como en las listas desplegables de propiedades de página.
   1. Opcionalmente, escriba un **Nombre** para utilizarlo para el nodo del repositorio que almacena la configuración.
1. En la ventana **Editar configuración**, configure las propiedades en las pestañas **Sitios** y **Recursos** y, a continuación, haga clic o pulse **Guardar y cerrar**.

### Propiedades de configuración de sitios {#sites-configuration-properties}

La pestaña **Sites** controla cómo se realiza la traducción del contenido de la página.

| Propiedad | Descripción |
|---|---|
| Flujo de trabajo de traducción | Esta propiedad define el método de traducción que realiza el marco para el contenido del sitio:<br>- Traducción automática: El proveedor de traducción realiza la traducción mediante traducción automática en tiempo real.<br>- Traducción humana: El contenido se envía al proveedor de traducción para que lo traduzcan los traductores.<br>- No Traducir: El contenido no se envía para su traducción. Esto sirve para omitir ciertas ramas de contenido que no se traducirían, pero que podrían actualizarse con el contenido más reciente. |
| Proveedor de traducciones | Esta propiedad define el proveedor de traducción para realizar la traducción. Cuando se instala su conector correspondiente, aparece un proveedor en la lista. |
| Categoría de contenido | (Solo traducción automática) Esta propiedad es una categoría que describe el contenido que está traduciendo. La categoría puede afectar a la elección de terminología y frases al traducir contenido. |
| Traducir etiquetas | Esta opción permite traducir las etiquetas asociadas con la página. |
| Traducir recursos de la página | Esta propiedad define cómo traducir recursos que se agregan a componentes del sistema de archivos o a los que se hace referencia desde recursos:<br>- No traducir: Los recursos de página no se traducen.<br>- Uso del flujo de trabajo de traducción de sitios: Los recursos se gestionan según las propiedades de configuración de la  **** pestaña Sitio .<br>- Uso del flujo de trabajo de traducción de recursos: Los recursos se gestionan según las propiedades configuradas en la  **** pestaña Recursos. |
| Ejecución automática de la traducción | Active esta propiedad para ejecutar los trabajos de traducción automáticamente después de crear los proyectos de traducción. No tiene la oportunidad de revisar y ampliar el ámbito del trabajo de traducción cuando selecciona esta opción. |

### Propiedades de configuración de recursos {#assets-configuration-properties}

Las propiedades de recursos controlan cómo configurar los recursos. Para obtener más información sobre la traducción de recursos, consulte [Creación de copias de idioma para recursos](/help/assets/translate-assets.md).

| Propiedad | Descripción |
|---|---|
| Flujo de trabajo de traducción | Esta propiedad selecciona el tipo de traducción que realiza el marco para los recursos:<br>- Traducción automática: El proveedor de traducción realiza la traducción inmediatamente mediante traducción automática.<br>- Traducción humana: El contenido se envía automáticamente al proveedor de traducción para que se traduzca manualmente.<br>-No Traducir: Los recursos no se envían para su traducción. |
| Proveedor de traducciones | Esta propiedad define el proveedor de traducción para realizar la traducción. Cuando se instala su conector correspondiente, aparece un proveedor en la lista. |
| Categoría de contenido | (Solo traducción automática) Esta propiedad describe el contenido que está traduciendo. La categoría puede afectar a la elección de terminología y frases al traducir contenido. |
| Traducir recursos | Active esta propiedad para incluir recursos en el proyecto de traducción. |
| Traducir metadatos | Active esta propiedad para traducir metadatos de recursos. |
| Traducir etiquetas | Active esta propiedad para traducir las etiquetas asociadas al recurso. |
| Ejecución automática de la traducción | Seleccione esta propiedad para ejecutar los trabajos de traducción automáticamente después de crear los proyectos de traducción. No tiene la oportunidad de revisar o ampliar el ámbito del trabajo de traducción cuando selecciona esta opción. |

## Configuración de páginas para traducción {#configuring-pages-for-translation}

Para configurar la traducción de las páginas de origen a otros idiomas, asocie las páginas con las siguientes configuraciones de nube:

* La configuración de nube que se conecta AEM con su proveedor de traducción.
* Marco de integración de traducción que configura los detalles de la traducción.

Tenga en cuenta que la configuración de nube del marco de integración de traducción identifica la configuración de nube que se utilizará para la conexión con el proveedor de servicios. Cuando asocia una página de origen con una configuración de nube de marco, la página debe asociarse a la configuración de nube del proveedor de servicios que utiliza la configuración de nube de marco.

Cuando asocia una página con una configuración de nube, los descendientes de la página heredan la asociación. Por ejemplo, si asocia la página `/content/wknd/language-masters/en/magazine` con un marco de integración de traducción, la página `magazine` y las páginas secundarias debajo de él se traducen según el marco.

Si es necesario, puede anular la asociación en una página descendiente. Por ejemplo, el contenido de un sitio web se refiere principalmente a viajes y estilo de vida. Sin embargo, una rama de páginas describe la empresa. En tal caso, la página raíz del sitio puede asociarse con un marco de integración de traducción que especifique la traducción automática mediante la categoría Estilo de vida, mientras que la rama que describe la empresa utilizará un marco que realice la traducción automática mediante la categoría General .

### Asociación de una página con un proveedor de traducción {#associating-a-page-with-a-translation-provider}

Asocie una página al proveedor de traducción que esté utilizando para traducir la página y las páginas descendientes.

1. En la consola Sitios, seleccione la página que desea configurar y toque o haga clic en **Ver propiedades**.
1. Toque o haga clic en la pestaña **Cloud Services**.
1. En la lista desplegable **Add Configuration**, seleccione la configuración.
1. Toque o haga clic en **Guardar y cerrar**.

### Asociación de páginas a un marco de integración de traducción {#associating-pages-with-a-translation-integration-framework}

Asocie una página al marco de integración de traducción que define cómo desea realizar la traducción de la página y de las páginas descendientes.

1. En la consola Sitios, seleccione la página que desea configurar y toque o haga clic en **Ver propiedades**.
1. Toque o haga clic en la pestaña **Cloud Services**.
1. En la lista desplegable **Add Configuration**, seleccione la configuración.
1. Toque o haga clic en **Guardar y cerrar**.
