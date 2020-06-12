---
title: Información general sobre el analizador de preparación para la nube
description: Información general sobre el analizador de preparación para la nube
translation-type: tm+mt
source-git-commit: 64b685a7c9fbb105ed66dc4b3212b2bf91dee4af
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# Información general {#overview-cloud-readiness-analyzer}

El analizador de preparación para la nube ayuda a acelerar los procesos de evaluación de la preparación para pasar de una implementación existente de Adobe Experience Manager (AEM) a AEM como servicio de nube.

Esta herramienta genera un informe que identifica las áreas de posible refactorización, que es el primer paso en el viaje de transición a AEM como servicio de nube.

## Informe de resumen en el analizador de preparación para la nube {#summary-report}

El informe de resumen del analizador de preparación para la nube se utiliza para obtener una comprensión de alto nivel de la preparación general para la actualización. El informe consta de categorías de problemas que deben solucionarse antes de una implementación correcta de AEM como servicio de nube.

El informe resumido incluye las siguientes categorías:

* Funcionalidad de la aplicación que se debe refactorizar
* Elementos de repositorio que deben moverse a una ubicación admitida
* Los cuadros de diálogo y los componentes de la interfaz de usuario heredados que deben modernizarse
* Problemas de implementación y configuración
* Funciones de AEM 6.x que se han sustituido por nuevas funciones o que actualmente no son compatibles con AEM como servicio de nube

En el informe resumido se proporciona información adicional sobre las categorías y las posibles consecuencias y soluciones asociadas con esas categorías mediante enlaces.

>[!NOTE]
>El informe del analizador de preparación para la nube acelera el proceso de estimación del tiempo y el coste necesarios para realizar la transición a AEM como servicio de nube al proporcionar información que, de lo contrario, tendría que recopilarse y evaluarse manualmente.

El informe de resumen está disponible en la interfaz de usuario de AEM. Existe una opción para descargar el informe completo en un formato de valores separados por comas (CSV) que resulta útil durante el proceso de refactorización.