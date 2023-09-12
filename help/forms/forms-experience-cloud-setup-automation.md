---
title: Habilitar Adobe Analytics para un formulario adaptable mediante la automatización de la configuración de Experience Cloud
description: La automatización de la configuración de Experience Cloud ayuda a conectar Adobe Analytics a un formulario adaptable. Ayuda a rastrear y analizar la interacción del usuario con un formulario adaptable, lo que ofrece perspectivas sobre las interacciones y la participación de los visitantes.
source-git-commit: c88f8f61cf54059b1d141d08b77983dd45edfaa6
workflow-type: tm+mt
source-wordcount: '1011'
ht-degree: 2%

---


# Habilitar Adobe Analytics para un formulario adaptable mediante la automatización de la configuración de Experience Cloud {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

La automatización de la configuración del Experience Cloud ayuda a conectar Adobe Analytics con el Forms adaptable, lo que permite rastrear y analizar la interacción del usuario con los formularios y ofrecer perspectivas sobre las interacciones y la participación de los visitantes. La automatización de la configuración de Experience Cloud también ayuda a monitorizar el rendimiento del formulario, lo que implica evaluar métricas como las horas de finalización y los puntos de entrega. Este análisis ayuda a optimizar los formularios para una mejor experiencia del usuario, a la vez que distingue el comportamiento del usuario en función del estado de inicio de sesión, por ejemplo, de usuarios anónimos, para identificar tendencias y patrones generales.

## Ventajas de integrar Adobe Analytics con Forms adaptable {#advantages-of-integrating-adobe-analytics-with-aem-forms}

* **Perspectivas del comportamiento del usuario final**: Adobe Analytics ayuda a obtener perspectivas sobre el comportamiento del usuario final, revela las acciones de los usuarios, los abandonos y las tasas de finalización, lo que permite comprender mejor cómo los individuos se relacionan con los formularios.
* **Permitir que los usuarios empresariales no técnicos obtengan perspectivas**: Adobe Analytics, a través de su interfaz fácil de usar, permite que incluso los usuarios no técnicos accedan e interpreten los datos de uso del formulario, lo que fomenta las decisiones basadas en datos para mejorar las experiencias de inscripción.
* **Optimización de la experiencia de captura de datos en función del uso**: las organizaciones identifican fácilmente los puntos problemáticos de la captura de datos, lo que conduce a mejoras específicas que mejoran la facilidad de uso del formulario y aumentan los envíos exitosos.

## Ámbito de las métricas de uso de Forms adaptable {#scope-of-adaptive-forms-usage-metrics}

Adobe Analytics ofrece una matriz completa de métricas de rendimiento de Forms adaptables diseñadas para proporcionar información valiosa sobre el uso del formulario. Estas métricas son:

* **Representaciones de formularios, envíos de formularios, errores de validación y visitantes únicos**, lo que le permite evaluar el uso y la eficacia de los formularios.

* **Perspectivas del visitante** que incluyen frecuencias de visita y envío, y recuentos de visitantes únicos, lo que ofrece una vista completa de la audiencia del formulario.

* **Tipo de dispositivo** datos que le informan sobre los dispositivos que utilizan los usuarios para acceder a los formularios.

* **Desglose geográfico** revela la distribución regional de los usuarios del formulario.

* **Fuentes de tráfico** y **Formularios populares** Las métricas de que constan de los dominios de referencia principales y de los formularios más visitados le ayudan a comprender dónde se origina el tráfico y qué formularios son los más populares.

* **Actividad del usuario en los formularios principales** proporciona perspectivas sobre las visitas al campo, las representaciones de formularios, los errores de validación, los formularios abandonados y los envíos de formularios, lo que le permite analizar el comportamiento del usuario.

* **Cronología del tiempo empleado en los formularios** que ofrece una vista basada en la cronología de la participación del usuario en los formularios.

* **Áreas que requieren asistencia del visitante** métricas que incluyen vistas de ayuda, instancias de error de validación y frecuencias de visita de campo, lo que resalta dónde pueden necesitar ayuda los usuarios para rellenar los formularios.

![Informe de Analytics](assets/analytics-report.png)


