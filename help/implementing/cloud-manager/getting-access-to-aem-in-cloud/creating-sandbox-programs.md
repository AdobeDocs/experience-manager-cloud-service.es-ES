---
title: Creación de programas de zona protegida
description: Aprenda a utilizar Cloud Manager para crear su propio programa de zona protegida para formación, demostración, POC u otros fines que no sean de producción.
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: b916bf5b252045120659600293e004fc34b96e7a
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 67%

---

# Creación de programas de zona protegida {#create-sandbox-program}

Un programa de zona protegida suele crearse para servir a los fines de formación, ejecución de demostraciones, habilitación, POC o documentación, y no está diseñado para transportar tráfico en directo.

Obtenga más información sobre los tipos de programas en el documento [Explicación de los programas y sus tipos.](program-types.md)

## Creación de un programa de zona protegida {#create}

Siga estos pasos para crear un programa de zona protegida.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la página de aterrizaje de Cloud Manager, haga clic en **Agregar programa** en la esquina superior derecha de la pantalla.

   ![Página de aterrizaje de Cloud Manager](assets/cloud-manager-my-programs.png)

1. En el asistente crear programa, seleccione **Configuración de un simulador para pruebas** y proporcione un nombre de programa.

   ![Creación de tipo de programa](assets/create-sandbox.png)

1. De forma opcional, puede agregar una imagen al programa arrastrando y soltando un archivo de imagen al **Agregar una imagen de programa** haga clic o establezca como destino una imagen para seleccionarla en un explorador de archivos. Haga clic o pulse **Continuar**.

   * La imagen solo sirve como mosaico en la ventana de información general del programa y ayuda a identificar el programa.

1. En el **Configuración del simulador para pruebas** , elija las soluciones que desea habilitar en el programa de simulación de pruebas comprobando las opciones de **Soluciones y complementos** tabla.

   * Utilice las comillas angulares situadas junto a los nombres de las soluciones para mostrar complementos adicionales y opcionales para las soluciones.

   * La variable **Sitios** y **Recursos** las soluciones de siempre se incluyen en los programas de entornos limitados y no se pueden anular las selecciones.

   ![Seleccionar soluciones y complementos para un simulador de pruebas](assets/sandbox-solutions-add-ons.png)

1. Una vez seleccionadas las soluciones y los complementos para el programa de simulación de pruebas, pulse en **Crear**.

Verá una nueva tarjeta de programa de zona protegida en la página de aterrizaje con un indicador de estado a medida que avance el proceso de configuración.

![Creación de una zona protegida desde la página Información general](assets/sandbox-setup.png)

## Acceso a Simulador para pruebas {#access}

Puede ver los detalles de la configuración de la zona protegida, así como acceder al entorno (una vez disponible) en la página de información general del programa.

1. En la página de aterrizaje de Cloud Manager, haga clic en el botón de puntos suspensivos del programa recién creado.

   ![Acceso a la información general del programa](assets/program-overview-sandbox.png)

1. Una vez completado el paso de creación del proyecto, puede acceder al vínculo **Acceder a la info del repositorio** para poder usar su repositorio de Git.

   ![Configuración del programa](assets/create-program4.png)

   >[!TIP]
   >
   >Para obtener más información sobre el acceso y la administración del repositorio de Git, consulte el documento [Acceso a Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

1. Una vez creado el entorno de desarrollo, puede usar el vínculo **Acceso a AEM** para iniciar sesión en AEM.

   ![Vínculo Acceso a AEM](assets/create-program-5.png)

1. Una vez completada la implementación de la canalización de no producción en el desarrollo, el asistente le guía para acceder al entorno de desarrollo de AEM o para implementar código en el entorno de desarrollo.

   ![Implementación de zonas protegidas](assets/create-program-setup-deploy.png)

Si en cualquier momento necesita cambiar a otro programa o volver a la página de información general para crear otro programa, haga clic en el nombre del programa en la parte superior izquierda de la pantalla para mostrar la opción **Vaya a**.

![Vaya a](assets/create-program-a1.png)
