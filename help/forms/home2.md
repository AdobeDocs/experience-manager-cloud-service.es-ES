---
title: Introducción a  [!DNL AEM Forms]  as a Cloud Service
description: Descubra AEM Forms para producir formularios preparados para la empresa, crear flujos de trabajo de procesos empresariales y utilizar los servicios de documentos para producir y proteger documentos.
landing-page-description: Obtenga información sobre cómo utilizar formularios en AEM as a Cloud Service.
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
hide: true
hidefromtoc: true
source-git-commit: 4b4bc6f754c6336136d409cf49617c7fafd4f4c3
workflow-type: tm+mt
source-wordcount: '1145'
ht-degree: 11%

---


# AEM Forms as a Cloud Service {#introduction}

<!-- Version Navigation -->
<div class="version-selector">
  <p><strong>¿Busca documentación para una versión diferente?</strong></p>
  <ul>
    <li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/home.html?lang=es">Documentación de AEM 6.5 Forms</a></li>
    <li><strong>AEM Forms as a Cloud Service</strong> (actual)</li>
  </ul>
</div>

## ¿Qué es AEM Forms as a Cloud Service?

AEM Forms as a Cloud Service es la solución nativa en la nube de Adobe para crear, administrar y entregar formularios y comunicaciones digitales. Permite a las organizaciones transformar transacciones complejas en experiencias digitales simples en todo el recorrido del cliente. Puede utilizar el servicio para lo siguiente:

* Digitalización y optimización de la experiencia de inscripción e incorporación
* Comunicaciones personalizadas
* Automatización de flujos de trabajo de back-office
* Integración de experiencias de formularios y comunicaciones con fuentes de datos
* Seguimiento y optimización del rendimiento de los formularios

El servicio siempre está actualizado, siempre está disponible, y aprende constantemente. Las organizaciones pueden utilizar [!DNL AEM Forms] as a Cloud Service y disfrutar de todas estas funciones en la nube sin necesidad de ninguna infraestructura local. El servicio también permite prescindir de los ciclos de actualización complejos, ya que siempre está actualizado con las últimas funciones.

Adobe [!DNL Experience Manager Forms as a Cloud Service] es una solución centrada en apoyar cada paso del recorrido del cliente:

