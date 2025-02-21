---
title: Creación de un sitio de Edge Delivery en Cloud Manager
description: Aprenda a crear un sitio de Edge Delivery rápidamente en Cloud Manager con solo hacer clic en un botón.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 0e1248ee8ceb324ee44dce296135d651d28c9f97
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 25%

---


# Acerca de la creación de un sitio de Edge Delivery en Cloud Manager {#about-one-click-edge-delivery-site}

La función Crear un sitio de Edge Delivery está diseñada para ayudarle a automatizar la incorporación y la implementación de sitios de Edge Delivery en Cloud Manager. Simplifica enormemente el proceso, ya que solo tiene que hacer clic en un botón. Con un solo clic se aprovisiona la infraestructura necesaria, se integra con GitHub para el control de versiones y se configura el almacenamiento de documentos y recursos en Google Drive.

Esta automatización ayuda a reducir el esfuerzo manual necesario para configurar el sitio inicial. Garantiza flujos de trabajo y escalabilidad fluidos y mejora el rendimiento de sus equipos en lo que respecta a la administración de contenido en el extremo.

## Conceptos clave {#key-concepts}

Conceptos clave al crear un sitio de Edge Delivery en Cloud Manager con un solo clic.

| Concepto clave | Descripción |
| --- | --- |
| Implementación automatizada de Edge | <ul><li>Los usuarios pueden crear y configurar sitios de Edge Delivery de forma instantánea.</li><li>Al utilizar la integración de Cloud Manager con el flujo de trabajo de CI/CD, reduce o elimina la necesidad de procesos de incorporación manuales.</li><li>Integrado con Cloud Manager para flujos de trabajo de CD/CI sin problemas.</li></ul> |
| Integración con Cloud Manager | <ul><li>Utiliza la interfaz de usuario de Cloud Manager para activar el proceso de solo un clic de Edge Delivery.</li><li>Proporcionar acceso a la creación e implementación automatizadas de repositorios.</li></ul> |
| Control de versiones basado en GitHub | <ul><li>Crea un repositorio de GitHub en una organización utilizando plantillas de elementos repetitivos predefinidas para estandarizar las implementaciones.</li><li>Vínculos con el bot de AEM para las actualizaciones de contenido.</li></ul> |
| Integración del almacenamiento de documentos y recursos | <ul><li>Genera una carpeta de Google Drive para el almacenamiento.<li>Instala la aplicación de sincronización de código de AEM en el repositorio, lo que garantiza una sincronización e implementación perfectas.</li></li><li>Los colaboradores pueden administrar documentos fácilmente.</li></ul> |
| Seguridad y escalabilidad | <ul><li>Garantiza el cumplimiento de las normas de seguridad empresariales.</li><li>Admite varios sitios de Edge Delivery con diferentes inquilinos de Cloud Manager.</li></ul> |

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

## Creación de un sitio de Edge Delivery en Cloud Manager con un clic {#one-click-edge-delivery-site}

Para crear un sitio de entrega de Adobe Edge con un solo clic, su organización debe tener una licencia de Edge Delivery Services disponible. Esta licencia forma parte de Adobe Experience Manager (AEM) y es necesaria para crear Edge Delivery Services en Cloud Manager.

En cuanto a los permisos, debe ser miembro de la función Propietario del negocio o tener los permisos adecuados para añadir o editar programas en Cloud Manager. Este nivel de acceso le permite administrar la integración de Edge Delivery Services en sus programas.

