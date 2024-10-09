---
title: Añadir un sitio de Edge Delivery a Cloud Manager
description: Obtenga información sobre cómo agregar un sitio de Edge Delivery a su programa de producción o programa de zona protegida.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 9cde6e63ec452161dbeb1e1bfb10c75f89e2692c
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 5%

---


# Añadir un sitio de Edge Delivery a Cloud Manager {#adding}

Después de agregar un sitio de Edge Delivery al programa de producción, se le aplica la licencia de Edge Delivery Services.

Se requiere agregar un sitio de Edge Delivery a Cloud Manager para [registrar un ticket de asistencia para su proyecto de Edge Delivery](/help/edge/overview.md##support-ticket).

Vea también [Introducción a los Edge Delivery Services en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

**Para agregar un sitio de Edge Delivery a Cloud Manager:**

1. Inicie sesión en Cloud Manager en [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) y seleccione el programa apropiado.
1. Realice una de las siguientes acciones:

   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. A continuación, cerca de la esquina inferior derecha de la página, haga clic en **Agregar sitio de Edge Delivery**.

     ![Agregar sitio de Edge Delivery desde la ficha Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de navegación lateral.
Bajo el encabezado **Servicios**, haga clic en ![icono de página web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Sitios Edge Delivery**.
Cerca de la esquina superior derecha de la página, haga clic en **Agregar sitio**.

     ![Agregar sitio Edge Delivery desde el botón Sitios Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. En el cuadro de diálogo **Agregar sitio Edge Delivery**, proporcione la siguiente información en los campos obligatorios:

   | Campo de texto | Descripción |
   | - | --- |
   | Nombre del sitio | Escriba el nombre del sitio de Edge Delivery que está agregando.<br>El nombre sirve como identificador único para el sitio dentro de Cloud Manager. |
   | URL del repositorio | Introduzca el repositorio de Git donde se almacena el código del sitio web.<br>Este campo permite a Cloud Manager extraer el código de ese repositorio durante el proceso de implementación. |
   | Descripción del sitio (opcional) | Escriba una breve descripción del sitio de Edge Delivery que está agregando.<br>Una descripción ayuda a identificar y diferenciar el sitio, lo que facilita la administración y el reconocimiento, entre otros sitios que ha agregado. |

1. En la esquina inferior derecha del cuadro de diálogo, haga clic en **Agregar**.

1. En el cuadro de diálogo **Verificar la propiedad del repositorio**, compruebe la propiedad del repositorio siguiendo estos pasos:

   | Número de paso | Descripción |
   | - | - |
   | **1** | Agregue un archivo con la ruta de acceso y el nombre `well-known/adobe/cloudmanager-challenge.txt` a la rama `main` del repositorio Git que aparece en el campo **URL del repositorio**. *no* agrega un punto al inicio de la ruta de ubicación.<br>Si es necesario, haga clic en ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) para copiar la ruta de acceso en el portapapeles. |
   | **2** | Agregue el código visto en el campo de texto del paso 2 al archivo que acaba de crear en el paso 1.<br>Si es necesario, haga clic en ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) para copiar el código en el portapapeles. |
   | **3** | Cree una solicitud de extracción en el repositorio de Git para los cambios que acaba de crear y, a continuación, fusiónela en `main` para confirmar el código. |

1. Haga clic en **Verificar**.

Una vez verificado el repositorio, su estado en la tabla de sitios de Edge Delivery cambia a un círculo verde con una marca de verificación blanca dentro de él.

En la misma tabla, haga clic en ![Información sobre el sitio de Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg) para ver detalles sobre el sitio, como la dirección URL comprobada del repositorio y la dirección URL del sitio web de Previsualización y Producción.


