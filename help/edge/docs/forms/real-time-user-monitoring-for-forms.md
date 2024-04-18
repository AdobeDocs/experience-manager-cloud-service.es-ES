---
title: Monitorización de usuarios en tiempo real para Edge Delivery Services Forms
description: La monitorización de usuarios en tiempo real para Edge Delivery Services de Forms implica el seguimiento y análisis continuos de las interacciones de los usuarios con los formularios.
feature: Edge Delivery Services
exl-id: 184fc7dc-d583-4a63-9e30-80d324ec9d7e
source-git-commit: 2affe155b285986128487043fcc4f2938fc15842
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---


# Monitorización de usuarios en tiempo real para Edge Delivery Services Forms

Adobe Experience Manager utiliza Real User Monitoring (RUM) para comprender las interacciones de los visitantes con sitios impulsados por Adobe Experience Manager. Ayuda a diagnosticar los desafíos de rendimiento y a medir la eficacia de los experimentos. La Monitorización de usuarios reales mantiene la privacidad del visitante mediante el uso de técnicas de muestreo, lo que garantiza que los sitios que visita no recopilen información personal. No se permite añadir datos personales a la recopilación de datos de RUM. La monitorización de usuarios reales en Adobe Experience Manager está diseñada para preservar la privacidad del visitante y minimizar la recopilación de datos.

## Ventajas de utilizar la monitorización de usuarios en tiempo real para Edge Delivery Services Forms {#advantages}

AEM Utiliza la monitorización de usuarios en tiempo real para lo siguiente:

* Para identificar y corregir los cuellos de botella de rendimiento en los sitios.
* Para calcular la cantidad de vistas de página a los sitios de los clientes
* Para comprender la interacción de Adobe Experience Manager con las bibliotecas de análisis, segmentación o externas en la misma página, se mejora la compatibilidad.

## Requisitos previos

Puede ver el panel de monitorización de usuarios en tiempo real de Edge Delivery Services Forms accediendo a la siguiente URL: https://data.aem.live/?ext=forms

![Pantalla de inicio de sesión RUM para Edge Delivery Services Forms ](/help/edge/assets/rum-login-screen.png)

Para iniciar sesión en el panel de monitorización de usuarios en tiempo real de Edge Delivery Services Forms, introduzca lo siguiente:
* **URL**: la dirección URL es específica del sitio o dominio del usuario. Los usuarios tienen la opción de filtrar el sitio o dominio para ver el panel según sus necesidades.
* **Clave de dominio**: el usuario genera manualmente la clave de dominio. Para obtener ayuda o consultas, consulte la [Generar clave de dominio RUM](https://aemcs-workspace.adobe.com/rum/generate-domain-key) documentación.

### Panel de monitorización de usuarios en tiempo real para Edge Delivery Services Forms

Después de introducir la URL y la clave de dominio en la pantalla de inicio de sesión, obtiene acceso al panel de monitorización de usuarios en tiempo real para Edge Delivery Services Forms.

La siguiente ilustración muestra el panel RUM para Edge Delivery Services Forms:

![Tablero de RUM Forms](/help/edge/assets/rum-forms-dashboard.png)

### Diferentes métricas clave del tablero de RUM para Forms {#different-metrics-rum-dashboard-forms}

Puede evaluar las interacciones de los visitantes con sitios impulsados por Adobe Experience Manager mediante las siguientes métricas clave:

* **Formviews**: es el número total de formularios procesados para una URL dentro del intervalo de fechas especificado.
* **Formsubmission**: es el número total de formularios enviados para una dirección URL dentro del intervalo de fechas especificado.
* **Pintura de contenido más grande**: muestra la velocidad a la que se carga la URL, indicando el tiempo necesario para que el elemento de contenido más grande sea visible en la ventanilla móvil desde el momento en que el usuario solicita la URL. Este elemento de contenido más grande puede ser una imagen, un vídeo o un elemento de texto sustancial de nivel de bloque. Las clasificaciones de rendimiento para la velocidad de carga de la URL se clasifican de la siguiente manera:
   * **Bueno**: si el tiempo de carga es de 2,5 segundos o menos.
   * **Okay**: si el tiempo de carga es superior a 2,5 segundos, pero 4 segundos o menos.
   * **Malo**: Si el tiempo de carga supera los 4 segundos

* **Desplazamiento de diseño acumulativo**: Mide la suma total de todas las puntuaciones de cambios de diseño individuales para cada cambio de diseño inesperado que se produce a lo largo de toda la duración de la página. Desempeña un papel crucial a la hora de identificar el rendimiento de una página porque cuando los elementos de la página cambian mientras un usuario intenta interactuar con ellos, la experiencia del usuario es mala. Esta puntuación va desde cero a cualquier número positivo: cero indica que no se ha producido ningún desplazamiento, mientras que un número mayor indica que se han producido más cambios de diseño en la página. Las métricas de rendimiento utilizadas para evaluar las puntuaciones de cambio de diseño se clasifican de la siguiente manera:

   * **Bueno**: si la puntuación del cambio de diseño es 0,1 o menos.
   * **Okay**: si la puntuación del cambio de diseño es mayor de 0,1 pero 0,25 o menor.
   * **Malo**: si la puntuación del cambio de diseño supera el 0,25.

* **Interacción con la siguiente pintura**: evalúa la rapidez con la que una página reacciona a las interacciones del usuario, teniendo en cuenta el tiempo que tarda la página en responder a clics, toques e entradas del teclado durante la visita de un usuario a la página. El valor final es la interacción más larga observada, sin tener en cuenta las anomalías. Las métricas de rendimiento para Interacción con la siguiente pintura se clasifican de la siguiente manera:
   * **Bueno**: Si la duración entre las acciones del usuario es de 200 milisegundos (ms) o menos.
   * **Okay**: Si la duración es superior a 200 ms pero inferior a 500 ms.
   * **Malo**: Si la duración supera los 500 ms.
