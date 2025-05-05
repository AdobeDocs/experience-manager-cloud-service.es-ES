---
title: Configuración de un dominio personalizado para el nivel de publicación
description: Obtenga información sobre cómo configurar un dominio personalizado para el nivel de publicación en Adobe Cloud Manager.
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 20%

---

# Configurar un dominio personalizado para el nivel de publicación{#configure-custom-domain}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime y Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> integración de <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets con Edge Delivery Services</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nueva</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>extensibilidad de la interfaz de usuario</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>Nuevo</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>Habilitar Dynamic Media Prime y Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>Prácticas recomendadas de búsqueda</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>Prácticas recomendadas de metadatos</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Centro de contenido</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>Dynamic Media con funciones de OpenAPI</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>Documentación de desarrollador de AEM Assets</b></a>
        </td>
    </tr>
</table>

>[!AVAILABILITY]
>
>La guía de Dynamic Media con funciones de OpenAPI ya está disponible en formato de PDF. Descargue la guía completa y utilice el Asistente de IA de Adobe Acrobat para responder sus consultas.
>
>[!BADGE Guía en PDF de Dynamic Media con funciones OpenAPI]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/dynamic-media-with-openapi-capabilities.pdf"}

En Adobe Cloud Manager, puede hacer que su sitio web destaque añadiendo un dominio personalizado. Aunque AEM as a Cloud Service viene con un dominio predeterminado, puede personalizarlo según sus necesidades.

## Antes de empezar

* Debe tener un certificado TLS o SSL de varias SAN (nombre alternativo del sujeto).
* El certificado SSL debe tener SAN distintas para el certificado asignado para el nivel de publicación dentro del mismo dominio.
* La directiva de certificado debe adherirse a la directiva Validación extendida (EV) u Validación de organización (OV), y no a la directiva Validación de dominio (DV).


## Configurar un dominio personalizado para el nivel de publicación

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
