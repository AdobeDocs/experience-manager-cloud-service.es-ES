---
title: Configuración de canalizaciones que no sean de producción
description: Configuración de canalizaciones que no sean de producción
index: false
source-git-commit: 84d04d8399668b8b1051d4edf9de851bca271071
workflow-type: tm+mt
source-wordcount: '311'
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

1. Select **Código de pila completa** o **Código front-end**. Puede elegir el **Repositorio** y **Rama de Git**. Haga clic en **Guardar**.

   >[!NOTE]
   >Antes de empezar a configurar las canalizaciones del front-end, consulte AEM Recorrido de creación rápida de sitios para obtener un flujo de trabajo completo a través de la herramienta de creación rápida AEM sitios, fácil de usar. Este sitio de documentación le ayudará a optimizar el desarrollo front-end de su sitio AEM y a personalizar rápidamente su sitio sin AEM conocimiento back-end.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add3.png)

1. La canalización que no es de producción recién creada ahora se muestra en la **Canalizaciones** tarjeta.

   ![](/help/implementing/cloud-manager/assets/configure-pipeline/nonprod-pipeline-add4.png)


   La canalización se muestra en la tarjeta de la pantalla principal con tres acciones, como se muestra a continuación:

   * **Agregar** : permite añadir una nueva canalización.
   * **Acceder a información de repositorios** : permite al usuario obtener la información necesaria para acceder al repositorio Git de Cloud Manager.
   * **Más información** : navega para comprender el recurso de documentación de canalización CI/CD.