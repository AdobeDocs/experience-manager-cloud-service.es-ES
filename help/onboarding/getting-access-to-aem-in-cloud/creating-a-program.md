---
title: 'Creación de un programa: Cloud Service'
description: 'Creación de un programa: Cloud Service'
translation-type: tm+mt
source-git-commit: d85c0e9035ee09cf86aeea1cae20d545823eaca0
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 3%

---


# Creación de un programa {#create-a-program}

La solución nativa de la nube proporciona al usuario los permisos necesarios y la capacidad de crear un programa en un modelo de autoservicio.

Un asistente para la creación de programas pedirá al usuario que envíe detalles, según el objetivo del usuario al crear el programa dentro de los límites de lo que está disponible para el cliente u organización específico.

En caso de acceso por primera vez a Cloud Manager o si no hay programas en el inquilino, el usuario verá **Crear su primer programa** en la pantalla. Si el usuario selecciona *Esc* o hace clic fuera del cuadro de diálogo, se muestra la siguiente pantalla:

![](assets/create-program1.png)


## Uso del Asistente para crear programas {#using-create-program-wizard}

Según el objetivo del usuario al crear el programa dentro de los límites de lo que está disponible para el cliente u organización específico, un asistente para la creación de programas pedirá al usuario que envíe uno o más detalles.

![](assets/create-sandbox.png)


## Creación de un programa de espacio aislado {#create-sandbox-program}

Siga los pasos a continuación para crear un programa de simulación de pruebas:

1. En el asistente de creación de programa, seleccione **Configurar un simulador de pruebas**. El usuario envía el nombre del programa antes de seleccionar **Crear**.

   ![](assets/create-sandbox.png)

1. El usuario verá la nueva tarjeta de programa de simulación de pruebas en la página de aterrizaje y podrá pasar el ratón por encima para seleccionar el icono de Cloud Manager para navegar a la página de información general de Cloud Manager. La tarjeta informará al usuario sobre el estado de la configuración automática del programa de espacio aislado recién creado. El usuario verá progresión.

   ![](assets/program-create-setupdemo2.png)

1. Una vez que se haya configurado el programa y se haya completado el paso de creación del proyecto, el usuario puede acceder al enlace **Administrar Git**, como se muestra en la figura siguiente:

   ![](assets/create-program4.png)

   >[!NOTE]
   >
   >Para obtener más información sobre el acceso y la administración del repositorio de Git mediante la administración de cuentas de Git de autoservicio desde la interfaz de usuario de Cloud Manager, consulte [Acceso a Git](/help/implementing/cloud-manager/accessing-git.md).


1. Una vez creado el entorno de desarrollo, el usuario puede **acceder al vínculo AEM**, como se muestra en la figura siguiente:

   ![](assets/create-program-5.png)

1. Una vez finalizada la implementación de la canalización de no producción en el desarrollo, el asistente guía al usuario para acceder a AEM (en desarrollo) o para implementar código en el entorno de desarrollo:

   ![](assets/create-program-setup-deploy.png)

   >[!NOTE]
   >También puede editar, cambiar o agregar un programa desde la página Información general de Cloud Manager , como se muestra a continuación:

   ![](assets/create-program-a1.png)

## Eliminación de un programa de espacio aislado {#delete-sandbox-program}

Un usuario de programa de espacio aislado en la función *Propietario empresarial* o *Administrador de implementación* en Cloud Manager puede eliminar su conjunto de entornos de producción y ensayo a través de la interfaz de usuario de Cloud Manager.

>[!NOTE]
>Al seleccionar la opción de eliminación en producción o fase también se eliminan las otras del conjunto.

La opción de eliminación está disponible en la página de aterrizaje, como se muestra a continuación:

![](assets/delete-sandbox1.png)

O bien,

Seleccione **Eliminar programa** en la página **Información general del programa** para eliminar el programa de espacio aislado para pruebas.

![](assets/delete-sandbox2.png)


## Creación de un programa regular {#create-regular-program}

Un programa *Regular* está pensado para un usuario familiarizado con AEM y Cloud Manager y listo para empezar a escribir, crear y probar código con el objetivo de implementarlo en Producción.

Siga los pasos a continuación para crear un programa normal:

1. Seleccione **Configurar para producción** en el asistente Crear programa para crear un programa normal. El usuario puede aceptar el nombre de programa predeterminado o editarlo antes de seleccionar **Continuar**.

   ![](assets/create-prod1.png)

1. El usuario selecciona las soluciones que se incluirán en el programa en la pantalla que se presentará después de la pantalla anterior.



   >[!NOTE]
   >
   >La siguiente pantalla solo se muestra para el segmento de clientes que han comprado más de una solución. Para los clientes que solo han comprado una solución, no se mostrará la siguiente pantalla de selección de soluciones.

   ![](assets/set-up-prod2.png)

1. Una vez seleccionadas las soluciones, haga clic en **Crear**.

   ![](assets/set-up-prod3.png)

1. Una vez que vea la tarjeta del programa en la página de aterrizaje, pase el ratón por encima para seleccionar el icono de Cloud Manager para navegar a la página **Información general** de Cloud Manager.

   ![](assets/set-up-prod4.png)

1. La tarjeta de llamada a acción principal guiará al usuario para crear un entorno, crear una canalización que no sea de producción y, finalmente, una canalización de producción.
   ![](assets/set-up-prod5.png)


   >[!NOTE]
   >
   >Un programa normal no tiene la función **Auto-setup**.





