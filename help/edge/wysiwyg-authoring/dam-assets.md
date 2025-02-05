---
title: Publicación de páginas con DAM Assets mediante Edge Delivery Services
description: Descubra qué configuración es necesaria para garantizar que los recursos DAM para sus páginas se publiquen sin problemas para los Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 160f0474-a72d-4183-a2b2-2f8ba177605d
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 2%

---

# Publicación de páginas con DAM Assets mediante Edge Delivery Services {#dam-assets}

Descubra qué configuración es necesaria para garantizar que los recursos DAM para sus páginas se publiquen sin problemas para los Edge Delivery Services.

## Universal Editor, DAM Assets y Edge Delivery {#overview}

Al editar contenido para el editor universal, por supuesto, puede seleccionar recursos de DAM. Al publicar el contenido en Edge Delivery Services, también se publica el contenido DAM relacionado.

AEM Para garantizar este comportamiento sin problemas, los Edge Delivery Services y los deben tener acceso adecuado a DAM para poder publicar. Esto incluye:

* [Garantizando que las carpetas de recursos sean accesibles](#accessible).
* [Comprobando que la carpeta de recursos tenga asignada la configuración adecuada (según sea necesario)](#configuration).

## Garantizar que las carpetas de Assets sean accesibles {#accessible}

AEM Al publicar páginas desde la publicación de la página a los Edge Delivery Services, se utiliza [una cuenta técnica](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md). AEM Esta cuenta, con un nombre con el formato `<hash>@techacct.adobe.com`, se crea automáticamente como usuario en la que se crea la cuenta de Cloud Manager cada vez que se publica por primera vez una página creada con el Editor universal.

![Cuenta técnica](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

Esta cuenta técnica debe tener derechos de acceso a todas las carpetas DAM para publicar su contenido. Puede:

* No utilice carpetas DAM privadas.
* Conceda al usuario de la cuenta técnica acceso a las carpetas de DAM.

## Garantizar que la carpeta de Assets tenga la configuración adecuada {#configuration}

Normalmente, garantizar que su cuenta técnica tenga acceso a sus recursos en DAM es suficiente para publicar sus recursos junto con sus páginas en los Edge Delivery Services.

Sin embargo, se necesita una configuración adicional en dos casos adicionales:

* Si desea publicar páginas con recursos que no sean imágenes, como PDF o vídeos, en Edge Delivery Services.
* Si desea publicar recursos de imagen en Edge Delivery Services independientemente de las páginas.

Para admitir ambos casos de uso, se debe asignar una [configuración](/help/implementing/developing/introduction/configurations.md) a la carpeta DAM.

1. AEM Inicie sesión en el entorno de creación de la.
1. En **Sitios**, seleccione el sitio en el que va a publicar los recursos o el sitio con el que se asociarán los recursos.
1. Pulse o haga clic en **Propiedades** en la barra de herramientas.
1. En la ficha **Avanzado** de la ventana de propiedades, anote la configuración en el campo **Configuración de nube**.
   * Esto se crea automáticamente al crear el sitio con el formato `/conf/<site-name>`.
1. Pulse o haga clic en **Cancelar** en la ventana de propiedades, navegue hasta **Assets** -> **Archivos** y seleccione la carpeta DAM.
1. Pulse o haga clic en **Propiedades** en la barra de herramientas.
1. En la ficha **Cloud Service** de la ventana de propiedades, en el campo **Configuración de nube**, seleccione la misma configuración que anotó anteriormente.
1. Haga clic o pulse en **Guardar y cerrar**.