<div class="card-container" style="display: flex; flex-wrap: wrap; gap: 20px; margin-bottom: 30px;">
  <div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Formularios adaptables</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Cree formularios dinámicos y adaptables que se adapten a los datos introducidos por el usuario y al tipo de dispositivo:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components">Crear Forms adaptable</a>: cree formularios que se ajusten automáticamente a diferentes tamaños de pantalla y entradas de usuario</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type">Biblioteca de componentes enriquecidos</a>: utilice una variedad de campos de entrada y componentes de interfaz de usuario</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components">Estilo de Forms adaptable</a>: aplique una marca y un diseño visual coherentes en sus formularios</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components">Usar temáticas y plantillas prediseñadas</a>: acelere el desarrollo con componentes listos para usar</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components">Validación de formularios</a> - Implementar reglas de validación del lado del cliente y del lado del servidor</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/configure-submit-actions-core-components">Acciones de envío</a>: configure lo que sucede cuando los usuarios envían formularios</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/generate-document-of-record-core-components">Documento de registro</a> - Crear registros permanentes de datos de formularios enviados</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/create-or-add-an-adaptive-form-to-aem-sites-page">Agregar Forms a las páginas de AEM Sites</a>: integre fácilmente formularios en su sitio web</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/services/embed-adaptive-form-core-components-external-web-page">Agregar Forms a páginas de sitios web de terceros</a>: integre fácilmente formularios en su sitio web</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>API de comunicación</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Generar, manipular y proteger documentos mediante programación:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-generation">Generar comunicaciones personalizadas</a>: cree documentos personalizados basados en plantillas y datos</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation">Montar y manipular archivos PDF</a>: combinar, dividir y modificar documentos de PDF</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">Crear documentos de PDF/A</a>: generar documentos con calidad de archivo</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#signature-apis">Aplicar firmas</a> - Proteger documentos con firmas</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#encryption-apis">Cifrar y descifrar archivos PDF</a> - Proteger contenido confidencial del documento</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">Convertir XDP a PostScript</a>: transforme documentos XDP a formato PostScript</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">Convertir XDP a PCL</a>: transforme documentos XDP al idioma de comando de impresora</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#create-PS-PCL-ZPL-documents">Convertir XDP a ZPL</a>: transforme documentos XDP al lenguaje de impresión Zebra</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-to-and-validate-pdfa-compliant-documents">Convertir PDF a estándares PDF/A</a>: cree documentos PDF compatibles con archivos</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#convert-pdf-documents-to-pdf-x-standards">Agregar firmas digitales</a>: firme digitalmente los documentos para la autenticación</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Edge Delivery Services para Forms</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Crear y enviar formularios con Edge Delivery Services:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/overview">Información general sobre Edge Delivery Forms</a>: obtenga información sobre los formularios con Edge Delivery Services</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/getting-started-universal-editor">Editor universal para Forms</a>: cree formularios con el Editor universal de WYSIWYG</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial">Creación basada en documentos</a>: cree formularios con Microsoft Word o Google Docs</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/universal-editor/style-theme-forms">Aplicar estilo a Edge Delivery Forms</a> - Aplicar estilo personalizado a los formularios</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Forms sin encabezado</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Ofrezca experiencias de formulario en cualquier canal o marco de trabajo de front-end:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-headless-adaptive-forms/using/overview">Introducción a Forms sin encabezado</a>: Obtenga información sobre el enfoque sin encabezado para los formularios</li>
        <li>Generar formularios mediante React u otros marcos de front-end</li>
        <li>Integración de formularios en aplicaciones móviles, sitios web y aplicaciones de chat</li>
        <li>Aproveche los componentes de la IU existentes con la funcionalidad de formularios</li>
        <li>Mantener la lógica del formulario back-end mientras se tiene flexibilidad de front-end</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Automatización del flujo de trabajo</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Automatice los procesos empresariales con formularios y documentos:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#assign-task-step">Crear procesos empresariales</a>: envíe formularios para recibir aprobación o comentarios, flujos de trabajo posteriores al envío o flujos de trabajo back-end para administrar los procesos de inscripción</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step">Usar Adobe Sign en un flujo de trabajo de AEM</a> - Enviar un documento para su firma </li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step">Generar un documento de registro </a> - Generar bajo demanda o en envío de formulario</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Firmas electrónicas</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Agregar firmas electrónicas legalmente vinculantes a sus formularios y documentos:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/services/adobe-sign-integration-adaptive-forms">Integración de Adobe Sign</a> - Habilitar firmas electrónicas en Forms adaptable</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#sign-document-step">Agregar firmas electrónicas a flujos de trabajo</a>: incluya pasos de firma en los procesos empresariales</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference#generate-document-of-record-step">Documento de registro con firmas</a> - Generar registros firmados de envíos de formularios</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Analytics y perspectivas</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Obtenga información sobre el uso y el rendimiento del formulario:</p>
      <ul>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation">Habilitar Adobe Analytics</a> - Rastrear el uso y el rendimiento de los formularios</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-aem-forms-with-adobe-analytics">Integración manual de Analytics</a>: configure análisis para un seguimiento detallado</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/services/view-understand-aem-forms-analytics-reports">Ver informes de Analytics</a> - Analizar el rendimiento del formulario y el comportamiento del usuario</li>
      </ul>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Integración de datos</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <p>Conecte los formularios a sus fuentes de datos y sistemas existentes:</p>
      <h4>Ecosistema de Adobe</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign">Adobe Sign</a> - Enviar para obtener firmas electrónicas a través de Adobe Sign</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/services/integrate-adaptive-form-with-market-engage/integrate-form-to-marketo-engage">Marketo Engage</a>: integración de formularios con Adobe Marketo Engage</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#invoke-an-aem-workflow">Flujo de trabajo de AEM</a>: Déclencheur flujos de trabajo de AEM con envíos de formularios</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#workfront-fusion">Workfront</a> - Enviar un formulario adaptable a Adobe Workfront Fusion</li>
      </ul>
      <h4>Integraciones de Microsoft</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics">Microsoft Dynamics 365</a> - Integración con CRM de Microsoft</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage">Almacenamiento de Azure Blob</a>: Almacene datos de formulario en el almacenamiento en la nube de Microsoft</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/connect-to-sharepoint/connect-forms-to-sharepoint-document-library">Biblioteca de documentos de SharePoint</a> - Conectar con bibliotecas de documentos de Microsoft SharePoint</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#connect-af-sharepoint-list">Lista de SharePoint</a> - Conectarse a la lista de Microsoft SharePoint</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-onedrive">OneDrive</a>: conectar con Microsoft OneDrive</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/services/forms-microsoft-power-automate-integration">Microsoft Power Automate</a>: flujos de Déclencheur de Microsoft Power Automate</li>
      </ul>
      <h4>Otras fuentes de datos y servicios</h4>
      <ul>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/aem-forms-salesforce-integration">Salesforce</a> - Integración con Salesforce CRM</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-to-rest-endpoint">Servicios RESTful</a> - Conectarse a cualquier extremo de API REST</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources">Bases de datos RDBMS</a> - Conectar con bases de datos relacionales</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-email">Correo electrónico</a> - Enviar datos de formulario por correo electrónico</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/introduction-to-forms-portal/save-core-component-based-form-as-draft">Portal de Forms</a> - Enviar al portal de Forms para guardar el borrador</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#send-pdf-via-email">Enviar PDF por correo electrónico</a>: envía por correo electrónico una versión de PDF del formulario enviado</li>
        <li><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions#submit-using-form-data-model">Enviar mediante el modelo de datos de formulario</a> - Enviar datos mediante un modelo de datos de formulario</li>
      </ul>
    </div>
  </div>
