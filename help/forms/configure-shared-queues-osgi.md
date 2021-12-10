---
title: Configuración de colas compartidas
seo-title: Configure shared queues
description: Aprenda a utilizar colas compartidas para flujos de trabajo centrados en Forms en [!DNL AEM Forms] en OSGi.
seo-description: Learn how to use shared queues for Forms-centric workflows on [!DNL AEM Forms] on OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 1%

---


# Compartir y solicitar acceso a los elementos de la bandeja de entrada de un usuario {#share-and-request-access}

Una cola es una lista de elementos de AEM bandeja de entrada de un usuario. Pueden ser elementos asignados a un usuario o elementos compartidos al grupo al que pertenece un usuario. Puede acceder a la Bandeja de entrada para ver y realizar acciones en el elemento Bandeja de entrada. Por ejemplo, comparta un elemento con otro usuario.

También puede compartir los elementos de la Bandeja de entrada con otro usuario. Una vez que otro usuario tiene acceso a los elementos de la Bandeja de entrada, el usuario puede reclamar y tomar las medidas adecuadas sobre los elementos compartidos. Del mismo modo, puede solicitar acceso a los elementos de la Bandeja de entrada a otros usuarios.

## Requisitos previos {#pre-requisites}

El usuario que ha iniciado sesión debe ser miembro de la [!DNL `workflow-users`] grupo. El usuario puede compartir elementos o solicitar acceso a elementos solo de los usuarios en los que el usuario que ha iniciado sesión tenga permisos de lectura o solo de los usuarios que han habilitado el perfil público.

## Compartir uno o todos los elementos de la bandeja de entrada con otro usuario

AEM bandeja de entrada permite compartir un solo elemento o todos los elementos de la bandeja de entrada con otro usuario.

### Compartir todos los elementos de la bandeja de entrada

Siga estos pasos para compartir todos los elementos de una bandeja de entrada con otro usuario:

1. Inicie sesión en la instancia de AEM. Toque . ![Bandeja de entrada](assets/bell.svg) icono y toque **[!UICONTROL Ver todo]**. Aparecerá una lista de los elementos de la bandeja de entrada.
1. Toque . ![Selector de vista](assets/viewlist.svg) o ![Selector de vista](assets/calendar.svg) junto al icono **[!UICONTROL Crear]** pulse **[!UICONTROL Configuración]**. Aparecerá el cuadro de diálogo de configuración.
1. Abra el **[!UICONTROL Compartir]** en el cuadro de diálogo configuración.
1. Introduzca el nombre de un usuario en la **[!UICONTROL Conceder acceso a los elementos de la bandeja de entrada]** cuadro de texto y toque **[!UICONTROL Concesión]**. Repita el paso para agregar más usuarios. Todos los usuarios con acceso a sus elementos aparecen en la sección **Nombre de usuario** para obtener más información.
1. Toque **[!UICONTROL Guardar]**.

>[!NOTE]
>
>(Solo para elementos de flujo de trabajo centrados en Forms) Active la variable **[Permitir que el usuario asignado comparta a través del uso compartido de la bandeja de entrada](aem-forms-workflow-step-reference.md)** de **Asignar tarea** del flujo de trabajo. Solo se muestran a los demás usuarios los elementos que tienen la opción mencionada habilitada.

### Compartir elementos individuales

Realice los siguientes pasos para compartir un elemento de la Bandeja de entrada con otro usuario:

1. Inicie sesión en la instancia de AEM. Toque . ![Bandeja de entrada](assets/bell.svg) icono y toque **[!UICONTROL Ver todo]**. Aparecerá una lista de los elementos de la bandeja de entrada.
1. Seleccionar un elemento y tocar **[!UICONTROL Compartir]**. Aparecerá un cuadro de diálogo.
1. Escriba el nombre de un usuario en el cuadro de texto Agregar usuarios para compartir este elemento y pulse **[!UICONTROL Agregar]**. Repita el paso para agregar más usuarios. Todos los usuarios con acceso a sus elementos aparecen en la sección **[!UICONTROL Nombre de usuario]** para obtener más información.
1. Toque **[!UICONTROL Guardar]**.


