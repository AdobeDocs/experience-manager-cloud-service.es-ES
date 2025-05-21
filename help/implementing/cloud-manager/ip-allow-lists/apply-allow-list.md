---
title: Aplicación y cancelación de listas de permitidos de IP
description: Aprenda a aplicar y dejar de aplicar Listas de permitidos IP a entornos de Cloud Manager.
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: aa33f84e6b38019f41ea0a4db8f49ccc201869f7
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 14%

---


# Aplicar y dejar de aplicar Listas de permitidos IP {#apply-allow-list}

Al aplicar Listas de permitidos IP, todos los intervalos de IP incluidos en la definición de la lista se asocian a un servicio de autor o publicación dentro de un entorno. Cancelar la aplicación de una lista es lo contrario a este proceso.

{{add-cm-allowlist-frontend-pipeline}}
{{ip-allow-lists-ue}}

## Aplicar Listas de permitidos IP {#applying}

Un usuario con el rol **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para aplicar una Lista de permitidos IP.

**Para aplicar Listas de permitidos IP:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Seleccione la organización adecuada.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.
1. Desde la página **Información general**, vaya a la pantalla **Entornos**.
1. En la pantalla **Entornos**, vaya a la página de detalles específicos del entorno.
1. Vaya a la tabla **Lista de permitidos IP**.
1. Utilice los campos de entrada de la parte superior de la tabla para poder seleccionar la Lista de permitidos IP y el servicio de autor, publicación o vista previa al que desea aplicarla.
La Lista de permitidos IP ya debe existir en Cloud Manager para aplicarla. Consulte [Agregar Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md).
1. Haga clic en ![Agregar icono](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Add_18_N.svg) **Aplicar** y confirme el envío.

## No aplicar Listas de permitidos IP {#un-applying}

Un usuario con el rol **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para anular la aplicación de una Lista de permitidos IP.

**Para anular la aplicación de Listas de permitidos IP:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Seleccione la organización adecuada.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.
1. Desde la página **Información general**, vaya a la página **Entornos**.
1. Vaya a la página de detalles específicos del entorno.
1. En la ficha General, desplácese hasta la tabla **Lista de permitidos IP**.
1. Identifique la fila de la Lista de permitidos IP que desea anular.
1. En el lado derecho de la fila identificada, haga clic en ![Icono de más](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg).
1. Haga clic en **Anular la aplicación**.
1. En el cuadro de diálogo **No aplicar Lista de permitidos IP**, haga clic en **No aplicar**.
