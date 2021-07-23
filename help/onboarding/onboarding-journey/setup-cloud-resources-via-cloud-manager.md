---
title: Configuración de recursos de Cloud mediante Cloud Manager
description: Siga esta página para obtener información sobre cómo configurar los recursos de Cloud a través de Cloud Manager
hide: true
hidefromtoc: true
index: false
source-git-commit: 730dcb038a3080ff736a83963811aaf39d270845
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 0%

---

# Configuración de recursos de Cloud mediante Cloud Manager {#setup-cloud-resources}

El administrador del sistema asignado a la función *Propietario del negocio* debe acceder a Cloud Manager e iniciar sesión. A continuación, un miembro del equipo asignado al perfil de producto *Propietario empresarial* debe iniciar sesión en Cloud Manager y crear el programa y los entornos de la nube para que su equipo de expertos pueda empezar.

## Objetivo {#objective}

Este documento le ayuda a comprender cómo se crean los recursos de la nube y quién puede hacerlo.

Después de leer esta sección debe comprender:

* Un administrador del sistema asignado a la función *Propietario del negocio* debe ser el primero en acceder a Cloud Manager e iniciar sesión en él.
* Cómo se crean el programa y los entornos de la nube.

## Introducción {#introduction}

La adición de recursos de nube se realiza mediante Cloud Manager a través de un miembro del equipo asignado al perfil de producto de Cloud Manager Business Owner. Normalmente, esta persona comprende las necesidades comerciales y completa la configuración inicial de Cloud Manager.

Siga las secciones a continuación para aprender a crear sus [programas de servicios en la nube](#create-cloud-service-program) y [entornos](#create-cloud-environments).

### Requisitos previos {#prerequisites}

* El administrador del sistema asignado a la función *Propietario del negocio* debe acceder a Cloud Manager e iniciar sesión.

* Obtenga información sobre cómo [navegar e iniciar sesión en Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/navigate-to-cloud-manager.html?lang=en).

* Familiarícese con los [perfiles de producto de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/aem-cs-team-product-profiles.html?lang=en#cloud-manager-product-profiles).

* Comprenda las consideraciones para crear su programa. Vea este vídeo para obtener más información.

* Entender los conceptos de los [programas](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html?lang=en) y [entornos](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en) de Cloud Manager

## Vaya a Cloud Manager {#navigate-cloud-manager}

1. El usuario *Propietario del negocio* recibirá un correo electrónico de bienvenida desde el que podrá empezar, o si no puede encontrarlo, vaya directamente a [Adobe Experience Cloud](https://experience.adobe.com/#/@ccs/home) e inicie sesión con su Adobe ID.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources1.png)

1. En la página de inicio de Adobe Experience Cloud, seleccione **Experience Manager**.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources2.png)

1. Esto lo llevará a la página principal de AEM. A partir de aquí, inicie **Cloud Manager** .

   ![](/help/onboarding/onboarding-journey/assets/setup-resources3.png)

1. Aparece la página de aterrizaje de Cloud Manager, como se muestra en la figura siguiente.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources4.png)

1. Compruebe que se le ha asignado el perfil de producto del propietario del negocio. Para ello, seleccione su perfil en la parte superior derecha, como se muestra a continuación.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources5.png)

1. Seleccione **Funciones de usuario** y asegúrese de que está asignado a Propietario empresarial.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources6.png)

1. Esto confirma la función de usuario como propietario empresarial.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources7.png)

   ¡bueno trabajo! Ha iniciado sesión correctamente en Cloud Manager como propietario empresarial.

## Crear programa de Cloud Service {#create-cloud-service-program}

Siga los pasos a continuación para crear su programa de servicios en la nube desde Cloud Manager:

