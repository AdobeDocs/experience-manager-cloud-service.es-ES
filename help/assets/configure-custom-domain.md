---
title: Configuración de un dominio personalizado para el nivel de entrega
description: Obtenga información sobre cómo configurar un dominio personalizado para el nivel de entrega en Adobe Cloud Manager.
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: d2859c547c87bd1856ba0e05fac835db434d824c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 6%

---

# Configuración de un dominio personalizado para el nivel de entrega{#configure-custom-domain}

En Adobe Cloud Manager, puede hacer que su sitio web destaque añadiendo un dominio personalizado. Aunque AEM as a Cloud Service viene con un dominio predeterminado, puede personalizarlo según sus necesidades.

## Antes de empezar

* Debe tener un certificado TLS o SSL de varias SAN (nombre alternativo del sujeto).
* El certificado SSL debe tener distintas SAN según el certificado asignado para el nivel de entrega dentro del mismo dominio.
* La directiva de certificado debe adherirse a la directiva Validación extendida (EV) u Validación de organización (OV), y no a la directiva Validación de dominio (DV).


## Configuración de un dominio personalizado para el nivel de entrega

1. Vaya a **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Descripción general del programa]** > **[!UICONTROL Certificados SSL]** y agregue su certificado SSL.
   ![imagen](/help/assets/assets/ssl-certificate.png)
Aprenda a agregar [certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) en Adobe Cloud Manager.

1. Después de agregar el certificado SSL, agregue un dominio personalizado. Haga clic en **[!UICONTROL Configuración de dominio]** y especifique el dominio personalizado con la opción **[!UICONTROL Servicio de publicación]**.
Más información sobre [dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Agregue dos [registros CNAME](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) en su registro DNS correspondientes a los dominios de publicación.
La verificación del DNS puede tardar unas horas en procesarse debido a los retrasos de propagación del DNS.

1. Registre un caso de compatibilidad para facilitar la configuración del dominio personalizado, lo que garantiza que se dirija al nivel de entrega.

>[!NOTE]
>
>Añada el dominio personalizado a la lista de direcciones URL de redireccionamiento permitidas. La lista está en el cliente IMS para el selector de recursos.<br>Coordinar con el equipo respectivo de Adobe para ejecutar esta tarea proporcionando la cadena de dominio personalizada.
