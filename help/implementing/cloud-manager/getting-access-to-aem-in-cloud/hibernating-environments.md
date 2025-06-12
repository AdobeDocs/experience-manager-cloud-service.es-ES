---
title: Entornos de zona protegida en hibernación y dehibernación
description: Descubra cómo los entornos de un programa de zona protegida entran automáticamente en modo de hibernación y cómo puede anularlo.
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 169de7971fba829b0d43e64d50a356439b6e57ca
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 42%

---


# Entornos de zona protegida en hibernación y dehibernación {#hibernating-introduction}

Los entornos de un programa de zona protegida entran en modo de hibernación si no se detecta ninguna actividad durante ocho horas. La hibernación es única para entornos de programa de zona protegida. Los entornos de programa de producción no pueden hibernar.

## Hibernación {#hibernation-introduction}

La hibernación puede producirse de forma automática o manual.

* **Automática**: Los entornos de programa de zona protegida hibernan automáticamente tras ocho horas de inactividad. La inactividad se define como la ausencia de solicitudes a los servicios de autor, vista previa y publicación.
* **Manual**: Como usuario, puede hacer hibernar manualmente un entorno de zona protegida. No es necesario hacerlo porque la hibernación se produce automáticamente como se describió anteriormente.

Puede tardar hasta unos minutos en que los entornos de programa de zona protegida entren en modo de hibernación. Los datos se conservan durante la hibernación.

### Hibernar manualmente un entorno de programa de zona protegida {#using-manual-hibernation}

Puede hibernar manualmente el programa de zona protegida desde Developer Console. Cualquier usuario de Cloud Manager puede acceder a Developer Console para un programa de zona protegida.

**Para hibernar manualmente un entorno de programa de zona protegida:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, haga clic en un *programa de zona protegida* que desee hibernar para mostrar sus detalles.

1. En la tarjeta **Entornos**, haga clic en ![Más icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y luego en **Developer Console**.

   * Consulte [Acceso a Developer Console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) para obtener más información sobre Developer Console.

   ![Opción del menú de Developer Console](/help/implementing/cloud-manager/assets/developer-console-menu-option.png)

1. En la página **Developer Console**, haga clic en **Hibernar**.

<!-- UPDATE THESE SCREENSHOTS WHEN NEW AEM DEVELOPER CONSOLE UI IS RELEASED. AS OF OCTOBER 14, 2024, NEW UI IS STILL IN PRIVATE BETA -->

![Botón Hibernar](assets/hibernate-1.png)

1. Haga clic en **Hibernar** para confirmar el paso.

   ![Confirmar hibernación](assets/hibernate-2.png)

Cuando la hibernación se realice correctamente, verá la notificación de finalización del proceso de hibernación para su entorno en la pantalla **Developer Console**.

![Confirmación de hibernación](assets/hibernate-4.png)

En Developer Console, haga clic en el vínculo **Entornos** en las rutas de exploración encima de la lista desplegable **Pod** para ver los entornos disponibles para la hibernación.

![Lista de entornos para hibernar](assets/hibernate-1b.png)

## Anular la hibernación manual de un programa de zona protegida desde Developer Console {#de-hibernation-introduction}

Puede hibernar manualmente el programa de zona protegida desde Developer Console.

>[!IMPORTANT]
>
>Un usuario con un rol de **Desarrollador** puede anular la hibernación de un entorno de programa de zona protegida.

**Para anular manualmente la hibernación de un programa de zona protegida de Developer Console:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, haga clic en el programa que desea anular la hibernación para mostrar sus detalles.

1. En la tarjeta **Entornos**, haga clic en ![Más icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) y luego en **Developer Console**.

   * Consulte [Acceso a Developer Console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) para obtener más información sobre Developer Console.

1. Haga clic en **Deshibernar**.

   ![Botón Deshibernar](assets/de-hibernation-img1.png)

1. Haga clic en **Deshibernar** para confirmar el paso.

   ![Confirmar anulación de hibernación](assets/de-hibernation-img2.png)

1. Recibirá una notificación que le avisa de que el proceso de anulación de la hibernación se ha iniciado y se actualiza con el progreso.

   ![Notificación del progreso de la hibernación](assets/de-hibernation-img3.png)

1. Una vez finalizado el proceso, el entorno del programa de zona protegida vuelve a estar activo.

   ![Finalización de la hibernación](assets/de-hibernation-img4.png)

En Developer Console, haga clic en el vínculo **Entornos** en las rutas de exploración encima de la lista desplegable **Pod** para acceder a los entornos disponibles para la dehibernación.

![Lista de pods hibernados](assets/de-hibernate-1b.png)

### Permisos para anular la hibernación {#permissions-de-hibernate}

Cualquier usuario con un perfil de producto que le permita acceder a AEM as a Cloud Service debe poder acceder a **Developer Console**, permitiéndole anular la hibernación del entorno.

## Acceso a un entorno en hibernación {#accessing-hibernated-environment}

Cuando un usuario realiza una solicitud de explorador al servicio de autor, vista previa o publicación de un entorno hibernado, se encuentra con una página de aterrizaje. En esta página se explica el estado de hibernación del entorno y se proporciona un vínculo a Developer Console para la anulación de la hibernación.

![Página de aterrizaje del servicio en hibernación](assets/de-hibernation-img5.png)

## Implementaciones y actualizaciones de AEM {#deployments-updates}

Los entornos en hibernación aún permiten implementaciones y actualizaciones manuales de AEM.

* Un usuario puede utilizar una canalización para implementar código personalizado en entornos en hibernación. El entorno permanece en hibernación y el nuevo código aparece en el entorno una vez deshibernado.

* Las actualizaciones de AEM se pueden aplicar a entornos hibernados y se pueden activar manualmente desde Cloud Manager. El entorno permanece en hibernación y la nueva versión aparece en el entorno una vez que se ha anulado la hibernación.

## Hibernación y eliminación {#hibernation-deletion}

* Los entornos de un programa de zona protegida hibernan automáticamente tras ocho horas de inactividad.
   * La inactividad se define como la ausencia de solicitudes a los servicios de autor, vista previa y publicación.
   * Una vez hibernados, se puede [anular la hibernación manualmente](#de-hibernation-introduction).
* Los programas de zona protegida se eliminan después de seis meses de estar en modo de hibernación continua, después de lo cual se pueden volver a crear.

>[!NOTE]
>
>Solo los entornos de zona protegida se eliminan automáticamente después de seis meses de hibernación continua. Se conserva el programa de zona protegida con su repositorio y código.
