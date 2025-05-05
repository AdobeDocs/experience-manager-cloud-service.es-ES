---
title: Conexión de AEM Forms con Adobe Experience Platform (AEP) | Guía de integración de datos
description: Aprenda a integrar AEM Forms con Adobe Experience Platform para aprovechar los perfiles de los clientes, enviar datos de formulario y crear experiencias personalizadas. Guía paso a paso.
contentOwner: Khushwant Singh
docset: CloudService
role: Admin, Developer, User
feature: Adaptive Forms, Core Components
source-git-commit: 4144c726a6f8551df9497732c2ca95b8eec5c63a
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 1%

---


# Integración de AEM Forms con Adobe Experience Platform (AEP) {#aem-forms-aep-integration}

<span class="preview"> La capacidad de conexión de Forms adaptable (AEM Forms) con Adobe Experience Platform (AEP) se encuentra en el programa de acceso anticipado. Para solicitar acceso a la funcionalidad, simplemente envía un correo electrónico desde tu dirección oficial a [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D). También puede visitar la página <a href="/help/forms/early-access-ea-features.md">Programa de acceso anticipado </a>para descubrir todas las innovaciones y capacidades disponibles. . </span>

## Información general {#overview}

Puede conectar AEM Forms con Adobe Experience Platform para transformar las experiencias de los formularios. Esta potente integración permite a las organizaciones aprovechar los perfiles de clientes en tiempo real para experiencias de formulario personalizadas, optimizar el envío de datos de **AEM Forms a Experience Platform** y crear registros de clientes unificados en todo el ecosistema de Adobe. Al conectar los formularios adaptables con las sólidas capacidades de administración de datos de Experience Platform, puede crear experiencias más relevantes y mejorar las tasas de conversión, al tiempo que mantiene una única fuente fiable para los datos de los clientes.

### ¿Qué es el conector de AEM Forms para Adobe Experience Platform (AEP)? {#what-is-connector}

El conector AEM Forms para Adobe Experience Platform (AEP) es un conector predeterminado (OOTB) proporcionado por AEM Forms que permite una integración perfecta entre AEM Forms y Adobe Experience Platform (AEP). Esta integración le permite crear formularios utilizando esquemas XDM disponibles en AEP y enviar datos de nuevo a AEP para fines de personalización e hidratación de perfiles.

## ¿Por qué conectar AEM Forms con Adobe Experience Platform (AEP)? {#benefits}

La conexión de su Forms adaptable con Adobe Experience Platform ofrece ventajas significativas tanto para su organización como para sus clientes:

* **Perfiles de cliente unificados**: enriquezca los perfiles de cliente con datos de envío de formularios y cree una vista completa de las interacciones y preferencias del cliente
* **Experiencias de formulario personalizadas**: aproveche los datos de perfil existentes para rellenar previamente campos y personalizar formularios basados en información conocida de clientes
* **Recopilación de datos optimizada**: capture datos de formulario directamente en conjuntos de datos de AEP sin crear conectores personalizados ni código de integración
* **Activación de datos en tiempo real**: envíe datos de envío de formularios a otras aplicaciones de Adobe a través de Real-Time CDP para su activación inmediata
* **Administración simplificada del cumplimiento**: administre directivas de consentimiento y control de datos de forma centralizada a través de AEP
* **Tiempo de desarrollo reducido**: elimine el trabajo de integración personalizada con un conector generado previamente que siga las prácticas recomendadas
* **Enriquecimiento del perfil del cliente con datos de formulario**: actualice y mejore automáticamente los perfiles del cliente con cada envío de formulario, lo que creará perspectivas del cliente más detalladas

## Funciones principales {#key-features}

* Creación de formularios con esquemas XDM de AEP
* Enviar datos de formulario a AEP para su personalización
* Compatibilidad con la ingesta de datos de streaming
* Habilitar la hidratación de perfiles para mejorar las experiencias del usuario
* Integración con el sistema de perfiles de AEP
* Integración de esquemas XDM con formularios adaptables para la recopilación de datos estandarizada
* Conexión de flujo continuo de AEP para formularios que permiten el procesamiento de datos en tiempo real

