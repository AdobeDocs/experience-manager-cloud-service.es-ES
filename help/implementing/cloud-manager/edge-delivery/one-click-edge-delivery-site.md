---
title: Creación de un sitio de Edge Delivery en Cloud Manager con un solo clic
description: Aprenda a crear rápidamente un sitio de Edge Delivery en Cloud Manager con solo hacer clic en un botón.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8034fc8454fca41c2430fa1179f80d2d2ab80563
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 7%

---


# Crear un sitio de Edge Delivery en Cloud Manager con un solo clic {#about-one-click-edge-delivery-site}

El servicio One Click Edge Delivery (EDS) está diseñado para automatizar la incorporación y la implementación de sitios de Edge Delivery dentro de Cloud Manager. Simplifica considerablemente el proceso al hacer clic en un solo botón. Con un solo clic se aprovisiona la infraestructura necesaria, se integra con GitHub para el control de versiones y se configura el almacenamiento de documentos y recursos en Google Drive.

Esta automatización ayuda a reducir el esfuerzo manual necesario para configurar el sitio inicial. Garantiza flujos de trabajo y escalabilidad fluidos y mejora el rendimiento de sus equipos en lo que respecta a la administración de contenido en el perímetro.

## Conceptos clave {#key-concepts}

Conceptos clave al utilizar un clic para crear un sitio de Edge Delivery.

| Concepto clave | Descripción |
| --- | --- |
| Implementación automatizada de Edge | <ul><li>Los usuarios pueden crear y configurar sitios de Edge Delivery de forma instantánea.</li><li>Reduce o elimina la necesidad de procesos de incorporación manuales mediante la integración de Cloud Manager con el flujo de trabajo de CI/CD.</li><li>Integrado con Cloud Manager para flujos de trabajo de CD/CI sin problemas.</li></ul> |
| Integración con Cloud Manager | <ul><li>Utiliza la interfaz de usuario de Cloud Manager para almacenar en déclencheur el proceso de One Click Edge Delivery.</li><li>Proporciona acceso a la creación e implementación automatizadas de repositorios.</li></ul> |
| Control de versiones basado en GitHub | <ul><li>Crea un repositorio de GitHub dentro de una organización utilizando plantillas de plantillas predefinidas para estandarizar las implementaciones.</li><li>Vínculos con AEM Bot para actualizaciones de contenido.</li></ul> |
| Integración del almacenamiento de documentos y recursos | <ul><li>Genera una carpeta de Google Drive para almacenamiento.<li>Instala la aplicación AEM Code Sync en el repositorio, lo que garantiza una sincronización e implementación sin problemas.</li></li><li>Permite que varios colaboradores administren documentos fácilmente.</li></ul> |
| Seguridad y escalabilidad | <ul><li>Garantiza el cumplimiento de las normas de seguridad empresariales.</li><li>Admite varios sitios de Edge Delivery en diferentes inquilinos de Cloud Manager.</li></ul> |



## Creación de un sitio de Edge Delivery en Cloud Manager con un clic {#one-click-edge-delivery-site}

Para poder crear un sitio de entrega de Adobe Edge con un solo clic, su organización debe tener una licencia de Edge Delivery Services disponible. Esta licencia forma parte de Adobe Experience Manager (AEM) y es necesaria para crear Edge Delivery Services en Cloud Manager.

En cuanto a los permisos, debe ser miembro de la función Propietario empresarial o se le han concedido los permisos adecuados para agregar o editar programas en Cloud Manager. Este nivel de acceso le permite administrar la integración de Edge Delivery Services en sus programas.

Consulte también [Introducción a Edge Delivery Services en Cloud Manager](/help/implementing/cloud-manager/edge-delivery/introduction-to-edge-delivery-services.md).

LAS CONFIGURACIONES DE BOTS DE AEM ADECUADAS DEBEN ESTAR CONFIGURADAS PRIMERO PARA QUE LAS ACTUALIZACIONES DE CONTENIDO SE REALICEN AUTOMÁTICAMENTE. ¿VERDADERO? ¿FALSO?

**Para crear un sitio de Edge Delivery en Cloud Manager con un solo clic:**

1. Inicie sesión en Cloud Manager en [`https://my.cloudmanager.adobe.com`](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la esquina superior izquierda de la página, haga clic en ![Mostrar icono de menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) para mostrar el menú de la izquierda.
1. En el menú del lado izquierdo, bajo el encabezado **Servicios**, haga clic en ![Icono de página web](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Sitios Edge Delivery**.
1. En la página Edge Delivery, en el cuadro de diálogo **Lista de tareas pendientes de Edge Delivery**, en el cuadro de grupo **Completar requisitos previos**, haga clic en **Aprovisionar**.
1. En el cuadro de diálogo **Aprovisionar sitio Edge Delivery**, en el campo de texto **Nombre del proyecto**, escriba el nombre del sitio y, a continuación, haga clic en **Aprovisionar**.
Aparece un mensaje cerca de la parte superior central de la pantalla que le informa de que se ha iniciado el aprovisionamiento del sitio Edge Delivery.
Cuando se completa el aprovisionamiento y se valida el sitio, el nombre del sitio aparece en el área de **sitios de Edge Delivery** de la página de Edge Delivery.

### Explorar un sitio de Edge Delivery recién creado


1. Haga clic en el vínculo Repositorio Git a la derecha del nombre del sitio.

Publicar.

Haga clic en Nombre del sitio,

realice algunos cambios y luego publique

Vea la página en la vista previa y, a continuación, cambie la URL para ver la versión en directo.

Añadir colaboradores.


## Previsualización de un sitio de Edge Delivery de un solo clic

## Publicación de un sitio de Edge Delivery con un solo clic





## Añadir colaboradores al sitio de Edge Delivery con un solo clic


































Estas mejoras tienen como objetivo mejorar la automatización, simplificar los procesos de configuración y mejorar la colaboración entre los usuarios de Edge Delivery Services. <!-- CMGR-59362 -->

![Crear un sitio Edge Delivery con un clic](/help/implementing/cloud-manager/release-notes/assets/eds-one-click-60.png)

![Aprovisionar cuadro de diálogo del sitio de Edge Delivery](/help/implementing/cloud-manager/release-notes/assets/eds-provision-60.png)