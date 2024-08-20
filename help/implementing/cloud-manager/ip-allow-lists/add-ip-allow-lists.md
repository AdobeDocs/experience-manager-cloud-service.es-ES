---
title: Añadir Listas de permitidos IP
description: Aprenda a añadir sus propias Listas de permitidos IP con Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f4c6331491bb08e81964476ad58065c1ee022967
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 14%

---


# Agregar una lista de IP permitidas {#add-ip-allow-list}

Aprenda a añadir su propia Lista de permitidos IP con Cloud Manager.

Un usuario con el rol **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para agregar una Lista de permitidos IP.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En la página **Resumen del programa**, usando el panel lateral del lado izquierdo (puede que tengas que hacer clic en el icono de hamburguesa en la esquina superior izquierda para ver el panel), haz clic en **Listas de permitidos IP**.

   ![Opción de Listas de permitidos IP en el panel lateral](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Cerca de la esquina superior derecha de la página Listas de permitidos IP, haga clic en **Agregar Lista de permitidos IP**.

   ![Cuadro de diálogo Añadir lista de IP permitidas](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. En el cuadro de diálogo **Agregar Lista de permitidos IP**, en el campo **Nombre de Lista de permitidos IP**, escriba un nombre que desee usar para hacer referencia a la Lista de permitidos IP. Este nombre es meramente informativo. Asegúrese de que sea lo suficientemente descriptivo como para ayudarle a identificar la lista.

1. En el campo **Dirección IP / CIDR**, introduzca un bloque CIDR IP o IP. Separe varios bloques con una coma o una tabulación.

1. Haga clic en **Guardar**.

Después de guardar, la Lista de permitidos IP recién creada aparece como una fila en la tabla de la página **Listas de permitidos IP**.
