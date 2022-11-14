---
title: Agregar una lista de IP permitidas
description: Aprenda a agregar su propia lista de IP permitidas con Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 378ff582435f1ab3db431a0c9c3e80a4661cccc4
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 100%

---


# Agregar una lista de IP permitidas {#add-ip-allow-list}

Aprenda a agregar su propia lista de IP permitidas con Cloud Manager.

Un usuario con el rol de **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para agregar una lista de IP permitidas.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Navegue hasta la página **Listas de IP permitidas** desde la pantalla **Entornos**.

   ![Opción Listas de IP permitidas del panel lateral](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Haga clic en **Agregar lista de IP permitidas** para abrir el cuadro de diálogo **Agregar lista de IP permitidas**.

   ![Cuadro de diálogo Agregar lista de IP permitidas](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Escriba un nombre que desee usar para hacer referencia a la lista de permitidos en el campo **Nombre de la lista de IP permitidas**.

   * Esto es solo informativo y debe ser descriptivo para ayudarle a identificar la lista.

1. Introduzca un bloque IP o IP CIDR en el campo **dirección IP/CIDR**.

   * Los bloques múltiples pueden separarse mediante una coma o una tabulación.

1. Haga clic en **Guardar** para confirmar el envío.

Al guardar, la lista de IP permitidas recién creada aparecerá como una fila en la tabla de la página **Listas de IP permitidas**.
