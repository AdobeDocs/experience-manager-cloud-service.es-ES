---
title: Monitorización de uso real (RUM) para Edge Delivery Services para AEM Forms as a Cloud Service
description: La Monitorización de uso real (RUM) para Edge Delivery Services para AEM Forms as a Cloud Service implica el seguimiento y análisis continuos de las interacciones del usuario con los formularios.
feature: Edge Delivery Services
hide: true
hidefromtoc: true
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 6c56f753d2a32de6fe11fd47843cee5bcb8cac4e
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 45%

---


# Monitorización de uso real (RUM) para Edge Delivery Services para AEM Forms as a Cloud Service

La Monitorización de uso real (RUM) le permite obtener información real sobre cómo los visitantes interactúan con los sitios web de Adobe Experience Manager AEM (). Esta herramienta integrada proporciona datos valiosos para comprender el comportamiento del usuario, diagnosticar problemas de rendimiento y medir la eficacia de los experimentos de sitios web. RUM va más allá de las pruebas sintéticas al capturar las interacciones de uso real, ofreciendo una imagen más precisa del rendimiento de su sitio.

Sin embargo, RUM prioriza la privacidad del visitante. Utiliza técnicas de muestreo para recopilar datos de un subconjunto representativo de usuarios, lo que garantiza que nunca se capture información de identificación personal (PII). Además, RUM está diseñado teniendo en cuenta la minimización de datos y recopila solo las métricas esenciales necesarias para el análisis del rendimiento. AEM Este enfoque le permite optimizar los sitios de la al tiempo que mantiene la confianza del usuario.


## Requisitos previos

Puede ver el panel de monitorización de los Edge Delivery Services de AEM Forms as a Cloud Service accediendo a la siguiente URL:

https://data.aem.live/?ext=forms

![Pantalla de inicio de sesión de RUM para Edge Delivery Services de Forms](/help/edge/assets/rum-login-screen.png)

Para iniciar sesión en el tablero de monitorización de Edge Delivery Services para AEM Forms as a Cloud Service, introduzca lo siguiente:

* **URL**: la dirección URL es específica del sitio o dominio del usuario. Los usuarios tienen la opción de filtrar el sitio o dominio para ver el panel según sus necesidades.

* **Clave de dominio**: el usuario genera manualmente la clave de dominio. Para obtener claves de dominio para los formularios, póngase en contacto con el representante del Adobe.

### Panel de monitorización para Edge Delivery Services de AEM Forms as a Cloud Service

Después de introducir la dirección URL y las claves de dominio en la pantalla de inicio de sesión, obtiene acceso al panel de monitorización para Edge Delivery Services de AEM Forms as a Cloud Service.

En la siguiente ilustración se muestra el tablero de Edge Delivery Services for AEM Forms as a Cloud Service:

![Tablero de formularios de RUM](/help/edge/assets/rum-forms-dashboard.png)

### Diferentes métricas clave del tablero de Forms {#different-metrics-rum-dashboard-forms}

Este tablero proporciona información clave sobre cómo los visitantes interactúan con los formularios del sitio web de Adobe Experience Manager AEM (). Al monitorizar estas métricas, puede identificar áreas que deben mejorarse y optimizar los formularios para mejorar la experiencia del usuario y las tasas de conversión:

* **Vistas de formularios**: Realice un seguimiento de la cantidad total de veces que se muestran los formularios
* **Envíos de formularios**: Rastree el número total de envíos completados

* **Pintura de contenido más grande**: muestra la velocidad a la que se carga la URL, indicando el tiempo necesario para que el elemento de contenido más grande sea visible en la ventanilla desde el momento en que el usuario solicita la URL. Este elemento de contenido más grande puede ser una imagen, un vídeo o un elemento de texto sustancial a nivel de bloque. Las clasificaciones de rendimiento para la velocidad de carga de la URL se clasifican de la siguiente manera:
   * **Bueno**: si el tiempo de carga es de 2,5 segundos o menos.
   * **Correcto**: si el tiempo de carga es superior a 2,5 segundos, pero 4 segundos o menos.
   * **Malo**: si el tiempo de carga supera los 4 segundos

* **Cambio de diseño acumulativo**: mide la suma total de todas las puntuaciones de cambios de diseño individuales para cada cambio de diseño inesperado que se produce a lo largo de todo el tiempo de duración de la página. Desempeña un papel crucial a la hora de identificar el rendimiento de una página porque cuando los elementos de la página cambian mientras un usuario intenta interactuar con ellos, la experiencia del usuario es mala. Esta puntuación va desde cero a cualquier número positivo: cero indica que no se ha producido ningún cambio, mientras que un número mayor indica que se han producido más cambios de diseño en la página. Las métricas de rendimiento utilizadas para evaluar las puntuaciones de cambio de diseño se clasifican de la siguiente manera:

   * **Bueno**: si la puntuación del cambio de diseño es 0,1 o menos.
   * **Correcto**: si la puntuación del cambio de diseño es mayor que 0,1 pero igual o menor que 0,25.
   * **Malo**: si la puntuación del cambio de diseño supera el 0,25.

* **Interacción con la siguiente pintura**: evalúa la rapidez con la que una página reacciona a las interacciones del usuario, teniendo en cuenta el tiempo que tarda la página en responder a clics, toques e entradas del teclado durante la visita de un usuario a la página. El valor final es la interacción más larga observada, sin tener en cuenta las anomalías. Las métricas de rendimiento para Interacción con la siguiente pintura se clasifican de la siguiente manera:
   * **Bueno**: si la duración entre las acciones del usuario es de 200 milisegundos (ms) o menos.
   * **Correcto**: si la duración es superior a 200 ms pero inferior a 500 ms.
   * **Malo**: si la duración supera los 500 ms.

## Perspectivas procesables

Al analizar estas métricas, puede identificar oportunidades para lo siguiente:

* Simplifique los formularios y reduzca el número de campos.
* Mejore la claridad del formulario con instrucciones y etiquetas claras.
* Optimizar el diseño del formulario para la capacidad de respuesta móvil.
* Solucionar problemas técnicos que ralentizan la carga de formularios.

Al centrarse en estas áreas, puede crear formularios que sean más fáciles de usar y que animen a los visitantes a completarlos, lo que a la larga conduce a tasas de conversión más altas.

## Consulte también

{{see-more-forms-eds}}