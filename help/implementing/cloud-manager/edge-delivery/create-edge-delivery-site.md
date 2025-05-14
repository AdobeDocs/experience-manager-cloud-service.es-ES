---
title: Creación de un sitio de Edge Delivery en Cloud Manager con un clic
description: Aprenda a crear rápidamente un sitio de Edge Delivery en Cloud Manager con solo hacer clic en un botón.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 292bf0b4-990b-4980-b971-91b8aedde3de
source-git-commit: 767b1f89f42340cc9307a43ff9e97e9a074e592e
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 97%

---

# Crear un sitio de Edge Delivery en Cloud Manager con un solo clic{#about-one-click-edge-delivery-site}

La función Crear un sitio de Edge Delivery está diseñado para ayudarle a automatizar la incorporación y la implementación de sitios de Edge Delivery en Cloud Manager. Simplifica enormemente el proceso, ya que solo tiene que hacer clic en un botón. Con un solo clic se aprovisiona la infraestructura necesaria, se integra con GitHub para el control de versiones y se configura el almacenamiento de documentos y recursos en Google Drive.

Esta automatización ayuda a reducir el esfuerzo manual necesario para configurar el sitio inicial. Garantiza flujos de trabajo y escalabilidad fluidos y mejora el rendimiento de sus equipos en lo que respecta a la administración de contenido en el extremo.

<!-- >
## Practical use cases {#use-cases}

| Use case | Description |
| --- | --- |
| Website and application deployment | <ul><li>Automate the hosting and delivery of static or dynamic sites.</li><li>Ensure fast performance through edge caching. </li></ul> |
| API gateway and content delivery | <ul><li>Optimize API responses by caching data at the edge.</li><li>Reduce backend load and improved response times. </li></ul> |
| Real-time content updates | <ul><li>Instant deployment of new content across edge locations.</li><li>Support integration with automated content pipelines. </li></ul> |
| Edge computing workloads | <ul><li>Support serverless computing to process workloads closer to users.</li><li>Reduce latency and enhance performance. </li></ul> |
| Security and governance | <ul><li>Security is provided with integrated DDoS (Distributed Denial of Service) protection and WAF (Web Application Firewall) integration.</li><li>Ensure that content is delivered securely through TLS (Transport Security Layer) encryption. </li></ul> |
-->

## Creación de un sitio de Edge Delivery en Cloud Manager con un solo clic {#one-click-edge-delivery-site}

Para crear un sitio de Adobe Edge Delivery con un solo clic, su organización debe tener una licencia de Edge Delivery Services disponible. Esta licencia forma parte de Adobe Experience Manager (AEM) y es necesaria para crear Edge Delivery Services en Cloud Manager.

En cuanto a los permisos, debe ser miembro de la función Propietario del negocio o tener los permisos adecuados para añadir o editar programas en Cloud Manager. Este nivel de acceso le permite administrar la integración de Edge Delivery Services en sus programas.

