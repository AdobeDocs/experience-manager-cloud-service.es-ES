---
title: Centro de notificaciones
description: Aproveche el Centro de notificaciones para tomar medidas adecuadas sobre problemas y conocer otra información importante
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: 3aa753fb5cc5130ced7e9baafde63e8825394dce
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 35%

---

# Centro de notificaciones {#notification-center}

>[!NOTE]
>Esta función no se ha publicado.

AEM como Cloud Service envía notificaciones cuando se producen incidentes críticos que requieren una acción inmediata, así como recomendaciones proactivas para optimizaciones. Algunos ejemplos son una cola bloqueada o un conjunto de credenciales que caducan; el conjunto completo de tipos de notificación se puede ver en la [tabla siguiente](#supported-notification-types), que se expandirá con el tiempo.

Estas notificaciones se pueden configurar para recibirlas por correo electrónico y en el widget de notificaciones, al que se accede haciendo clic en el icono de campana situado en la esquina superior derecha de Adobe Experience Cloud.

Cuando se recibe una notificación, se puede hacer clic en ella para abrir AEM Centro de notificaciones del as a Cloud Service, con una ventana emergente que muestra un contexto adicional que explica la acción que debe realizar un cliente.

Además de mostrar información sobre la notificación en la que se acaba de hacer clic, el Centro de notificaciones sirve como centro central donde puede ver y administrar el conjunto de notificaciones actuales y anteriores. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers don't find it) -->

Existen dos categorías de notificaciones de alto nivel que aparecen en el Centro de notificaciones:

1. Incidentes operativos: se ha producido un evento, que generalmente requiere una rápida resolución. Por ejemplo, resolver una cola bloqueada.
1. Recomendaciones dinámicas : el Adobe recomienda una acción que un cliente debe llevar a cabo en un futuro próximo. Por ejemplo, para dejar de hacer referencia a una IU obsoleta.

Consulte la [tabla siguiente](#supported-notification-types) para las notificaciones admitidas actualmente.

Desde el Centro de notificaciones, puede seleccionar un programa y un entorno específicos, que tiene el efecto de filtrar para ese ámbito.

## Configuración {#configuration}

Siga los pasos a continuación para configurar la recepción de notificaciones:

1. Cree los siguientes perfiles de producto, tal como se describe [en este artículo](/help/journey-onboarding/notification-profiles.md), también asignando los ID de Adobe correspondientes de su organización a esos perfiles. Esto permite a un administrador determinar qué usuarios cumplen los requisitos para recibir estas notificaciones.
1. Cada usuario asignado asignado en el paso anterior puede configurar cómo desea recibir sus notificaciones. En el [página de preferencias del Experience Cloud](https://experience.adobe.com/preferences/notification-section), asegúrese de que la suscripción del Experience Manager esté habilitada y la variable **Incidentes operativos** y **Recomendaciones dinámicas** las casillas de verificación están seleccionadas para las columnas de correo electrónico y en la aplicación (consulte la imagen siguiente). Además, se recomienda que la sección Correos electrónicos esté configurada como **Notificaciones instantáneas** por lo tanto, las notificaciones se reciben inmediatamente cuando se produce un incidente.

![Configurar suscripciones](/help/operations/assets/configure-subscriptions.png)

>[!NOTE]
>Las notificaciones funcionan a nivel de organización, por lo que los suscriptores recibirán notificaciones para todos los programas y entornos dentro de esos programas.

## Flujo de usuario detallado {#detailed-user-flow}

Al hacer clic en el correo electrónico, se le dirigirá al Centro de notificaciones, y la ventana emergente muestra el contexto de la notificación en la que hizo clic y, en algunos casos, vínculos a información adicional que describe cómo realizar acciones correctivas.

![Detalles del problema](/help/operations/assets/incident-details.png)

Al hacer clic en el enlace **Más información** se le conduce al usuario a este artículo, donde se puede hacer referencia a la notificación en la siguiente tabla, que proporciona instrucciones sobre qué acción realizar.

En el Centro de notificaciones, puede ver una lista de otras notificaciones recientes. Se recomienda que, en la lista Acciones, reconozca una notificación para indicar al Adobe que su organización está al tanto de la tarea y que luego la resuelva cuando se hayan adoptado medidas correctivas.

![Lista de notificaciones](/help/operations/assets/notification-list.png)

En la mayoría de los casos, la notificación debe proporcionar todo el contexto necesario para resolver el problema. Sin embargo, si tiene preguntas para el Soporte de Adobe, puede hacer clic en el enlace **Contactar con Soporte** en la ventana emergente de notificación. Esto mostrará un formulario desde el cual puede describir la pregunta y enviarla para crear el ticket de soporte, que también incluirá una referencia a la notificación específica para que un ingeniero de soporte de Adobe tenga el contexto relevante.

![Contacto con el soporte 1](/help/operations/assets/contact-support1.png)

![Contacto con el soporte 2](/help/operations/assets/contact-support2.png)

Al igual que todos los tickets de soporte, aparecerá en la [pestaña Casos de soporte de Adobe Admin Console](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html?lang=es), donde podrá rastrearlo y agregar comentarios adicionales.

![Soporte de Admin Console](/help/operations/assets/admin-console-support.png)

## ¿Qué notificaciones aparecen? {#which-notification}

AEM as a Cloud Service tiene varios tipos de notificaciones, pero solo un subconjunto aparece en el Centro de notificaciones, como se ilustra en la tabla siguiente.

| Tipo de notificación | Descripción | Configuración | Aparece en el Centro de notificaciones |
|---|---|---|---|
| Incidentes operativos | Incidentes críticos que requieren una acción inmediata | El usuario asignado al perfil de producto &quot;Notificación de incidentes - Cloud Service&quot;, casilla &quot;Incidentes operativos&quot; seleccionada en [Preferencias de Experience Cloud](https://experience.adobe.com/preferences) | X |
| Recomendaciones dinámicas | Optimizaciones que deben planificarse | Usuario asignado al perfil de producto &quot;Notificación proactiva - Cloud Service&quot;, casilla de verificación &quot;Recomendaciones proactivas&quot; seleccionada en [Preferencias de Experience Cloud](https://experience.adobe.com/preferences) | X |
| Estados de canalización de Cloud Manager | Información sobre el estado de sus canalizaciones | Usuario con las funciones Propietario empresarial, Administrador de programas o Administrador de implementación, casilla &quot;Otros&quot; seleccionada en [Preferencias de Experience Cloud](https://experience.adobe.com/preferences) |  |

## Tipos de notificación compatibles {#supported-notification-types}

La siguiente tabla enumera los tipos de notificación admitidos actualmente.

| Tipo de notificación | Perfil de producto relacionado | Acción correctiva |
|---|---|---|
| Cola de replicación bloqueada | Problema | Desbloquear la cola siguiendo las instrucciones de la [Documentación de replicación](/help/operations/replication.md#troubleshooting) |
| Certificado S2S caducado | Proactivo | Obtenga información sobre cómo actualizar una credencial en la [documentación de Generación de tokens de acceso para las API del lado del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |

