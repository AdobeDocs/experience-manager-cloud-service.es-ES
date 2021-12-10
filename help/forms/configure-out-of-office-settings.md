---
title: Configuración de la configuración fuera de Office
seo-title: Configure Out of Office settings
description: Configuración fuera de la oficina
seo-description: Configure Out of Office settings
exl-id: c7e436f1-8e1c-4334-b3dc-ab9800695301
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# Configuración de fuera de Office {#configure-out-of-office-settings}

Si planea estar fuera de la oficina, puede especificar qué sucede con los artículos que se le han asignado durante ese período.

Tiene la opción de especificar una fecha y hora de inicio y una fecha y hora de finalización para que la configuración fuera de la oficina esté en vigor. Si se encuentra en una zona horaria diferente de la del servidor, la zona horaria utilizada es la del cliente.

Puede establecer una persona predeterminada a la que se envían todos los elementos. También puede especificar excepciones para que los elementos de procesos específicos se envíen a un usuario diferente o se mantengan en la bandeja de entrada hasta que vuelva. Si la persona designada también está fuera de la oficina, el artículo se dirige al usuario que ha designado. Si el elemento no se puede asignar a un usuario que no está fuera de la oficina, permanece en la bandeja de entrada.

Puede separar la delegación de elementos según los modelos de flujo de trabajo. Por ejemplo, puede asignar un elemento relacionado con el flujo de trabajo A al usuario A y asignar un elemento relacionado con el flujo de trabajo B al usuario B.


>[!NOTE]
>
>* Cuando habilita la configuración Fuera de la oficina, todos los elementos disponibles en la Bandeja de entrada, antes de habilitar dicha configuración, permanecen en la bandeja de entrada. Solo se delegan los elementos recibidos después de habilitar la configuración.
>* Cuando desactiva la configuración de Fuera de la oficina, los elementos delegados no se le asignan automáticamente. Puede utilizar la funcionalidad de reclamación para asignarle artículos.
>* Cuando el usuario A delega elementos al usuario B y el usuario B delega más al usuario C, entonces los elementos se asignan únicamente al usuario C y no al usuario B.
>* Cuando hay un bucle en la asignación, las tareas permanecen con el usuario original. Por ejemplo, cuando el usuario A delega elementos al usuario B delega al usuario C, el usuario C delega al usuario D y el usuario D delega al usuario B, se crea un bucle en . En tal situación, el elemento permanece con el Usuario original. El usuario A es el usuario original del ejemplo anterior.


## Habilite la configuración de Fuera de la oficina para su cuenta {#enable-out-of-office}

Realice los siguientes pasos para habilitar la configuración fuera de la oficina para su cuenta y delegar los elementos de la bandeja de entrada en otro usuario:

1. Inicie sesión en la instancia de AEM. Toque . ![Bandeja de entrada](assets/bell.svg) icono y toque **[!UICONTROL Ver todo]**. Aparecerá una lista de los elementos de la bandeja de entrada.
1. Toque . ![Selector de vista](assets/viewlist.svg) o ![Selector de vista](assets/calendar.svg) junto al icono **[!UICONTROL Crear]** pulse **[!UICONTROL Configuración]**. Aparecerá el cuadro de diálogo de configuración.
1. Abra el **[!UICONTROL Fuera de la oficina]** en el cuadro de diálogo configuración.
1. Toque . **[!UICONTROL Habilitar/Deshabilitar]** para habilitar la configuración fuera de Office.
1. Especifique la variable **[!UICONTROL Hora de inicio]**  y **[!UICONTROL Hora de finalización]** para la configuración. Los elementos se delegan únicamente durante el período especificado. Deje el **[!UICONTROL Hora de finalización]** campo vacío para delegar elementos durante un período de tiempo indefinido.
1. Seleccione el **[!UICONTROL Reenviar mis artículos durante este periodo]** casilla de verificación. Si no selecciona la opción y no especifica un usuario asignado, los elementos no se reenviarán a ningún usuario. Aunque no esté presente y la configuración esté habilitada, los elementos permanecerán en la bandeja de entrada.
1. Toque **[!UICONTROL Agregar usuario asignado]**. Especifique un usuario en la variable **[!UICONTROL Usuario asignado]** para delegar los elementos. Especifique la variable **[!UICONTROL Modelo de flujo de trabajo]** para delegar al usuario especificado. Puede seleccionar más de un modelo de flujo de trabajo.

   Además, para asignar todos los elementos, independientemente del modelo de flujo de trabajo, a un usuario en particular, seleccione **[!UICONTROL Todos los flujos de trabajo]** en la lista desplegable Modelo de flujo de trabajo . <br>

   Para asignar artículos a un usuario determinado para todos los modelos de flujo de trabajo excepto algunos, seleccione **[!UICONTROL Todos los flujos de trabajo]** en la lista desplegable Modelo de flujo de trabajo , pulse **[!UICONTROL + Agregar excepciones]**y especifique los modelos de flujo de trabajo que desea excluir.
   <br>

   Repita el paso para agregar más usuarios asignados. <br>

   >[!NOTE]
   >
   >El orden de los cesionarios es importante. Cuando se asigna un elemento a un usuario que ha habilitado la configuración de fuera de la oficina, el elemento se evalúa según la lista de usuarios asignados especificada en el orden en que se agregan los usuarios asignados. Cuando un elemento coincide con los criterios, se asigna al usuario asignado y el siguiente usuario asignado no se marca.

1. Toque **[!UICONTROL Guardar]**. La configuración se aplica en la fecha y hora de inicio especificadas. Si inicia sesión mientras está fuera de la oficina, no se le considerará en la oficina hasta que cambie su configuración.

Ahora, los elementos asignados a usted durante el período de tiempo fuera de la oficina se asignan automáticamente al usuario asignado especificado.
![Fuera de la oficina](assets/out-of-office.png)

>[!NOTE]
>
>(Solo para elementos de flujo de trabajo centrados en Forms) Active la variable **[!UICONTROL Permitir que el usuario asignado delegue mediante la configuración &quot;Fuera de la oficina&quot;]** de **[!UICONTROL Asignar tarea]** del flujo de trabajo. Solo se delegan a otros usuarios los elementos que tienen la opción mencionada habilitada.

## Restricciones     {#limitations}

* No se admite la asignación de elementos a un grupo.
* Actualmente no se admite la activación de Fuera de la oficina para tareas de proyecto.
