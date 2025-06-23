---
title: Visualización y comprensión de los informes de análisis de formularios adaptables
description: Los formularios adaptables se integran fácilmente con Adobe Analytics para capturar y realizar un seguimiento de las métricas de rendimiento de los formularios y documentos publicados.
keywords: Visualización y comprensión de los informes de análisis de formularios adaptables, el informe de análisis de Adobe, el informe de análisis de formularios
topic-tags: develop
feature: Adaptive Forms
role: Admin, User
level: Intermediate
exl-id: 756dee1f-4685-4783-961d-b172a5bd0692
source-git-commit: 56a3d50d7cc8db532097b97f0898f87fc6ba0b3d
workflow-type: ht
source-wordcount: '984'
ht-degree: 100%

---

# Visualización y comprensión de los informes de análisis de formularios adaptables {#viewing-and-understanding-aem-forms-analytics-reports}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Este artículo |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html?lang=es) |

En el panorama en rápida evolución del análisis digital, es imprescindible estar al tanto de las tendencias globales para tomar decisiones fundamentadas y optimizar las experiencias digitales. Para solucionarlo, los formularios adaptables se integran perfectamente con Adobe Analytics para capturar y realizar un seguimiento de las métricas de rendimiento de los formularios y documentos publicados. El objetivo detrás del análisis de estas métricas es tomar decisiones basadas en datos, utilizando métricas y análisis para mejorar la facilidad de uso y la eficacia de los formularios.

Al capturar y rastrear los indicadores de rendimiento clave, las empresas pueden identificar áreas de mejora, optimizar las experiencias de los usuarios y, en última instancia, impulsar mejores resultados para crear experiencias de cliente excepcionales.

## Configuración de Adobe Analytics en los formularios adaptables {#setup-adobe-analytics-to-aem-forms}

Para el informe de análisis de AEM, primero debe integrar Adobe Analytics en AEM Forms mediante la automatización de la configuración de Experience Cloud. La automatización de la configuración de Experience Cloud en los formularios adaptables requiere una licencia de Adobe Analytics, recopilación de datos (anteriormente, Adobe Launch) para administrar scripts de seguimiento, y la integración con la API de Experience Platform Launch para agilizar la agregación de datos y la generación de información. Visite [Habilitar Adobe Analytics para un formulario adaptable mediante la automatización de la configuración de Experience Cloud](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md) para obtener información completa sobre la configuración.

>[!CAUTION]
>
>La funcionalidad de automatización de la configuración de Experience Cloud está en desuso.

## Ver informe de Adobe Analytics de Formularios adaptables {#view-adobe-analytics-report}

1. En la instancia de AEM, vaya a **[!UICONTROL Formularios]** >> **[!UICONTROL Formularios y documento]**.
1. Seleccione el formulario y verá que Adobe Analytics está integrado, como se muestra a la izquierda, en el Forms activado para Adobe Analytics.

   ![Ver informe](assets/activ-aa.png){width="100%"}

1. Haga clic en **Adobe Analytics** para ver el informe y analizar los datos de rendimiento.

## Comprensión del informe de análisis de formularios adaptables {#understanding-aem-forms-analytics-reports}

Adobe Analytics ofrece una matriz completa de métricas de rendimiento de Formularios adaptables diseñadas para proporcionar información valiosa sobre el uso del formulario. Estas métricas son las siguientes:

### **¿Cuál es el rendimiento de los formularios adaptables?** {#how-your-adaptive-form-is-performing}

Dispone las métricas de representaciones de formularios, envíos de formularios, errores de validación y visitantes únicos, lo que le permite evaluar el uso y la eficacia de los formularios:

* **Representaciones de formularios**: las representaciones de formularios revelan el número de veces que se ha representado o abierto el formulario.

* **Envíos de formularios**: los envíos de formularios indican la cantidad de veces que los usuarios completan y envían correctamente los formularios adaptables.

* **Errores de validación**: muestran el número total de errores relacionados con la validación que se han producido en los campos de los formularios.

* **Visitantes únicos**: representan la cantidad de veces que un visitante accede al formulario. Para obtener más información sobre los visitantes únicos, consulte [Visitantes únicos, visitas y comportamiento del cliente](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html?lang=es).

  ![Rendimientos de los formularios](assets/forms-performance.png){width="100%"}

### **Visitantes de sus formularios** {#visitors-to-your-forms}

Le permite obtener información valiosa sobre la actividad del visitante en los formularios:

