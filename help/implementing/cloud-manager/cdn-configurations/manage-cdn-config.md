---
title: Administrar configuraciones de CDN
description: Obtenga información sobre cómo utilizar Cloud Manager para editar y actualizar o eliminar configuraciones de CDN para un sitio de Edge Delivery o un entorno de Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8e2fc0d4ee82e79d1a822a528b1a46acce3c192a
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 6%

---


# Administrar configuraciones de CDN {#manage-cdn-configurations}

Obtenga información sobre cómo utilizar Cloud Manager para editar y actualizar o eliminar configuraciones de CDN para un sitio de Edge Delivery o un entorno de Cloud Manager.

## Editar una configuración de CDN {#edit-cdn}

En Adobe Cloud Manager, es posible que desee editar una configuración de CDN, incluido el nivel de entorno (Publish o Vista previa) y el certificado SSL, por varios motivos.

* **Cambios de entorno**: el ajuste del nivel ayuda a hacer coincidir la configuración de CDN con el entorno correcto, ya sea para la producción en directo (Publish) o para las pruebas (vista previa).
* **Mejoras de seguridad**: Puede que sea necesario seleccionar un certificado SSL diferente al actualizar certificados o al abordar las necesidades de cumplimiento y seguridad.
* **Optimización del rendimiento**: editar la configuración garantiza la configuración de CDN correcta para entregar contenido en función de las necesidades operativas cambiantes.

Puede editar una configuración sin quitar completamente la configuración existente. Los cambios se aplican al entorno seleccionado (por ejemplo, ensayo o producción) y pueden afectar a cómo se entrega y protege el contenido.

Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para completar esta tarea.

**Para editar una configuración de CDN:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.
1. En el panel de navegación izquierdo, en **Servicios**, haga clic en **Configuraciones de CDN**.
1. En la tabla **Configuraciones de CDN**, haga clic en los puntos suspensivos al final de una fila cuya configuración de CDN desee editar.

   ![Editando una configuración de CDN](/help/implementing/cloud-manager/assets/cdn-config-edit.png)

1. Haga clic en **Editar**.
1. En el cuadro de diálogo **Editar configuración de CDN**, establezca una o más de las opciones en la lista desplegable correspondiente.

   Las opciones que ve en el cuadro de diálogo pueden variar según si utiliza una CDN administrada por Adobe o una CDN administrada por el cliente.

1. Haga clic en **Actualizar**.

   El estado de la CDN editada se actualiza en la tabla **Configuraciones de CDN** para reflejar los cambios que ha realizado.

## Eliminar una configuración de CDN {#delete-cdn}

Al eliminar una configuración de CDN administrada por el Adobe o por el cliente en Adobe Cloud Manager, se elimina la configuración de enrutamiento y certificado SSL del dominio asociado. El dominio ya no utiliza la CDN para la entrega de tráfico y se pierde cualquier mejora de seguridad o rendimiento proporcionada por la CDN. Puede experimentar interrupciones en el servicio hasta que se configure una nueva, ya sea volviendo a añadir la CDN eliminada o añadiendo una nueva.

Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para completar esta tarea.

**Para eliminar una configuración de CDN:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. En el panel de navegación izquierdo, en **Servicios**, haga clic en **Configuraciones de CDN**.

1. En la tabla Configuraciones de CDN, haga clic en los puntos suspensivos al final de una fila cuya CDN desee eliminar.

   ![Eliminando una configuración de CDN](/help/implementing/cloud-manager/assets/cdn-config-delete.png)

1. Haga clic en **Eliminar**.
1. Vuelva a hacer clic en **Eliminar** para confirmar la eliminación de la CDN del sitio.