>[!NOTE]
>
>(Solo para elementos de flujo de trabajo centrados en Forms) Active la variable **[Permitir que el usuario asignado comparta explícitamente en la bandeja de entrada](aem-forms-workflow-step-reference.md)** de **Asignar tarea** del flujo de trabajo. Solo se muestran a los demás usuarios los elementos que tienen la opción mencionada habilitada.

## Solicitar acceso a los elementos de la bandeja de entrada {#request-access}

Puede solicitar acceso a los elementos de la Bandeja de entrada de otro usuario. Una vez concedido el acceso, puede ver, reclamar y tomar las medidas adecuadas sobre los artículos compartidos. Realice los siguientes pasos para solicitar acceso a los elementos de la Bandeja de entrada de otro usuario:

1. Inicie sesión en la instancia de AEM. Toque . ![Selector de vista](assets/bell.svg) icono y toque **[!UICONTROL Ver todo]**.
1. Toque . ![Selector de vista](assets/viewlist.svg) o ![Selector de vista](assets/calendar.svg) junto al icono **[!UICONTROL Crear]** pulse **[!UICONTROL Configuración]**. Aparecerá el cuadro de diálogo de configuración.
1. Introduzca el nombre de un usuario en la **[!UICONTROL Solicitar acceso a los elementos de la bandeja de entrada del usuario]** cuadro de texto y toque **[!UICONTROL Solicitud]**. Se envía una solicitud al usuario y el estado de la misma se muestra contra el nombre del usuario. Repita el paso para agregar más usuarios.
1. Toque **[!UICONTROL Guardar]**. La solicitud se envía como un elemento de la Bandeja de entrada a los usuarios. El usuario puede seleccionar el elemento y pulsar Aprobar o Rechazar para conceder o rechazar el acceso.


## Reclamar elementos compartidos por otros usuarios {#claim-items}

Solo puede empezar a trabajar en un elemento compartido después de reclamarlo. Evita que varios usuarios trabajen en un solo elemento. Realice los siguientes pasos para reclamar un artículo:

1. Inicie sesión en la instancia de AEM. Puntee en la bandeja de entrada ![Bandeja de entrada](assets/bell.svg) icono y toque **[!UICONTROL Ver todo]**.
1. Toque . ![Solo contenido](assets/railleft.svg) para abrir el selector de filtros.
1. Toque . **[!UICONTROL Seleccionar usuario asignado]** para ver y seleccionar usuarios que han compartido sus elementos de la Bandeja de entrada con usted.
1. Seleccionar un elemento y tocar **[!UICONTROL Reclamación]**. El elemento se agrega a la bandeja de entrada.

## Liberar artículos reclamados {#release-items}

Solo puede trabajar en un elemento compartido después de reclamarlo. Otros usuarios no pueden ver ni trabajar en artículos que usted ha reclamado. Si no puede continuar trabajando en un elemento, puede liberarlo de nuevo en el grupo.   Una vez liberado el artículo, otros usuarios pueden reclamarlo y trabajar con él:

Realice los siguientes pasos para liberar un elemento:

1. Inicie sesión en la instancia de AEM. Puntee en la bandeja de entrada ![Bandeja de entrada](assets/bell.svg) icono y toque **[!UICONTROL Ver todo]**. Aparecerá una lista de los elementos de la bandeja de entrada.
1. Seleccione el elemento que desea liberar y toque **[!UICONTROL Reclamar]**. El elemento se vuelve a agregar al grupo. Otros ahora pueden reclamar el artículo.

## Restricciones     {#limitations}

* No se admite el uso compartido de elementos con un grupo.
* No se admite el uso compartido de tareas de proyecto.
