---
title: Añadir un sitio de Edge Delivery a Cloud Manager
description: Aprenda a añadir un sitio de Edge Delivery a su programa de producción o programa de zona protegida.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 17e842c9-599a-4877-9834-1e7220f508a8
source-git-commit: e99bec4515c79e181ce38b94b1ea327fd99d2695
workflow-type: ht
source-wordcount: '521'
ht-degree: 100%

---

# Añadir un sitio de Edge Delivery a Cloud Manager {#adding}

>[!IMPORTANT]
>
>Descubra por qué debe incorporar su sitio de Edge Delivery Services a Cloud Manager. 
>>Consulte [Ventajas de utilizar la ruta recomendada por Adobe para Edge Delivery Services](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md#recommended-path-eds).

**Añadir un sitio de Edge Delivery a Cloud Manager:**

1. Asegúrese de haber creado primero el programa con una licencia de Edge Delivery Services antes de incorporar un sitio de Edge Delivery en Cloud Manager.
Consulte [Creación de un programa de producción](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md).
1. Inicie sesión en Cloud Manager en [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. Realice una de las siguientes acciones:

   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. A continuación, cerca de la esquina inferior derecha de la página, haga clic en **Añadir sitio de Edge Delivery**.

     ![Añadir sitio de Edge Delivery desde la ficha Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add1.png)

   * En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda.
Bajo el encabezado **Servicios**, haga clic en el ![icono de página web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Sitios de Edge Delivery**.
Cerca de la esquina superior derecha de la página, haga clic en **Añadir sitio**.

     ![Añadir sitio de Edge Delivery desde el botón Sitios de Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-add2.png)

1. En el cuadro de diálogo **Añadir sitio de Edge Delivery**, proporcione la siguiente información en los campos obligatorios:

   | Campo de texto | Descripción |
   | - | --- |
   | Nombre del sitio | Escriba el nombre del sitio de Edge Delivery que va a añadir.<br>El nombre sirve como identificador único para el sitio en Cloud Manager. |
   | Origen de Edge Delivery | Este valor especifica la ruta de la URL al origen de contenido para el sitio de Edge Delivery Services. También vincula Cloud Manager con su sitio activo.<br>La dirección URL suele incluir la *rama*, el *proyecto* y el *inquilino*, como en el siguiente ejemplo (solo con fines ilustrativos):<br>`https://main--{site}--{org}.aem.live` |
   | Descripción del sitio (opcional) | Escriba una breve descripción del sitio de Edge Delivery que va a añadir.<br>Una descripción ayuda a identificar y diferenciar el sitio, lo que facilita administrarlo y reconocerlo entre los otros sitios que haya añadido. |

1. En la esquina inferior derecha del cuadro de diálogo, haga clic en **Añadir**.

1. En el cuadro de diálogo **Verificar la propiedad del repositorio**, compruebe la propiedad del repositorio siguiendo estos pasos:

   | Número de paso | Descripción |
   | - | - |
   | **1** | Añada un archivo con la ruta y el nombre `well-known/adobe/cloudmanager-challenge.txt` a la rama `main` del repositorio de Git que aparece en el campo **URL del repositorio**. *No* añada un punto al principio de la ruta de ubicación.<br>Si es necesario, haga clic en ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) para copiar la ruta en el portapapeles. |
   | **2** | Añada el código visto en el campo de texto del paso 2 al archivo que acaba de crear en el paso 1.<br>Si es necesario, haga clic en ![Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) para copiar el código en el portapapeles. |
   | **3** | Cree una solicitud de extracción en el repositorio de Git para los cambios que acaba de crear y, a continuación, combínela en `main` para confirmar el código. |

1. Haga clic en **Verificar**.

Una vez verificado el repositorio, se actualiza su estado en la tabla de sitios de Edge Delivery. El círculo verde con una marca de verificación blanca en el interior indica el estado.

En la misma tabla, haga clic en el icono de ![Información acerca del sitio de Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_InfoOutline_18_N.svg) para ver los detalles del sitio. Esta información incluye la URL del repositorio verificada, junto con las URL del sitio web de previsualización y producción.
