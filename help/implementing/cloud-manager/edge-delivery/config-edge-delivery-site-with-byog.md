---
title: Configuración de un sitio de Edge Delivery para utilizar un repositorio Git externo
description: Obtenga información sobre cómo vincular un sitio de Edge Delivery a un repositorio Git privado o empresarial.
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 1dbaef34-efa3-4287-b7b1-f60db938146d
source-git-commit: e1922bd862a2106a274694ea1d3a98da9c186049
workflow-type: ht
source-wordcount: '325'
ht-degree: 100%

---

# Configuración de un sitio de Edge Delivery para utilizar un repositorio Git externo

Puede configurar su sitio de Edge Delivery para que extraiga código de cualquier repositorio Git privado ya incorporado en Cloud Manager.

**Proveedores Git compatibles**

| Niveles de soporte | Proveedores | Notas |
| --- | --- | --- |
| Disponibilidad general | • GitHub Enterprise (versión autoalojada)<br>• Bitbucket (versión en la nube)<br>• GitLab (versión en la nube y autoalojada) | Conectar sin solicitudes de habilitación |
| Programa Alpha | Azure DevOps (versión en la nube) | [Solicitar acceso](mailto:grp-cloudmanager_byog@adobe.com) |
| Programa Beta | Repositorio alojado en Adobe (creado en Cloud Manager) | [Solicitar acceso](mailto:grp-cloudmanager_byog@adobe.com) |

**Para configurar un sitio de Edge Delivery para que use un repositorio Git externo:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione el programa adecuado.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa con Edge Delivery Services configurado donde desee configurar un sitio de Edge Delivery para usar un repositorio Git externo.
1. En el carril izquierdo, bajo el encabezado **Programa**, haga clic en **![Icono de información general](/help/implementing/cloud-manager/edge-delivery/assets/overview.svg) Información general**.
1. En la página **Resumen del programa**, haga clic en la pestaña **Edge Delivery**.
1. En la tabla **Sitios de Edge Delivery**, haga clic en ![Icono Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de una fila cuyo sitio desee configurar para que utilizar un repositorio externo y, a continuación, haga clic en **Traer su propio Git**.
1. En el cuadro de diálogo Traer su propio Git, en la lista desplegable **Nombre del repositorio**, elija un repositorio Git con el estado `READY` y luego haga clic en **Confirmar**.

   Cloud Manager devuelve un token secreto de un solo uso. Si vuelve a configurar el sitio, Cloud Manager genera un nuevo token secreto.

1. Copie el token y agréguelo a la configuración del sitio en **helix-admin**, tal como se describe en la [guía BYO Git](https://www.aem.live/developer/byo-git).
1. Cuando vuelva a Cloud Manager, haga clic en ![Más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) al final de una fila cuyo sitio acaba de configurar para que use un repositorio externo y, a continuación, haga clic en **Código de sincronización**.
1. Elija la rama que desea sincronizar y haga clic en **Sincronizar**.

Cada confirmación en cualquier rama ahora desencadena una sincronización automática. Vuelva a usar **Código de sincronización** cada vez que se requiera una sincronización manual completa.
