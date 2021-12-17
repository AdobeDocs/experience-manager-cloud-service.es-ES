---
title: Conceder acceso al desarrollador de front-end
description: Onboard the front-end developers into Cloud Manager so they have access to your AEM site git repository and pipeline.
source-git-commit: 5e1a89743c5ac36635a139ada690849507813c30
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---


# Conceder acceso al desarrollador de front-end {#grant-fed-access}

Onboard the front-end developers into Cloud Manager so they have access to your AEM site git repository and pipeline.

## La historia hasta ahora {#story-so-far}

In the previous document of the AEM Quick Site Creation journey, [Set Up Your Pipeline,](pipeline-setup.md) you learned how to create a front-end pipeline to manage the customization of your site&#39;s theme, and you should now:

* Comprender qué es una canalización front-end.
* Obtenga información sobre cómo configurar una canalización front-end en Cloud Manager.

Ahora debe otorgar a su desarrollador de front-end acceso a Cloud Manager a través del proceso de incorporación para que el desarrollador de front-end pueda acceder al repositorio de Git de AEM y a la canalización que ha creado.

## Objetivo {#objective}

El proceso de conceder acceso a Cloud Manager y asignar funciones de usuario a los usuarios se llama integración. This document will give an overview of the most important steps for onboarding a front-end developer and after reading you will know:

* How to add a front-end developer as a user.
* Cómo conceder las funciones necesarias al desarrollador del front-end.

>[!TIP]
>
>Hay un recorrido de documentación completo dedicado a integrar su equipo en AEM as a Cloud Service, vinculado a en la variable [Sección Recursos adicionales](#additional-resources) de este documento, si necesita detalles adicionales sobre el proceso.

## Responsible Role {#responsible-role}

Esta parte del recorrido se aplica al administrador de Cloud Manager.

## Requisitos {#requirements}

* Debe ser miembro de **Propietario empresarial** en Cloud Manager.
* Debe ser un **Administrador de sistemas** en Cloud Manager.
* Debe tener acceso al Admin Console.

## Agregar el desarrollador de front-end como usuario {#add-fed-user}

En primer lugar, debe agregar el desarrollador front-end como usuario mediante el Admin Console .

1. Inicie sesión en el Admin Console en [https://adminconsole.adobe.com/](https://adminconsole.adobe.com/).

1. Una vez que haya iniciado sesión, aparecerá una página de información general similar a la siguiente imagen.

   ![Información general del Admin Console](assets/admin-console.png)

1. Make sure you are in the appropriate org, by checking the org name in the top-right corner of the screen.

   ![Comprobar nombre de organización](assets/correct-org.png)

1. Select **Adobe Experience Manager as a Cloud Service** de la variable **Productos y servicios** tarjeta.

   ![Select AEMaaCS](assets/select-aemaacs.png)

1. You see the list of pre-configured Cloud Manager product profiles. Si no ve estos perfiles, póngase en contacto con el administrador de Cloud Manager, ya que es posible que no tenga los permisos correctos en su organización.

   ![Product profiles](assets/product-profiles.png)

1. To assign the front-end developer to the correct profiles, tap or click on the **Users** tab and then the **Add User** button.

   ![Add user](assets/add-user.png)

1. In the **Add users to your team** dialog box, type the email ID of the user you want to add. For the ID Type, select Adobe ID, if the Federated ID for your team members has not yet been set up.

   ![Add user to team](assets/add-to-team.png)

1. In the **Product** selection, tap or click the plus sign and then select **Adobe Experience Manager as a Cloud Service** and assign the **Deployment Manager** and **Developer** product profiles to the user.

   ![Assign team profiles](assets/assign-team.png)

1. Toque o haga clic **Guardar** y se envía un correo electrónico de bienvenida al desarrollador front-end que agregó como usuario.

El desarrollador front-end invitado puede acceder a Cloud Manager haciendo clic en el vínculo del correo electrónico de bienvenida e iniciando sesión con su Adobe ID.

## Envío al desarrollador de Front-End {#handover}

Con una invitación por correo electrónico a Cloud Manager dirigida al desarrollador front-end, usted y el administrador de AEM ahora pueden proporcionar al desarrollador de front-end la información necesaria restante para comenzar la personalización.

* A [path to typical content](#example-page)
* La fuente del tema que [descargado](#download-theme)
* La variable [credenciales de usuario proxy](#proxy-user)
* El nombre del programa o la URL a él [copiado desde Cloud Manager](pipeline-setup.md#login)
* The front-end design requirements

## Siguientes pasos {#what-is-next}

Now that you have completed this part of the AEM Quick Site Creation journey you should know:

* Cómo añadir un desarrollador front-end como usuario.
* Cómo conceder las funciones necesarias al desarrollador del front-end.

Build on this knowledge and continue your AEM Quick Site Creation journey by next reviewing the document [Retrieve Git Repository Access Information,](retrieve-access.md) which switches perspective exclusively to the front-end developer and explains how the front-end developer users Cloud Manager to access git repository information.

## Recursos adicionales {#additional-resources}

While it is recommended that you move on to the next part of the Quick Site Creation journey by reviewing the document [Retrieve Front-End Developer Credentials,](retrieve-access.md) the following are some additional, optional resources that do a deeper dive on some concepts mentioned in this document, but they are not required to continue on the journey.

* [Recorrido de incorporación](/help/journey-onboarding/home.md) - Esta guía sirve como punto de partida para garantizar que sus equipos estén configurados y tengan acceso a AEM as a Cloud Service.


