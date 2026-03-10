---
title: Configuración de Dynamic Media
description: Para configurar Dynamic Media, debe configurar Dynamic Media y administrar los ajustes preestablecidos de visualizador e imagen.
mini-toc-levels: 3
contentOwner: Rick Brough
feature: Configuration,Viewer Presets,Image Presets,Dynamic Media
role: Admin,User
badgeSaas: label="AEM Assets" type="Positive" tooltip="(Se aplica a los AEM Assets)."
exl-id: 83b70b17-7ee3-41cb-be90-c92ca161660e
source-git-commit: a641933d1049cd07ee8935672c8ef357a5bbf18c
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 5%

---

# Configuración de Dynamic Media {#setting-up-dynamic-media}

{{work-with-dynamic-media}}

[Dynamic Media](https://business.adobe.com/es/products/experience-manager/assets/dynamic-media.html) le ayuda a administrar sus recursos al proporcionarle recursos de marketing y comercialización visual enriquecidos bajo demanda, escalados automáticamente para su consumo en sitios web, móviles y sociales. Al utilizar un conjunto de recursos de origen principales, Dynamic Media genera y ofrece varias variaciones de contenido enriquecido en tiempo real a través de su red global, escalable y optimizada para el rendimiento.

<!-- OBSOLETE UNTIL THE INTEGRATING SCENE7 TOPIC GETS A MAJOR UPDATE

>[!NOTE]
>
>This documentation describes Dynamic Media capabilites, which are integrated directly into [!DNL Experience Manager]. If you are using Dynamic Media Classic (previously called Scene7) integrated into [!DNL Experience Manager], see [Dynamic Media Classic integration documentation](/help/sites-cloud/administering/integrating-scene7.md).
>
>See [Dual Use Scenario](/help/sites-cloud/administering/integrating-scene7.md#dual-use-scenario) for times when you may want to use [!DNL Experience Manager] integrated with Dynamic Media Classic along with Dynamic Media.

-->

Si está administrando Dynamic Media, los siguientes temas le interesan:

* [Configuración de Dynamic Media](config-dm.md)
* [Administrar ajustes preestablecidos de imagen](managing-image-presets.md)
* [Administrar ajustes preestablecidos de visor](managing-viewer-presets.md)
* [Resolución de problemas de Dynamic Media](troubleshoot-dm.md)

Consulte también los temas siguientes:

* [Codificación de vídeo y perfiles de vídeo](video-profiles.md)
* [Perfiles de imagen](image-profiles.md)

>[!NOTE]
>
>**Si está actualizando:**
>
>* Una vez que Adobe [!DNL Experience Manager] esté en funcionamiento, cualquier recurso que cargue tendrá Dynamic Media habilitado automáticamente (a menos que el administrador del sistema lo haya deshabilitado explícitamente). Si se encuentra en una instancia actualizada de [!DNL Experience Manager] y es su primera vez en Dynamic Media, es probable que deba volver a procesar los recursos para que estén habilitados para Dynamic Media. Ver [Volver a procesar recursos en una carpeta](/help/assets/dynamic-media/about-image-video-profiles.md#reprocessing-assets).


## Se requiere una actualización de DNS única para las renovaciones de certificados de Dynamic Media {#dns-update-dynamic-media-certificate-renewals}

Si su dominio utiliza un registro DNS CAA (Autorización de entidad de certificación), debe autorizar a DigiCert para permitir la renovación continua de los certificados TLS/SSL utilizados por los nombres de host de Dynamic Media.

Añada el siguiente registro de CA en la raíz (Apex) de su dominio:

```
<yourdomain> CAA 0 issue "digicert.com"
```

Este es un cambio único.

Puede comprobar si existe un registro de CAA con las herramientas del proveedor DNS o con una [utilidad de búsqueda de CAA](https://caatest.co.uk/).

Si existe un registro CAA y DigiCert no está autorizado, la renovación del certificado falla cuando caduca el certificado actual, lo que puede causar tiempo de inactividad para la entrega de imágenes y vídeos. Si no existe ningún registro de CA para el dominio, no se requiere ninguna acción.
