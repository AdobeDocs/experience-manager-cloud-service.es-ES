---
title: Compatibilidad con sitios de Edge Delivery en Cloud Manager
description: Obtenga información sobre cómo añadir una configuración de CDN a un sitio de Edge Delivery o eliminar un sitio de Edge Delivery.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: e28e4bf06c28f97d665e5fd86ab87d484116504f
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 1%

---

# Administración del sitio de Edge Delivery en Cloud Manager {#manage-edge-delivery-sites}

Obtenga información sobre cómo administrar sitios de Edge Delivery en Cloud Manager agregando una configuración de CDN a un sitio existente. O bien, elimine un sitio de Edge Delivery.

## Añadir una configuración de CDN a un sitio de Edge Delivery existente {#add-cdn-to-edge-delivery-site}

Consulte [Agregar una configuración de CDN](/help/implementing/cloud-manager/cdn-configurations/add-cdn-config.md).

## Cambiar el nombre de un sitio de Edge Delivery (#rename-edge-delivery-site)

En Adobe Cloud Manager, es posible que desee cambiar el nombre de un sitio de Edge Delivery por varios motivos:

* **Claridad y organización**: para describir mejor el propósito del sitio o su entorno asociado (por ejemplo, producción, ensayo).
* **Evitar confusiones**: si se usan varios sitios, cambiar el nombre puede ayudar a diferenciar fácilmente entre ellos, lo que reduce la posibilidad de aplicar configuraciones o actualizaciones al sitio incorrecto.
* **Estandarización**: Para seguir una convención de nombres coherente que se ajuste a las directrices de su organización para facilitar la administración y la auditoría.

**Para cambiar el nombre de un sitio de Edge Delivery:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa apropiado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa con Edge Delivery Services configurados, donde desee agregar un sitio de Edge Delivery.
1. Realice una de las siguientes acciones:

   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. En la tabla del sitio de Edge Delivery, haga clic en los puntos suspensivos al final de una fila cuyo sitio desee cambiar de nombre.
Haga clic en **Cambiar nombre**.
   * En la esquina superior izquierda de la página, haga clic en el icono de hamburguesa para mostrar el menú de navegación izquierdo. Bajo el encabezado **Servicios**, haga clic en **Sitios Edge Delivery**.
En la tabla del sitio de Edge Delivery, haga clic en los puntos suspensivos al final de una fila cuyo sitio desee cambiar de nombre. Haga clic en **Cambiar nombre**.

1. En el cuadro de diálogo **Editar sitio Edge Delivery**, en el campo de texto **Nombre del sitio**, escriba el nuevo nombre del sitio.

1. Haga clic en **Editar**.

## Eliminación de un sitio de Edge Delivery {#delete-edge-delivery-site}

Si elimina un sitio de Edge Delivery Services, también se eliminarán todas las configuraciones de CDN asociadas. Esta acción interrumpe la conexión entre los dominios personalizados y el sitio. Para obtener más información, consulte Configuraciones de CDN. <!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**Para eliminar un sitio de Edge Delivery:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa apropiado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa con Edge Delivery Services configurados, donde desee agregar un sitio de Edge Delivery.
1. Realice una de las siguientes acciones:

   * En la página **Resumen del programa**, haga clic en la ficha **Edge Delivery**. En la tabla del sitio de Edge Delivery, haga clic en los puntos suspensivos al final de una fila cuyo sitio desee quitar.
Haga clic en **Eliminar** y, a continuación, haga clic en **Eliminar** de nuevo para confirmar la eliminación del sitio.

     ![Agregar sitio Edge Delivery desde la ficha Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * En la esquina superior izquierda de la página, haga clic en el icono de hamburguesa para mostrar el menú de navegación izquierdo. Bajo el encabezado **Servicios**, haga clic en **Sitios Edge Delivery**.
En la tabla del sitio de Edge Delivery, haga clic en los puntos suspensivos al final de una fila cuyo sitio desee quitar. Haga clic en **Eliminar** y, a continuación, haga clic en **Eliminar** de nuevo para confirmar la eliminación del sitio.


     ![Agregar sitio Edge Delivery desde el botón Sitios Edge Delivery](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## Registrar un ticket de asistencia {#eds-support-ticket}

{{support-ticket}}


