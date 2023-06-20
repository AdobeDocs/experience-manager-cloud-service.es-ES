---
title: Compatibilidad con cookies de SameSite para Adobe Experience Manager as a Cloud Service
description: Compatibilidad con cookies de SameSite para Adobe Experience Manager as a Cloud Service
exl-id: 2cec7202-4450-456f-8e62-b7ed3791505c
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 85%

---

# Compatibilidad con cookies de SameSite para Adobe Experience Manager as a Cloud Service {#same-site-cookie-support-for-adobe-experience-manager-as-a-cloud-service}

Desde la versión 80, Chrome y posterior Safari, introdujeron un nuevo modelo para la seguridad de las cookies. Este modo está diseñado para introducir controles de seguridad en torno a la disponibilidad de cookies en sitios de terceros, a través de una configuración denominada `SameSite`. Para obtener información más detallada, consulte este [artículo](https://web.dev/samesite-cookies-explained/).

El valor predeterminado de esta configuración (`SameSite=Lax`) puede causar que la autenticación entre instancias o servicios de AEM no funcione. Esto se debe a que es posible que los dominios o las estructuras URL de estos servicios no entren dentro de las restricciones de esta directiva de cookies.

Para evitarlo, debe establecer el atributo de cookie SameSite en `None` para el token de inicio de sesión.

>[!CAUTION]
>
>La configuración `SameSite=None` solo se aplica si el protocolo es seguro (HTTPS).
>
>Si el protocolo no es seguro (HTTP), la configuración se ignora y el servidor muestra este mensaje ADVERTENCIA:
>
>`WARN com.day.crx.security.token.TokenCookie Skip 'SameSite=None'`

Puede agregar la configuración siguiendo los pasos siguientes:

1. Instale una versión de Quickstart de SDK de AEM localmente
1. Vaya a la consola web en `http://serveraddress:serverport/system/console/configMgr`
1. Busque y haga clic en el **controlador de autenticación de token de Granite de Adobe**
1. Configure el **atributo SameSite para la cookie de token de inicio de sesión** a `None`, como se muestra en la imagen siguiente
   ![samesite](/help/security/assets/samesite1.png)
1. Haga clic en Guardar
1. Genere las configuraciones de formato JSON para esta configuración en particular siguiendo los pasos descritos en [Generación de configuraciones de OSGi mediante Quickstart de SDK de AEM](/help/implementing/deploying/configuring-osgi.md#generating-osgi-configurations-using-the-aem-sdk-quickstart)
1. Aplique la configuración siguiendo los pasos de la sección [Formato de API de Cloud Manager para la configuración de propiedades](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) de la documentación de OSGi.

Después de actualizar esta configuración y de cerrar la sesión de los usuarios y volver a iniciarla, `login-token` Las cookies tienen el `None` conjunto de atributos y se incluye en solicitudes entre sitios.