El siguiente vídeo proporciona una guía paso a paso sobre los requisitos previos (como crear un esquema, configurar datos y autenticarse) y muestra cómo crear y conectar Forms adaptable a Adobe Experience Platform (AEP)

>[!VIDEO](https://video.tv.adobe.com/v/3457850/)

## Requisitos previos {#prerequisites}

Antes de configurar el conector de AEP en AEM Forms, asegúrese de completar lo siguiente en Adobe Experience Platform:

1. Configuración del esquema
   * [Crear un esquema XDM](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/tutorials/create-schema-ui)
   * [Habilitar esquema para la generación de perfiles](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)
   * [Definir campo de identidad](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/tutorials/create-schema-ui#profile)

2. Configuración de datos
   * [Crear un conjunto de datos](https://experienceleague.adobe.com/es/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-datasets)
   * [Configure la conexión de flujo continuo](https://experienceleague.adobe.com/es/docs/experience-platform/ingestion/tutorials/create-streaming-connection) (necesita la dirección URL del extremo de flujo continuo más tarde, así que anótela ahora).

3. Autenticación
   * [Generar credenciales de API](https://experienceleague.adobe.com/es/docs/experience-platform/landing/platform-apis/api-authentication#generate-credentials) (ID de cliente y secreto de cliente) desde Adobe Developer Console


## Pasos de implementación

### 1. Crear la configuración de nube de AEP

1. Vaya a su **instancia de Adobe Experience Manager** > **Herramientas** > **Cloud Services** > **Adobe Experience Platform**.
1. Seleccione un **contenedor de configuración** para almacenar la configuración.
1. Haga clic en **Crear** para abrir el asistente de configuración de AEP
1. Introduzca la siguiente información:
   * Título
   * ID de cliente (obtenido de la consola de desarrollador)
   * Secreto de cliente (obtenido de la consola de desarrollador)
   * URL de OAuth (hay una URL predeterminada, pero también se puede obtener desde Developer Console)

1. Haga clic en **Conectar** para establecer la conexión. Después de establecer la conexión, configure estas opciones adicionales:
   * URL básica: platform.adobe.io (esta es una URL predeterminada que también se puede obtener desde la consola de desarrollador; las URL de oauth y de plataforma tienen de forma predeterminada las URL de producción). En este caso, es necesario conectarse a stage; se deben utilizar las URL de stage).
   * ID de organización (se obtiene de la consola de desarrollador junto con el ID/secreto de cliente)
   * Nombre de la zona protegida (necesario para los entornos de desarrollo y producción)

### 2. Creación de formularios con integración de esquemas XDM {#form-creation}

1. Acceda al asistente de creación de formularios:
   * Vaya a su **instancia de Adobe Experience Manager** > **Forms** > **Forms y documentos**.
   * Haga clic en **Crear** > **Formulario adaptable**.
1. En la ficha **origen**, seleccione una plantilla
1. En la ficha **Datos**, seleccione la opción **Adobe Experience Platform**.

1. En el panel de propiedades, seleccione la configuración de nube. El sistema carga todos los esquemas disponibles de Adobe Experience Platform

   >[!NOTE]
   >
   >
   > * Solo se recuperan los esquemas habilitados para perfiles y no generados por el sistema.
   > * La carga inicial del esquema puede tardar algún tiempo en configurarse por primera vez.
1. Seleccione los campos adecuados/obligatorios del esquema. (Vea el vídeo para ver los pasos detallados)
1. En la pestaña Envío:
   * Seleccione la acción de envío **Enviar a Adobe Experience Platform**
   * Configure las opciones de envío de formularios para **Envío de datos de AEM Forms a Experience Platform**
1. En el panel de propiedades:
   * Añada la URL de flujo continuo (obtenida desde Orígenes de AEP > Conexión de flujo continuo).
   * Añada el ID del flujo de datos (que se encuentra en Fuentes de AEP > Flujo > Información de uso de API)
1. Haga clic en **Guardar**. Proporcione los detalles del formulario:
   * Título
   * Nombre
   * Ruta de almacenamiento
1. Agregue el botón Enviar al formulario. El formulario está listo para enviar datos a AEP.


## Notas importantes {#important-notes}

* Los datos enviados a través de formularios se vuelven visibles en AEP después de aproximadamente 10-15 minutos
* De forma predeterminada, solo se muestran los esquemas habilitados para perfiles
* Aunque el envío de datos funciona para todos los esquemas, la funcionalidad de relleno previo se limita a los esquemas con perfil habilitado
* Los datos de esquemas no habilitados para perfiles no se utilizarán para la creación de perfiles, aunque el esquema esté habilitado posteriormente para la generación de perfiles
* **El enriquecimiento del perfil del cliente con datos de formulario** requiere la configuración adecuada del campo de identidad en el esquema XDM
* **El envío de datos de AEM Forms a Experience Platform** usa **conexión de flujo continuo de AEP para formularios** para garantizar el flujo de datos en tiempo real

## Prácticas recomendadas {#best-practices}

1. Planifique con cuidado la estructura del esquema antes de habilitar la creación de perfiles
1. Tenga en cuenta los requisitos de escalado del sistema y volumen de datos al configurar la conexión de flujo continuo de **AEP para los formularios**
1. Pruebe la integración exhaustivamente antes de la implementación de producción
1. Monitorización de los procesos de ingesta de datos y creación de perfiles
1. Diseñe su integración de esquema **XDM con formularios adaptables** para recopilar solamente los datos necesarios
1. Use **enriquecimiento del perfil del cliente con datos de formulario** estratégicamente para mejorar la personalización

## Consideraciones técnicas {#technical-considerations}

* El conector utiliza las API de flujo público para el envío de datos
* La creación del perfil se basa en el campo de identidad
* La unificación de datos se produce automáticamente en AEP
* La integración admite la creación de formularios nuevos y la modificación de formularios existentes
* La integración del esquema XDM con los formularios adaptables estandariza la estructura de datos en diferentes puntos de contacto
* La conexión de flujo continuo de AEP para formularios proporciona funciones de ingesta de datos en tiempo real

## Preguntas frecuentes {#faq}

### Preguntas generales {#general-questions}

**Q: ¿Puedo usar este conector con cualquier versión de AEM Forms?**
R: No, esta integración solo está disponible para AEM Forms as a Cloud Service en el programa de acceso anticipado.

**Q: ¿Funciona este conector con los componentes principales de Forms adaptable y los componentes de base?**
R: Este conector funciona mejor con los componentes principales de Forms adaptable, que es el método recomendado para todos los formularios nuevos.

**Q: ¿Puedo enviar datos a varios conjuntos de datos de AEP desde un solo formulario?**
R: Actualmente, cada formulario solo puede enviarse a un conjunto de datos. Para varios envíos de conjuntos de datos, debería crear flujos de trabajo personalizados.

**Q: ¿Hay un límite en la cantidad de envíos de formularios que se pueden procesar?**
R: Los envíos de formularios están sujetos a las cuotas de ingesta de transmisión de AEP y a los límites de tasa.

**Q: ¿Se pueden enviar datos adjuntos de formularios a AEP?**
R: No, los archivos adjuntos del formulario no se pueden enviar directamente a AEP. Debe almacenar los archivos adjuntos por separado y solo enviar metadatos a AEP.

### Preguntas de implementación {#implementation-questions}

**Q: ¿Cómo puedo solucionar problemas de conexión entre AEM Forms y AEP?**
R: Compruebe los ajustes de configuración en la nube, asegúrese de que las credenciales de la API son correctas y que la dirección URL del extremo de flujo continuo está configurada correctamente.

**Q: ¿Puedo usar esquemas XDM personalizados con esta integración?**
R: Sí, puede utilizar cualquier esquema XDM personalizado siempre y cuando esté configurado correctamente en AEP y, para la funcionalidad de relleno previo, esté habilitado para los perfiles.

**Q: ¿Cómo habilito el relleno previo de formularios con datos de perfil de AEP?**
R: Asegúrese de que el esquema tenga habilitado el perfil y de que el formulario esté configurado para utilizar el mismo campo de identidad definido en el esquema.

**Q: ¿Qué sucede si necesito transformar datos antes de enviarlos a AEP?**
R: Puede utilizar reglas de formularios o funciones personalizadas para transformar los datos antes del envío. Para transformaciones complejas, considere la posibilidad de utilizar una acción de envío personalizada.

**Q: ¿Puedo usar esta integración en un modelo de implementación híbrido?**
R: No, esta integración es específica de AEM Forms as a Cloud Service.

## Resumen y pasos siguientes {#summary-next-steps}

La integración de AEM Forms con Adobe Experience Platform permite a las organizaciones crear un flujo de datos fluido entre los formularios y el ecosistema de Experience Platform en general. Esta integración le permite crear experiencias de formulario más personalizadas, optimizar la recopilación de datos y mejorar los perfiles de los clientes con datos valiosos de envío de formularios.

Para empezar con esta integración:

1. **Solicitar acceso** - Si aún no lo ha hecho, únase al programa Acceso anticipado poniéndose en contacto con [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com?subject=Request%20for%20Early%20Access%20to%20AEP%20Connector%20\(AEM%20Forms%20Integration%20with%20Adobe%20Experience%20Platform\)&body=Dear%20AEM%20Forms%20Team%2C%0D%0A%0D%0AI%20hope%20this%20message%20finds%20you%20well.%0D%0A%0D%0AI%20am%20writing%20to%20request%20access%20to%20the%20Early%20Access%20Program%20for%20the%20AEP%20Connector%2C%20which%20enables%20integration%20between%20AEM%20Forms%20and%20Adobe%20Experience%20Platform.%0D%0A%0D%0AOrganization%20Name%3A%20%5BYour%20organization%20name%5D%0D%0AOrganization%20ID%3A%20%5BYour%20organization%20ID%2C%20if%20available%5D%0D%0AUse%20Case%3A%20%5BBriefly%20describe%20your%20intended%20use%20case%2C%20including%20goals%20or%20benefits%20you%20aim%20to%20achieve%20with%20the%20integration%5D%0D%0A%0D%0AThank%20you%20for%20your%20time%20and%20consideration.%0D%0A%0D%0ABest%20regards%2C%0D%0A%5BYour%20Full%20Name%5D%0D%0A%5BYour%20Job%20Title%2C%20if%20applicable%5D%0D%0A%5BYour%20Contact%20Information%2C%20if%20appropriate%5D)
2. **Prepare su entorno**. Asegúrese de que dispone de los permisos y configuraciones necesarios tanto en AEM Forms como en Adobe Experience Platform
3. **Siga los pasos de implementación**. Use la guía anterior para configurar la nube y crear su primer formulario conectado a AEP con integración de esquema XDM
4. **Realizar pruebas exhaustivas**: valide las capacidades de envío de datos y relleno previo en un entorno de desarrollo
5. **Plan de producción**: colabore con su equipo de implementación para programar la implementación del envío de datos de AEM Forms a Experience Platform en producción

## Recursos relacionados {#related-resources}

* [Documentación de AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html?lang=es)
* [Documentación de Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html?lang=es)
* [Información general del sistema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=es)
* [Ingesta de transmisión en Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=es)
* [Información general del perfil del cliente en tiempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=es)
* [Funciones de acceso anticipado de AEM Forms](/help/forms/early-access-ea-features.md)
* [Creación de Forms adaptable con componentes principales](/help/forms/creating-adaptive-form-core-components.md)
* [Uso de modelos de datos de formulario en AEM Forms](/help/forms/using-form-data-model.md)

<!--
Schema markup for technical documentation
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "Connect AEM Forms with Adobe Experience Platform (AEP) | Data Integration Guide",
  "description": "Learn how to integrate AEM Forms with Adobe Experience Platform to leverage customer profiles, submit form data, and create personalized experiences.",
  "datePublished": "2025-05-28",
  "author": {
    "@type": "Corporation",
    "name": "Adobe"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Adobe Experience League",
    "logo": {
      "@type": "ImageObject",
      "url": "https://experienceleague.adobe.com/assets/img/favicons/apple-touch-icon.png"
    }
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/aem-forms-aep-connector.html"
  },
  "articleSection": "AEM Forms",
  "keywords": "AEM Forms, Adobe Experience Platform, XDM schema, data integration, form submission, customer profiles, personalization"
}
-->


