---
title: Habilitar la alternancia de funciones para integrar las funciones de pionero y prelanzamiento
description: La alternancia de funciones es una funcionalidad de AEM que permite a los administradores habilitar nuevas funciones en un entorno de tiempo de ejecución.
feature: Adaptive Forms, Foundation Components, Core Components
role: User, Developer
exl-id: 3ad1370a-a399-4fbe-8168-c3a1cee06336
source-git-commit: c1d62f0dd5a25da7fbeef537e1c28fa8421f42cd
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 8%

---

# Habilitar la alternancia de funciones en el kit de desarrollo de software de Adobe Experience (SDK de AEM)

La alternancia de funciones en AEM permite a los administradores habilitar o deshabilitar funciones en tiempo de ejecución, lo que resulta ideal para administrar las funciones de la versión preliminar y de la versión preliminar sin cambios en el código. Admite despliegues graduales, pruebas A/B y la desactivación rápida de funciones inestables.

Este artículo explica cómo habilitar las alternancias de funciones en la configuración local de SDK en AEM, que simula AEM as a Cloud Service con SDK y Dispatcher. Esta configuración ayuda a los equipos a realizar pruebas en un entorno de producción antes de implementarlas en la nube.

## ¿Por qué utilizar las alternancias de funciones en una configuración de AEM SDK?

Al trabajar en una configuración de AEM SDK, la función activa o desactiva la ayuda en:

* Prueba de características experimentales de forma segura.

* Despliegue de nuevos componentes por fases.

* Mantener un único código base en varios entornos.

* Reducción del riesgo durante las implementaciones y actualizaciones.

## Requisitos previos

Antes de habilitar los alternadores de funciones en la configuración de AEM SDK, asegúrese de lo siguiente:

* El usuario es miembro del grupo `forms-users`.

* Vaya a `http://<author-instance-url>:portnumber/system/console/bundles` y compruebe si el paquete **(com.adobe.granite.toggle.impl.dev-1.1.2.jar)** está presente o no. En caso de que no esté presente, [descargue el paquete desde el vínculo](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]s/cq650/hotfix/com.adobe.granite.toggle.impl.dev-1.1.8.jar).

  ![Alternar característica](/help/forms/assets/aem-web-console-bundle.png)

### Activar conmutador de función

Siga estos pasos para habilitar los toggles de características en la instancia de AEM SDK:

1. Inicie sesión en la instancia de AEM Forms.

1. Navegue hasta `http://author-instance-url:portnumber/system/console/configMgr`.

1. Busque Proveedor de alternancia dinámica de Adobe Granite en el Administrador de configuración.

   ![Alternar característica](/help/forms/assets/aem-web-console-confi.png)

1. Haga clic en el icono ✏️
1. En la sección Conmutadores habilitados, haga clic en ➕ .
1. Añada el ID de alternancia de función para la función como se muestra en la siguiente imagen.
   ![Alternar característica](/help/forms/assets/feature-toggle.png)

1. Haga clic en Guardar

>[!NOTE]
>
> Puede encontrar el ID de alternancia de funciones en el documento específico de las funciones que adoptaron por primera vez.


### Deshabilitar alternancia de funciones

Para desactivar las opciones de características para aquellas características cuyas opciones están activadas, siga los pasos a continuación:

1. Inicie sesión en la instancia de AEM Forms.
1. Navegue hasta `http://author-instance-url:portnumber/system/console/configMgr`.
1. Busque Proveedor de alternancia dinámica de Adobe Granite en el Administrador de configuración.
1. Haga clic en el icono ✏️.
1. En la sección Conmutadores deshabilitados, haga clic en ➕.
1. Añada el número de conmutador para que la función se desactive.

   ![Alternar característica](/help/forms/assets/disable-toggle-feature.png)

### Consideración técnica

Los conmutadores de funciones se administran en tiempo de ejecución y son los más adecuados para configuraciones de desarrollo o prueba. En la configuración de AEM SDK, asegúrese de que las alternancias estén controladas por versiones y sincronizadas con CI/CD. Puede que sea necesario actualizar la página o borrar la caché para que se reflejen los cambios.

>[!NOTE]
>
> Para habilitar la opción de funciones para el entorno de producción, póngase en contacto con el equipo de asistencia de Adobe.
