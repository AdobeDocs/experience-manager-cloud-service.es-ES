---
title: Configurar el dominio personalizado para el nivel de publicación
description: Obtenga información sobre cómo configurar el dominio personalizado para el nivel de publicación en Adobe Cloud Manager.
source-git-commit: f6c0e8e5c1d7391011ccad5aa2bad4a6ab7d10c3
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 6%

---


# Configurar el dominio personalizado para el nivel de publicación{#configure-custom-domain}

En Adobe Cloud Manager, puede hacer que su sitio web destaque añadiendo un dominio personalizado. Aunque AEM as a Cloud Service viene con un dominio predeterminado, puede personalizarlo según sus necesidades.

## Antes de empezar

* Debe tener un certificado TLS o SSL de varias SAN (nombre alternativo del sujeto).
* El certificado SSL debe tener SAN distintas para el certificado asignado para el nivel de publicación dentro del mismo dominio.
* La directiva de certificado debe adherirse a la directiva Validación extendida (EV) u Validación de organización (OV), y no a la directiva Validación de dominio (DV).


## Añadir dominio personalizado

Para configurar un dominio personalizado para el nivel de publicación, siga estos pasos:

1. Ir a **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Resumen del programa]** > **[!UICONTROL Certificados SSL]**y agregue el certificado SSL.
   ![imagen](/help/assets/assets/ssl-certificate.png)
Aprenda a añadir [Certificado SSL](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) en Adobe Cloud Manager.

1. Después de agregar el certificado SSL, agregue un dominio personalizado. Clic **[!UICONTROL Configuración de dominio]** y especifique el dominio personalizado en la variable **[!UICONTROL servicio de Publish]** opción.
Más información sobre [dominio personalizado](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Añadir 2 [Registros CNAME](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) en el registro DNS correspondiente a los dominios de publicación.
La verificación del DNS puede tardar unas horas en procesarse debido a los retrasos de propagación del DNS.

1. Registre un caso de compatibilidad para facilitar la configuración del dominio personalizado, lo que garantiza que se dirija al nivel de entrega.

>[!NOTE]
>
> Asegúrese de añadir el dominio personalizado a la lista de URL de redireccionamiento permitidas en el cliente IMS para el selector de recursos.<br>Coordine con el equipo de Adobe correspondiente para ejecutar esta tarea proporcionando la cadena de dominio personalizada.
