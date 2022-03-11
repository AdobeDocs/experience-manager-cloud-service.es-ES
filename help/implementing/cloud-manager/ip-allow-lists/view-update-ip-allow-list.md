---
title: 'Visualización y actualización: Listas de permitidos IP en Cloud Manager'
description: 'Visualización y actualización: Listas de permitidos IP en Cloud Manager'
exl-id: 9f9aebcd-b6d0-497a-b262-0a24b4938b45
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 2%

---

# Visualización y actualización de una lista de permitidos de IP {#view-update}

Puede ver y actualizar las Listas de permitidos IP en los siguientes casos:

* Para ver y actualizar para ver simplemente los detalles de una o varias Listas de permitidos IP.
* Para editar una o más de las siguientes opciones:
   * Intervalos IP en la definición del nombre de regla
   * Nombre reconocible de la regla de Lista de permitidos IP

## Actualizar Lista de permitidos IP {#update-ip-allow-lists}


Un usuario con la función Propietario empresarial o Administrador de implementación debe haber iniciado sesión para poder actualizar una Lista de permitidos IP.

>[!NOTE]
>El asistente Ver y actualizar mostrará los rangos de IP, IP o IP que definen la regla. Además, muestra los entornos y el servicio en los que se aplica la regla.

Siga los pasos a continuación para actualizar una Lista de permitidos IP:

1. Vaya a la **LISTAS DE PERMITIDOS IP** desde la página **Entornos** en el Navegador.
1. Identifique la fila en la que se muestra la regla de Lista de permitidos IP que desea ver/actualizar.
1. Seleccione el **...** del extremo derecho de la fila.
1. Seleccione el **Ver y actualizar** .
1. Realice cambios en el nombre o las IP y confirme el envío.

## Consideraciones importantes al agregar, actualizar o eliminar Listas de permitidos IP {#considerations}

* Añadir un nuevo rango de IP a la Lista de permitidos IP lo aplicará automáticamente a todos los servicios de entorno correspondientes.
* Si se elimina un rango de IP de la Lista de permitidos IP, se cancelará la aplicación automáticamente de todos los servicios de entorno correspondientes.
* No se pueden realizar actualizaciones en una Lista de permitidos IP mientras una actualización anterior esté en curso y no se haya completado.
* No se pueden realizar actualizaciones en una Lista de permitidos IP si existe algún error de una actualización anterior. Se deben borrar todos los errores intentando volver a intentar la actualización.
Consulte [Comprobación del estado de Lista de permitidos de IP](/help/implementing/cloud-manager/ip-allow-lists/check-ip-allow-list-status.md) para obtener más información.
