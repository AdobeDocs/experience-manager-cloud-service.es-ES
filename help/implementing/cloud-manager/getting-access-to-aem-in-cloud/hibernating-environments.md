---
title: 'Entornos de zona protegida en hibernación y dehibernación '
description: Descubra cómo los entornos de un programa de simulación de pruebas entran automáticamente en modo de hibernación y cómo puede anular la hibernación.
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
source-git-commit: 5cb58b082323293409aad08d4e5dd9289283e0a6
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---


# Entornos de espacio aislado en hibernación y dehibernación {#hibernating-introduction}

Los entornos de un programa de espacio aislado entran en un modo de hibernación si no se detecta ninguna actividad durante ocho horas.La hibernación es única para los entornos de programa de espacio aislado. Los entornos de programas de producción no hibernan.

## Hibernación {#hibernation-introduction}

La hibernación puede producirse de forma automática o manual.

* **Automático** - Los entornos de programa del Simulador para pruebas hibernan automáticamente tras ocho horas de inactividad. La inactividad se define como que ni el servicio de autor ni la vista previa o los servicios de publicación reciben solicitudes.
* **Manual** - Como usuario, puede hibernar manualmente un entorno de programa de simulación de pruebas. No es necesario hacerlo, ya que la hibernación se producirá automáticamente como se describió anteriormente.

Puede tardar hasta unos minutos en que los entornos de programa del simulador de pruebas entren en modo de hibernación. Los datos se conservan durante la hibernación.

### Uso de hibernación manual {#using-manual-hibernation}

Puede hibernar manualmente el programa de simulación de pruebas desde Developer Console. Cualquier usuario de Cloud Manager puede acceder a Developer Console para un programa de simulador de pruebas.

Siga estos pasos para hibernar manualmente los entornos de programa del simulador para pruebas.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa que desea hibernar para mostrar sus detalles.

1. En el **Entornos** , haga clic en el botón de puntos suspensivos y seleccione **Developer Console**.

   * Consulte el documento [Acceso a Developer Console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) para obtener más información sobre Developer Console.

   ![Opción de menú de Developer Console](assets/developer-console-menu-option.png)

1. En Developer Console, haga clic en **Hibernar**.

   ![Botón Hibernar](assets/hibernate-1.png)

1. Haga clic en **Hibernar** para confirmar el paso.

   ![Confirmar hibernación](assets/hibernate-2.png)

Cuando la hibernación se realice correctamente, verá la notificación de finalización del proceso de hibernación para su entorno en la sección **Developer Console** en el Navegador.

![Confirmación de hibernación](assets/hibernate-4.png)

En Developer Console también puede hacer clic en la **Entornos** en las rutas de exploración por encima de la **Pod** lista desplegable de una lista de entornos para hibernar.

![Lista de entornos para hibernar](assets/hibernate-1b.png)

## Deshibernación {#de-hibernation-introduction}

Puede hibernar manualmente el programa de espacio aislado para pruebas desde Developer Console.

>[!IMPORTANT]
>
>Un usuario con un **Desarrollador** puede anular la hibernación de un entorno de programa de entorno limitado.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. Haga clic en el programa que desea hibernar para mostrar sus detalles.

1. En el **Entornos** , haga clic en el botón de puntos suspensivos y seleccione **Developer Console**.

   * Consulte el documento [Acceso a Developer Console](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) para obtener más información sobre Developer Console.

1. Haga clic en **Deshibernar**.

   ![Botón Deshibernar](assets/de-hibernation-img1.png)

1. Haga clic en **Deshibernar** para confirmar el paso.

   ![Confirmar anulación de hibernación](assets/de-hibernation-img2.png)

1. Recibirá una notificación avisando de que el proceso de deshibernación se ha iniciado y se actualiza con el progreso.

   ![Notificación de progreso de hibernación](assets/de-hibernation-img3.png)

1. Una vez finalizado el proceso, el entorno del programa del simulador para pruebas vuelve a estar activo.

   ![Finalización de la dehibernación](assets/de-hibernation-img4.png)


En Developer Console también puede hacer clic en la **Entornos** en las rutas de exploración por encima de la **Pod** lista desplegable de una lista de entornos para anular la hibernación.

![Lista de pods hibernados](assets/de-hibernate-1b.png)

### Permisos para anular la hibernación {#permissions-de-hibernate}

Cualquier usuario con un perfil de producto que les permita acceder a AEM as a Cloud Service debe poder acceder a la variable **Developer Console**, permitiéndoles anular la hibernación del entorno.

## Acceso a un entorno en hibernación {#accessing-hibernated-environment}

Al realizar solicitudes de explorador contra el servicio de autor, vista previa o publicación de un entorno hibernado, el usuario se encontrará con una página de aterrizaje que describe el estado de hibernación del entorno junto con un vínculo a Developer Console donde el servicio se puede anular de hibernación.

![Página de aterrizaje de servicio en hibernación](assets/de-hibernation-img5.png)

## Implementaciones y actualizaciones AEM {#deployments-updates}

Los entornos en hibernación aún permiten implementaciones y actualizaciones de AEM manuales.

* Un usuario puede utilizar una canalización para implementar código personalizado en entornos en hibernación. El entorno permanecerá en hibernación y el nuevo código aparecerá en el entorno una vez que se haya deshibernado.

* AEM actualizaciones se pueden aplicar a entornos hibernados y se pueden activar manualmente desde Cloud Manager. El entorno permanecerá en hibernación y la nueva versión aparecerá en el entorno una vez que esté en desuso.

## Hibernación y eliminación {#hibernation-deletion}

* Los entornos de un programa de simulación de pruebas hibernan automáticamente tras ocho horas de inactividad.
   * La inactividad se define como que ni el servicio de autor ni la vista previa o los servicios de publicación reciben solicitudes.
   * Una vez hibernados, se pueden anular manualmente la hibernación.
* Los programas de espacio aislado se eliminan después de seis meses de estar en modo de hibernación continua, después de lo cual se pueden volver a crear.