Consulte también [Introducción a Edge Delivery Services en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**Para crear un sitio de Edge Delivery en Cloud Manager con un solo clic:**

1. Inicie sesión en Cloud Manager en [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda.
1. En el menú de la izquierda, bajo el encabezado **Programa**, haga clic en **Información general**.
1. En la página **Resumen del programa**, haga clic en la pestaña **Edge Delivery**.
1. En la página de Edge Delivery, en el cuadro de diálogo **Lista de tareas pendientes de Edge Delivery**, en el cuadro de grupo **Añadir el sitio de Edge Delivery** y haga clic en **Crear sitio ahora**.
1. En el cuadro de diálogo **Crear sitio de Edge Delivery**, en el campo de texto **Nombre del proyecto**, escriba el nombre del sitio y, a continuación, haga clic en **Crear sitio ahora**.

   Aparece un mensaje cerca de la parte superior central de la pantalla que le informa de que se ha iniciado el aprovisionamiento del sitio de Edge Delivery.

Cuando Cloud Manager completa el aprovisionamiento y la validación del sitio, el **Nombre del sitio** (el nombre del proyecto introducido anteriormente) aparece en el cuadro de lista **Sitios de Edge Delivery** de la página de Edge Delivery. Además, aparecerá una marca de verificación verde a la izquierda de la URL del repositorio.


### Exploración de un sitio de Edge Delivery creado con un clic {#explore-one-click-ed-site}

1. Inicie sesión en Cloud Manager en [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda.
1. En el menú de la izquierda, bajo el encabezado **Programa**, haga clic en **Información general**.
1. En la página **Resumen del programa**, haga clic en la pestaña **Edge Delivery**.
1. En la página Edge Delivery, realice una de las siguientes acciones:

   | Qué explorar | Etapas |
   | --- | --- |
   | Repositorio de GitHub de un sitio | <ul><li>En el cuadro de lista **Sitios de Edge Delivery**, en el encabezado de la columna **Repositorio**, haga clic en la URL del sitio que acaba de crear.<br>Es posible que deba iniciar sesión en GitHub con su nombre de usuario o dirección de correo electrónico y su contraseña.</li> |
   | Publicar un sitio | <ul><li> En el cuadro de lista **Sitios de Edge Delivery**, en el extremo derecho del nombre del sitio, haga clic en ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir el menú desplegable.</li><li>Haga clic en ![icono de publicación verificada](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg) **Publicar sitio** en el menú desplegable.<br>Aparecerá un mensaje que le informa de que la publicación del sitio se ha iniciado correctamente.</li></ul> |
   | Previsualización de un sitio publicado | <ul><li>En el cuadro de lista **Sitios de Edge Delivery**, en el encabezado de la columna **Nombre del sitio**, haga clic en la URL del sitio que acaba de crear y publicar.<br>En la barra de direcciones URL del explorador, tenga en cuenta que la URL del sitio termina con `.page`, lo que indica que está viendo una vista previa del sitio.</li><li>Para ver el sitio activo, cambie manualmente `.page` a `.live` en la barra de direcciones URL.</li></ul> |
   | Conceder a los usuarios acceso al repositorio de contenido en Google Drive | <ul><li> En el cuadro de lista **Sitios de Edge Delivery**, en el extremo derecho del nombre del sitio, haga clic en ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir el menú desplegable.</li><li>Haga clic en ![icono de adición de usuarios](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **Obtener acceso al repositorio de contenido** en el menú desplegable.</li><li>En el cuadro de diálogo **Añadir colaboradores al sitio**, escriba la dirección de correo electrónico de un colaborador y, a continuación, haga clic en ![icono de verificación](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Siga añadiendo correos electrónicos de colaboradores, según sea necesario.</li><li>Cuando termine, haga clic en **Añadir colaborador**.</li><li>Para compartir el vínculo con sus colaboradores de contenido, en el cuadro de diálogo **Colaboración añadida correctamente**, haga clic en **Aceptar**.</li><li>En el cuadro de diálogo Colaboración añadida correctamente, haga clic en ![icono Copiar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) para copiar el vínculo y compartirlo con sus colaboradores.<br>Antes de compartir el vínculo, confirme que los colaboradores han iniciado sesión con la dirección de correo electrónico asociada a sus respectivas cuentas de IMS. Si sus cuentas de correo electrónico de IMS no están disponibles, deberán utilizar la dirección de correo electrónico añadida como colaborador. De este modo, los colaboradores podrán acceder al vínculo y ver el contenido que se va a editar o actualizar en Google Drive.</li><li>Cuando termine de editar, haga clic en **Publicar sitio** en Cloud Manager, tal como se ha descrito anteriormente.<br>O bien, obtenga una vista previa de los cambios realizados, tal como se ha descrito anteriormente.</li></ul> |
   | Conceder a los usuarios acceso al repositorio base en GitHub | <ul><li> En el cuadro de lista **Sitios de Edge Delivery**, en el extremo derecho del nombre del sitio, haga clic en ![icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir el menú desplegable.</li><li>Haga clic en ![icono de código](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **Obtener acceso al repositorio base** en el menú desplegable.</li><li>En el cuadro de diálogo **Acceder al repositorio base del sitio**, escriba el nombre de usuario de GitHub de un colaborador y, a continuación, haga clic en ![icono de verificación](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Siga añadiendo nombres de usuario de GitHub, según sea necesario.</li><li>Cuando termine, haga clic en **Añadir colaborador**.</li>Los usuarios deben conceder acceso al nombre de usuario de su propio GitHub para ver el repositorio. |
