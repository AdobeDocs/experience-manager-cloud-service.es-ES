---
title: Añadir Listas de permitidos IP
description: Aprenda a añadir sus propias Listas de permitidos IP con Cloud Manager.
exl-id: 769be71f-5c11-4f98-8906-7a5667a25aee
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1415d07235641262814e81362c806572bcf582ba
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 12%

---


# Agregar una lista de IP permitidas {#add-ip-allow-list}

Aprenda a añadir su propia Lista de permitidos IP con Cloud Manager.

Un usuario con el rol **Propietario del negocio** o **Administrador de implementación** puede seguir estos pasos para agregar una Lista de permitidos IP.

{{add-cm-allowlist-frontend-pipeline}}

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

## Añadir la Lista de permitidos IP de Cloud Manager {#add-cm-allowlist}

La canalización front-end requiere que se agregue de antemano la siguiente Lista de permitidos IP de Cloud Manager.

**Lista de permitidos IP DE Cloud Manager**

`52.254.106.192/28,20.186.185.181,52.254.106.240/28,52.254.107.128/28,52.254.105.192/28,52.254.106.176/28,20.186.185.227,52.254.106.144/28,52.254.107.64/28,20.186.185.239,20.22.83.112,52.254.107.80/28,52.254.107.144/28,52.254.106.224/28,20.14.241.153,52.254.107.0/28,52.254.107.32/28,52.254.106.208/28,40.70.154.136/29,52.254.106.160/28,52.254.107.16/28,52.254.106.0/28,4.152.211.251`

Para evitar interrupciones en la ejecución de la canalización front-end, asegúrese de que esta Lista de permitidos IP de Cloud Manager se agregue y luego se aplique al servicio de creación del entorno *antes de* de habilitar la canalización.

**Para agregar la Lista de permitidos IP de Cloud Manager:**

1. Inicie sesión en Cloud Manager en [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) y seleccione la organización adecuada.

1. En la consola **[Mis programas](/help/implementing/cloud-manager/navigation.md#my-programs)**, seleccione el programa.

1. En la página **Resumen del programa**, usando el panel lateral del lado izquierdo (puede que tengas que hacer clic en el icono de hamburguesa en la esquina superior izquierda para ver el panel), haz clic en **Listas de permitidos IP**.

1. Cerca de la esquina superior derecha de la página Listas de permitidos IP, haga clic en **Agregar Lista de permitidos IP**.

1. En el cuadro de diálogo **Agregar Lista de permitidos IP**, en el campo **Nombre de Lista de permitidos IP**, escriba *`Cloud Manager`*.

1. Copie el bloque de direcciones de Lista de permitidos IP de Cloud Manager anterior. Cada dirección ya está separada por una coma.

1. En el cuadro de diálogo **Agregar Lista de permitidos IP**, pegue el bloque en el campo **Dirección IP / CIDR**.

1. Coloque el cursor justo después de la primera coma en la lista de direcciones y presione **Intro**.

1. Haga clic en **Guardar**.

Ahora, [aplique la Lista de permitidos IP de Cloud Manager](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) a sus entornos de programa.