1. Vaya a la página de aterrizaje de Cloud Manager como se muestra a continuación.

   >[!NOTE]
   >Debe ser un miembro del equipo asignado al perfil de producto Propietario empresarial de Cloud Manager para completar correctamente este paso.

   Desde aquí, haga clic en **Agregar programa** para iniciar el asistente Agregar programa.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources4.png)

   >[!NOTE]
   >Vea el [vídeo](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en) para aprender a crear su programa AEM as a Cloud y conocer las consideraciones importantes antes de crear su programa.

   >[!IMPORTANT]
   >Para obtener instrucciones paso a paso sobre cómo utilizar el asistente Agregar programa, vaya [aquí](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/production-programs/creating-production-program.html?lang=en).
   >
   >* Recuerde que el nombre del programa no se puede cambiar después de la creación. Le recomendamos que sepa con certeza qué nombre desea dar a su programa.
   >* En el caso de que tenga que cambiar el nombre de su programa, implicará abrir un caso con el Soporte de Adobe o contactar con su representante de Adobe. Ayudarán a eliminar eficazmente el programa. Tendrá que empezar de nuevo con la posible pérdida de trabajo que su equipo ha hecho.


1. Una vez creado correctamente su programa en la nube, puede navegar hasta su programa para ver la página **Información general** de su programa, como se muestra a continuación.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources8.png)

   >[!NOTE]
   >Si aún no lo ha hecho, es un buen momento para agregar sus miembros de desarrollador a su equipo de Cloud Manager. Consulte Añadir usuarios al perfil de producto del desarrollador y siga los pasos descritos.

1. Los miembros asignados al perfil de producto del desarrollador pueden iniciar sesión en Cloud Manager y [Administrar Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en).

   ¡bueno trabajo! Ahora que el programa se ha creado correctamente, el Git de Cloud Manager está disponible para que sus desarrolladores tengan acceso a él.


## Crear entornos de Cloud {#create-cloud-environments}

Una vez que haya creado correctamente su programa de nube, cree sus entornos de nube.

Siga los pasos a continuación para crear los entornos de nube desde Cloud Manager:

1. Vaya a la página **Información general** de Cloud Manager y seleccione **Agregar** en la tarjeta de entorno.

   ![](/help/onboarding/onboarding-journey/assets/setup-resources9.png)

   >[!IMPORTANT]
   >Un usuario de Cloud Manager con la función Propietario empresarial o Administrador de implementación debe iniciar sesión para completar correctamente este paso.

   Además, vea el rápido tutorial [video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en) para obtener más información sobre los entornos de Cloud Manager y cómo puede añadirlos a su programa.

1. Esto iniciará el asistente para agregar entorno que le guiará en la adición de su entorno. Agregue primero su entorno de desarrollo para familiarizarse. Consulte [Adición de un entorno](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html?lang=en#adding-environments) para obtener más información.

   >[!NOTE]
   >Si aún no lo ha hecho, es un buen momento para agregar sus miembros de desarrollador a su equipo de Cloud Manager. Consulte Añadir usuarios al perfil de producto del desarrollador y siga los pasos descritos.

1. Los miembros asignados al perfil de producto del desarrollador pueden iniciar sesión en Cloud Manager y [Administrar Cloud Manager Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en).

   ¡bueno trabajo! Ahora que el programa se ha creado correctamente, el Git de Cloud Manager está disponible para que sus desarrolladores tengan acceso a él.

   Felicitaciones! Ahora, se han creado los entornos de programa de nube y los desarrolladores se han añadido al equipo.

## Siguientes pasos {#whats-next}

Los miembros del equipo deben tener permisos para la instancia, ya que los permisos para administrar Cloud Manager no serán suficientes. Ahora que los recursos de la nube se han creado y están listos para que su equipo los pueda acceder, el administrador del sistema debe asignar a los integrantes del equipo AEM como perfiles de producto de Cloud Service de Admin Console.

Debe continuar con su recorrido de incorporación revisando el documento Asignando integrantes del equipo a AEM como perfiles de producto de Cloud Service.

>[!NOTE]
>Para que se le conceda acceso a AEM como Cloud Service, los usuarios deben pertenecer a uno de los dos perfiles de producto &quot;AEM usuarios&quot; o &quot;AEM administradores&quot;. Más información.

## Recursos adicionales {#additional-resources}

Siga los recursos adicionales para obtener más información:

* [Tipos de programas y adición de un programa](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en)
* [Tipos de entorno y adición de un entorno](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en)
* [Administración de Git de Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/accessing-git.html?lang=en)
* [Configuración del acceso a AEM como Cloud Service desde el Admin Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#adobe-ims-users)
