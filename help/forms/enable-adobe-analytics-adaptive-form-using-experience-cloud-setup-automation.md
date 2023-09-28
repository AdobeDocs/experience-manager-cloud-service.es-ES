---
title: Habilitar Adobe Analytics para un formulario adaptable
description: La automatización de la configuración de Experience Cloud ayuda a conectar Adobe Analytics a un formulario adaptable para realizar un seguimiento de las perspectivas sobre las interacciones y la participación de los visitantes.
keywords: Habilitar Adobe Analytics para un formulario adaptable mediante la automatización de la configuración del Experience Cloud, habilitar Adobe Analytics en Forms, Adobe Analytics en Forms adaptable, integración de Forms Analytics, Forms y Adobe Analytics
source-git-commit: 4daba42c9d8a7eff5d3ef6f9581c52c787666ed1
workflow-type: tm+mt
source-wordcount: '1591'
ht-degree: 7%

---


# Habilitar Adobe Analytics para un formulario adaptable mediante la automatización de la configuración de Experience Cloud {#integrate-adobe-analytics-to-aem-forms-with-experience-cloud-setup-automation}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM as a Cloud Service | Este artículo |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/integrate-aem-forms-with-experience-cloud-solutions/configure-analytics-forms-documents.html) |

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

![Informe de Analytics](assets/analytics-report.png){width="100%"}


Para obtener información detallada sobre cada métrica, visite [Ver y comprender los informes de AEM Forms Analytics](/help/forms/view-understand-aem-forms-analytics-reports.md)

## Requisitos previos {#prerequisites}

<!--
Analytics, Data Collection (Formerly Adobe Launch), and Experience Manager (experience.adobe.com)
-->

La automatización de la configuración de Experience Cloud requiere un **Licencia de Adobe Analytics**, **Recopilación de datos (anteriormente, Adobe Launch)** para administrar scripts de seguimiento, y **Licencia de Experience Manager Forms** para una agregación de datos y generación de perspectivas optimizadas.

Si tiene una licencia activa para **Adobe Analytics** y **Experience Manager Forms**, y tiene integración con **Recopilación de datos (anteriormente, Adobe Launch)**, debe verificar su disponibilidad en la consola para desarrolladores.

