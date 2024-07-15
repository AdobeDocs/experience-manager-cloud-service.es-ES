---
title: Creación de programas de zona protegida
description: Aprenda a utilizar Cloud Manager para crear su propio programa de zona protegida para formación, demostración, POC u otros fines que no sean de producción.
exl-id: 10011392-3059-4bb0-88db-0af1d390742e
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 74%

---

# Creación de programas de zona protegida {#create-sandbox-program}

Un programa de zona protegida suele crearse para servir a los fines de formación, ejecución de demostraciones, habilitación, POC o documentación, y no está diseñado para transportar tráfico en directo.

Obtenga más información sobre los tipos de programas en el documento [Explicación de los programas y sus tipos.](program-types.md)

## Creación de un programa de zona protegida {#create}

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, toque o haga clic en **Agregar programa** cerca de la esquina superior derecha de la pantalla.

   ![Página de aterrizaje de Cloud Manager](assets/log-in.png)

1. En el asistente Crear programa, seleccione **Configuración de una zona protegida** y proporcione un nombre de programa.

   ![Creación de tipo de programa](assets/create-sandbox.png)

1. Si lo desea, puede agregar una imagen al programa arrastrando y soltando un archivo de imagen en el destino **Agregar una imagen de programa** o haciendo clic en él para seleccionar una imagen de un explorador de archivos. Seleccione **Continuar**.

   * La imagen solo sirve como mosaico en la ventana de información general del programa y ayuda a identificar el programa.

1. En el cuadro de diálogo **Configurar la zona protegida**, elija qué soluciones desea habilitar en el programa de zona protegida marcando las opciones en la tabla **Soluciones y complementos**.

   * Utilice las comillas angulares que aparecen junto a los nombres de las soluciones para mostrar complementos opcionales adicionales para las soluciones.

   * Las soluciones de **Sites** y **Assets** siempre se incluyen en los programas de zonas protegidas y no se pueden anular.

   ![Seleccionar soluciones y complementos para una zona protegida](assets/sandbox-solutions-add-ons.png)

1. Una vez seleccionadas las soluciones y los complementos de su programa de zona protegida, haga clic en **Crear**.

Verá una nueva tarjeta de programa de zona protegida en la página de aterrizaje con un indicador de estado a medida que avance el proceso de configuración.

![Creación de una zona protegida desde la página Información general](assets/sandbox-setup.png)

## Acceso a zona protegida {#access}

Puede ver los detalles de la configuración de la zona protegida, así como acceder al entorno (una vez disponible) en la página de información general del programa.

1. En la página de aterrizaje de Cloud Manager, haga clic en el botón de puntos suspensivos del programa creado.

   ![Acceso a la información general del programa](assets/program-overview-sandbox.png)

1. Una vez completado el paso de creación del proyecto, puede acceder al vínculo **Acceder a la información del repositorio** para poder usar su repositorio de Git.

   ![Configuración del programa](assets/create-program4.png)

   >[!TIP]
   >
   >Para obtener más información sobre el acceso y la administración del repositorio de Git, consulte el documento [Acceso a Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

1. Una vez creado el entorno de desarrollo, puede usar el vínculo **Acceso a AEM** para iniciar sesión en AEM.

   ![Vínculo Acceso a AEM](assets/create-program5.png)

1. AEM Una vez completada la implementación de la canalización que no es de producción en el entorno de desarrollo, el asistente de la llamada a la acción le guía para acceder al entorno de desarrollo de o para implementar código en el entorno de desarrollo.

   ![Implementación de zonas protegidas](assets/create-program-setup-deploy.png)

>[!TIP]
>
>Consulte el documento [Navegación por la interfaz de usuario de Cloud Manager](/help/implementing/cloud-manager/navigation.md) para obtener más información sobre cómo navegar por Cloud Manager y comprender la consola **Mis programas**.
