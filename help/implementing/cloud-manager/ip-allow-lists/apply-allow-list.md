---
title: Aplicar y anular la aplicación de Listas de permitidos IP
description: Aprenda a aplicar y dejar de aplicar Listas de permitidos IP a entornos de Cloud Manager.
exl-id: 7158496c-b0c4-4228-a306-71dc51003c57
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1415d07235641262814e81362c806572bcf582ba
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 18%

---


# Aplicar y dejar de aplicar Listas de permitidos IP {#apply-allow-list}

Al aplicar Listas de permitidos IP, todos los intervalos de IP incluidos en la definición de la lista se asocian a un servicio de autor o publicación dentro de un entorno. Cancelar la aplicación de una lista es lo contrario a este proceso.

{{add-cm-allowlist-frontend-pipeline}}

## Aplicar Listas de permitidos IP {#applying}

Un usuario con el rol **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para aplicar una Lista de permitidos IP.

**Para aplicar Listas de permitidos IP:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Seleccione la organización adecuada.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.
1. Desde la página **Información general**, vaya a la pantalla **Entornos**.
1. En la pantalla **Entornos**, vaya a la página de detalles específicos del entorno.
1. Vaya a la tabla **Lista de permitidos IP**.
1. Utilice los campos de entrada de la parte superior de la tabla para poder seleccionar la Lista de permitidos IP y el servicio de autor o publicación al que desea aplicarla.
La Lista de permitidos IP ya debe existir en Cloud Manager para aplicarla. Consulte [Agregar Listas de permitidos IP](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md).
1. Haga clic en **Aplicar** y confirme el envío.

## No aplicar Listas de permitidos IP {#un-applying}

Un usuario con el rol **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para anular la aplicación de una Lista de permitidos IP.

**Para anular la aplicación de Listas de permitidos IP:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).
1. Seleccione la organización adecuada.
1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.
1. Vaya a la pantalla **Entornos** de la página **Información general**.
1. Vaya a la página de detalles específicos del entorno en la pantalla **Entornos**.1. Vaya a la tabla **Lista de permitidos IP**.
1. Identifique la fila de la Lista de permitidos IP que desea anular.
1. En el lado derecho de la fila identificada, haga clic en el botón de puntos suspensivos y, a continuación, seleccione **No aplicar**.
1. Confirme el envío.
