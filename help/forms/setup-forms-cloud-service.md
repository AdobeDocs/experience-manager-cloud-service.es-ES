---
title: Configuración de un entorno de  [!DNL AEM Forms]  as a Cloud Service
description: Aprenda a instalar y configurar un entorno de  [!DNL AEM Forms]  as a Cloud Service.
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 42f53662-fbcf-4676-9859-bf187ee9e4af
source-git-commit: 81951a9507ec3420cbadb258209bdc8e2b5e2942
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 100%

---

# Incorporación de [!DNL AEM Forms] as a Cloud Service {#overview}

| Versión | Vínculo del artículo |
| -------- | ---------------------------- |
| AEM 6.5 | [Haga clic aquí](https://experienceleague.adobe.com/docs/experience-manager-65/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi.html?lang=es) |
| AEM as a Cloud Service | Este artículo |


## Elección de las personas {#personas-aem-forms-project}

<!-- When you sign up for the service, Adobe creates an Organization identifier for your company in the Adobe Identity Management System (IMS), where your users and their permissions can be managed. So, --> Antes de incorporarse a un entorno de Adobe Experience Manager (AEM) Forms as a Cloud Service, elija a las personas que conformarán el equipo para su proyecto. Un equipo del proyecto típico de [!DNL AEM Forms] se conforma de las siguientes personas:

* **Diseñador de experiencia del usuario (UX)**: un Diseñador de experiencia del usuario (UX) define el estilo, el diseño y la marca de los recursos de [!DNL AEM Forms].

* **Profesional de Forms**: un profesional de Forms crea formularios adaptables, temáticas y plantillas según el estilo, el diseño y la promoción de la marca que proporcione el Diseñador de experiencias de usuario. El profesional también crea e integra formularios adaptables con un modelo de datos de formulario (FDM) y flujos de trabajo de AEM. También suele realizar tareas relacionadas con el front-end.

* **Desarrollador de Forms**: un desarrollador de Forms desarrolla una solución de formularios personalizada. Normalmente, se encarga del desarrollo back-end, como el desarrollo de componentes personalizados, flujos de trabajo de AEM, el servicio de prerrellenado y mucho más.

* **Administrador de AEM**: este ayuda con la configuración general, como la de usuarios, la de fuentes de datos, los correos electrónicos, el software de terceros y refuerza el entorno. El administrador de AEM también ayuda con las integraciones, como la integración con Adobe Analytics, Adobe Target y Adobe Sign.

* **Usuario final**: un usuario final interactúa con el formulario publicado y lo envía, firma los formularios enviados, realiza un seguimiento de las aplicaciones enviadas a través del portal web y recibe comunicaciones personalizadas.

<!-- While onboarding to the service, assign the following AEM groups to [!DNL AEM Forms] as a Cloud Service based on their role:

| User type | AEM group |
|---|---|
| Form Practitioner | forms-users (AEM Forms Users), template-authors, workflow-user, workflow-editors, and fdm-author  |
| UX Designer| forms-users, template-authors|
| End-User| <ul> <li>When a user must login to view and submit an Adaptive Form, add such users to forms-users group. </li> <li>When no user authentication is required to access Adaptive Forms, do not assign any group to such users. </li> </ul>| -->

## Incorporación al servicio {#onboarding}

* [Incorpórese](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/overview.html?lang=es) a [!DNL Adobe Experience Manager] as a Cloud Service.

* (Solo para entornos limitados) Después de incorporarse al servicio, [cree](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/pipelines/production-pipelines.html?lang=es) y [ejecute](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/using/code-deployment.html?lang=es) canalizaciones de producción y de no producción. Esto habilita e incorpora las últimas funciones de [!DNL AEM Forms] as a Cloud Service a su entorno.

Puede utilizar Forms as a Cloud Service para crear un formulario adaptable (inscripción digital) o generar una comunicación con el cliente. Tras finalizar la [incorporación](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/overview.html?lang=es) a [!DNL Adobe Experience Manager] as a Cloud Service, realice una de las siguientes acciones para habilitar Formularios: funciones de inscripción digital o comunicaciones con el cliente. <!--You can also enable both the features-->:

1. Inicie sesión en Cloud Manager y abra su instancia de AEM Forms as a Cloud Service.
1. Abra la opción Editar programa, vaya a la pestaña Soluciones y complementos y realice lo siguiente:

   * Si tiene un entorno de producción, seleccione la opción **[!UICONTROL Formularios y Comunicaciones]** para habilitar Formularios, Inscripción digital y Formularios - Complemento de comunicaciones.

     ![Comunicaciones](assets/communications.png)

   <!-- If you have already enabled the **[!UICONTROL Forms - Digital Enrollment]** option, then select the **[!UICONTROL Forms - Communications Add-On]** option. ![Addon](assets/add-on.png) -->

   * Si tiene un entorno de zona protegida, seleccione **[!UICONTROL Formularios]** para habilitar el complemento Formularios, Inscripción digital y Formularios y Comunicaciones.

     ![Selección de inscripción en formulario digital](assets/forms-digital-enrollment1.png)


1. Haga clic en **[!UICONTROL Actualizar]**.
1. Ejecute la canalización de la versión. Una vez que la canalización de la versión se haya realizado correctamente, la solución seleccionada se habilita para su entorno.

>[!NOTE]
>
> Para habilitar y configurar las API de manipulación de documentos, agregue la siguiente regla a la [Configuración de Dispatcher](setup-local-development-environment.md#forms-specific-rules-to-dispatcher):
>
> `# Allow Forms Doc Generation requests`
> `/0062 { /type "allow" /method "POST" /url "/adobe/forms/assembler/*" }`

## Configuración de usuarios {#config-users}

Una vez que haya completado la incorporación al servicio, inicie sesión en su entorno de [!DNL AEM Forms] as a Cloud Service, abra las instancias de autor y publicación y agregue usuarios a [grupos de AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=es#accessing) específicos de Forms en función de su personalidad. En la tabla siguiente se enumeran los grupos de AEM específicos de Forms disponibles de forma predeterminada y los tipos de usuarios correspondientes. La tabla también proporciona el tipo de instancia de AEM de cada tipo de usuario:

| Tipos de usuarios (personalidades) | Grupos de usuarios | Instancia de AEM |
|---|---|---|
| Profesional/Desarrollador de Forms | <ul> <li> [!DNL forms-users] </li><li> [!DNL template-author] </li><li> [!DNL workflow-users] </li><li> [!DNL workflow-editors] </li><li> [!DNL fdm-authors] </li></ul> | Instancia de autor |
| Diseñador de experiencias del usuario (UX) | <ul> <li> [!DNL forms-users]</li><li> [!DNL template-author] </li></ul> | Instancia de autor |
| Administrador de AEM | <ul> <li>[!DNL aem-administrators],</li> <li>[!DNL fd-administrators] </li> </ul> | Instancia de autor y publicación |
| Usuario final | <ul> <li>Cuando un usuario deba iniciar sesión para ver y enviar un formulario adaptable, agréguelo al grupo [!DNL forms-users]. </li> <li>Cuando no se requiera autenticación de usuario para acceder a los formularios adaptables, no asigne ningún grupo a esos usuarios. </li> </ul> | Instancia de autor y publicación |

Para obtener más información sobre los grupos de AEM específicos de Forms y los permisos correspondientes, consulte [Grupos y permisos](forms-groups-privileges-tasks.md).

<!-- You can also create  [user groups](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=es#accessing) specific  to your organization, assign policies, and [users](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions.html?lang=es#accessing) to the groups. The policies help control permissions of the users that are part of the group. For information a -->

## Siguiente paso {#next-steps}

[Configure un entorno de desarrollo de local](setup-local-development-environment.md). Puede utilizar un entorno de desarrollo local para crear un formulario adaptable y recursos relacionados (temáticas, plantillas, acciones de envío personalizadas, servicio de rellenado previo, etc.). Y, la [conversión de PDF Forms a Formularios adaptables](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html?lang=es) sin iniciar sesión en un entorno de desarrollo de nube.

<!-- ### Business unit and end-users {#business-unit-and-end-users}

| Role| Organization| Description|
|-----|-------|-----|
| UX Designer                  | Customer/System Integrator/Partner | Defines user experience design (style, layout, branding) as per organizational requirements for Adaptive Forms to allow AEM Forms practitioners to design the corresponding themes and templates.                                     |
| Forms Practitioner           | Customer                           | Authors Adaptive Forms, creates Form Data Model integrations, and creates business workflows using the Experience Manager Workflows. Typically undertakes the front-end work.                                                         |
| Business Executive - Digital | Customer                           | Responsible for business unit's product marketing strategy and revenues, main business stakeholders for digital use cases, solutions, and service offerings for the end-users, signs off on the use case implementation and delivery. |
| Customer Experience Lead     | Customer                           | Business user persona. Authors, personalizes and updates Adaptive Forms fields/rules/styling, identifies, and prioritizes business needs. Validates business use-case with SI/Partner developers/practitioners during UAT.            |
| Forms Back-Office User       | Customer                           | End-user internal to organization filling forms, participating in back-office Forms workflows such as review/approval of applications and so on.                                                                                            |
| Forms End-User               | External to customer               | Interacts with and submits the published form as end customer or citizen, signs submitted forms, tracks her applications through web portal, receives personalized interactive communications.                                        |

### Project team {#project-team}

| Role | Org | Description|
|-----|-----|-----|
| Experience Manager Administrator | System Integrator /Partner/Customer | Helps with overall installation, configures SSL certificates, configures data sources, email, and other third-party software, integrations like Adobe Analytics, Adobe Target, Automated Forms Conversion Services with Experience Manager instance. |
| Project Manager                  | System Integrator /Partner/Customer | Converts customer use-case into technical requirements, manages schedule/cost/scope for overall project.                                                                                                                                             |
| Product Owner                    | System Integrator /Partner/Customer | Prioritizes and evaluates scrum team's work for high-quality delivery on time.                                                                                                                                                                       |
| Scrum Master                     | System Integrator /Partner/Customer | Ensures agile values and processes in place to deliver on defined requirements as per prioritization by PO.                                                                                                                                          |
| Infrastructure / security expert | System Integrator /Partner/Customer | Provisions and configures best possible infrastructure, security controls and infra processes to address current and projected RASP requirements.                                                                                                    |
| Technical Architect              | System Integrator /Partner/Customer | Provides best high-level architecture and infrastructure guidance for use-case implementation and address RASP (Reliability, Availability, Scalability, and Performance) and security challenges.                                                    | -->

<!-- ## Onboard to the service {#onboarding}

[Onboard](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=es) to the [!DNL Adobe Experience Manager] as a Cloud Service. 

After you onboard the service, configure a [local development environment](setup-local-development-environment.md). 

Administrators are responsible for managing Adobe software and services for their organization. Administrators grant access to developers in their organization to connect and use your [!DNL AEM Forms] as a Cloud Service program. When an administrator is provisioned for an organization, the administrator receives an email with title 'You now have administrator rights to manage Adobe software and services for your organization'. If you are an administrator, check your mailbox for email with previously mentioned title and proceed to [add users](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=es#onboarding-users-in-admin-console) by way of IMS and assign [form-specific groups](forms-groups-privileges-tasks.md) to users based on their role.

## Next step {#next-steps} -->

<!-- ## Prerequisites {#prerequisites}

If you are new to AEM as a cloud service, contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS). Once Adobe has created an organization for your company, your designated administrator is added as the first member of the organization. The administrator can setup an [!DNL AEM Forms] as a Cloud Service instance. 

## Onboard and set up a new environment {#onboard-and-setup-a-new-environment}

Log in to Cloud Manager and create a program. After the program is ready, create environments, add developers or users to environments, and run the pipeline to get the latest version of [!DNL AEM Forms] as a Cloud Service and start developing for your environment. The detailed steps are:

1. Contact your Adobe representative to create an organization identifier for your company in the Adobe Identity Management System (IMS) and provide access to an administrator in your organization.
1. Configure [Automated Forms Conversion Service](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html?lang=es). After a configuration is complete, a profile for Automated Forms Conversion Service is available in [Admin Console](https://adminconsole.adobe.com/).

    If the service is not available, log in to [Admin Console](https://adminconsole.adobe.com/). Use Adobe ID of administrator provisioned to use Automated Forms Conversion Service to login. Do not use any other ID or Federated ID to login.
    1. Click **[!UICONTROL Automated Forms Conversion Service]** option.
    1. Click **[!UICONTROL New Profile]** in the Products tab.
    1. Specify **[!UICONTROL Name]**, **[!UICONTROL Display Name]**, and **[!UICONTROL Description]** for the profile. Click **[!UICONTROL Done]**. A profile is created. 
1. Log in to [Cloud Manager](https://experience.adobe.com/#/@marketinghub/experiencemanager) and [create a program](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) for your organization.
1. [Create environments](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=es#adding-environments) within your program.
1. Log in to [Admin console](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/what-is-required/add-users-roles.html) and add developers or users to your organization.
1. Run the [build pipeline](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-manager/using/how-to-use/deploying-code.html). It brings latest [!DNL Experience Manager Forms] as a Cloud Service features to your environment.
1. [Start developing](https://docs.adobe.com/content/help/es-ES/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html) and creating Adaptive Forms on [!DNL Experience Manager Forms] as a Cloud Service environment.
1. Configure the [local development environment](setup-local-development-environment.md) for rapid development

## Configure dispatcher caching {#caching}

You can make dispatcher caching related configuration changes to code on your local development instance and deploy the changes to your [!DNL AEM Forms] as a Cloud Service instance. For details, see [update dispatcher configuration](setup-local-development-environment.md).
 -->