* **Visitas y envíos**: describe la frecuencia de visitas a los formularios en un intervalo de fechas y el número correspondiente de envíos de formularios. Para obtener más información al respecto, haga clic en [Visitas](https://experienceleague.adobe.com/docs/analytics/components/metrics/visits.html?lang=es).
* **Visitantes únicos y sus visitas totales**: distingue entre los usuarios nuevos y los que regresan. Por ejemplo: un visitante puede acceder a su sitio todos los días durante un mes, pero seguirá contando como un visitante único. Visite [Visitantes únicos](https://experienceleague.adobe.com/docs/analytics/components/metrics/unique-visitors.html?lang=es) para obtener información detallada.

  ![Visitantes de formularios](assets/forms-visitors.png){width="100%"}

### **Tipo de dispositivo** {#device-type}

El tipo de dispositivo ayuda a identificar el tipo de dispositivo que se utiliza para acceder a los formularios. Clasifica el tipo de dispositivo como Tipo de dispositivo móvil. Por ejemplo, en este caso, es Tipo de dispositivo móvil: Otro y Tipo de dispositivo móvil: Teléfono móvil. Los distintos tipos de dispositivos móviles incluyen teléfono móvil, tableta, reproductor multimedia, consola de juegos, etc.

![Tipo de dispositivo](assets/device-type.png){width="100%"}

### **Desglose geográfico** {#geographical-breakdown}

Muestra la ubicación desde la que se accede a Forms. Proporciona información específica de la región acerca de los usuarios del formulario; por ejemplo, puede ver que la información específica de la región acerca de un usuario del formulario es India, como se muestra en la imagen.

![Desglose geográfico](assets/geographical-breakdown.png){width="100%"}

### **Principales fuentes de tráfico y formularios populares** {#top-sources-of-traffic-and-popular-forms}

Esto le ayuda a identificar la fuente principal o el vínculo desde el que se hace referencia a los formularios. Por ejemplo, en la imagen siguiente puede ver instancias de búsqueda de sus formularios adaptables donde el 18,9 % son **Escritos o añadidos como marcador**, 70,49 % basado en **Motores de búsqueda**, y el 24 % son de **Otros sitios web**. Puede definir elementos de dimensión en función de sus necesidades. Además, puede averiguar cuáles son los formularios más visitados o populares.

![Sitios recomendados](assets/referred-sites.png){width="100%"}

### **Actividad del usuario en los formularios principales** {#user-activity-on-top-forms}

Una vista completa de la participación del usuario en las visitas de campo, las representaciones de formularios, los errores de validación, los formularios abandonados y los envíos de formularios proporciona información sobre los formularios más activos. En la imagen que se muestra a continuación, verá que el formulario de solicitud es el más activo, según las métricas de Evento de formulario.

![Actividad de usuario](assets/user-activity.png){width="100%"}

### **Cronología del tiempo empleado en los formularios** {#timeline-for-time-spent-on-forms}

Es el tiempo que los usuarios invierten en los formularios a lo largo del tiempo, lo que le ayuda a identificar los patrones de participación.

![Tiempo empleado en los formularios](assets/time-spent-on-forms.png){width="100%"}

### **Áreas en las que los visitantes requieren ayuda para rellenar el formulario** {#areas-requiring-assistance}

Las métricas como las vistas de ayuda, los errores de validación y las visitas a los campos revelan dónde necesitan asistencia los usuarios o cómo podemos rastrear errores en los campos. Por ejemplo, en la siguiente imagen puede ver que en un formulario con campos como **Nombre completo**, **Número de teléfono**, **DoB**. El campo **Nombre completo** tiene 12 visitas, de las 12 visitas, 8 visitas tienen error de validación y 1 hizo clic en el icono de ayuda para ver la ayuda en este campo. Se pueden ver los datos de métricas de otros campos de formulario.

![Áreas de asistencia](assets/assisting-areas.png){width="100%"}

### **El último campo de formulario que vieron los visitantes antes de abandonar el formulario** {#last-form-field-that-visitors-viewed}

Le ayuda a analizar los campos del formulario en los que los usuarios han invertido tiempo antes de abandonarlo. Por ejemplo, en la siguiente imagen, de 5 formularios abandonados, quedan 2 en el campo **Nombre completo**, quedan 2 en el campo **Número de teléfono**, y queda 1 en el campo **Entrada de texto**.

![Visitantes del campo](assets/field-visitors.png){width="100%"}

## Consulte también {#see-also}

* [Habilitar Adobe Analytics para un formulario adaptable mediante la automatización de la configuración de Experience Cloud](/help/forms/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.md)
* [Agregar un formulario adaptable a una página de AEM Sites o a un fragmento de experiencia](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Integración de AEM Forms con Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)
