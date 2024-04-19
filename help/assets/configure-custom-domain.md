---
title: Configurar el dominio personalizado para el nivel de publicación
description: Obtenga información sobre cómo configurar el dominio personalizado para el nivel de publicación en Adobe Cloud Manager.
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 1%

---


# Configurar el dominio personalizado para el nivel de publicación{#configure-custom-domain}

En Adobe Cloud Manager, puede resaltar su sitio web agregando un dominio personalizado. AEM Aunque el as a Cloud Service viene con un dominio predeterminado, puede personalizarlo según sus necesidades.
<!-- For example, AEM sites can use `sites.custom_domain.com`, and the AEM publish domain can be accessed via `assets.custom_domain.com`. Additionally, getting an SSL certificate for assets.pmi.com with a SAN entry for `delivery.custom_domain.com` improves security and trustworthiness. -->

## Antes de empezar

* Debe tener un certificado TLS o SSL de varias SAN (nombre alternativo del sujeto).
* El certificado SSL debe tener SAN distintas para el certificado asignado para el nivel de publicación dentro del mismo dominio.
* La directiva de certificado debe adherirse a la directiva Validación extendida (EV) u Validación de organización (OV), y no a la directiva Validación de dominio (DV).


## Añadir dominio personalizado

Para configurar un dominio personalizado para el nivel de publicación, siga estos pasos:

1. Ir a **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Resumen del programa]** > **[!UICONTROL Certificados SSL]**y agregue el certificado SSL.
   ![imagen](/help/assets/assets/ssl-certificate.png)
Aprenda a añadir [Certificado SSL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) en Adobe Cloud Manager.

1. Después de agregar el certificado SSL, agregue un dominio personalizado. Clic **[!UICONTROL Configuración de dominio]** y especifique el dominio personalizado en la variable **[!UICONTROL Servicio de publicación]** opción.
   <br> Más información sobre [dominio personalizado](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html?lang=en).

1. Agregue 2 registros CNAME en el registro DNS correspondientes a los dominios de publicación.
   <br> La verificación DNS puede tardar unas horas en procesarse debido a los retrasos de propagación de DNS.

1. Registre un caso de compatibilidad para facilitar la configuración del dominio personalizado, lo que garantiza que se dirija al nivel de entrega.

>[!NOTE]
>
> Asegúrese de añadir el dominio personalizado a la lista de URL de redireccionamiento permitidas en el cliente IMS para el selector de recursos.<br>Coordine con el equipo de Adobe correspondiente para ejecutar esta tarea proporcionando la cadena de dominio personalizada.
