---
title: Añadir un sitio de Edge Delivery a Cloud Manager
description: Aprenda a añadir un sitio de Edge Delivery a su programa de producción o programa de zona protegida y las ventajas que aporta.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 68f05c49ebc3d46aa44b3998e6142ab8547e5455
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 2%

---


# Añadir un sitio de Edge Delivery a Cloud Manager {#eds-add-site}

Aprenda a añadir un sitio de Edge Delivery a su programa de producción o programa de zona protegida y las ventajas que aporta.

## Introducción {#introduction}

Como parte del proyecto de Edge Delivery Services con AEM as a Cloud Service, se le recomienda añadir su sitio de Edge Delivery a Cloud Manager. Añadir su sitio web de Edge Delivery a Cloud Manager le ofrece las siguientes ventajas.

* [Acceso a CDN administrada por Adobe](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md)
* [Acceso a los informes de SLA](/help/implementing/cloud-manager/sla-reporting.md)
* [Acceso a informes de uso de licencias](/help/implementing/cloud-manager/license-dashboard.md)

Tenga en cuenta que es necesario agregar el sitio de Edge Delivery a Cloud Manager para [registrar un ticket de asistencia para el proyecto de Edge Delivery.](/help/edge/overview.md##support-ticket)

## Adición de un sitio de Edge Delivery a Cloud Manager {#adding}

1. Inicie sesión en Cloud Manager en [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) y seleccione el programa apropiado.
1. Realice una de las siguientes acciones:
   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. A continuación, cerca de la esquina inferior derecha de la página, haga clic en **Agregar sitio de Edge Delivery**.

     ![Agregar sitio Edge Delivery desde la ficha Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * En la esquina superior izquierda de la página, haga clic en el icono de hamburguesa para mostrar el menú de navegación izquierdo. Bajo el encabezado **Servicios**, haga clic en **Sitios Edge Delivery**. Cerca de la esquina superior derecha de la página, haga clic en **Agregar sitio**.

     ![Agregar sitio Edge Delivery desde el botón Sitios Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. En el cuadro de diálogo **Agregar sitio Edge Delivery**, proporcione la siguiente información en los campos obligatorios:

   | Campo de texto | Datos que proporcionar |
   | --- | --- |
   | Nombre del sitio | Escriba el nombre del sitio de Edge Delivery que está agregando. El nombre sirve como identificador único del sitio en Cloud Manager. |
   | URL del repositorio | Este campo hace referencia al repositorio de Git donde se almacena el código del sitio web. Este campo permite a Cloud Manager extraer el código de ese repositorio durante el proceso de implementación. |
   | Descripción del sitio (opcional) | Escriba una breve descripción del sitio de Edge Delivery que está agregando. Esta descripción ayuda a identificar y diferenciar el sitio, lo que facilita la administración y el reconocimiento, entre otros sitios que ha agregado. |

1. En la esquina inferior derecha del cuadro de diálogo, haga clic en **Agregar**.

1. Se abre el cuadro de diálogo **Verificar propiedad del repositorio**. Con la aplicación abierta, realice los siguientes pasos:

   1. Agregue un archivo con la ruta de acceso y el nombre `well-known/adobe/cloudmanager-challenge.txt` a la rama `main` del repositorio Git que aparece en el campo **URL del repositorio**.
      * Si es necesario, haga clic en el icono **Copiar** para copiar la ruta de acceso en el portapapeles.
      * *no* agrega un punto al inicio de la ruta de ubicación.
   1. Agregue el código del campo **Step &amp;num; 1** al archivo que creó en el paso anterior.
      * Si es necesario, haga clic en el icono **Copiar** para copiar el código en el portapapeles.
   1. En el repositorio Git, cree una solicitud de extracción para los cambios que acaba de crear y, a continuación, fusiónela a `main`.

1. Haga clic en **Verificar**.

Una vez verificado el repositorio, su estado en la tabla Edge Deliver Sites cambia a un círculo verde con una marca de verificación blanca dentro de él.

Una vez que añada Edge Delivery Services a un programa de producción, se le aplicará la licencia de Edge Delivery Services.

Cada sitio de Edge Delivery tiene una **lista de tareas pendientes de Edge Delivery** que lo guiará a través de la creación de su sitio de Edge Delivery.

![Aplicación pendiente de Edge Delivery](/help/implementing/cloud-manager/assets/edge-delivery-to-do-ist.png)

Consulte el documento [Introducción a los Edge Delivery Services en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#ed-todo-list) para obtener más información sobre estos pasos.