Para obtener información detallada sobre cada métrica, visite [Ver y comprender los informes de AEM Forms Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Requisitos previos {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

La automatización de la configuración de Experience Cloud en Adobe Experience Manager Forms requiere un **Licencia de Adobe Analytics**, **Recopilación de datos (anteriormente, Adobe Launch)** para administrar los scripts de seguimiento y la integración con **Experience Platform Launch (API)** para una agregación de datos y generación de perspectivas optimizadas.

Si tiene una licencia activa para la automatización de la configuración de Experience Cloud, Adobe Analytics y la API de Experience Platform Launch, debe comprobar su disponibilidad en la consola de desarrollador.

Para comprobar que las opciones mencionadas están disponibles para su entorno as a Cloud Service de Forms, visite la [consola para desarrolladores](https://developer.adobe.com/console/projects), vaya al proyecto y busque el proyecto con el ID de programa, por ejemplo, para el entorno con URL `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`, el id del programa es `p45913-e175111`. Asegúrese de que la automatización de la configuración del Experience Cloud, Adobe Analytics y la API del Experience Platform Launch aparecen en la lista. Si aparece, puede habilitar Adobe Analytics para su Forms adaptable.

![Requisito previo para la integración con Forms Analytics](assets/analytics-aem.png)

<!-- 
>[!NOTE]
> If you have an active licenses for Experience Cloud Setup Automation, Adobe Analytics, and Experience Platform Launch API, you should verify their availability within your developer console.
-->

<!-- For more information about your available integrations, see [troubleshooting Adaptive Forms with Analytics Integration](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/view-understand-aem-forms-analytics-reports.html)
-->

## Configuración de Adobe Analytics {#configure-adobe-analytics}

Siga los pasos que se indican a continuación para habilitar y configurar Adobe Analytics para su Forms adaptable:

* [Habilitar Adobe Analytics para Forms adaptable basado en componentes de base](#integrate-adobe-analytics-with-aem-forms-for-foundation-component)
* [Habilitar Adobe Analytics para Forms adaptable basado en componentes principales](#integrate-adobe-analytics-with-aem-forms-for-core-components)

### Habilitar Adobe Analytics con el componente de Forms adaptable para base {#integrate-adobe-analytics-with-aem-forms-for-foundation-component}

1. Cree un contenedor de configuración para Cloud Services:
   1. Vaya a **[!UICONTROL Herramientas > General > Explorador de configuración]**.
   1. Seleccione o cree un contenedor de configuración y habilite la carpeta para **[!UICONTROL Configuraciones de nube]**.
   1. Pulse **[!UICONTROL Guardar y cerrar]** para guardar la configuración y salir del cuadro de diálogo.
1. AEM En la instancia de la, vaya a **[Forms]** >> **[Forms y documento]**.
1. Seleccione su **[!UICONTROL Form]** >> **[!UICONTROL Propiedades]**, en el **[!UICONTROL Contenedor de configuración]**, seleccione el contenedor de configuración que creó o seleccionó en la **[!UICONTROL Explorador de configuración]** en el paso 1.
1. Seleccione el Panel de tareas en el carril izquierdo y haga clic en **Análisis de configuración** y **Activar Adobe Analytics**.
1. Proporcione el nombre que prefiera para el grupo de informes y haga clic en **[!UICONTROL Siguiente]** y **[!UICONTROL Guardar]**.
1. Una vez guardado el proyecto, la configuración se ejecuta durante un tiempo hasta la integración de Adobe Analytics con el formulario adaptable. También puede comprobar el **estado de integración**.

   >[!NOTE]
   >
   >Si la configuración tarda más de 15 minutos, vuelva a intentar habilitar Analytics para los formularios.

1. AEM En la instancia de la, vaya a **[!UICONTROL Forms]** >> **[Forms y documento]** y seleccione su **[!UICONTROL Form]**, verá que Adobe Analytics está integrado en el formulario, como se muestra en la siguiente imagen.
1. Ahora puede ver su [Informe de Adobe Analytics de formulario adaptable](#view-adobe-analytics-report).

![AEM Análisis integrado](assets/analytics-aem-integrated.png)

### Habilitar Adobe Analytics con Forms adaptable para componentes principales {#integrate-adobe-analytics-with-aem-forms-for-core-components}

1. AEM En la instancia de la, vaya a **[!UICONTROL Forms]** >> **[!UICONTROL Forms y documento]** y seleccione su **[!UICONTROL Form]**.
1. Seleccione el Panel de tareas de la izquierda y haga clic en **Análisis de configuración** y **Activar Adobe Analytics**.
1. Proporcione el nombre que prefiera para el grupo de informes y haga clic en **[!UICONTROL Siguiente]** y **[!UICONTROL Guardar]**.
1. Una vez guardado el proyecto, la configuración se ejecuta durante un tiempo hasta la integración de Adobe Analytics con el formulario adaptable. También puede comprobar el **estado de integración**.

   >[!NOTE]
   >
   >Si la configuración tarda más de 15 minutos, vuelva a intentar habilitar Analytics para los formularios.

1. AEM En la instancia de la, vaya a **[!UICONTROL Forms]** >> **[!UICONTROL Forms y documento]** y seleccione su **[!UICONTROL Form]**, verá que Adobe Analytics está integrado en el formulario.
1. Ahora puede ver su [Informe de Adobe Analytics de formulario adaptable](#view-adobe-analytics-report).

## Ver informe de Adobe Analytics de Forms adaptable {#view-adobe-analytics-report}

1. AEM En la instancia de la, vaya a **[!UICONTROL Forms]** >> **[!UICONTROL Forms y documento]**.
1. Seleccione el formulario y verá que Adobe Analytics está integrado, como se muestra a la izquierda, en el Forms activado para Adobe Analytics.

   ![Ver informe](assets/activ-aa.png)

1. Clic **Adobe Analytics** para ver el informe y analizar los datos de rendimiento.


Para conectar un formulario adaptable con Adobe Analytics mediante un método antiguo, visite [Integración de AEM Forms con Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md).
