---
title: Aprovisionar un sitio de Edge Delivery en Cloud Manager
description: Aprenda a crear rápidamente un sitio de Edge Delivery en Cloud Manager con solo hacer clic en un botón.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: ac110fb006ed377403bce52c961712e6e449be88
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 8%

---


# Acerca del aprovisionamiento de un sitio Edge Delivery en Cloud Manager {#about-provision-edge-delivery-site}

El servicio One Click Edge Delivery (EDS) está diseñado para automatizar la incorporación y la implementación de sitios de Edge Delivery dentro de Cloud Manager. Simplifica considerablemente el proceso al hacer clic en un solo botón. Con un solo clic se aprovisiona la infraestructura necesaria, se integra con GitHub para el control de versiones y se configura el almacenamiento de documentos y recursos en Google Drive.

Esta automatización ayuda a reducir el esfuerzo manual necesario para configurar el sitio inicial. Garantiza flujos de trabajo y escalabilidad fluidos y mejora el rendimiento de sus equipos en lo que respecta a la administración de contenido en el perímetro.

## Conceptos clave {#key-concepts}

Conceptos clave al utilizar el aprovisionamiento de sitios de Edge Delivery con un solo clic.

| Concepto clave | Descripción |
| --- | --- |
| Implementación automatizada de Edge | <ul><li>Los usuarios pueden aprovisionar y configurar sitios de Edge Delivery al instante.</li><li>Reduce o elimina la necesidad de procesos de incorporación manuales mediante la integración de Cloud Manager con el flujo de trabajo de CI/CD.</li><li>Se integra con Cloud Manager para lograr flujos de trabajo de CI/CD fluidos.</li></ul> |
| Integración con Cloud Manager | <ul><li>Utiliza la interfaz de usuario de Cloud Manager para almacenar en déclencheur el proceso de One Click Edge Delivery.</li><li>Proporciona acceso a la creación e implementación automatizadas de repositorios.</li></ul> |
| Control de versiones basado en GitHub | <ul><li>Crea un repositorio de GitHub dentro de una organización utilizando plantillas de plantillas predefinidas para estandarizar las implementaciones.</li><li>AEM Vínculos con el bot de la para actualizaciones de contenido.</li></ul> |
| Integración del almacenamiento de documentos y recursos | <ul><li>Genera una carpeta de Google Drive para almacenamiento.<li>AEM Instala la aplicación de sincronización de código de la en el repositorio, lo que garantiza una sincronización e implementación sin problemas.</li></li><li>Permite que varios colaboradores administren documentos fácilmente.</li></ul> |
| Seguridad y escalabilidad | <ul><li>Garantiza el cumplimiento de las normas de seguridad empresariales.</li><li>Admite varios sitios de Edge Delivery en diferentes inquilinos de Cloud Manager.</li></ul> |



## Aprovisionar un sitio de Edge Delivery en Cloud Manager {#provision-edge-delivery-site}

Para poder aprovisionar un sitio de entrega de Adobe Edge con un clic, su organización debe tener una licencia de Edge Delivery Services disponible. Esta licencia forma parte de Adobe Experience Manager AEM () y es necesaria para aprovisionar Edge Delivery Services en Cloud Manager.

En cuanto a los permisos, debe ser miembro de la función Propietario empresarial o se le han concedido los permisos adecuados para agregar o editar programas en Cloud Manager. Este nivel de acceso le permite administrar la integración de Edge Delivery Services en sus programas.

Consulte también [Introducción a Edge Delivery Services en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

AEM LAS CONFIGURACIONES ADECUADAS DE BOT DE DEBEN ESTAR CONFIGURADAS PRIMERO PARA LAS ACTUALIZACIONES AUTOMÁTICAS DE CONTENIDO. ¿VERDADERO? ¿FALSO?

**Para aprovisionar un sitio de Edge Delivery en Cloud Manager:**

1. Inicie sesión en Cloud Manager en [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda.
1. En el menú del lado izquierdo, bajo el encabezado **Servicios**, haga clic en ![Icono de página web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Sitios Edge Delivery**.
1. En la página Edge Delivery, en el cuadro de diálogo **Lista de tareas pendientes de Edge Delivery**, en el cuadro de grupo **Completar requisitos previos**, haga clic en **Aprovisionar**.
1. En el cuadro de diálogo **Aprovisionar sitio Edge Delivery**, en el campo de texto **Nombre del proyecto**, escriba el nombre del sitio y, a continuación, haga clic en **Aprovisionar**.
Aparece un mensaje cerca de la parte superior central de la pantalla que le informa de que se ha iniciado el aprovisionamiento del sitio Edge Delivery.
Cuando se completa el aprovisionamiento y se valida el sitio, el nombre del sitio aparece en el área de **sitios de Edge Delivery** de la página de Edge Delivery.

### Explorar un sitio de Edge Delivery recién aprovisionado




1. Haga clic en el vínculo Repositorio Git a la derecha del nombre del sitio.

Publish. Haga clic en Nombre del sitio, realice algunos cambios y luego publique

Vea la página en la vista previa y, a continuación, cambie la URL para ver la versión en directo.

Añadir colaboradores.




## Sitio de Publish y Edge Delivery



## Añadir colaboradores a un sitio de Edge Delivery


































Estas mejoras tienen como objetivo mejorar la automatización, simplificar los procesos de configuración y mejorar la colaboración entre los usuarios de Edge Delivery Services. <!-- CMGR-59362 -->

![Aprovisionar un sitio de Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

![Aprovisionar cuadro de diálogo del sitio de Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)