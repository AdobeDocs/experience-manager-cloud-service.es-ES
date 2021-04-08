---
title: 'Edición de un programa de espacio aislado '
description: Edición de un programa de espacio aislado
exl-id: e4545f7e-5329-40ad-81bb-a383c68f5d66
translation-type: tm+mt
source-git-commit: 6a5882a942511a07b9dcdd2e2bf47eb311235f92
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# Edición de un programa de espacio aislado {#create-sandbox-program}

Los usuarios con los permisos necesarios ahora pueden editar un programa de producción, lo que les permite hacer lo siguiente de forma autoservicio:

* Agregar la solución Sitios a un programa existente con Assets (o viceversa).
* Elimine Sitios (o Recursos) de un programa existente con Sitios y Recursos.
* Agregue el derecho a una solución no utilizada a un programa existente o como un nuevo programa.

   >[!NOTE]
   >Un usuario con la función Propietario empresarial debe iniciar sesión para editar correctamente el programa.

Siga los pasos a continuación para editar un programa de espacio aislado:

1. Vaya a la página **Editar programa** desde la página *Información general* de Cloud Manager.

1. La página **Editar Programa** muestra tres opciones (**Sitios**, **Comercio** y **Recursos**) tanto para los programas de producción como para los de entornos limitados.
   ![](assets/edit-prg.png)


## Consideraciones al editar un programa {#considerations-editing}

Al editar un programa, deben revisarse algunas consideraciones:

* Se debe seleccionar al menos una solución para un programa que, por lo tanto, no se permitirá que el usuario anule la selección de todas las soluciones durante el flujo de trabajo Editar programa .

* Al hacer clic en el botón **Save**, si las soluciones seleccionadas han cambiado, las actualizaciones de la solución para los entornos surtirán efecto tras la siguiente implementación.
