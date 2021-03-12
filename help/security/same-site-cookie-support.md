---
title: Compatibilidad con cookies del mismo sitio para Adobe Experience Manager as a Cloud Service
description: Compatibilidad con cookies del mismo sitio para Adobe Experience Manager as a Cloud Service
translation-type: tm+mt
source-git-commit: 4f25aa54bd40644912e0e430a81f1a17d545e3f8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Compatibilidad con cookies del mismo sitio para Adobe Experience Manager como Cloud Service {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

Desde la versión 80, Chrome y posterior Safari, introdujeron un nuevo modelo para la seguridad de las cookies. Este modo está diseñado para introducir controles de seguridad en torno a la disponibilidad de cookies en sitios de terceros, a través de una configuración denominada `SameSite`. Para obtener información más detallada, consulte este [artículo](https://web.dev/samesite-cookies-explained/).

El valor predeterminado de esta configuración (`SameSite=Lax`) puede causar que la autenticación entre instancias o servicios de AEM no funcione. Esto se debe a que es posible que los dominios o las estructuras URL de estos servicios no entren dentro de las restricciones de esta directiva de cookies.

Para evitarlo, debe establecer el atributo de cookie SameSite en `None` para el token de inicio de sesión.

Para ello, siga los siguientes pasos:

1. Instale una versión de AEM SDK Quickstart localmente
1. Vaya a la consola web en `http://serveraddress:serverport/system/console/configMgr`
1. Busque y haga clic en **Adobe Granite Token Authentication Handler**
1. Establezca el atributo **SameSite para la cookie de token de inicio de sesión** en `None`, como se muestra en la imagen siguiente
   ![samesite](/help/security/assets/samesite1.png)
1. Haga clic en Guardar
1. Genere las configuraciones de formato JSON para esta configuración en particular siguiendo los pasos descritos en [Generación de configuraciones OSGi mediante el inicio rápido del SDK de AEM](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. Aplique la configuración siguiendo los pasos de la documentación de OSGi [Cloud Manager API Format for Setting Properties](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties).

Una vez que esta configuración se actualice y los usuarios cierren la sesión y vuelvan a iniciarla, las cookies `login-token` tendrán el atributo `None` establecido y se incluirán en las solicitudes entre sitios.