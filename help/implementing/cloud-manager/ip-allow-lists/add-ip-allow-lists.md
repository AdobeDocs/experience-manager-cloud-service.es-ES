---
title: Agregar una lista de IP permitidas
description: Aprenda a añadir su propia lista de permitidos de IP con Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 90250c13c5074422e24186baf78f84c56c9e3c4f
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 69%

---


# Agregar una lista de IP permitidas {#add-ip-allow-list}

Aprenda a añadir su propia lista de permitidos de IP con Cloud Manager.

Un usuario con la función de **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para agregar una lista de IP permitidas.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En el **[Mis programas](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/editing-programs.md#my-programs)** , seleccione el programa.

1. Desde el **Información general** , vaya a la página **Entornos** pantalla.

1. Desde el **Entornos** , vaya a la **LISTAS DE PERMITIDOS IP** página.

   ![Opción Listas de IP permitidas del panel lateral](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Clic **Añadir Lista de permitidos IP**.

   ![Cuadro de diálogo Añadir lista de IP permitidas](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. En el **Añadir Lista de permitidos IP** , escriba un nombre que desee utilizar para hacer referencia a la lista de permitidos en la **Nombre de Lista de permitidos IP** field.

   * Este nombre es solo informativo y debe ser descriptivo para ayudarle a identificar la lista.

1. Introduzca un bloque IP o IP CIDR en el campo **dirección IP/CIDR**.

   * Los bloques múltiples pueden separarse mediante una coma o una tabulación.

1. Haga clic en **Guardar**.

Al guardar, la lista de IP permitidas recién creada aparece como una fila en la tabla de la página **lista de IP permitidas**.
