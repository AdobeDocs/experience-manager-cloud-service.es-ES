---
title: Introducción a AEM Screens as a Cloud Service
description: Comprender AEM Screens as a Cloud Service.
exl-id: b1cc0a63-ecd3-4d89-ac49-f384cc610cdc
feature: Screens Deployments
role: Admin, Developer, User
source-git-commit: 53086e2ec6d9d962a8f1cb1cc40f0601da74ac63
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 59%

---


# Introducción a AEM Screens as a Cloud Service {#introduction-screens-cloud}

Con Adobe Experience Manager AEM () Screens as a Cloud Service, puede crear experiencias de señalización digital atractivas y dinámicas pensadas para consumirse en espacios públicos. Es la siguiente evolución del producto AEM Screens y representa un gran avance en la capacidad de uso y la escalabilidad.

AEM Screens as a Cloud Service es una solución de señalización digital que permite a los especialistas en marketing crear y administrar experiencias digitales dinámicas a escala. Además, implica diferentes tipos de pantallas físicas como parte de una estrategia de marketing digital integral. Amplía la oferta omnicanal de Adobe más allá de los canales web y móviles habituales, para incluir también canales de señalización digital que nos rodean. AEM Screens as a Cloud Service permite experiencias de usuario más relevantes, contextuales, productivas y anticipadoras mediante una comprensión profunda de la creación y el ensamblado de contenido, la administración de eventos activada y la reproducción de contenido para todos los consumidores y visitantes de cualquier espacio público.

## Comprender los componentes en Screens as a Cloud Service {#understanding-components}

Screens as a Cloud Service tiene dos componentes principales:

* **[Proveedor de contenido](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html?lang=es)**, que es el complemento de Screens que se ejecuta en AEM Cloud Service o en Adobe Managed Services (AMS). El proveedor de contenido de Screens permite al autor de contenido crear y administrar canales. Los autores de contenido pueden agregar contenido nuevo, editarlo sin tener que preocuparse por los detalles de creación de visualizaciones o registro del reproductor. El proveedor de contenido proporciona una abstracción de los detalles subyacentes del desarrollo de contenido, las visualizaciones o el registro del reproductor.

* **[Proveedor de servicios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=es)**, que es el servicio de administración de señalización digital que se ejecuta en Adobe I/O Runtime. El proveedor de servicios de Screens permite a los autores, desarrolladores y administradores de contenido administrar pantallas y reproductores para la reproducción de contenido una vez que este se añade a los canales. Además, el proveedor de servicios de Screens informa al orquestador de dónde y cuándo se va a reproducir el contenido en un nivel superior.


## Información general de la arquitectura {#architectural-overview}

Como usuario as a Cloud Service de AEM Screens, puede agregar y administrar contenido en canales. Puede registrar y administrar pantallas y reproductores desde las interfaces diseñadas específicamente para Screens as a Cloud Service, concretamente, **Screens Services Provider** y **Screens Content Provider**.

![Información general de arquitectura](/help/screens-cloud/assets/architecture-screenscloud.png)
