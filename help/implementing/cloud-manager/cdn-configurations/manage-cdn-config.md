---
title: Administrar asignaciones de dominio
description: Obtenga información sobre cómo utilizar Cloud Manager para editar y actualizar o eliminar configuraciones de CDN para un sitio de Edge Delivery o un entorno de Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: a764a9d1e7d9fcd0be6abf9e2fb409346dc0f549
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 8%

---

# Administrar asignaciones de dominio {#manage-cdn-configurations}

Obtenga información sobre cómo utilizar Cloud Manager para editar o eliminar configuraciones de CDN para un sitio de Edge Delivery o un entorno de Cloud Manager.

## Editar una configuración de CDN desde la página Asignaciones de Dominio {#edit-cdn}

En Adobe Cloud Manager, es posible que desee editar una configuración de CDN (red de distribución de contenido), incluido el nivel de entorno (publicación o vista previa) y el certificado SSL, por varios motivos.

* **Cambios de entorno**: Ajustar el nivel ayuda a hacer coincidir la configuración de CDN con el entorno correcto, ya sea para producción en vivo (Publicación) o para pruebas (Previsualización).
* **Mejoras de seguridad**: Puede que sea necesario seleccionar un certificado SSL diferente al actualizar certificados o al abordar las necesidades de cumplimiento y seguridad.
* **Optimización del rendimiento**: editar la configuración garantiza la configuración de CDN correcta para entregar contenido en función de las necesidades operativas cambiantes.

Puede editar una configuración sin quitar completamente la configuración existente. Los cambios se aplican al entorno seleccionado (por ejemplo, ensayo o producción) y pueden afectar a cómo se entrega y protege el contenido.

Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para completar esta tarea.

