---
title: 'Edición de un programa de producción '
description: 'Edición de un programa de producción '
translation-type: tm+mt
source-git-commit: 78bc94f7e3dab37b7f83f480ef5438165e1897bc
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---


# Edición de un programa de producción {#create-production-program}

Los usuarios con los permisos necesarios ahora pueden editar un programa de producción, lo que les permite hacer lo siguiente de forma autoservicio:

* Agregar la solución Sitios a un programa existente con Assets (o viceversa).
* Elimine Sitios (o Recursos) de un programa existente con Sitios y Recursos.
* Agregue el derecho a una solución no utilizada a un programa existente o como un nuevo programa.

   >[!NOTE]
   >Un usuario con la función Propietario empresarial debe iniciar sesión para editar correctamente el programa.

Siga los pasos a continuación para editar un programa de producción:

1. Vaya a la página **Editar programa**.

1. La página **Editar programa** mostrará dos fichas (General y Soluciones) tanto para los programas de producción como para los de entornos limitados.

   ![](assets/edit-program.png)

   >[!NOTE]
   >Aunque se mostrarán tanto Sitios como Recursos, uno de ellos puede deshabilitarse según lo que se haya comprado y no se use. Específicamente, si la organización no tiene derechos no utilizados para una solución en particular, se mostrará esa solución, pero se deshabilitará.

## Consideraciones al editar un programa {#considerations-editing}

Al editar un programa, deben revisarse algunas consideraciones:

* Se debe seleccionar al menos una solución para un programa que, por lo tanto, no se permitirá que el usuario anule la selección de todas las soluciones durante el flujo de trabajo Editar programa .

* Al hacer clic en el botón **Save**, si las soluciones seleccionadas han cambiado, las actualizaciones de la solución para los entornos surtirán efecto tras la siguiente implementación.