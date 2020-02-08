---
title: Uso compartido de carpetas privadas
description: Obtenga información sobre cómo crear una carpeta privada en Recursos Adobe Experience Manager (AEM) y compartirla con otros usuarios, así como sobre cómo asignarles varios privilegios.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Uso compartido de carpetas privadas {#private-folder-sharing}

Puede crear una carpeta privada en la interfaz de usuario Recursos Adobe Experience Manager (AEM) que esté disponible exclusivamente para usted. Puede compartir esta carpeta privada con otros usuarios y asignarles varios privilegios. En función del nivel de privilegios que asigne, los usuarios podrán realizar varias tareas en la carpeta, por ejemplo, ver recursos dentro de la carpeta o editar los recursos.

1. En la consola Recursos, toque o haga clic en **[!UICONTROL Crear]** en la barra de herramientas y, a continuación, elija **[!UICONTROL Carpeta]** en el menú.
1. En el cuadro de diálogo **[!UICONTROL Agregar carpeta]** , introduzca un título y un nombre (opcional) para la carpeta y seleccione **[!UICONTROL Privado]**.
1. Toque o haga clic en **[!UICONTROL Crear]**. Se crea una carpeta privada en la interfaz de usuario.
1. Para compartir la carpeta con otros usuarios y asignarles privilegios, seleccione la carpeta y toque o haga clic en el icono **[!UICONTROL Propiedades]** de la barra de herramientas.

   >[!NOTE]
   >
   >La carpeta no estará visible para ningún otro usuario hasta que la comparta.

1. En la página Propiedades de la carpeta, seleccione un usuario de la lista **[!UICONTROL Agregar usuario]** , asigne una función al usuario de la carpeta privada y haga clic en **[!UICONTROL Agregar]**.

   >[!NOTE]
   >
   >Puede asignar varias funciones, como Editor, Propietario o Visor, al usuario con el que comparte la carpeta. Si asigna una función Propietario al usuario, este tiene privilegios de editor en la carpeta. Además, el usuario puede compartir la carpeta con otros usuarios. Si asigna una función de editor, el usuario puede editar los recursos de la carpeta privada. Si asigna una función de visor, el usuario solo puede ver los recursos de la carpeta privada.

1. Haga clic en **[!UICONTROL Guardar.]** Según la función que asigne, al usuario se le asignará un conjunto de privilegios en su carpeta privada cuando inicie sesión en Recursos AEM.
1. Haga clic en **[!UICONTROL Aceptar]** para cerrar el mensaje de confirmación.
1. El usuario con el que comparte la carpeta recibe una notificación de uso compartido. Inicie sesión en Recursos AEM con las credenciales del usuario para ver la notificación.
1. Toque o haga clic en el icono Notificación para abrir la lista de notificaciones.
1. Toque o haga clic en la entrada de la carpeta privada compartida por el administrador para abrir la carpeta.

>[!NOTE]
>
>Para poder crear una carpeta privada, necesita permisos de lectura y edición de ACL en la carpeta principal en la que desea crear una carpeta privada. Si no es administrador, estos permisos no se habilitan de forma predeterminada en */content/dam*. En este caso, obtenga primero estos permisos para su ID de usuario o grupo antes de intentar crear carpetas privadas o ver la configuración de carpetas.
