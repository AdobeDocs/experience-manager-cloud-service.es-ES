---
title: 'Visualización y actualización: Listas de permitidos IP en el Administrador de podría'
description: 'Visualización y actualización: Listas de permitidos IP en el Administrador de podría'
translation-type: tm+mt
source-git-commit: b353de1a58eb8c31de7289677a589cf192ebc0b9
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Visualización y actualización de Listas de permitidos IP {#view-update}

Puede realizar la vista y actualización de Listas de permitidos IP en los siguientes escenarios:

* Para el menú Vista y actualización para simplemente vista los detalles de una o varias Listas de permitidos IP.
* Para editar una o varias de las siguientes opciones:
   * Intervalos IP en la definición del nombre de la regla
   * Nombre práctico de la regla de Lista de permitidos IP

## Actualizar Lista de permitidos IP {#update-ip-allow-lists}


Para poder actualizar una Lista de permitidos IP, debe iniciar sesión un usuario con la función Propietario de la empresa o Administrador de implementación.

>[!NOTE]
>El asistente de Vista y actualización mostrará el nombre, los intervalos IP o los intervalos IP que definen la regla. Además, mostrará los entornos y el servicio en los que se aplica la regla.

Siga los pasos a continuación para actualizar una Lista de permitidos IP:

1. Vaya a la página de Lista de permitidos IP desde la pantalla Entornos.
1. Identifique la fila donde se muestra la regla de Lista de permitidos IP que desea vista o actualización.
1. Seleccione **...** desde el extremo derecho de la fila.
1. Seleccione la opción Vista y actualización.
1. Realice cambios en el nombre o las IP y confirme el envío.

## Consideraciones importantes al Añadir, actualizar o eliminar Listas de permitidos IP {#considerations}

* Añadir un nuevo intervalo de IP a la Lista de permitidos de IP automáticamente lo aplicará a todos los servicios de entorno correspondientes.
* Al eliminar un intervalo de IP de la Lista de permitidos de IP automáticamente se anulará su aplicación de todos los servicios de entorno correspondientes.
* No se pueden realizar actualizaciones en una Lista de permitidos IP mientras una actualización anterior esté en curso y no se haya completado.
* No se pueden realizar actualizaciones en una Lista de permitidos IP si existe algún error de una actualización anterior. Se debe borrar cualquier error al intentar volver a intentar la actualización.
Consulte Comprobación del estado de Lista de permitidos de IP para obtener más información.