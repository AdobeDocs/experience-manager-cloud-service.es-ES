---
title: Agregar una canalización de Edge Delivery
description: Aprenda a añadir una canalización de Edge Delivery para crear e implementar su código en entornos de producción.
index: false
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
badge: label="Beta privada" type="Positive" url="/help/implementing/cloud-manager/release-notes/current.md#gitlab-bitbucket"
hide: true
hidefromtoc: true
source-git-commit: 169de7971fba829b0d43e64d50a356439b6e57ca
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 38%

---



# Añadir una canalización de Edge Delivery {#configure-production-pipeline}

Obtenga información sobre cómo configurar canalizaciones de Edge Delivery para crear e implementar su código en entornos de producción. Una canalización de producción implementa el código primero en el entorno de ensayo. En el momento de la aprobación, implementa el mismo código en el entorno de producción.

Un usuario debe tener la función **[Administrador de implementación](/help/onboarding/cloud-manager-introduction.md#role-based-permissions)** para configurar las canalizaciones de producción.

>[!NOTE]
>
>No se puede configurar una canalización de producción hasta que se produzca lo siguiente:
>
>* Se crea el programa.
>* El repositorio de Git tiene al menos una rama.
>* Se crean los entornos de producción y ensayo.

Antes de comenzar a implementar el código, establece la configuración de la canalización desde [!UICONTROL Cloud Manager].

>[!NOTE]
>
>Puede [editar la configuración de canalización](managing-pipelines.md) después de la configuración inicial.

## Añadir una nueva canalización de Edge Delivery {#adding-production-pipeline}

Una vez que haya configurado el programa y tenga al menos un entorno usando la interfaz de usuario de [!UICONTROL Cloud Manager], puede añadir una canalización de producción siguiendo estos pasos.

>[!TIP]
>
>Antes de configurar una canalización front-end, consulte el [Recorrido de creación rápida de sitios de AEM](/help/journey-sites/quick-site/overview.md) para obtener una guía completa a través de la herramienta de creación rápida de sitios de AEM fácil de usar. Este recorrido puede ayudarle a optimizar el desarrollo front-end de su sitio de AEM, lo que le permite personalizar su sitio rápidamente sin conocimiento del back-end de AEM.

**Para agregar una nueva canalización de Edge Delivery:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. Vaya a la tarjeta **Canalizaciones** de la página **Resumen del programa** y haga clic en **Agregar** para seleccionar **Agregar canalización de producción**.

   ![Información general de la tarjeta Canalizaciones de Administrador de programa](/help/implementing/cloud-manager/assets/configure-pipeline/add-prod-1.png)

1. Aparece el cuadro de diálogo **Agregar canalización de producción**. Proporcione un **Nombre de canalización** para identificar la canalización junto con las siguientes opciones. Haga clic en **Continuar**.

   **Activador de implementación**: dispone de las siguientes opciones al definir los activadores de implementación para iniciar la canalización.

   * **Manual**: inicie la canalización manualmente.
   * **Cambios en Git**: inicia la canalización de CI/CD cada vez que se agregan confirmaciones a la rama Git configurada. Con esta opción, aún puede iniciar la canalización manualmente según sea necesario.

   **Comportamiento de errores de métricas importantes**: durante la configuración o edición de la canalización, el **Administrador de implementación** tiene la opción de definir el comportamiento de la canalización cuando se encuentra un error importante en cualquiera de las puertas de calidad. Las opciones disponibles son:

   * **Preguntar cada vez**: configuración predeterminada. Requiere intervención manual en cualquier fallo importante.
   * **Fallo inmediatamente**: si se selecciona, la canalización se cancela siempre que se produzca un fallo importante. Básicamente, este proceso emula a un usuario rechazando manualmente cada error.
   * **Continuar inmediatamente**: si se selecciona, la canalización se ejecuta automáticamente cada vez que se produce un error importante. Básicamente, este proceso emula al usuario que aprueba manualmente cada error.

   ![Configuración de canalización de producción](/help/implementing/cloud-manager/assets/configure-pipeline/production-pipeline-configuration.png)

1. En la ficha **Código Source**, seleccione qué tipo de código debe procesar la canalización.

   * **[Configurar una canalización de código de pila completa](#full-stack-code)**
   * **[Configurar una canalización de implementación de destino](#targeted-deployment)**

Consulte [Canalizaciones de CI/CD](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) para obtener más información sobre los tipos de canalizaciones.

Los pasos para completar la creación de la canalización de producción varían según el tipo de código fuente seleccionado. Siga los vínculos anteriores para ir a la siguiente sección de este documento para poder completar la configuración de la canalización.

