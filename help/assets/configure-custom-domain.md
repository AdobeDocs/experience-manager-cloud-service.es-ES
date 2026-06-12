---
title: Configuración de un dominio personalizado para el nivel de entrega
description: Obtenga información sobre cómo configurar un dominio personalizado para el nivel de entrega en Adobe Cloud Manager.
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: b24faf23435948a8f122223bf38227a0936bbeb5
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 3%

---


# Configuración de un dominio personalizado para el nivel de entrega{#configure-custom-domain}

En Adobe Cloud Manager, puede hacer que su sitio web destaque añadiendo un dominio personalizado. Aunque AEM as a Cloud Service viene con un dominio predeterminado, puede personalizarlo según sus necesidades.

>[!NOTE]
>
>Los clientes con licencias de Dynamic Media Prime o Dynamic Media Ultimate deben utilizar la configuración de dominio personalizado de autoservicio disponible en Cloud Manager.
>Consulte [Documentación de Dynamic Media Prime y Ultimate](/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md#configure-custom-domain-in-delivery-tier) para obtener más información.
>
>Los clientes que utilicen configuraciones de Dynamic Media antiguas en las que Dynamic Media con OpenAPI está habilitado manualmente, deben seguir esta documentación. Para estas configuraciones, la asignación de dominio personalizado se completa mediante una solicitud de asistencia de Adobe.

## Prepárese para empezar

Asegúrese de cumplir los siguientes requisitos antes de iniciar el proceso de configuración:

* Acceso a Cloud Manager
* Dynamic Media ya está habilitado con OpenAPI en su entorno a través de un ticket de asistencia
* Certificado SSL de tipo EV u OV para el dominio utilizado en el nivel de entrega. Consulte [Introducción a los certificados SSL](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/introduction-to-ssl-certificates) para obtener más información

## Configuración de dominios personalizados en el nivel de envío mediante Cloud Manager

Ejecute los siguientes pasos en Cloud Manager:

1. [Agregar un certificado SSL administrado por el cliente](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate#add-customer-managed-ssl-cert)

2. [Añadir un nombre de dominio personalizado](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name#adding-cdn-settings)

Después de completar los pasos anteriores, genere un ticket de asistencia de Adobe para la asignación de dominios personalizados. Adobe realiza la asignación de dominios como parte del proceso de asistencia.