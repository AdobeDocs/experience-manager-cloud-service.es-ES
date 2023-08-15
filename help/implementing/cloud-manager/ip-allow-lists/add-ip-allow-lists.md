---
title: Agregar una lista de IP permitidas
description: Obtenga información sobre cómo agregar su propia lista de permitidos IP mediante Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 40%

---


# Agregar una lista de IP permitidas {#add-ip-allow-list}

Obtenga información sobre cómo agregar su propia lista de permitidos IP mediante Cloud Manager.

Un usuario en la **Propietario del negocio** o **Administrador de implementación** Esta función puede seguir estos pasos para agregar una lista de permitidos IP.

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización y programa adecuados.

1. Vaya a la pantalla **Entornos** de la página **Información general**.

1. Navegue hasta la página **Listas de IP permitidas** desde la pantalla **Entornos**.

   ![Opción Listas de IP permitidas del panel lateral](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create.png)

1. Clic **Añadir Lista de permitidos IP** para abrir **Añadir Lista de permitidos IP** Cuadro de diálogo.

   ![Cuadro de diálogo Agregar Lista de permitidos IP](/help/implementing/cloud-manager/assets/ip-allow-list/ip-allow-list-create02.png)

1. Introduzca un nombre que desee utilizar para hacer referencia a la lista de permitidos en la **Nombre de Lista de permitidos IP** field.

   * Este nombre es solo informativo y debe ser descriptivo para ayudarle a identificar la lista.

1. Introduzca un bloque IP o IP CIDR en el campo **dirección IP/CIDR**.

   * Los bloques múltiples pueden separarse mediante una coma o una tabulación.

1. Haga clic en **Guardar** para confirmar el envío.

Después de guardar, la lista de permitidos IP recién creada aparece como una fila en la tabla de **LISTAS DE PERMITIDOS IP** página.
