---
title: Adición de Listas de permitidos IP
description: Aprenda a añadir su propia lista de permitidos IP con Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 378ff582435f1ab3db431a0c9c3e80a4661cccc4
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 3%

---


# Adición de una lista de permitidos de IP {#add-ip-allow-list}

Aprenda a añadir su propia lista de permitidos IP con Cloud Manager.

Un usuario en la variable **Propietario empresarial** o **Administrador de implementación** puede seguir estos pasos para agregar una lista de permitidos IP.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y el programa adecuados.

1. Vaya a **Entornos** de la **Información general** página.

1. Vaya a **LISTAS DE PERMITIDOS IP** desde la página **Entornos** en el Navegador.

   ![Opción listas de permitidos IP del panel lateral](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Haga clic en **Añadir Lista de permitidos IP** para abrir el **Añadir Lista de permitidos IP** diálogo.

   ![Cuadro de diálogo Añadir Lista de permitidos IP](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Escriba un nombre que desee usar para hacer referencia a la lista de permitidos en la **Nombre de Lista de permitidos IP** campo .

   * Esto es solo informativo y debe ser descriptivo para ayudarle a identificar la lista.

1. Introduzca un bloque IP o IP CIDR en la variable **Dirección IP/CIDR.** campo .

   * Los bloques múltiples pueden separarse con una coma o una pestaña.

1. Haga clic en **Guardar** para confirmar el envío.

Al guardar, la lista de permitidos IP recién creada aparecerá como una fila en la tabla de la **LISTAS DE PERMITIDOS IP** página.
