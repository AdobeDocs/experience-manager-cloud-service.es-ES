---
title: Agregar una canalización de Edge Delivery
description: Aprenda a añadir una canalización de Edge Delivery para crear e implementar su código en entornos de producción.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: false
index: false
hidefromtoc: false
exl-id: 5ad342fa-dd71-4105-a9cb-2d999d402780
source-git-commit: 9ad50747b46b75c33cb5b034e8b8e41d5079e967
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 9%

---

# Añadir una canalización de Edge Delivery {#configure-production-pipeline}

<!--badge: label="Beta" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket" -->

Obtenga información sobre cómo configurar canalizaciones de Edge Delivery para crear e implementar su código en entornos de producción. Las canalizaciones de Edge Delivery le permiten configurar funciones, incluido el reenvío de registros y la CDN administrada por Adobe.

Para obtener una lista de la configuración admitida, consulte [Usar canalizaciones de configuración: configuraciones admitidas](/help/operations/config-pipeline.md#configurations).

Un usuario debe tener la función **[Administrador de implementación](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar las canalizaciones de producción.

>[!IMPORTANT]
>
>No se puede configurar una canalización de Edge Delivery hasta que se haya producido lo siguiente:
>
>* Se crea un programa que contiene un sitio de Edge Delivery Services y un dominio asignado. De lo contrario, la opción **Agregar canalización de Edge Delivery** aparecerá deshabilitada en la interfaz de usuario y se mostrará información sobre los requisitos que faltan. Ver [Crear un sitio de Edge Delivery en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/create-edge-delivery-site.md)
>* El repositorio de Git tiene al menos una rama. Ver [Administrar repositorios en Cloud Manager](/help/implementing/cloud-manager/managing-code/managing-repositories.md).
>* Se crean los entornos de producción y ensayo. Consulte [Introducción a las canalizaciones de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md).

<!-- CMGR‑69680 -->

Antes de comenzar a implementar el código, establece la configuración de la canalización desde [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Puede [editar la configuración de canalización](managing-pipelines.md) después de la configuración inicial.

**Para agregar una canalización de Edge Delivery:**

1. Inicie sesión en Cloud Manager en [experience.adobe.com](https://experience.adobe.com).
1. En la sección **Acceso rápido**, haga clic en **Experience Manager**.
1. En el panel lateral izquierdo, haga clic en **Cloud Manager**.
1. Seleccione la organización que desee.
1. En la consola **Mis programas**, haga clic en un programa.

   ![Página de mis programas en Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/assets/my-programs.png)

1. Realice una de las siguientes acciones:

   * **Agregar una canalización de Edge Delivery desde la tarjeta Canalizaciones**

      1. En el carril izquierdo, debajo de **Programa**, haga clic en **![icono Información general](/help/implementing/cloud-manager/configuring-pipelines/assets/overview.svg) [Información general](/help/implementing/cloud-manager/navigation.md#my-programs)**.
      1. En la página **Información general del programa**, en la tarjeta **Canalizaciones**, haga clic en **![Signo más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg)Agregar** y, a continuación, seleccione **Agregar canalización de Edge Delivery**.

         ![La tarjeta Canalizaciones en la página Información general del programa](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinescard-add-ed-pipeline.png)

         >[!TIP]
         >
         >Además de usar la tarjeta **Canalización**, como se ve en la captura de pantalla anterior, también puede administrar la canalización desde la página **Canalizaciones**.
         >
         >![Widget de canalización de Edge Delivery que muestra el nombre, el estado, el repositorio y la rama de la canalización](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)

   * **Agregar una canalización de Edge Delivery desde la página Canalizaciones**

      1. En el carril izquierdo, debajo de **Programa**, haga clic en **![icono de flujo de trabajo o icono de canalizaciones](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) Canalizaciones**.
      1. En la página Canalizaciones, cerca de la esquina superior derecha, haga clic en **Agregar canalización** > **Agregar canalización de Edge Delivery**.

         ![La página Canalizaciones con el botón Agregar canalización](/help/implementing/cloud-manager/configuring-pipelines/assets/pipelinespage-add-ed-pipeline.png)

         >[!TIP]
         >
         >Cerca de la esquina superior izquierda, haga clic en **Filtros** y, a continuación, en la sección **Tipo de entrega**, active la casilla de verificación **Envío de Edge** para filtrar la lista y establecer que solo haya canalizaciones de Edge Delivery (es decir, canalizaciones que utilicen Edge Delivery Services). <!-- (CMGR-69682) -->
         >
         >![Panel de filtro que muestra el nuevo tipo de envío de Edge y el envío de publicación](/help/implementing/cloud-manager/release-notes/assets/filter-delivery-type.png)

1. En el cuadro de diálogo **Agregar canalización de Edge Delivery**, en el campo de texto **Nombre de canalización**, escriba una etiqueta de canalización descriptiva.

   ![Cuadro de diálogo Agregar canalización de Edge Delivery](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-configuration.png)

1. Seleccione la opción de canalización **Déclencheur de implementación** que desee.

   * **Manual**: usted inicia la implementación.
   * **Cambios en Git**: Git confirma el inicio de la implementación automáticamente. Con esta opción, aún puede iniciar la canalización manualmente, si es necesario.

1. Haga clic en **Continuar**.

1. En **Código Source**, defina las siguientes opciones:

   * **Entorno de implementación** - Muestra el campo de entorno de destino; permanece como de solo lectura.

   * **Repositorio**: utilice la lista desplegable para dirigir la canalización al repositorio Git exacto que almacena la configuración de Edge Delivery.

     Consulte también [Agregar y administrar repositorios](/help/implementing/cloud-manager/managing-code/managing-repositories.md) para obtener información sobre cómo agregar y administrar repositorios en Cloud Manager.

   * **Rama de Git**: utilice la lista desplegable para seleccionar una rama específica dentro del repositorio elegido. Si es necesario, haga clic en ![Icono de reciclaje o en Actualizar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) para volver a cargar la lista desplegable de la rama Git después de inserciones recientes.
   * **Ubicación del código**: define la ruta de carpeta dentro del repositorio donde se inicia el código listo para la canalización ( `/` es igual a la raíz del repositorio).

   ![Canalización de configuración](/help/implementing/cloud-manager/configuring-pipelines/assets/add-edge-delivery-pipeline-sourcecode.png)

1. Haga clic en **Guardar**.

Ahora puede [administrar su canalización](managing-pipelines.md) desde la tarjeta **Canalizaciones** en la página **Información general del programa** o desde la página **Canalizaciones**.


![Widget de canalización de Edge Delivery que muestra el nombre, el estado, el repositorio y la rama de la canalización](/help/implementing/cloud-manager/release-notes/assets/edge-delivery-pipeline-widget.png)



