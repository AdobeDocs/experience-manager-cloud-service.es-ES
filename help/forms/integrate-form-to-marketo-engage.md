---
Title: How to Integrate Marketo Engage with AEM Forms?
Description: Learn how to integrate your Marketo Engage instance with AEM Forms.
Keywords: How to connect a Marketo instance with form? , Connect a form to Marketo, Integrate a form with Marketo Engage, Integrate an Adaptive Form with a Marketo instance.
Feature: Adaptive Forms, Form Data Model
Role: User, Developer
exl-id: 74cd25f9-1ee1-4f3f-8e02-8714071e7c86
source-git-commit: dabf8029577c5fb6bb5eebdbf10d77f3d4d95a5d
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 7%

---

# Integrar Marketo Engage con AEM Forms

<span class="preview"> La funcionalidad está disponible en el programa de primeros usuarios. Puede escribir a aem-forms-ea@adobe.com desde su ID de correo electrónico oficial para unirse al programa de primeros usuarios y solicitar acceso a esta funcionalidad. </span>

La integración de AEM Forms con [Adobe Marketo Engage](https://experienceleague.adobe.com/es/docs/marketo/using/home) permite a los usuarios aprovechar las capacidades de Marketo Engage para crear lógica empresarial a partir de los datos capturados y automatizar los flujos de trabajo, incluidas las campañas inteligentes y la automatización de correo electrónico. El formulario configurado puede enviar los datos capturados a Marketo Engage para su procesamiento.

## Ventajas de integrar Marketo Engage con formularios

A continuación se muestran algunas ventajas de conectar un formulario AEM con Adobe Marketo Engage:

* **Integración simplificada**: la conexión de formularios con Marketo Engage elimina la necesidad de crear un modelo de datos de formulario independiente. El proceso de integración es sencillo y sencillo de usar.
* **Captura automática de datos**: Ayuda a capturar automáticamente los envíos de formularios y almacenarlos en Marketo, lo que elimina la entrada manual de datos y reduce los errores.

* **Administración de posibles clientes**: optimiza los procesos de administración de posibles clientes al integrar los envíos de formularios directamente en la base de datos de marketing, lo que permite un mejor seguimiento y mantenimiento de los posibles clientes.

* **Rendimiento de campaña mejorado**: Utiliza datos de formulario para analizar y optimizar las campañas de marketing, lo que mejora el rendimiento general y el retorno de la inversión (ROI).

* **Análisis e informes**: ayudan a obtener acceso a sólidas herramientas de análisis e informes, como Munchkin, en Marketo para medir la efectividad de formularios y campañas.

* **Automatización de seguimiento**: ayuda a automatizar los correos electrónicos de seguimiento y los flujos de trabajo activados por los envíos de formularios, lo que garantiza una comunicación oportuna con los posibles clientes.

## Ventajas clave de utilizar AEM Forms sobre soluciones de formulario alternativas

En la tabla siguiente se describen las pocas razones para elegir AEM Forms en lugar de otras soluciones de formulario alternativas:

| **Función** | **AEM Forms** | **Otras soluciones de formularios** |
|-------------------------------------|----------------------------------------------------------------------|-----------------------------------------------------------|
| **Personalizaciones** | Permite agregar funciones personalizadas específicas, ajustar acciones de formulario y modificar comportamientos de campo para mejorar interacciones de formulario y flujos de trabajo complejos | No se admiten personalizaciones |
| **Editor de reglas** | Admite un editor de reglas integrado para agregar lógica y condiciones. | No hay compatibilidad con el Editor de reglas |
| **Opciones de diseño** | Admite varias opciones de diseño | Opciones de diseño limitadas |
| **Servicio de relleno previo** | Ofrece un servicio de rellenado previo para rellenar automáticamente los datos del formulario. | No hay servicio de relleno previo disponible |
| **Incrustación en sitios** | Se puede incrustar en Sites mediante iFrame | No se puede incrustar en Sites mediante iFrame |
| **Facilidad de integración con Sites** | No se requiere aprendizaje adicional; AEM Forms utiliza las mismas habilidades que Sites | Puede ser necesario un aprendizaje adicional |
| **Envío de datos** | Puede enviar datos a varias plataformas y ofrece varios conectores, como Conectarse a SharePoint, Conectarse a OneDrive, Conectarse a Salesforce, etc. | Puede enviar datos a conectores limitados, por ejemplo a Salesforce |

## Consideraciones para la integración de Marketo Engage con formularios

Algunas consideraciones al integrar Marketo Engage con AEM Forms:

* AEM solo admite la base de datos People(Leads) entre las distintas bases de datos de Marketo.
* Marketo permite la [creación de 10 objetos personalizados](https://experienceleague.adobe.com/es/docs/marketo/using/product-docs/administration/marketo-custom-objects/add-marketo-custom-object-fields) como objetos definidos por el usuario para almacenar datos especializados más allá de los campos estándar en posibles clientes, lo que admite necesidades comerciales únicas.
* AEM solo puede acceder a los objetos personalizados si están asociados a la base de datos de posibles clientes

## Requisitos previos para integrar Marketo Engage con formularios

A continuación se indican los requisitos previos para conectar Marketo Engage con AEM Forms:

* Una licencia de Adobe Marketo Engage válida
* Una instancia de trabajo de Marketo Engage para [recuperar el ID de cliente y el secreto de cliente](https://experienceleague.adobe.com/es/docs/marketo/using/product-docs/administration/additional-integrations/create-a-custom-service-for-use-with-rest-api) para crear una configuración de nube.

## Cree una configuración de servicio en la nube para conectar AEM Forms (Forms adaptable) con Marketo Engage

![Flujo de trabajo](/help/forms/assets/workflow-marketo-1.png)

>[!VIDEO](https://video.tv.adobe.com/v/3442865/engage-marketo-aem-forms-aem)

<span> Este vídeo solo es aplicable a los componentes principales. Para componentes UE/Foundation, consulte el artículo.</span>

La configuración de nube conecta la instancia de Experience Manager con la instancia de Adobe Marketo Engage. Siga estos pasos para crear una configuración de nube de Marketo Engage:

1. Vaya a **Herramientas** > **Cloud Services** > **Marketo Engage**.

   ![Marketo Engage](/help/forms/assets/marketo-engage.png)

2. Abra una carpeta para hospedar la configuración y haga clic en **Crear**. Aparece la ventana **Crear configuración de Marketo Engage**.

   >[!NOTE]
   >
   > También puede [configurar la carpeta para las configuraciones del servicio en la nube](/help/forms/configure-data-sources.md#configure-folder-for-cloud-service-configurations).

3. Especifique el **Título** de la configuración y las credenciales para conectarse al servicio. Puede recuperar las credenciales de autenticación del panel de Adobe Marketo Engage:
   * **ID de cliente** y **Secreto de cliente** están disponibles en **Administración** > **Integración** > **LaunchPoint** al seleccionar el servicio personalizado y hacer clic en **Ver detalles**.
   * La **URL de identidad** está disponible en **Administración** > **Integración** > **Servicios web** como **Identidad** en la sección **API de REST**.

4. Haga clic en **Conectar**.  Si la conexión se realiza correctamente, aparece el mensaje `Authentication Successful`.
5. Haga clic en **[!UICONTROL Crear]** para guardar las opciones de configuración de la nube.

![Configuración de nube de Marketo Engage](/help/forms/assets/marketo-engage-cloud-configuration.png)

Ahora puede utilizar la configuración del servicio en la nube creada para conectar la fuente de datos de Marketo Engage a un formulario adaptable.

## Siguiente paso

Ha creado la configuración del servicio en la nube para integrar Adobe Marketo Engage con AEM Forms. Ahora puede integrar lo siguiente:
* [Nuevo formulario adaptable con Marketo Engage](/help/forms/integrate-adaptive-form-with-marketo-engage.md)
* [Formulario adaptable existente con Marketo Engage](/help/forms/use-marketo-engage-data-source-in-form.md)

## Artículos relacionados

{{af-submit-action}}

## Véase también

{{marketo-engage-see-also}}
