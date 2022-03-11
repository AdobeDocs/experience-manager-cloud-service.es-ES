---
title: Conceder acceso al desarrollador de front-end
description: Incorpore a los desarrolladores del front-end en Cloud Manager para que tengan acceso al repositorio de Git del sitio AEM y a la canalización.
exl-id: 58e95c92-b859-4bb9-aa62-7766510486fd
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 0%

---

# Conceder acceso al desarrollador de front-end {#grant-fed-access}

Incorpore a los desarrolladores del front-end en Cloud Manager para que tengan acceso al repositorio de Git del sitio AEM y a la canalización.

## La historia hasta ahora {#story-so-far}

En el documento anterior del recorrido de Creación Rápida del Sitio de AEM, [Configurar la canalización,](pipeline-setup.md) ha aprendido a crear una canalización front-end para administrar la personalización del tema de su sitio y ahora debería:

* Comprender qué es una canalización front-end.
* Obtenga información sobre cómo configurar una canalización front-end en Cloud Manager.

Ahora debe otorgar a su desarrollador de front-end acceso a Cloud Manager a través del proceso de incorporación para que el desarrollador de front-end pueda acceder al repositorio de Git de AEM y a la canalización que ha creado.

## Objetivo {#objective}

El proceso de conceder acceso a Cloud Manager y asignar funciones de usuario a los usuarios se llama integración. En este documento se ofrece una descripción general de los pasos más importantes para incorporar a un desarrollador de front-end y, después de leer, se dará cuenta de lo siguiente:

* Cómo añadir un desarrollador front-end como usuario.
* Cómo conceder las funciones necesarias al desarrollador del front-end.

>[!TIP]
>
>Hay un recorrido de documentación completo dedicado a integrar su equipo en AEM as a Cloud Service, vinculado a en la variable [Sección Recursos adicionales](#additional-resources) de este documento, si necesita detalles adicionales sobre el proceso.

## Función responsable {#responsible-role}

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

1. Asegúrese de que está en la organización adecuada, comprobando el nombre de la organización en la esquina superior derecha de la pantalla.

   ![Comprobar nombre de organización](assets/correct-org.png)

1. Select **Adobe Experience Manager as a Cloud Service** de la variable **Productos y servicios** tarjeta.

   ![Seleccione AEMaaCS](assets/select-aemaacs.png)

1. Verá la lista de perfiles de producto preconfigurados de Cloud Manager. Si no ve estos perfiles, póngase en contacto con el administrador de Cloud Manager, ya que es posible que no tenga los permisos correctos en su organización.

   ![Perfiles de producto](assets/product-profiles.png)

1. Para asignar el desarrollador de front-end a los perfiles correctos, toque o haga clic en el **Usuarios** y, a continuación, **Agregar usuario** botón.

   ![Agregar usuario](assets/add-user.png)

1. En el **Agregar usuarios a su equipo** , escriba el ID de correo electrónico del usuario que desea agregar. Para el tipo de ID, seleccione Adobe ID si el Federated ID de los integrantes del equipo aún no se ha configurado.

   ![Agregar usuario al equipo](assets/add-to-team.png)

1. En el **Product** selección, pulse o haga clic en el signo más y, a continuación, seleccione **Adobe Experience Manager as a Cloud Service** y asigne **Administrador de implementación** y **Desarrollador** perfiles de producto para el usuario.

   ![Asignación de perfiles de equipo](assets/assign-team.png)

1. Toque o haga clic **Guardar** y se envía un correo electrónico de bienvenida al desarrollador front-end que agregó como usuario.

El desarrollador front-end invitado puede acceder a Cloud Manager haciendo clic en el vínculo del correo electrónico de bienvenida e iniciando sesión con su Adobe ID.

## Envío al desarrollador de Front-End {#handover}

Con una invitación por correo electrónico a Cloud Manager dirigida al desarrollador front-end, usted y el administrador de AEM ahora pueden proporcionar al desarrollador de front-end la información necesaria restante para comenzar la personalización.

* A [ruta al contenido típico](#example-page)
* La fuente del tema que [descargado](#download-theme)
* La variable [credenciales de usuario proxy](#proxy-user)
* El nombre del programa o la URL a él [copiado desde Cloud Manager](pipeline-setup.md#login)
* Los requisitos de diseño del front-end

## Siguientes pasos {#what-is-next}

Ahora que ha completado esta parte del recorrido de creación rápida AEM sitio, debe saber:

* Cómo añadir un desarrollador front-end como usuario.
* Cómo conceder las funciones necesarias al desarrollador del front-end.

Aproveche este conocimiento y continúe con su recorrido de Creación Rápida AEM Sitio revisando el documento [Recuperar información de acceso al repositorio Git,](retrieve-access.md) que cambia la perspectiva exclusivamente al desarrollador front-end y explica cómo los usuarios de desarrollador front-end Cloud Manager acceden a la información del repositorio de Git.

## Recursos adicionales {#additional-resources}

Aunque se recomienda pasar a la siguiente parte del recorrido de creación rápida del sitio revisando el documento [Recupere Credenciales de Desarrollador de Front-End,](retrieve-access.md) los siguientes son algunos recursos opcionales adicionales que profundizan en algunos conceptos mencionados en este documento, pero no son necesarios para continuar en el recorrido.

* [Recorrido de incorporación](/help/journey-onboarding/home.md) - Esta guía sirve como punto de partida para garantizar que sus equipos estén configurados y tengan acceso a AEM as a Cloud Service.
