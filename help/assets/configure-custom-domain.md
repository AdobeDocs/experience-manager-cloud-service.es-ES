---
title: Configuración de un dominio personalizado para el nivel de Publish
description: Obtenga información sobre cómo configurar un dominio personalizado para el nivel de publicación en Adobe Cloud Manager.
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: ed7331647ea2227e6047e42e21444b743ee5ce6d
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 11%

---

# Configurar un dominio personalizado para el nivel de publicación{#configure-custom-domain}

| [Prácticas recomendadas de búsqueda](/help/assets/search-best-practices.md) | [Prácticas recomendadas de metadatos](/help/assets/metadata-best-practices.md) | [Centro de contenido](/help/assets/product-overview.md) | [Dynamic Media con funciones de OpenAPI](/help/assets/dynamic-media-open-apis-overview.md) | [Documentación de desarrollador de AEM Assets](https://developer.adobe.com/experience-cloud/experience-manager-apis/) |
| ------------- | --------------------------- |---------|----|-----|

>[!AVAILABILITY]
>
>La guía de funciones de Dynamic Media con OpenAPI ya está disponible en formato de PDF. Descargue toda la guía y utilice Adobe Acrobat AI Assistant para responder a sus consultas.
>
>[!BADGE PDF de la Guía de Dynamic Media con funciones OpenAPI]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

En Adobe Cloud Manager, puede hacer que su sitio web destaque añadiendo un dominio personalizado. Aunque AEM as a Cloud Service viene con un dominio predeterminado, puede personalizarlo según sus necesidades.

## Antes de empezar

* Debe tener un certificado TLS o SSL de varias SAN (nombre alternativo del sujeto).
* El certificado SSL debe tener SAN distintas para el certificado asignado para el nivel de publicación dentro del mismo dominio.
* La directiva de certificado debe adherirse a la directiva Validación extendida (EV) u Validación de organización (OV), y no a la directiva Validación de dominio (DV).


## Configurar un dominio personalizado para el nivel de publicación

1. Vaya a **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Resumen del programa]** > **[!UICONTROL Certificados SSL]** y agregue su certificado SSL.
   ![imagen](/help/assets/assets/ssl-certificate.png)
Aprenda a agregar [certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) en Adobe Cloud Manager.

1. Después de agregar el certificado SSL, agregue un dominio personalizado. Haga clic en **[!UICONTROL Configuración de dominio]** y especifique el dominio personalizado con la opción **[!UICONTROL servicio de Publish]**.
Más información sobre [dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Agregue dos [registros CNAME](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) en su registro DNS correspondientes a los dominios de publicación.
La verificación del DNS puede tardar unas horas en procesarse debido a los retrasos de propagación del DNS.

1. Registre un caso de compatibilidad para facilitar la configuración del dominio personalizado, lo que garantiza que se dirija al nivel de entrega.

>[!NOTE]
>
Añada el dominio personalizado a la lista de direcciones URL de redireccionamiento permitidas. La lista está en el cliente IMS para el selector de recursos.<br>Coordinar con el equipo de Adobe correspondiente para ejecutar esta tarea proporcionando la cadena de dominio personalizada.
