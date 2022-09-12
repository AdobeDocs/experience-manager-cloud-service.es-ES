---
title: Creación de programas de zona protegida
description: Aprenda a utilizar Cloud Manager para crear su propio programa de simulación de pruebas para formación, demostración, POC u otros fines que no sean de producción.
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
source-git-commit: cf6941759dfc1e50928009490c7c518a89ed093e
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 6%

---

# Creación de programas de zona protegida {#create-sandbox-program}

Un programa de simulación de pruebas suele crearse para servir a los fines de formación, ejecución de demostraciones, habilitación, POC o documentación, y no está diseñado para transportar tráfico en directo.

Obtenga más información sobre los tipos de programas en el documento [Explicación de los tipos de programa y programa.](program-types.md)

## Crear un programa de espacio aislado {#create}

Siga estos pasos para crear un programa de simulación de pruebas.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la página de aterrizaje de Cloud Manager, haga clic en **Agregar programa** en la esquina superior derecha de la pantalla.

   ![Página de aterrizaje de Cloud Manager](assets/first_timelogin1.png)

1. En el asistente crear programa, seleccione **Configuración de un simulador para pruebas**, proporcione un nombre de programa y haga clic en **Crear**.

   ![Creación de tipo de programa](assets/create-sandbox.png)

Verá una nueva tarjeta de programa de simulación de pruebas en la página de aterrizaje con un indicador de estado a medida que avance el proceso de configuración.

![Creación de Simulador para pruebas desde la página de información general](assets/program-create-setupdemo2.png)

## Acceso a Sandbox {#access}

Puede ver los detalles de la configuración del entorno limitado, así como acceder al entorno (una vez disponible) en la página de información general del programa.

1. En la página de aterrizaje de Cloud Manager, haga clic en el botón de puntos suspensivos del programa recién creado.

   ![Acceso a la información general del programa](assets/program-overview-sandbox.png)

1. Una vez completado el paso de creación del proyecto, puede acceder al **Acceder a información de repositorios** para poder usar su repositorio de Git.

   ![Configuración del programa](assets/create-program4.png)

   >[!TIP]
   >
   >Para obtener más información sobre el acceso y la administración del repositorio de Git, consulte el documento [Acceso a Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

1. Una vez creado el entorno de desarrollo, puede usar la variable **Acceso AEM** para iniciar sesión en AEM.

   ![Acceso AEM vínculo](assets/create-program-5.png)

1. Una vez completada la implementación de la canalización de no producción en el desarrollo, el asistente le guía para acceder al entorno de desarrollo de AEM o para implementar código en el entorno de desarrollo.

   ![Implementación de entornos limitados](assets/create-program-setup-deploy.png)

Si en cualquier momento necesita cambiar a otro programa o volver a la página de información general para crear otro programa, haga clic en el nombre del programa en la parte superior izquierda de la pantalla para mostrar la **Vaya a** .

![Vaya a](assets/create-program-a1.png)
