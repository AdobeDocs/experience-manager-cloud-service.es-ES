---
title: 'Edición de un programa de producción '
description: Edición de un programa de producción
exl-id: 745c10af-f0a0-49e9-bb79-3fd058fad16c
source-git-commit: 8974217f8a3db6cfe96082fe2ed0277c243fa7e1
workflow-type: tm+mt
source-wordcount: '257'
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

1. Haga clic en la opción **Editar programa** de la página *Información general* de Cloud Manager

   ![](assets/edit-program-overview.png)

1. La página **Editar Programa** muestra dos fichas **General** y **Soluciones y complementos**.

   Vaya a la pestaña **General** para editar la descripción del programa.

   ![](assets/edit-program-prod1.png)

   La pestaña **Solutions &amp; Add-ons** muestra dos opciones, como **Sites** y **Assets** para los programas de producción y Sandbox. Además, puede seleccionar la opción de complemento **Comercio**, que está disponible en **Sitios**, como se muestra en la figura siguiente.

   ![](assets/edit-prg.png)

   >[!NOTE]
   >Se debe seleccionar al menos una solución para un programa, es decir, el usuario no puede anular la selección de todas las soluciones durante el flujo de trabajo Editar programa .

1. Haga clic en **Update** para completar el flujo de trabajo del programa de edición.


## Consideraciones al editar un programa {#considerations-editing}

Al editar un programa, deben revisarse algunas consideraciones:

* Se debe seleccionar al menos una solución para un programa, es decir, el usuario no puede anular la selección de todas las soluciones durante el flujo de trabajo Editar programa .

* Al hacer clic en el botón **Save**, si las soluciones seleccionadas han cambiado, las actualizaciones de la solución para los entornos surtirán efecto tras la siguiente implementación.