Para comprobar que las opciones mencionadas están disponibles para su entorno as a Cloud Service de Forms, visite la [consola para desarrolladores](https://developer.adobe.com/console/projects), vaya al proyecto y busque el proyecto con el id de programa o el id de entorno, por ejemplo, para el entorno con URL `https://author-p45913-e175111-cmstg.adobeaemcloud.com/index.html`, id de programa - id de entorno es `p45913-e175111`. Asegúrese de que la automatización de la configuración del Experience Cloud, Adobe Analytics y la API del Experience Platform Launch aparecen en la lista. Si aparece, puede habilitar Adobe Analytics para su Forms adaptable.

![Requisito previo para la integración con Forms Analytics](assets/analytics-aem.png){width="100%"}

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

>[!VIDEO](https://video.tv.adobe.com/v/3424577/enable-adobe-analytics/?quality=12&learn=on)


<!--
>[!NOTE]
>
> This is the demo video for **Foundation Component**. In **Core Component** you are required to perform similar steps but the container is not chosen for forms.
-->

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

![AEM Análisis integrado](assets/analytics-aem-integrated.png){width="100%"}


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

   ![Ver informe](assets/activ-aa.png){width="100%"}

1. Clic **Adobe Analytics** para ver el informe y analizar los datos de rendimiento.

Para conectar un formulario adaptable con Adobe Analytics mediante el método manual, visite [Integración de AEM Forms con Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md).

## Habilitar Analytics en Forms adaptable en Sites {#Connect-Analytics-to-Adaptive-Forms-in-Sites}

La configuración de análisis para el formulario adaptable en AEM Sites le ayuda a rastrear las interacciones de los usuarios y los envíos de formularios en el formulario de la página de Sites. Al integrar sin problemas los análisis en su Forms de Sites, obtiene una valiosa perspectiva del comportamiento del usuario, las tasas de conversión y las áreas para mejorar en su formulario.

### Requisitos previos {#Prerequisites-to-connect-forms-analytics-to-sites}

Para conectarse y habilitar Analytics en Forms adaptable para AEM Sites, debe asegurarse de que su AEM Sites tenga un Adobe Analytics activo.

### Conectar Forms adaptable en Sites para habilitar Analytics {#Connect-analytics-to-adaptive-forms}

Para conectar un formulario adaptable en una página de AEM Sites para habilitar Analytics, incluya el `customfooterlibs` de cliente a la página AEM Sites AEM mediante el repositorio de tipo de archivo/Git y la canalización de implementación de.

1. Abra su proyecto de [Arquetipo de AEM Forms o repositorio de Git clonado](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=es) en un editor de texto. Por ejemplo, código de Visual Studio.

1. Navegue hasta la página de Sites donde exista su formulario adaptable; por ejemplo, en este proyecto de demostración tenemos lo siguiente `ui.apps/src/main/content/jcr_root/apps/corecomponents/components/page/.content.xml`.

1. Copiar el valor de `sling:resourceSuperType`. Por ejemplo, el valor es `core/wcm/components/page/v3/page`.

   ![recurso de sling](/help/forms/assets/slingresource.png){width="100%"}

1. Crear una estructura similar en la ubicación `ui.apps/src/main/content/jcr_root/apps` igual que `core/wcm/components/page/v3/page`.

   ![estructura de superposición](/help/forms/assets/overlaystructure.png){width="100%"}

1. Añadir un `customfooterlibs.html` archivo.

       &quot;
       // customheaderlibs.html
       &lt;sly data-sly-use.page=&quot;com.adobe.cq.wcm.core.components.models.Page&quot;>
       &lt;sly data-sly-test=&quot;${page.data &amp;&amp; page.dataLayerClientlibIncluded}&quot; data-sly-call=&quot;${clientlib.js @ categories=&amp;#39;core.forms.components.commons.v1.datalayer&amp;#39;, async=true}&quot;>&lt;/sly>
       &lt;/sly>
       
       &quot;
   
   El `customfooterlibs.html` se utiliza para JavaScript.

1. [Ejecución de la canalización](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=es) para implementar los cambios.

### Habilitación de reglas de Form Analytics para Forms en Sites {#bind-forms-analytics-rules-to-forms-in-sites}

1. Visite la **Recopilación de datos de Adobe Experience Platform**.
1. Clic **Etiquetas** situado en el lado izquierdo.
1. Busque su proyecto con el ID de programa como se muestra en la siguiente imagen, por ejemplo, para el entorno con URL `https://author-p45921-e175111-cmstg.adobeaemcloud.com/index.html`, el id del programa es `45921`.

   ![Search-your-form-in-data-collection](/help/forms/assets/aep-data-collection.png){width="100%"}

1. Añadir configuración para **Reglas de formulario** y **Elementos de datos** como se indica a continuación:

#### Agregar reglas de formulario {#form-rules}

1. Seleccione el formulario y añada **Nueva propiedad** situado en la esquina superior derecha, o haga clic en el formulario.
1. En la página de propiedades, haga clic en **Reglas** y seleccione eventos para el formulario. En la siguiente imagen de ejemplo, se muestra **Eventos de formulario**.

   ![Search-your-form-in-data-collection](/help/forms/assets/aep-form-event-properties.png){width="100%"}

1. Seleccione todos los eventos del formulario y **copia** que se encuentra en el carril superior derecho.
1. Una vez copiado, un **Copiar regla** La ventana emergente aparece donde busca en la página de Sites con el ID del proyecto para pegar las reglas del formulario.

   ![Copy-form-rules](/help/forms/assets/copy-form-rules.png){width="100%"}

1. Clic **copia** para pegar las reglas del formulario en la página de Sites.

#### Añadir elementos de datos {#data-elements}

1. Seleccione el formulario y añada **Nueva propiedad** situado en la esquina superior derecha, o haga clic en el formulario.
1. En la página de propiedades, haga clic en **Elementos de datos** y seleccione eventos para el formulario.
1. Seleccione todos los eventos del formulario y **copia** situado en el carril superior derecho.
1. Una vez copiado, un **Copiar regla** La ventana emergente aparece donde busca en la página de Sites con el ID del proyecto para pegar las reglas del formulario.
1. Clic **copia** para pegar las reglas del formulario en la página de Sites.

   ![Form-data-elements](/help/forms/assets/form-data-elements.png){width="100%"}

Una vez que haya enlazado las reglas de Forms y Sites a través de los pasos mencionados, realice los siguientes pasos para habilitar Analytics en su formulario adaptable en la página de Sites:

1. Clic **Flujo de publicación** a la izquierda.
1. Clic **Añadir biblioteca** y escriba el nombre que prefiera.
1. En el **Entorno** desplegable a la derecha, seleccione **desarrollo**.
1. Clic **Añadir todos los recursos modificados**.
1. Clic **Guardar y generar en desarrollo**.

![de publicación en desarrollo](/help/forms/assets/publish-to-dev.png){width="100%"}


<!--

## Best Practices

1.    Verify that Adobe Analytics is enabled on all the forms activated for Adobe Analytics.

1.    Check the Adobe Analytics report periodically to gain insights into user behavior and form performance. For instance, you may set the cadence to 15 days or the period you prefer to choose for report analysis. This enables you to improve the forms enrollment experience.

1.    Enable Analytics for all or most of your forms for tracking and analyzing user interaction with your forms and to gain insights into visitor interactions and engagement.

1. Check your forms performance after you update your form fields or components.

1.    Share Analytics report with your peer groups for review, you can schedule your report for a later time.

-->

## Vea también {#see-also}

* [Ver y comprender los informes de análisis de Forms adaptable](/help/forms/view-understand-aem-forms-analytics-reports.md)
* [Agregar un formulario adaptable a una página de AEM Sites o a un fragmento de experiencia](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
* [Integración de AEM Forms con Adobe Analytics](/help/forms/integrate-aem-forms-with-adobe-analytics.md)
