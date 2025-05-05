---
title: Navegación al proveedor de servicios de Screens
description: En esta página se describe cómo desplazarse a Screens Services Provider.
exl-id: 9eff6fe8-41d4-4cf3-b412-847850c4e09c
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 4%

---

# Navegación al proveedor de servicios de Screens {#setup-screens-services-provider}

## Introducción {#introduction}

**Proveedor de servicios de Screens**, permite al autor, desarrolladores y administradores de contenido administrar pantallas y reproductores para la reproducción de contenido una vez que este se agrega a los canales. Una vez que los usuarios tengan acceso a AEM Cloud Service, deberán poder iniciar sesión en el Proveedor de servicios de Screens.

Esta sección describe cómo configurar el proveedor de servicios de Screens.


## Objetivo {#objective}

En la siguiente sección se muestra cómo configurar y configurar el proveedor de servicios de Screens.

## Pasos para configurar el proveedor de servicios de Screens {#screens-services-provider}

Siga los pasos a continuación para configurar Screens Services Provider:

1. Vaya a [Proveedor de servicios de Screens](https://experience.adobe.com/screens).

   >[!CAUTION]
   >Si tiene acceso a varias organizaciones, asegúrese de haber iniciado sesión en la organización correcta. Para cambiar su organización, haga clic en el nombre de la organización en la esquina superior derecha de la pantalla y seleccione la organización a la que necesita acceder.

1. Haga clic en el icono de engranaje situado junto a Proyecto (esquina superior izquierda)

   ![imagen](/help/screens-cloud/assets/configure/configure-screens0.png)

1. Introduzca los siguientes detalles en el cuadro de diálogo Editar configuración.
   * **URL de Publish AEM** - URL de publicación de la publicación de la aplicación (por ejemplo, `https://publish-p12345-e12345.adobeaemcloud.com`)
   * AEM **URL del autor** - URL del autor de la (por ejemplo, `https://author-p12345-e12345.adobeaemcloud.com`)

   >[!NOTE]
   >AEM AEM Asegúrese de crear y publicar al menos un canal de pantalla de antes de configurar el canal en el proveedor de servicios de Screens, según se indica a continuación Para crear un canal, vaya a /screens.html en su proveedor de contenido.

   ![imagen](/help/screens-cloud/assets/configure/configure-screens4.png)

1. Haga clic en **Guardar** para conectarse al proveedor de contenido de Screens.

1. AEM Si ha configurado la instancia de publicación de la para permitir el acceso solo a direcciones IP de confianza mediante la función de Lista de permitidos IP de Cloud Manager, debe configurar un encabezado con un valor clave en el cuadro de diálogo de configuración, como se muestra a continuación.
Las IP que necesitan quedar en la lista blanca también deben moverse al archivo de configuración y deben [desaplicarse](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list) de la configuración de Cloud Manager.

   ![imagen](/help/screens-cloud/assets/configure/configure-screens20b.png)
AEM La misma clave debe configurarse en la configuración de CDN de la.  Se recomienda no colocar el valor del encabezado directamente en GITHub y usar una [referencia secreta](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-credentials-authentication#rotating-secrets).
A continuación se muestra un ejemplo de [configuración de CDN](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf):

   ```kind: "CDN"
       version: "1"
       metadata:
         envTypes: ["dev", "stage", "prod"]
       data:
         trafficFilters:
           rules:
             - name: "block-request-from-not-allowed-ips"
               when:
                 allOf:
                   - reqProperty: clientIp
                     notIn: ["101.41.112.0/24"]
                    reqProperty: tier
                     equals: publish
               action: block
             - name: "allow-requests-with-header"
               when:
                 allOf:
                   - reqProperty: tier
                     equals: publish
                   - reqProperty: path
                     equals: /screens/channels.json
                   - reqHeader: x-screens-allowlist-key
                     equals: $\
       {CDN_HEADER_KEY}
               action:
                 type: allow
   ```

1. Seleccione **Canales** en la barra de navegación izquierda y haga clic en **abrir en el proveedor de contenido**.

   ![imagen](/help/screens-cloud/assets/configure/configure-screens1.png)

1. El proveedor de contenido de Screens se abre en otra pestaña que le permite crear su contenido.

   ![imagen](/help/screens-cloud/assets/configure/configure-screens2.png)





## Siguientes pasos {#whats-next}

Después de haber aprendido a configurar el proveedor de servicios de Screens, vaya a [Usar el proveedor de contenido de Screens](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=es#screens-content-provider) para obtener más información.
