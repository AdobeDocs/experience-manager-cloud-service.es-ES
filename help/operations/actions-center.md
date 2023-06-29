---
title: Centro de acciones
description: Aproveche el Centro de Acciones para tomar medidas sobre incidentes y otra información importante
hidefromtoc: true
hide: true
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 27%

---

# Centro de acciones {#actions-center}

>[!NOTE]
>Esta función no se ha publicado.

AEM El Cloud Service de as envía notificaciones por correo electrónico al Centro de acciones cuando se producen incidentes críticos que requieren una acción inmediata y recomendaciones proactivas para las optimizaciones. Algunos ejemplos son una cola bloqueada o un conjunto de credenciales que caduca; el conjunto completo de tipos de notificación del Centro de acciones se puede ver en la [tabla siguiente](#supported-notification-types), que se ampliará con el tiempo.

AEM Cuando se recibe una notificación por correo electrónico del Centro de acciones, se puede hacer clic en ella para abrir el Centro de acciones de un as a Cloud Service, con una ventana emergente que muestra un contexto adicional que explica la acción que debe realizar un cliente.

Además de mostrar información sobre la notificación por correo electrónico en la que se acaba de hacer clic, el Centro de acciones sirve como centro en el que puede ver y administrar el conjunto de notificaciones actuales y anteriores. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

Existen dos categorías superiores de notificaciones que aparecen en el Centro de acciones:

1. Incidencias operativas: se ha producido un evento, que generalmente requiere una solución rápida. Por ejemplo, resolver una cola bloqueada.
1. Recomendaciones proactivas: Adobe recomienda una acción que un cliente debe llevar a cabo en un futuro próximo. Por ejemplo, para dejar de hacer referencia a una IU obsoleta.

Consulte la [tabla siguiente](#supported-notification-types) para las notificaciones admitidas actualmente en el Centro de acciones.

Desde el Centro de acciones, puede seleccionar un programa y un entorno específicos, lo que tiene el efecto de filtrar para ese ámbito.

## Configuración {#configuration}

Para configurar la recepción de notificaciones por correo electrónico del Centro de acciones, cree los perfiles de producto descritos [en este artículo](/help/journey-onboarding/notification-profiles.md), concretamente, Notificación de incidentes - Cloud Service y Notificación dinámica - Cloud Service. Asigne también los ID de Adobe adecuados de su organización a esos perfiles. Esto permite a un administrador determinar qué usuarios cumplen los requisitos para recibir estas notificaciones por correo electrónico.

>[!NOTE]
>Las notificaciones por correo electrónico del Centro de acciones funcionan en el nivel de organización, por lo que los suscriptores recibirán notificaciones para todos los programas y entornos dentro de esos programas.

## Flujo de usuario detallado {#detailed-user-flow}

Al hacer clic en el correo electrónico, se le lleva al Centro de acciones, con una ventana emergente que muestra el contexto de la notificación en la que ha hecho clic y, en algunos casos, vínculos a información adicional que describe cómo realizar acciones correctivas.

![Detalles del problema](/help/operations/assets/incident-details.png)

Haciendo clic en **Más información** El vínculo lleva al usuario a este artículo, donde se puede hacer referencia al tipo de notificación en la [tabla de tipos de notificación admitidos](#supported-notification-types) a continuación, que proporciona orientación sobre qué acción tomar.

En el Centro de acciones, puede ver una lista de otras notificaciones recientes. Se recomienda que, mediante la lista Acciones, acepte una notificación para indicar al Adobe que su organización conoce la tarea y que, posteriormente, la resuelva cuando se hayan tomado medidas correctivas.

![Lista de notificaciones](/help/operations/assets/notification-list.png)

En la mayoría de los casos, la ventana emergente debe proporcionar todo el contexto necesario para resolver el problema. Sin embargo, si tiene alguna duda sobre la asistencia de Adobe, puede hacer clic en el **Atención al cliente** en la ventana emergente. De este modo, aparece un formulario desde el que puede describir la pregunta y enviarla para crear un vale de soporte, que también incluye una referencia a la notificación específica de modo que un ingeniero de soporte técnico de Adobe tenga el contexto relevante.

![Contacto con el soporte 1](/help/operations/assets/contact-support1.png)

![Contacto con el soporte 2](/help/operations/assets/contact-support2.png)

Al igual que todos los tickets de soporte, aparecerá en la [pestaña Casos de soporte de Adobe Admin Console](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html?lang=es), donde podrá rastrearlo y agregar comentarios adicionales.

![Soporte de Admin Console](/help/operations/assets/admin-console-support.png)

## ¿Qué notificaciones aparecen? {#which-notification}

AEM El as a Cloud Service tiene varios tipos de notificaciones, pero solo aparece un subconjunto en el Centro de acciones, como se muestra en la tabla siguiente.

| Tipo de notificación | Descripción | Cómo configurar  | Aparece en el Centro de acciones |
|---|---|---|---|
| Incidencias operativas | Incidentes críticos que requieren una acción inmediata | Usuario asignado al perfil de producto &quot;Notificación de incidentes - Cloud Service&quot; | X |
| Recomendaciones proactivas | Optimizaciones que deben planificarse | Usuario asignado al perfil de producto &quot;Notificación proactiva: Cloud Service&quot; | X |
| Estados de canalización de Cloud Manager | Información sobre el estado de sus canalizaciones | Usuario con las funciones de Propietario empresarial, Administrador de programas o Administrador de implementación, casilla de verificación &quot;Otros&quot; seleccionada en las [Preferencias de Experience Cloud](https://experience.adobe.com/preferences), como [descrito aquí](/help/implementing/cloud-manager/notifications.md). |   |

## Tipos de notificación compatibles {#supported-notification-types}

En la tabla siguiente se enumeran los tipos de notificación admitidos actualmente en el Centro de acciones.

| Tipo de notificación | Perfil de producto relacionado | Acción correctiva |
|---|---|---|
| Cola de replicación bloqueada | Problema | Desbloquear la cola siguiendo las instrucciones de la [Documentación de replicación](/help/operations/replication.md#troubleshooting) |
| Certificado S2S caducado | Proactivo | Obtenga información sobre cómo actualizar una credencial en la [documentación de Generación de tokens de acceso para las API del lado del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) |

