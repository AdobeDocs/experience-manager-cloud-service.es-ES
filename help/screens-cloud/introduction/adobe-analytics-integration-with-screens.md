---
title: Integración de Adobe Analytics con AEM Screens
seo-title: Adobe Analytics Integration with AEM Screens
description: Siga esta página para obtener más información sobre la integración predeterminada de AEM Screens con Adobe Analytics y le ofrece una prueba de reproducción.
seo-description: Follow this page to learn about out of the box integration of AEM Screens with Adobe Analytics and provides you with a proof of play.
uuid: 80d61af7-bf4d-46ca-a026-99a666c2e1a0
contentOwner: trushton
content-type: reference
products: SG_EXPERIENCEMANAGER/Cloud/SCREENS
topic-tags: administering
discoiquuid: b1a0e00e-0368-42c9-8bcd-5f00b4d0990c
docset: aem65
role: Admin, Developer
level: Intermediate
source-git-commit: bf0a841a5cd5eb278fd3d59484c84d1cee172b4e
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Integración de Adobe Analytics con AEM Screens {#adobe-analytics-integration-with-aem-screens}

Esta sección trata los siguientes temas:

* **Información general**
* **Detalles arquitectónicos**

## Información general {#overview}

***AEM Screens*** aprovecha Adobe Analytics y, con él, puede lograr algo único en el mercado: análisis en canales múltiples que ayudan a correlacionar el contenido que se muestra en la ubicación con otras fuentes de datos.

AEM Screens ofrece una integración predeterminada con Adobe Analytics y le ofrece una prueba de reproducción.

En esta sección se describe la siguiente funcionalidad relacionada con la conexión de un proyecto de AEM Screens con Adobe Analytics:

* Permite informes de prueba de reproducción por dispositivo
* Permite informes de prueba de reproducción por recurso
* Garantiza que todos los eventos del reproductor se capturan y se marcan con la hora
* Garantiza que todos los eventos del reproductor se almacenen localmente si la reproducción no está conectada a una red
* Permite crear bucles de comentarios para rastrear eventos de reproducción a lo largo del tiempo
* Permite al sistema modificar el contenido y los diseños en función de los criterios de éxito definidos por el autor del contenido

Por lo tanto, la integración de Adobe Analytics con AEM Screens aplica lo siguiente *objetivos*:

* Activación del ROI desde implementaciones de señalización digital
* Integre Analytics como base para la futura habilitación de la recopilación y el análisis de información de uso

## Detalles arquitectónicos {#architectural-details}

Un cliente de AEM Screens quiere comprender qué contenido se mostró a qué hora y durante cuánto tiempo (acumulado). Esta es la capacidad común de la solución de señalización. En lugar de crear nuestros propios análisis, AEM Screens aprovechará Adobe Analytics y, con ellos, podremos lograr algo único en el mercado: análisis en canales múltiples que ayuden a correlacionar el contenido que se muestra en la ubicación con otras fuentes de datos.

En el siguiente diagrama de arquitectura se explica la integración de Adobe Analytics con AEM Screens:

![Integración con Adobe Analytics](/help/screens-cloud/assets/analytics-architecture.png)

## Habilitar Adobe Analytics en la nube de AEM Screens {#enabling-adobe-analytics-in-aem-screens-cloud}

Póngase en contacto con el administrador de relaciones con el Adobe para habilitar el análisis de Adobe en Screens Cloud.

## Screens Analytics: Flujo de habilitación {#screens-analytics-enablement-flow}

>[!CAUTION]
>
>Antes de configurar las propiedades, póngase en contacto con el administrador de relaciones con el Adobe para crear un ticket y obtener un **Clave de API de Analytics** y **Proyecto de Analytics** para su uso con AEM Screens.

## Uso del servicio Adobe Analytics en AEM Screens {#using-adobe-analytics-service-in-aem-screens}

Este escenario invoca la API de Analytics a través de llamadas REST desde un servicio de análisis en los componentes principales de pantallas de firmware e instrumentos para crear y enviar explícitamente eventos específicos de un caso de uso determinado, al tiempo que permite la extensibilidad en el que cualquier mensaje personalizado se puede enviar a Analytics desde un canal desarrollado personalizado.

Los eventos de Analytics se almacenan sin conexión en indexedDB y luego se fragmentan y se envían a la nube.
