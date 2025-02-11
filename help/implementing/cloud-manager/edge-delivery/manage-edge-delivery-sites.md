---
title: Administración de sitios de Edge Delivery en Cloud Manager
description: Obtenga información sobre cómo añadir una configuración de CDN a un sitio de Edge Delivery o eliminar un sitio de Edge Delivery.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: a078d45f81fc7081012ebf24fa8f46dc1a218cd7
workflow-type: ht
source-wordcount: '541'
ht-degree: 100%

---

# Administración de un sitio de Edge Delivery en Cloud Manager {#manage-edge-delivery-sites}

Obtenga información sobre cómo administrar sitios de Edge Delivery en Cloud Manager añadiendo una configuración de CDN a un sitio existente. O bien, elimine un sitio de Edge Delivery.

## Añadir una configuración de CDN a un sitio de Edge Delivery existente {#add-cdn-to-edge-delivery-site}

Consulte [Añadir una configuración de CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md).

## Cambiar el nombre de un sitio de Edge Delivery (#rename-edge-delivery-site)

En Adobe Cloud Manager, puede cambiar el nombre de un sitio de Edge Delivery por varios motivos:

* **Claridad y organización**: para describir mejor el propósito del sitio o su entorno asociado (por ejemplo, producción o ensayo).
* **Evitar confusiones**: si se usan varios sitios, cambiar el nombre puede ayudar a diferenciarlos fácilmente, lo que reduce la posibilidad de aplicar configuraciones o actualizaciones al sitio incorrecto.
* **Estandarización**: seguir una convención de nomenclatura coherente que se ajuste a las directrices de su organización para facilitar la administración y la auditoría.

**Para cambiar el nombre de un sitio de Edge Delivery:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa con Edge Delivery Services configurado donde desee añadir un sitio de Edge Delivery.
1. Realice una de las siguientes acciones:

   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. En la tabla del sitio de Edge Delivery, haga clic en los puntos suspensivos al final de una fila cuyo sitio desee cambiar de nombre.
Haga clic en **Cambiar nombre**.
   * En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda. Bajo el encabezado **Servicios**, haga clic en el ![icono de páginas web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) de **Sitios de Edge Delivery**.
En la tabla del sitio de Edge Delivery, haga clic en ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de la fila cuyo sitio desee cambiar de nombre. Haga clic en **Cambiar nombre**.

1. En el cuadro de diálogo **Editar sitio de Edge Delivery**, en el campo de texto **Nombre del sitio**, escriba el nuevo nombre del sitio.

1. Haga clic en **Editar**.

## Eliminar un sitio de Edge Delivery {#delete-edge-delivery-site}

Si elimina un sitio de Edge Delivery Services, también se eliminarán todas las configuraciones de CDN asociadas. Esta acción interrumpe la conexión entre los dominios personalizados y el sitio. Para obtener más información, consulte Configuraciones de CDN. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Para eliminar un sitio de Edge Delivery:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa con Edge Delivery Services configurado donde desee añadir un sitio de Edge Delivery.
1. Realice una de las siguientes acciones:

   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. En la tabla del sitio de Edge Delivery, haga clic en el icono ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de la fila cuyo sitio desee quitar. Haga clic en el ![icono Eliminar sitio Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Eliminar** y, a continuación, vuelva a hacer clic en **Eliminar** para confirmar la eliminación del sitio.

     ![Añadir sitio de Edge Delivery desde la ficha Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda. Bajo el encabezado **Servicios**, haga clic en el icono ![Página web de los sitios de Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Sitios de Edge Delivery**.
En la tabla del sitio de Edge Delivery, haga clic en el icono ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de la fila cuyo sitio desee quitar. Haga clic en el ![icono Eliminar sitio de Edge Delivery](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg) **Eliminar** y, a continuación, vuelva a hacer clic en **Eliminar** para confirmar la eliminación del sitio.

     ![Añadir sitio de Edge Delivery desde el botón Sitios de Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## Registro de un vale de asistencia {#eds-support-ticket}

{{support-ticket}}