</div>

## Introducción a AEM Forms as a Cloud Service

<div class="card-container" style="display: flex; flex-wrap: wrap; gap: 20px; margin-bottom: 30px;">
  <div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Para usuarios empresariales</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>Comprender los conceptos básicos</strong>: Obtenga información acerca de <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components">Forms adaptable</a> y cómo pueden ayudar a digitalizar los procesos empresariales.</li>
        <li style="margin-bottom: 8px;"><strong>Explorar plantillas</strong>: Examine las <a href="https://experienceleague.adobe.com/es/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components">plantillas y temas pregenerados</a> para comenzar con sus proyectos de formularios.</li>
        <li style="margin-bottom: 8px;"><strong>Aprenda a crear formularios</strong>: Siga la <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/introduction-forms-authoring">guía de creación de formularios</a> para crear su primer formulario.</li>
      </ol>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Para desarrolladores</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>Configure su entorno</strong>: configure su <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-local-development-environment">entorno de desarrollo local</a> para AEM Forms.</li>
        <li style="margin-bottom: 8px;"><strong>Conozca la arquitectura</strong>: Comprenda la <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture">arquitectura de AEM Forms as a Cloud Service</a>.</li>
        <li style="margin-bottom: 8px;"><strong>Explorar API</strong>: Familiarícese con <a href="https://developer-stage.adobe.com/experience-cloud/experience-manager-apis/api/stable/forms/"> las API </a> y SDK disponibles para ampliar e integrar Forms.</li>
      </ol>
    </div>
  </div>

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease;">
    <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
      <h3>Para administradores</h3>
    </div>
    <div class="card-body" style="padding: 20px; background-color: #ffffff;">
      <ol style="margin-top: 10px; padding-left: 25px;">
        <li style="margin-bottom: 8px;"><strong>Incorporación a Cloud Service</strong>: siga la <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service">guía de incorporación</a> para configurar AEM Forms as a Cloud Service.</li>
        <li style="margin-bottom: 8px;"><strong>Configurar servicios</strong>: configure <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation">integraciones con otros servicios de Adobe</a> como Adobe Analytics.</li>
        <li style="margin-bottom: 8px;"><strong>Migrar desde AEM 6.5</strong>: Si viene desde AEM 6.5, siga la <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html?lang=es">guía de migración</a> para pasar a Cloud Service.</li>
      </ol>
    </div>
  </div>
</div>

## Funciones de usuario pionero

<div class="card" style="flex: 1 1 calc(50% - 20px); min-width: 300px; border: 1px solid #e1e1e1; border-radius: 8px; overflow: hidden; box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1); transition: transform 0.3s ease, box-shadow 0.3s ease; margin-bottom: 30px;">
  <div class="card-header" style="background-color: #f5f5f5; padding: 15px 20px; border-bottom: 1px solid #e1e1e1;">
    <h3>Programa de acceso anticipado de AEM Forms</h3>
  </div>
  <div class="card-body" style="padding: 20px; background-color: #ffffff;">
    <p>El <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">Programa de acceso anticipado de AEM Forms</a> ofrece acceso exclusivo a funciones de vanguardia antes de que estén disponibles en general, entre ellas:</p>
    <ul style="margin-top: 10px; padding-left: 25px;">
      <li style="margin-bottom: 8px;"><strong>Asistente de IA de AEM Forms (IA general)</strong>: cree formularios más rápido con sugerencias con tecnología de IA</li>
      <li style="margin-bottom: 8px;"><strong>Conector de AEM Forms Workfront Fusion</strong>: Automatice los flujos de trabajo activados por los envíos de formularios</li>
      <li style="margin-bottom: 8px;"><strong>Forms de conversación</strong>: crea experiencias de formulario de estilo chat en cualquier página de AEM Sites</li>
      <li style="margin-bottom: 8px;"><strong>Creación de WYSIWYG para Edge Delivery</strong>: cree formularios con el editor universal para Edge Delivery Services</li>
      <li style="margin-bottom: 8px;"><strong>Conector de AEM Forms a Marketo</strong>: integrar envíos de formularios con Marketo Engage</li>
    </ul>
    <p>Para obtener una lista completa de las innovaciones de acceso anticipado y la documentación detallada, visite la <a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/forms-overview/early-access-ea-features">página Programa de acceso anticipado de AEM Forms</a>.</p>
  </div>
</div>

<div style="background-color: #f0f7ff; border-left: 4px solid #1473e6; padding: 20px; margin: 30px 0; border-radius: 4px;">
  <h3 style="margin-top: 0; color: #1473e6;">¿Listo para empezar?</h3>
  <p><a href="https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/setup-forms-cloud-service" style="font-weight: bold; color: #1473e6;">Incorpórese a AEM Forms as a Cloud Service</a> hoy y transforme la experiencia de formularios digitales de su organización.</p>
</div>
