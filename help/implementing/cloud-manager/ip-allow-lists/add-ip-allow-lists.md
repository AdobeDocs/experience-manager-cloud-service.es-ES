---
title: Añadir Listas de permitidos IP
description: Aprenda a añadir sus propias Listas de permitidos IP con Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: d36dc453097b1f2507ff1ca6d775acf8b9ac5add
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 6%

---


# Añadir una lista de IP permitidas {#add-ip-allow-list}

Aprenda a añadir su propia Lista de permitidos IP con Cloud Manager.

Para agregar una Lista de permitidos IP, un usuario con el rol **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos.

{{add-cm-allowlist-frontend-pipeline}}
{{ip-allow-lists-ue}}

**Para agregar una Lista de permitidos IP:**

{{sign-in-to-cloud-manager}}

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione un programa.

1. En la página **Información general del programa**, usando el menú del lado izquierdo (si es necesario, haga clic en ![Mostrar icono del menú](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) en la esquina superior izquierda para ver el menú), haga clic en ![Icono de lista de tareas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_TaskList_18_N.svg) **Listas de permitidos IP**.

   ![Opción de Listas de permitidos IP en el menú del lado izquierdo](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Cerca de la esquina superior derecha de la página Listas de permitidos IP, haga clic en **Agregar Lista de permitidos IP**.

   ![Cuadro de diálogo Añadir lista de IP permitidas](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. En el cuadro de diálogo **Agregar Lista de permitidos IP**, en el campo **Nombre de Lista de permitidos IP**, escriba un nombre que desee usar para hacer referencia a la Lista de permitidos IP. Este nombre es meramente informativo. Asegúrese de que sea lo suficientemente descriptivo como para ayudarle a identificar la lista.

1. En el campo **Dirección IP / CIDR**, ingrese hasta 50 direcciones IP o bloques CIDR. Puede agregarlos de cualquiera de las siguientes maneras:

   * Uno a la vez: escriba una dirección y luego presione `Enter`. Repita el proceso para cada dirección adicional.
   * Múltiples a la vez: escriba direcciones separadas por comas (,) o tabulaciones y, a continuación, presione `Enter` para que cada dirección se procese de forma individual.

1. Cuando termine de escribir la última dirección IP o bloque CIDR, presione `Enter` para confirmar la entrada. La entrada se reconoce solo después de presionar `Enter`, y el botón **Guardar** se activa.

1. Haga clic en **Guardar**.

Después de guardar, la Lista de permitidos IP recién creada aparecerá como una fila en la tabla de páginas **Listas de permitidos IP**.

