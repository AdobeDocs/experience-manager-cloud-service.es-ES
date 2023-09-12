---
title: Ver y comprender los informes de análisis de Forms adaptable
description: Los Forms adaptables se integran perfectamente con Adobe Analytics para capturar y rastrear las métricas de rendimiento de sus formularios y documentos publicados.
topic-tags: develop
feature: Adaptive Forms
role: User
level: Intermediate
source-git-commit: b44b54a88b87dc391dfeb51fb8b83095c274bd38
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---


# Ver y comprender los informes de análisis de Forms adaptable {#viewing-and-understanding-aem-forms-analytics-reports}

<span class="preview"> Esta es una función previa al lanzamiento y se puede acceder a ella a través de nuestra [canal previo al lanzamiento](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html#new-features). </span>

En el panorama de rápida evolución del análisis digital, mantenerse en sintonía con las tendencias globales es esencial para tomar decisiones informadas y optimizar las experiencias digitales. Para solucionarlo, Forms adaptable se integra perfectamente con Adobe Analytics para capturar y realizar un seguimiento de las métricas de rendimiento de los formularios y documentos publicados. El objetivo detrás del análisis de estas métricas es tomar decisiones basadas en datos, utilizando métricas y análisis para mejorar la facilidad de uso y la eficacia de los formularios.

Al capturar y rastrear los indicadores de rendimiento clave, las empresas pueden identificar áreas de mejora, optimizar las experiencias de los usuarios y, en última instancia, impulsar mejores resultados para crear experiencias de cliente excepcionales.

## Configuración de Adobe Analytics en Forms adaptable {#setup-adobe-analytics-to-aem-forms}

Para el informe de AEM Forms Analytics, primero debe integrar Adobe Analytics en AEM Forms mediante la automatización de la configuración del Experience Cloud. La automatización de la configuración de Experience Cloud en Forms adaptable requiere una licencia de Adobe Analytics, recopilación de datos (anteriormente, Adobe Launch) para administrar los scripts de seguimiento e integración con la API de Experience Platform Launch para optimizar la agregación de datos y la generación de perspectivas. Visita [Habilitar Adobe Analytics para un formulario adaptable mediante la automatización de la configuración de Experience Cloud](/help/forms/forms-experience-cloud-setup-automation.md) para obtener información completa sobre la configuración.

## Ver informe de Adobe Analytics de Forms adaptable {#view-adobe-analytics-report}

1. AEM En la instancia de la, vaya a **[!UICONTROL Forms]** >> **[!UICONTROL Forms y documento]**.
1. Seleccione el formulario y verá que Adobe Analytics está integrado, como se muestra a la izquierda, en el Forms activado para Adobe Analytics.

   ![Ver informe](assets/activ-aa.png)

1. Clic **Adobe Analytics** para ver el informe y analizar los datos de rendimiento.

## Explicación del informe de análisis de Forms adaptable {#understanding-aem-forms-analytics-reports}

Adobe Analytics ofrece una matriz completa de métricas de rendimiento de Forms adaptables diseñadas para proporcionar información valiosa sobre el uso del formulario. Estas métricas son:

### **¿Qué rendimiento tiene Forms adaptable?** {#how-your-adaptive-form-is-performing}

Tiene las métricas Representaciones de formularios, Envíos de formularios, Errores de validación y Visitantes únicos, que le permiten evaluar el uso y la eficacia de los formularios:

* **Representaciones de formularios**: las representaciones de formularios revelan el número de veces que se ha representado o abierto el formulario.

* **Envíos de formularios**: Los envíos de formularios indican la cantidad de veces que los usuarios completan y envían correctamente los formularios adaptables.

* **Errores de validación**: Error de validación muestra el número total de errores relacionados con la validación que se produjeron en los campos de los formularios.

* **Visitantes únicos**: Los visitantes únicos representan la cantidad de veces que un visitante procesa el formulario. Para obtener más información sobre los visitantes únicos, consulte [Visitantes únicos, visitas y comportamiento del cliente](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html).

  ![Rendimiento de Forms](assets/forms-performance.png)

### **Visitantes a sus formularios** {#visitors-to-your-forms}

Esto le permite obtener información valiosa sobre la actividad del visitante en los formularios:

* **Visitas y envíos**: Describe la frecuencia de visitas a los formularios en un intervalo de fechas y el número correspondiente de envíos de formularios, para obtener más información sobre este clic [Visitas](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html).
* **Visitantes únicos y sus visitas totales**: distingue entre los usuarios nuevos y los que regresan. Por ejemplo: un visitante puede llegar a su sitio todos los días durante un mes, pero contará como un visitante único. Visita [Visitantes únicos](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html) para obtener información detallada.

  ![Visitantes de Forms](assets/forms-visitors.png)

### **Tipo de dispositivo** {#device-type}

El tipo de dispositivo ayuda a identificar el tipo de dispositivo utilizado para acceder a los formularios. Clasifica el tipo de dispositivo como Tipo de dispositivo móvil. Por ejemplo, en este caso, es Tipo de dispositivo móvil: Otro y Tipo de dispositivo móvil: Teléfono móvil. Los distintos tipos de dispositivos móviles incluyen teléfono móvil, tableta, reproductor multimedia, consola de juegos y más.

![Tipo de dispositivo](assets/device-type.png)

### **Desglose geográfico** {#geographical-breakdown}

Muestra la ubicación desde la que se accede a Forms. Proporciona información específica de la región acerca de los usuarios del formulario; por ejemplo, puede ver que la información específica de la región acerca de un usuario del formulario es India, como se muestra en la imagen.

![desglose geográfico](assets/geographical-breakdown.png)

### **Principales fuentes de tráfico y formularios populares** {#top-sources-of-traffic-and-popular-forms}

Esto le ayuda a identificar la fuente principal o el vínculo desde el que se hace referencia a los formularios. Por ejemplo, en la imagen siguiente puede ver instancias de búsqueda de sus formularios adaptables donde el 18,9 % son **Escritos o marcadores**, 70,49 % basado en **Motores de búsqueda** y el 24 % son de **Otros sitios web**. Puede definir elementos de dimensión en función de sus necesidades. Además, puede averiguar cuáles son los formularios más visitados o populares.

![Sitios de referencia](assets/referred-sites.png)

### **Actividad del usuario en los formularios principales** {#user-activity-on-top-forms}

Una vista completa de la participación del usuario en las visitas de campo, las representaciones de formularios, los errores de validación, los formularios abandonados y los envíos de formularios proporciona información sobre los formularios más activos. En la imagen que se muestra a continuación, verá que el formulario de solicitud es el más activo, según las métricas de Evento de formulario.

![user-activity](assets/user-activity.png)

### **Cronología del tiempo empleado en los formularios** {#timeline-for-time-spent-on-forms}

Es el tiempo que los usuarios invierten en los formularios a lo largo del tiempo, lo que le ayuda a identificar los patrones de participación.

![time-spent-on-forms](assets/time-spent-on-forms.png)

### **Áreas en las que los visitantes requieren ayuda para rellenar el formulario** {#areas-requiring-assistance}

Las métricas como las vistas de ayuda, los errores de validación y las visitas a los campos revelan dónde necesitan asistencia los usuarios o cómo podemos rastrear errores en los campos. Por ejemplo, en la siguiente imagen puede ver que en un formulario con campos como **Nombre completo**, **Número de teléfono**, **DoB**. El **Nombre completo** El campo tiene 12 visitas, de las 12 visitas, 8 visitas tienen error de validación y 1 hizo clic en el icono de ayuda para ver la ayuda en este campo. Se pueden ver los datos de métricas de otros campos de formulario.

![áreas de asistencia](assets/assisting-areas.png)

### **El último campo de formulario que vieron los visitantes antes de abandonar el formulario** {#last-form-field-that-visitors-viewed}

Le ayuda a analizar los campos del formulario en los que los usuarios han invertido tiempo antes de abandonarlo. Por ejemplo, en la siguiente imagen, de 5 formularios abandonados, quedan 2 en el campo **Nombre completo**, quedan 2 en el campo **Número de teléfono** y 1 izquierda en el campo **Entrada de texto**.

![field-visitors](assets/field-visitors.png)