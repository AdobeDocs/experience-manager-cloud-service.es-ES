---
title: Centro de notificaciones
description: Aproveche el Centro de notificaciones para tomar medidas adecuadas sobre incidentes y otra información importante
hidefromtoc: true
source-git-commit: 55ecd685afa28226974f3415b550bd2e8d05e2e6
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 0%

---


# Centro de notificaciones {#notification-center}

>[!NOTE]
>Esta función no se ha lanzado.

Una vez configurada, AEM como Cloud Service envía notificaciones sobre información importante para la que los clientes deben actuar. Algunos ejemplos de notificaciones son una cola bloqueada o un conjunto de credenciales que caducan. El conjunto completo de tipos de notificación se puede ver en la [tabla siguiente](#current-notification-types), y se ampliará con el tiempo. Las notificaciones se reciben por correo electrónico y como una nueva entrada en el widget de notificaciones, al que se accede haciendo clic en el icono de campana en la esquina superior derecha de Adobe Experience Cloud. Se puede configurar la configuración de notificación.

Cuando se recibe una notificación, se puede hacer clic en ella para abrir AEM Centro de notificaciones del as a Cloud Service, con una ventana emergente que muestra un contexto adicional en el que se explica la acción recomendada para un cliente.

Además de mostrar información sobre la notificación en la que se acaba de hacer clic, el Centro de notificaciones sirve como centro central donde puede ver y administrar el conjunto de notificaciones actuales y anteriores. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Existen dos categorías de notificaciones de alto nivel:

1. Incidentes: se ha producido un evento, que generalmente requiere una resolución rápida. Por ejemplo, resolver una cola bloqueada
1. Proactivo : el Adobe recomienda una acción que un cliente debe llevar a cabo en un futuro próximo. Por ejemplo, para dejar de hacer referencia a una interfaz de usuario obsoleta.

Consulte la [tabla siguiente](#current-notification-types) para las notificaciones admitidas actualmente.

Desde la pantalla Centro de notificaciones, puede seleccionar un programa y un entorno específicos, que tiene el efecto de filtrar para ese ámbito.

## Configuración {#configuration}

Puede seguir los pasos a continuación para configurar la recepción de notificaciones:

1. Cree los siguientes perfiles de producto, tal como se describe [en este artículo](/help/journey-onboarding/notification-profiles.md), asignando los ID de Adobe correspondientes de su organización a esos perfiles.
1. Determine los ajustes de configuración de notificación. [En esta página](https://experience.adobe.com/preferences/notification-section), asegúrese de que la suscripción al Experience Manager esté habilitada y que la variable **Otros** está seleccionada. Además, se recomienda que la sección Correos electrónicos esté configurada como **Notificaciones instantáneas** por lo tanto, recibirá notificaciones inmediatamente después de que se produzca un incidente.

>[!NOTE]
>Las suscripciones funcionan a nivel de organización, por lo que los suscriptores recibirán notificaciones para todos los programas y entornos dentro de esos programas.

## Flujo de usuario detallado {#detailed-user-flow}

Al hacer clic en el correo electrónico, se le dirigirá al Centro de notificaciones, con una ventana emergente que muestra el contexto de la notificación en la que hizo clic y, en algunos casos, vínculos a información adicional que describe cómo realizar acciones correctivas.

![Detalles del incidente](/help/operations/assets/incident-details.png)

Al hacer clic en **Más información** navega del usuario a este artículo, donde se puede hacer referencia a la notificación en la siguiente tabla, que proporciona instrucciones sobre qué acción realizar.

En el Centro de notificaciones, puede ver una lista de otras notificaciones recientes. Se recomienda que, en la lista Acciones, reconozca una notificación para indicar al Adobe que su organización está al tanto de la tarea y que luego la resuelva cuando se hayan tomado medidas correctivas.

![Lista de notificaciones](/help/operations/assets/notification-list.png)

En la mayoría de los casos, la notificación debe proporcionar todo el contexto necesario para resolver el problema. Sin embargo, si tiene alguna duda sobre la compatibilidad con Adobe, puede hacer clic en la **Contacto con el servicio de asistencia** en la ventana emergente de notificación. Esto mostrará un formulario desde el cual puede describir la pregunta y enviarla para crear el ticket de soporte, que también incluirá una referencia a la notificación específica para que un ingeniero de soporte de Adobe tenga el contexto relevante.

![Contacto con el soporte técnico 1](/help/operations/assets/contact-support1.png)

![Contacto con el soporte técnico 2](/help/operations/assets/contact-support2.png)

Al igual que todos los tickets de asistencia técnica, aparecerán en la variable [Pestaña Casos de asistencia de Adobe Admin Console](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html), donde puede rastrearlo y agregar comentarios adicionales.

![Asistencia al Admin Console](/help/operations/assets/admin-console-support.png)

## Tipos de notificación actuales {#current-notification-types}

La tabla siguiente muestra los tipos de notificación admitidos actualmente

| Tipo de notificación | Perfil de producto relacionado | Acción correctiva |
|---|---|---|
| Cola de replicación bloqueada | Incidente | Desbloquear la cola siguiendo las instrucciones de [Documentación de replicación](/help/operations/replication.md#troubleshooting) |
| Certificado S2S caducado | Proactivo | Obtenga información sobre cómo actualizar una credencial en la variable [Generación de tokens de acceso para la documentación de las API del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |
