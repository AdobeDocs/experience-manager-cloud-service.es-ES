---
title: Publicación de páginas con activos DAM mediante Edge Delivery Services
description: Descubra qué configuración es necesaria para garantizar que los activos DAM de sus páginas se publiquen sin problemas en Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 160f0474-a72d-4183-a2b2-2f8ba177605d
index: false
hide: true
hidefromtoc: true
source-git-commit: 17c14a78c2cfa262e25c6196fa73c6c4b17e200a
workflow-type: ht
source-wordcount: '433'
ht-degree: 100%

---

# Publicación de páginas con activos DAM mediante Edge Delivery Services {#dam-assets}

Descubra qué configuración es necesaria para garantizar que los activos DAM de sus páginas se publiquen sin problemas en Edge Delivery Services.

## Editor universal, activos DAM y Edge Delivery {#overview}

Al editar contenido para el editor universal, por supuesto, puede seleccionar activos de DAM. Al publicar el contenido en Edge Delivery Services, también se publica el contenido de DAM relacionado.

Para garantizar este comportamiento sin problemas, AEM y Edge Delivery Services deben tener acceso adecuado a DAM para poder publicar. Esto incluye lo siguiente:

* [Garantizar que las carpetas de recursos sean accesibles](#accessible).
* [Comprobar que la carpeta de recursos tenga asignada la configuración adecuada (según sea necesario)](#configuration).

## Garantizar que las carpetas de recursos sean accesibles {#accessible}

Al publicar páginas de AEM en Edge Delivery Services, se usa [una cuenta técnica](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md). Esta cuenta, con el nombre del formato `<hash>@techacct.adobe.com`, se crea automáticamente como usuario en AEM mediante Cloud Manager, cada vez que publique por primera vez una página creada con el editor universal.

![Cuenta técnica](/help/edge/wysiwyg-authoring/assets/dam-assets/technical-account.png)

Esta cuenta técnica debe tener derechos de acceso a todas las carpetas DAM para publicar su contenido. Puede realizar una de las acciones siguientes:

* No utilizar carpetas DAM privadas.
* Conceda al usuario de la cuenta técnica acceso a las carpetas de DAM.

## Garantizar que la carpeta de recursos tenga la configuración adecuada {#configuration}

Normalmente, garantizar que su cuenta técnica tenga acceso a sus recursos en DAM es suficiente para publicar sus recursos junto con las páginas en Edge Delivery Services.

Sin embargo, se necesita una configuración adicional en dos casos adicionales:

* Si desea publicar páginas con recursos que no sean imágenes, como PDF o vídeos, en Edge Delivery Services.
* Si desea publicar recursos de imagen en Edge Delivery Services independientemente de las páginas.

Para admitir ambos casos de uso, se debe asignar una [configuración](/help/implementing/developing/introduction/configurations.md) a la carpeta DAM.

1. Inicie sesión en el entorno de creación de AEM.
1. En **Sites**, seleccione el sitio en el que va a publicar los recursos o el sitio con el que se asociarán los recursos.
1. Pulse o haga clic en **Editar** en la barra de herramientas.
1. En la pestaña **Avanzado** de la ventana de propiedades, anote la configuración en el campo **Configuración de nube**.
   * Esto se crea automáticamente al crear el sitio con el formato `/conf/<site-name>`.
1. Pulse o haga clic en **Cancelar** en la ventana de propiedades, navegue hasta **Activos** -> **Archivos** y seleccione la carpeta DAM.
1. Pulse o haga clic en **Propiedades** en la barra de herramientas.
1. En la pestaña **Cloud Services** de la ventana de propiedades, en el campo **Configuración de nube**, seleccione la misma configuración que anotó anteriormente.
1. Haga clic o pulse en **Guardar y cerrar**.
