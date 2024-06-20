---
title: Centro de acciones
description: Aproveche el Centro de Acciones para actuar convenientemente sobre incidentes y otra información importante
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
feature: Operations
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 64%

---

# Centro de acciones {#actions-center}

AEM as Cloud Service envía notificaciones al Centro de acciones por correo electrónico cuando se producen incidentes críticos que requieren una acción inmediata y recomendaciones proactivas para optimizaciones. Algunos ejemplos incluyen una cola bloqueada o un conjunto de credenciales que caducan; el conjunto completo de tipos de notificación el Centro de acciones se puede ver en la [tabla siguiente](#supported-notification-types), que se ampliará con el tiempo.

AEM Cuando se recibe una notificación por correo electrónico del Centro de acciones, se puede hacer clic en ella para abrir el Centro de acciones de un as a Cloud Service, con una ventana emergente que muestra un contexto adicional que explica la acción que debe realizar un cliente.

Además de mostrar información sobre la notificación de correo electrónico a la que se acaba de hacer clic, el Centro de acciones sirve como un lugar centralizado en el que se pueden ver y administrar el conjunto de notificaciones actuales y antiguas. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

Existen dos categorías de notificaciones de alto nivel que aparecen en el Centro de acciones:

1. Incidencias operativas: se ha producido un evento, que generalmente requiere una solución rápida. Por ejemplo, resolver una cola bloqueada.
1. Recomendaciones proactivas: Adobe recomienda una acción que un cliente debe llevar a cabo en un futuro próximo. Por ejemplo, para dejar de hacer referencia a una IU obsoleta.

Consulte la [tabla siguiente](#supported-notification-types) para las notificaciones admitidas actualmente en el Centro de acciones.

Desde el Centro de acciones, puede seleccionar un programa y un entorno específicos que tengan el efecto de filtrar para ese ámbito.

## Configuración {#configuration}

Para configurar la recepción de notificaciones por correo electrónico del Centro de acciones, cree los perfiles de producto descritos [en este artículo](/help/journey-onboarding/notification-profiles.md), concretamente, Notificación de incidentes - Cloud Service y Notificación dinámica - Cloud Service. Asigne también los ID de Adobe adecuados desde su organización a esos perfiles. Esto permite a un administrador determinar qué usuarios cumplen los requisitos para recibir estas notificaciones por correo electrónico.

>[!NOTE]
>Las notificaciones por correo electrónico del Centro de acciones funcionan a nivel de organización, por lo que los suscriptores recibirán notificaciones para todos los programas y entornos dentro de esos programas.

## Flujo de usuario detallado {#detailed-user-flow}

Al hacer clic en el correo electrónico, se le lleva al Centro de acciones, con una ventana emergente que muestra el contexto de la notificación en la que ha hecho clic y, en algunos casos, vínculos a información adicional que describe cómo realizar acciones correctivas. También puede acceder al Centro de acciones directamente en [https://experience.adobe.com/aem/actions-center](https://experience.adobe.com/aem/actions-center/), donde puede seleccionar el programa y el entorno relevantes.

![Detalles del problema](/help/operations/assets/incident-details.png)

Al hacer clic en el vínculo **Más información** se conduce al usuario a este artículo, donde el tipo de notificación se puede comprobar en la siguiente [tabla de tipos de notificaciones aceptadas](#supported-notification-types), que proporciona instrucciones sobre la acción realizar.

En el Centro de acciones, puede ver una lista de otras notificaciones recientes. Se recomienda que, en la lista Acciones, reconozca una notificación para indicar a Adobe que su organización está al tanto de la tarea y que luego la resuelva cuando se hayan adoptado medidas correctivas.

![Lista de notificaciones](/help/operations/assets/notification-list.png)

En la mayoría de los casos, la ventana emergente debe proporcionar todo el contexto necesario para resolver el problema. Sin embargo, si tiene alguna duda sobre la asistencia de Adobe, puede hacer clic en el **Atención al cliente** en la ventana emergente. Esto mostrará un formulario desde el cual puede describir la pregunta y enviarla para crear el ticket de Soporte, que también incluirá una referencia a la notificación específica para que un ingeniero de Soporte de Adobe tenga el contexto relevante.

![Contacto con el soporte 1](/help/operations/assets/contact-support1.png)

![Contacto con el soporte 2](/help/operations/assets/contact-support2.png)

Al igual que todos los tickets de soporte, aparecerá en la [pestaña Casos de soporte de Adobe Admin Console](https://helpx.adobe.com/enterprise/using/support-for-enterprise.html?lang=es), donde podrá rastrearlo y agregar comentarios adicionales.

![Soporte de Admin Console](/help/operations/assets/admin-console-support.png)

## ¿Qué notificaciones aparecen? {#which-notification}

AEM as a Cloud Service tiene varios tipos de notificaciones, pero solo un subconjunto aparece en el Centro de acciones, tal y como se muestra en la siguiente tabla.

| Tipo de notificación | Descripción | Cómo configurar | Aparece en el Centro de acciones |
|---------------------------------|-----------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|
| Incidencias operativas | Incidentes críticos que requieren una acción inmediata | Usuario asignado al perfil de producto &quot;Notificación de problemas - Cloud Service&quot; | X |
| Recomendaciones proactivas | Optimizaciones que deben planificarse | Usuario asignado al perfil de producto “Notificación proactiva - Cloud Service” | X |
| Estados de canalización de Cloud Manager | Información sobre el estado de sus canalizaciones | Usuario con los roles de Propietario del negocio, Administrador de programa o Administrador de implementación, casilla de verificación &quot;Otros&quot; seleccionada en [Preferencias del Experience Cloud](https://experience.adobe.com/preferences), como [descrito aquí](/help/implementing/cloud-manager/notifications.md). |                           |

## Tipos de notificación compatibles {#supported-notification-types}

En la tabla siguiente se enumeran los tipos de notificación admitidos actualmente en el Centro de acciones. Actualmente, las notificaciones se limitan a entornos de producción.

| Tipo de notificación | Perfil de producto relacionado | Acción correctiva |
|---------------------------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cola de replicación bloqueada | Problema | Desbloquear la cola siguiendo las instrucciones de la [Documentación de replicación](/help/operations/replication.md#troubleshooting) |
| Consulta GraphQL persistente no válida | Problema | Corrija la consulta de GraphQL no válida haciendo referencia a la variable [Documentación de solución de problemas de consultas persistentes de GraphQL](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/persisted-queries-troubleshoot.html) |
| Pico de tráfico en origen | Problema | Protect define su origen mediante la configuración de reglas de filtro de tráfico de límite de velocidad que aplican umbrales inferiores a los del pico de tráfico predeterminado en la alerta de déclencheur.  Consulte la [Bloqueo de ataques DoS y DDoS mediante reglas de tráfico](/help/security/traffic-filter-rules-including-waf.md#blocking-dos-and-ddos-attacks-using-traffic-filter-rules) de la documentación de Reglas del filtro de tráfico, que hace referencia a un tutorial. |
| Certificado S2S caducado | Proactivo | Obtenga información sobre cómo actualizar una credencial en la [documentación de Generación de tokens de acceso para las API del lado del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) | Recuento alto de conexiones | Proactivo | Obtenga información acerca de la agrupación de conexiones en [Agrupación de conexiones junto con documentación de redes avanzadas](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking) |
| Asignación de usuarios de servicio obsoleta | Proactivo | Aprenda a utilizar el formato más reciente de asignación de usuarios de Sling Service, como se indica en [Prácticas recomendadas para la asignación de usuarios al servicio Sling y la definición de usuarios del servicio](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/best-practices-for-sling-service-user-mapping-and-service-user-definition) |
| Recuento alto de conexiones | Proactivo | Obtenga información acerca de la agrupación de conexiones en [Documentación de redes avanzadas](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking) |
