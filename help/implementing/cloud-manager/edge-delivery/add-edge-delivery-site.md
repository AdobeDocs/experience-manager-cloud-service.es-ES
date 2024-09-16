---
title: Añadir un sitio de Edge Delivery a Cloud Manager
description: Obtenga información sobre cómo agregar un sitio de Edge Delivery a su programa de producción o programa de zona protegida.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 2%

---


## Añadir un sitio de Edge Delivery a Cloud Manager {#eds-add-site}

Después de agregar Edge Delivery Services a un programa de producción, se le aplica la licencia de Edge Delivery Services.

Se ve una ficha en la que se puede hacer clic llamada **Edge Delivery** en la página Información general. Al hacer clic en la pestaña, se muestra una tabla que enumera todos los sitios de Edge Delivery que ha agregado. En el panel de navegación izquierdo, en la agrupación **Servicios**, observe la opción de menú denominada **Sitios Edge Delivery**.

![Página de información general que muestra Edge Delivery Sites en el panel de navegación izquierdo y la pestaña Edge Delivery a la derecha de la pestaña Publish Delivery](/help/implementing/cloud-manager/assets/cm-overview-eds.png)

**Para agregar un sitio de Edge Delivery a Cloud Manager:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa apropiado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa con Edge Delivery Services configurados, donde desee agregar un sitio de Edge Delivery.
1. Realice una de las siguientes acciones:
   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. A continuación, cerca de la esquina inferior derecha de la página, haga clic en **Agregar sitio de Edge Delivery**.

     ![Agregar sitio Edge Delivery desde la ficha Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

     La **lista de tareas pendientes de Edge Delivery**, tal como se ve en la imagen anterior, es una guía de lista de comprobación de incorporación opcional diseñada para ayudarle a empezar a usar Edge Delivery. Ver [Acerca de la lista de tareas pendientes de Edge Delivery](#ed-todo-list).

   * En la esquina superior izquierda de la página, haga clic en el icono de hamburguesa para mostrar el menú de navegación izquierdo. Bajo el encabezado **Servicios**, haga clic en **Sitios Edge Delivery**. Cerca de la esquina superior derecha de la página, haga clic en **Agregar sitio**.

     ![Agregar sitio Edge Delivery desde el botón Sitios Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. En el cuadro de diálogo **Agregar sitio Edge Delivery**, haga lo siguiente:

   | Campo de texto | Qué hacer |
   | --- | --- |
   | Nombre del sitio | Escriba el nombre del sitio de Edge Delivery que está agregando. El nombre sirve como identificador único del sitio en Cloud Manager. |
   | URL del repositorio | Este campo hace referencia al repositorio de Git donde se almacena el código del sitio web.<br>Introduzca la URL del repositorio de Git que contiene los archivos y recursos necesarios (como HTML, CSS, JavaScript y otros recursos web) para su sitio de Edge Delivery. Esta disposición permite a Cloud Manager extraer el código de ese repositorio durante el proceso de implementación. |
   | Descripción del sitio (opcional) | Escriba una breve descripción del sitio de Edge Delivery que está agregando.<br>Esta descripción ayuda a identificar y diferenciar el sitio, lo que facilita la administración y el reconocimiento, entre otros sitios que ha agregado. Es posible que desee incluir detalles sobre el propósito, el contenido o cualquier otra información relevante que pueda ayudar a aclarar su función o alcance. |

1. En la esquina inferior derecha del cuadro de diálogo, haga clic en **Agregar**.

1. En el cuadro de diálogo **Verificar propiedad del repositorio**, realice cada una de las siguientes acciones:

   | Paso | Descripción |
   | --- | --- |
   | 1 | Agregue un archivo con la ruta de ubicación a la rama `main` del repositorio Git que aparece en el campo **URL del repositorio**. Si es necesario, haga clic en el icono Copiar para copiar la ruta de acceso en el portapapeles.<br> La ruta de acceso de la ubicación es:<br>`well-known/adobe/cloudmanager-challenge.txt`.<br><br>No *agregue un punto al inicio de la ruta de acceso de la ubicación, está en:<br>`.well-known/adobe/cloudmanager-challenge.txt`* |
   | 2 | Agregue el código generado al archivo que creó en el paso 1. Si es necesario, haga clic en el icono Copiar para copiar el código en el portapapeles. |
   | 3 | En el repositorio Git, cree una solicitud de extracción y, a continuación, fusiónela para validar el código. |

1. Haga clic en **Verificar**. Una vez verificado el repositorio, su estado en la tabla Edge Deliver Sites cambia a un círculo verde con una marca de verificación blanca dentro de él.
