---
title: Configuración de un sitio de Edge Delivery para utilizar un repositorio Git externo
description: Obtenga información sobre cómo vincular un sitio de Edge Delivery a un repositorio Git privado o empresarial.
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 1dbaef34-efa3-4287-b7b1-f60db938146d
source-git-commit: dea8a3df29876df1c97454a97602045eb50121ad
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 35%

---

# Configuración de un sitio de Edge Delivery para utilizar un repositorio Git externo

Para extraer código de cualquier repositorio Git privado ya incorporado en Cloud Manager, puede configurar su sitio Edge Delivery.

<!--
**Supported Git Vendors**

| Support level | Vendors | Notes |
| --- | --- | --- |
| General availability | &bull; GitHub Enterprise (self-hosted version)<br>&bull; Bitbucket (Cloud version)<br>&bull; GitLab (Cloud and self-hosted version) | Connect without enablement requests |
| Alpha program | Azure DevOps (Cloud version) | [Request access](mailto:grp-cloudmanager_byog@adobe.com) |
| Beta program | Adobe-hosted repository (created in Cloud Manager) | [Request access](mailto:grp-cloudmanager_byog@adobe.com) |
-->

**Para usar un repositorio Git externo, configure un sitio Edge Delivery:**

{{sign-in-to-cloud-manager}}

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa con Edge Delivery Services configurado. Seleccione el programa en el que desea configurar un sitio de Edge Delivery para utilizar un repositorio Git externo.
1. En el carril izquierdo, bajo el encabezado **Programa**, haga clic en **![Icono de información general](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg) Información general**.
1. En la página **Resumen del programa**, haga clic en la pestaña **Edge Delivery**.
1. En la tabla **Sitios de Edge Delivery**, haga clic en ![Icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de una fila cuyo sitio desee configurar para que utilizar un repositorio externo y, a continuación, haga clic en **Traer su propio Git**.
1. En el cuadro de diálogo **Traer su propio Git**, en la lista desplegable **Nombre del repositorio**, elija un repositorio Git con el estado `READY` y luego haga clic en **Confirmar**.

   Cloud Manager devuelve un token secreto de un solo uso. Si vuelve a configurar el sitio, Cloud Manager genera un nuevo token secreto.

1. Copie el token y agréguelo a la configuración del sitio en **helix-admin**, tal como se describe en la [guía BYO Git](https://www.aem.live/developer/byo-git).
1. En Cloud Manager, haga clic en ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de una fila en cuyo sitio configuró para usar un repositorio externo y luego haga clic en **Código de sincronización**.
1. Elija la rama que desea sincronizar y haga clic en **Sincronizar**.

Cada confirmación en cualquier rama ahora desencadena una sincronización automática. Vuelva a usar **Código de sincronización** cada vez que se requiera una sincronización manual completa.

## Autenticar solicitudes de clonación de Git {#authenticate-git-clone-requests}

Puede clonar su repositorio [!DNL Bring Your Own Git] desde Cloud Manager mediante un token de IMS o el secreto byogit que Cloud Manager genera al configurar el sitio. Ambas credenciales se autentican con el extremo clónico, por lo que puede utilizar el secreto que hélice-admin ya almacena para la sincronización de código de [!DNL Edge Delivery Services].

El extremo de clonación acepta la credencial en el encabezado `Authorization`. Cloud Manager valida el secreto byogit con el valor almacenado para ese repositorio. Las solicitudes que no incluyen un token de IMS válido ni un secreto byogit válido devuelven una respuesta `401`.

>[!NOTE]
>
>Los flujos de trabajo de clonación autenticados por IMS existentes no se ven afectados. El secreto byogit es una opción adicional, no un reemplazo.

**Para clonar el repositorio con el secreto byogit:**

1. Copie el secreto que Cloud Manager devuelve al configurar el sitio.
1. Ejecute el comando clone y pase el secreto en el encabezado `Authorization`.

   `git -c http.extraHeader="Authorization: <byogit-secret>"` clon `https://cm-repo.adobe.io/api/program/<program-id>/repository/<repository-id>.git`

   Reemplace `<byogit-secret>` por el secreto de Cloud Manager y reemplace `<program-id>` y `<repository-id>` por los valores de su programa.
