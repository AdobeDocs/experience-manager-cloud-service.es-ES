---
title: Configuración de canalizaciones que no sean de producción
description: Siga esta página para obtener más información sobre la configuración de una canalización que no sea de producción en Cloud Manager
index: true
source-git-commit: 2ac65af4cf410491d1196b9e20f67647e0a1b4d1
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---


# Configuración de canalizaciones que no sean de producción {#configure-non-production-pipeline}

Además de la canalización principal que se implementa en las fases de producción y producción, los clientes pueden configurar canalizaciones adicionales, denominadas canalizaciones que no son de producción.

Existen dos tipos de canalizaciones que no son de producción:

1. Calidad de código: Ejecuta análisis de calidad del código en el código de una rama de Git. Esta canalización ejecuta los pasos de compilación y calidad del código.
1. Implementación: Además de ejecutar los pasos de compilación y calidad del código, esta canalización implementa el código en el entorno no de producción seleccionado en AEM entorno as a Cloud Service.

## Adición de una nueva canalización que no sea de producción {#adding-non-production-pipeline}

En la pantalla de inicio, estas canalizaciones se enumeran en una tarjeta nueva:

1. Acceda a la **Canalizaciones** de la pantalla de inicio de Cloud Manager. Haga clic en **+Añadir** y seleccione **Agregar canalización que no sea de producción**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add1.png)

1. **Agregar canalización que no sea de producción**  se abre. Seleccione el tipo de canalización que desea crear, ya sea **Canalización de calidad de código** o **Canalización de implementación**.

   >[!NOTE]
   >Para las canalizaciones de implementación, debe seleccionar el entorno de implementación.

   Además, también puede configurar **Déclencheur de implementación** y **Comportamiento de errores de métricas importantes** from **Opciones de implementación**. Haga clic en **Continuar**.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add2.png)

   Puede definir los siguientes déclencheur de implementación para iniciar la canalización.

   * **Manual** : al usar la interfaz de usuario, se inicia manualmente la canalización.
   * **Cambios en Git** - inicia la canalización CI/CD cada vez que se añaden confirmaciones a la rama git configurada. Incluso si selecciona esta opción, siempre puede iniciar la canalización manualmente.

      Durante la configuración o edición de la canalización, el administrador de implementación tiene la opción de definir el comportamiento de la canalización cuando se encuentra un error importante en cualquiera de las puertas de calidad.

      Esto resulta útil para los clientes que desean procesos más automatizados. Las opciones disponibles son:
   Puede definir el comportamiento importante de las métricas de error para iniciar la canalización.

   * **Pregunte cada vez** - Esta es la configuración predeterminada y requiere una intervención manual en cualquier error importante.
   * **Fallo Inmediatamente** - Si se selecciona, la canalización se cancelará siempre que se produzca un error importante. Básicamente, esto emula a un usuario rechazando manualmente cada error.
   * **Continuar inmediatamente** - Si está seleccionada, la canalización se realizará automáticamente cada vez que se produzca un error importante. Básicamente, esto está emulando a un usuario que aprueba manualmente cada error.


1. Select **[Código de pila completa](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#full-stack-pipeline)** o **[Código front-end](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)**.

   Si ha seleccionado **Código front-end**, debe seleccionar **Repositorio**, **Rama de Git** y **Ubicación del código**, como se muestra en la figura siguiente:

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-confignew1.png)

   Si ha seleccionado **Código de pila completa**, debe seleccionar **Repositorio** y **Rama de Git**, como se muestra en la figura:
   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack1.png)

   >[!IMPORTANT]
   >Si ya existe una canalización de código de pila completa para el entorno seleccionado, esta selección se desactivará.

   >[!NOTE]
   >Antes de empezar a configurar las canalizaciones del front-end, consulte [AEM Recorrido de creación rápida de sitios](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/sites-journey/quick-site/overview.html) para obtener un flujo de trabajo completo mediante la herramienta de creación rápida AEM sitios, que es muy fácil de usar. Este sitio de documentación le ayudará a optimizar el desarrollo front-end de su sitio AEM y a personalizar rápidamente su sitio sin AEM conocimiento back-end.

1. La canalización que no es de producción recién creada ahora se muestra en la **Canalizaciones** tarjeta.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/non-prod-fullstack2.png)


   La canalización se muestra en la tarjeta de la pantalla principal con cuatro acciones, como se muestra a continuación:

   * **Agregar** : permite añadir una nueva canalización.
   * **Mostrar todo** : permite al usuario ver todas las canalizaciones.
   * **Acceder a información de repositorios** : permite al usuario obtener la información necesaria para acceder al repositorio Git de Cloud Manager.
   * **Más información** : navega para comprender el recurso de documentación de canalización CI/CD.