**Para editar una configuración de CDN desde la página Asignaciones de dominio:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.
1. En el menú del lado izquierdo, debajo de **Servicios**, haga clic en ![Icono de red social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Asignaciones de dominio**.
1. En la tabla **Asignaciones de dominio**, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de una fila cuya configuración de CDN desee actualizar.

1. En el menú desplegable, haga clic en **Editar**.

1. En el cuadro de diálogo **Editar configuración de CDN**, establezca una o más de las opciones en la lista desplegable correspondiente.

   Las opciones mostradas en el cuadro de diálogo dependen de si está usando una **CDN administrada por Adobe** o un **otro proveedor de CDN** (CDN administrada por el cliente).

1. Haga clic en **Actualizar**.

   El estado de la CDN editada se actualiza en la tabla **Asignaciones de dominio** para reflejar los cambios que ha realizado.


## Editar una configuración de CDN desde la página Entornos

Los pasos para editar una configuración de CDN desde la página **Entornos** son casi los mismos que cuando [edita una configuración de CDN desde la página Asignaciones de dominios](#edit-cdn), pero el punto de entrada difiere.

**Para editar una configuración de CDN desde la página Entornos:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. En el menú del lado izquierdo, haga clic en ![Icono de datos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Entornos**.

1. En la página **Entornos**, seleccione un entorno de interés.

1. En la página de detalles del entorno, en la agrupación Asignaciones de dominio, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) que corresponda a la configuración de CDN que desee editar.

1. En el menú emergente, haga clic en **Editar**.

1. En el cuadro de diálogo **Editar configuración de CDN**, establezca una o más de las opciones en la lista desplegable correspondiente.

   Las opciones mostradas en el cuadro de diálogo dependen de si está usando una **CDN administrada por Adobe** o un **otro proveedor de CDN** (CDN administrada por el cliente).

1. Haga clic en **Actualizar**.


## Preparación para el lanzamiento: configure los DNS para un dominio personalizado {#go-live-readiness}

Para que un dominio personalizado pueda servir tráfico, debe completar la configuración de DNS con su proveedor de DNS. Después de implementar una asignación de dominio y hacer clic en **Activar**, Cloud Manager muestra un cuadro de diálogo que le guiará a través del proceso de configuración de registros DNS. Tiene la opción de lanzarse agregando un tipo de registro CNAME o un tipo de registro A.

<!-- See also [APEX record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record#adobe-managed-cert-apex-record) and [CNAME record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record). -->

**Para configurar la preparación para el lanzamiento:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.
1. En el menú del lado izquierdo, debajo de **Servicios**, haga clic en ![Icono de red social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Asignaciones de dominio**.
1. En la tabla Asignaciones de dominio, haga clic en **Activar** cerca del final de una fila que corresponda a una CDN cuya preparación para la activación desea configurar.

   ![Cuadro de diálogo de preparación para lanzamiento](/help/implementing/cloud-manager/assets/domain-mappings-go-live-readiness.png)

1. En el cuadro de diálogo **Preparación para el lanzamiento**, realice una de las siguientes acciones:

   | Opción | Etapas |
   | --- | --- |
   | Configurar un REGISTRO | Recomendado para dominios raíz como `example.com`<br><ol><li>Inicie sesión en el portal de su proveedor de servicios DNS.<li>Vaya a la sección Registros DNS.<li>Cree un registro A para que apunte a todas las direcciones IP de la lista.</li></ol> |
   | Configurar CNAME | Recomendado para dominios personalizados como `www.example.com`<br><ol><li>Inicie sesión en el portal de su proveedor de servicios DMS.<li>Vaya a la sección Registros DNS.<li>Asigne `cdn.adobeaemcloud.com` (registro CNAME) en el registro DNS del proveedor de servicios DNS (su dominio personalizado). Esta asignación garantiza que las solicitudes recibidas en el dominio personalizado se redirijan a la CDN de Adobe.</li></ol> |

1. En el cuadro de diálogo **Preparación para el lanzamiento**, haga clic en **Aceptar** para guardar el registro.

   Espere a que se propague el DNS; puede tardar entre varios minutos y pocas horas.

   Cuando la columna **[!UICONTROL Estado]** de la tabla Asignaciones de dominios se actualice a **[!UICONTROL Verificado]**, el dominio personalizado estará listo para su uso. Es posible que tenga que hacer clic en ![Actualizar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) para actualizar el estado.

## Eliminar una configuración de CDN {#delete-cdn}

Al eliminar una configuración de CDN administrada por Adobe o por el cliente en Cloud Manager, se eliminan las opciones de enrutamiento y certificado SSL del dominio asociado. El dominio ya no utiliza la CDN para la entrega de tráfico y se pierde cualquier mejora de seguridad o rendimiento proporcionada por la CDN. Puede experimentar interrupciones en el servicio hasta que se configure una nueva, ya sea volviendo a añadir la CDN eliminada o añadiendo una nueva.

Un usuario debe ser miembro del rol **Propietario del negocio** o **Administrador de implementación** para completar esta tarea.

**Para eliminar una configuración de CDN:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. En el menú del lado izquierdo, debajo de **Servicios**, haga clic en ![Icono de red social](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Asignaciones de dominio**.

1. En la tabla Asignaciones de dominio, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de la fila que corresponda a la red de distribución de contenido (CDN) que desee eliminar y, a continuación, haga clic en **Eliminar**.

1. En el cuadro de diálogo **Eliminar configuración de CDN**, haga clic en **Eliminar**.

1. Vuelva a hacer clic en **Eliminar** para confirmar la eliminación de la CDN del sitio.


## Eliminar una configuración de CDN de la página Entornos

Los pasos para eliminar una configuración de CDN de la página **Entornos** son casi los mismos que al [eliminar una configuración de CDN de la página Asignaciones de dominios](#edit-cdn), pero el punto de entrada difiere.

**Para eliminar una configuración de CDN de la página Entornos:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. En el menú del lado izquierdo, haga clic en ![Icono de datos](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Entornos**.

1. En la página **Entornos**, seleccione un entorno de interés.

1. En la página de detalles del entorno, en la agrupación **Asignaciones de dominio**, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) que corresponde a la configuración de CDN que desea eliminar y, a continuación, haga clic en **Eliminar**.

1. En el cuadro de diálogo **Eliminar configuración de CDN**, haga clic en **Eliminar**.

1. Vuelva a hacer clic en **Eliminar** para confirmar la eliminación de la CDN del sitio.
