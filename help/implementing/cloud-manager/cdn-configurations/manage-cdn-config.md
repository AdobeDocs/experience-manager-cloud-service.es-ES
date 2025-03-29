---
title: Administrar asignaciones de dominio
description: Obtenga información sobre cómo utilizar Cloud Manager para editar y actualizar o eliminar configuraciones de CDN para un sitio de Edge Delivery o un entorno de Cloud Manager.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 2ec16c91-0195-4732-a26d-ac223e10afb9
source-git-commit: 41155a724f48ad28a12aac615a3e9a13bb3afa26
workflow-type: tm+mt
source-wordcount: '783'
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

<!-- 
## Go live readiness: Configure DNS settings for a custom domain {#go-live-readiness} 

Before a custom domain can serve traffic in Adobe Cloud Manager, you must complete DNS configuration with your DNS provider. After deploying a domain mapping and clicking **Go live**, Cloud Manager displays a dialog box that guides you through the DNS record setup process. You have the option to go live by adding either a CNAME record type or an A record type representing Fastly's IPs, simplifying domain routing. This ability eliminates the restriction of relying solely on CNAME records for domain setup with Fastly.

MAYBE There is support for A record types to improve Go Live readiness for domains using CDN configurations in AEM Cloud Manager. MAYBE

See also [APEX record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record#adobe-managed-cert-apex-record) and [CNAME record](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-cname-record).

**To configure Go live readiness:**

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate organization and program.

1. In the left side menu, under **Services**, click ![Social network icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Domain Mappings**.

1. In the Domain Mappings table, click **Go live** near the end of a row that corresponds to a CDN whose Go Live readiness you want to configure. 

1. In the Go live readiness dialog box, do one of the following:

    | Configure  | Steps |
    | --- | --- |
    | A RECORD | Recommended for root domains like `example.com`<br><ol><li>Log in to your DNS service provider's portal.<li>Go to the DNS Records section.<li>Create an A record to point to all the listed IP addresses.<li>In the Go live readiness dialog box, click **OK**.<li>In the Domain Mappings table, under the **Status** column, click ![Refresh icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg).<br>The status is updated to **Verified** when the resolution is complete.</li></ol> |
    | CNAME | Recommended for custom domains like `www.example.com`<br><ol><li>Log in to your DMS service provider's portal.<li>Go to the DNS Records section.<li>Map [cdn.adobeaemcloud.com](http://cdn.adobeaemcloud.com/) (CNAME record) in the DNS record of the DNS service provider (your custom domain). This mapping ensures that requests received at the custom domain are redirected to Adobe's CDN.<li>In the **Go live readiness** dialog box, click **OK** to save the record.<br>Wait for DNS propogation (may take several minutes to a few hours). When the **[!UICONTROL Status]** column in the Domamin Mappings table updates to **[!UICONTROL Verified]**, the custom domain is ready to use. You may need to click ![Refresh icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Refresh_18_N.svg) to refresh the status.</li></ol> | 
    
-->

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