Consulte también [Introducción a Edge Delivery Services en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

<!-- PROPER AEM BOT CONFIGURATIONS MUST BE IN PLACE FIRST FOR AUTOMATIC CONTENT UPDATES? TRUE or FALSE? -->

**Para crear un sitio de Edge Delivery en Cloud Manager con un solo clic:**

1. Inicie sesión en Cloud Manager en [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda.
1. En el menú del lado izquierdo, bajo el encabezado **Programa**, haga clic en **Información general**.
1. En la página **Información general del programa**, haga clic en la ficha **Edge Delivery**.
1. En la página de Edge Delivery, en el cuadro de diálogo **Lista de tareas pendientes de Edge Delivery**, en el cuadro de grupo **Agregar sitio de Edge Delivery**, haga clic en **Crear sitio ahora**.
1. En el cuadro de diálogo **Crear sitio de Edge Delivery**, en el campo de texto **Nombre del proyecto**, escriba el nombre del sitio y, a continuación, haga clic en **Crear sitio ahora**.

   Aparece un mensaje cerca de la parte superior central de la pantalla que le informa de que se ha iniciado el aprovisionamiento del sitio Edge Delivery.

Cuando Cloud Manager completa el aprovisionamiento y la validación del sitio, el **nombre del sitio** (el nombre del proyecto especificado anteriormente) aparece en el cuadro de lista **sitios de Edge Delivery** de la página de Edge Delivery. Además, aparecerá una marca de verificación verde a la izquierda de la dirección URL del repositorio.


### Explorar un sitio de Edge Delivery creado con un clic {#explore-one-click-ed-site}

1. Inicie sesión en Cloud Manager en [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda.
1. En el menú del lado izquierdo, bajo el encabezado **Programa**, haga clic en **Información general**.
1. En la página **Información general del programa**, haga clic en la ficha **Edge Delivery**.
1. En la página Edge Delivery, realice una de las siguientes acciones:

   | Qué explorar | Etapas |
   | --- | --- |
   | Repositorio de GitHub de un sitio | <ul><li>En el cuadro de lista **Sitios Edge Delivery**, en el encabezado de columna **Repositorio**, haga clic en la dirección URL del sitio que acaba de crear.<br>Es posible que deba iniciar sesión en GitHub con su nombre de usuario o dirección de correo electrónico y su contraseña.</li> |
   | Publicación de un sitio | <ul><li> En el cuadro de lista **Sitios Edge Delivery**, en el extremo derecho del nombre del sitio, haga clic en ![Icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir el menú desplegable.</li><li>Haga clic en el icono ![Publicar comprobación](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PublishCheck_18_N.svg) **Publicar sitio** en el menú desplegable.<br>Aparece un mensaje que le informa de que la publicación del sitio se ha iniciado correctamente.</li></ul> |
   | Previsualización de un sitio publicado | <ul><li>En el cuadro de lista **Sitios Edge Delivery**, en el encabezado de columna **Nombre del sitio**, haga clic en la dirección URL del sitio que acaba de crear y publicar.<br>En la barra de direcciones URL del explorador, tenga en cuenta que la dirección URL del sitio termina con `.page`, lo que indica que está viendo una vista previa del sitio.</li><li>Para ver el sitio activo, cambie manualmente `.page` a `.live` en la barra de direcciones URL.</li></ul> |
   | Conceder a los usuarios acceso al repositorio de contenido en Google Drive | <ul><li> En el cuadro de lista **Sitios Edge Delivery**, en el extremo derecho del nombre del sitio, haga clic en ![Icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir el menú desplegable.</li><li>Haga clic en ![Icono de usuarios agregados](https://spectrum.adobe.com/static/icons/workflow_18/Smock_UsersAdd_18_N.svg) **Obtener acceso al repositorio de contenido** en el menú desplegable.</li><li>En el cuadro de diálogo **Agregar colaboradores a su sitio**, escriba la dirección de correo electrónico de un colaborador y haga clic en ![Icono de marca de verificación](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Siga agregando correos electrónicos del colaborador según sea necesario.</li><li>Cuando termine, haga clic en **Agregar colaboradores**.</li><li>Para compartir el vínculo con sus colaboradores de contenido, en el cuadro de diálogo **Collaboration agregado correctamente**, haga clic en **Aceptar**.<br>Los colaboradores reciben una invitación por correo electrónico para contribuir a una carpeta compartida de Google Drive al hacer clic en **Abrir** en el correo electrónico; no es necesario iniciar sesión. Pueden editar y actualizar archivos en la carpeta compartida y, a continuación, hacer clic en **Publicar sitio** en Cloud Manager, como se ha descrito anteriormente. También pueden obtener una vista previa de los cambios realizados, tal como se ha descrito anteriormente.</li></ul> |
   | Conceder a los usuarios acceso al repositorio base en GitHub | <ul><li> En el cuadro de lista **Sitios Edge Delivery**, en el extremo derecho del nombre del sitio, haga clic en ![Icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) para abrir el menú desplegable.</li><li>Haga clic en ![Icono de código](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) **Obtener acceso al repositorio base** en el menú desplegable.</li><li>En el cuadro de diálogo **Acceder al repositorio base del sitio**, escriba el nombre de usuario de GitHub de un colaborador y haga clic en ![Icono de marca de verificación](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Checkmark_18_N.svg).</li><li>Siga agregando nombres de usuario de GitHub según sea necesario.</li><li>Cuando termine, haga clic en **Agregar colaboradores**.</li> |


