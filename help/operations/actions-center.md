---
title: Centro de acciones
description: Aproveche el Centro de Acciones para actuar convenientemente sobre incidentes y otra información importante
exl-id: d5a95ac4-aa88-44d5-ba02-7c9702050208
feature: Operations
role: Admin
source-git-commit: 821dd9f172ea286a7a3de74cf8dec8001e9afee9
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 47%

---

# Centro de acciones {#actions-center}

AEM as Cloud Service envía notificaciones al Centro de acciones por correo electrónico cuando se producen incidentes críticos que requieren una acción inmediata y recomendaciones proactivas para optimizaciones. Algunos ejemplos incluyen una cola bloqueada o un conjunto de credenciales que caducan; el conjunto completo de tipos de notificación el Centro de acciones se puede ver en la [tabla siguiente](#supported-notification-types), que se ampliará con el tiempo.

Cuando se recibe una notificación por correo electrónico del Centro de acciones, se puede hacer clic en ella para abrir el Centro de acciones de AEM as a Cloud Service, con una ventana emergente que muestra un contexto adicional que explica la acción que debe realizar un cliente.

Además de mostrar información sobre la notificación de correo electrónico a la que se acaba de hacer clic, el Centro de acciones sirve como un lugar centralizado en el que se pueden ver y administrar el conjunto de notificaciones actuales y antiguas. <!-- It can be accessed directly at the url TBD (Alexandru: I'm intentionally keeping it TBD for now so customers do not find it) -->

Existen dos categorías de notificaciones de alto nivel que aparecen en el Centro de acciones:

1. Incidencias operativas: se ha producido un evento, que generalmente requiere una solución rápida. Por ejemplo, resolver una cola bloqueada.
1. Recomendaciones proactivas: Adobe recomienda una acción que un cliente debe llevar a cabo en un futuro próximo. Por ejemplo, para dejar de hacer referencia a una IU obsoleta.

Consulte la [tabla siguiente](#supported-notification-types) para las notificaciones admitidas actualmente en el Centro de acciones.

Desde el Centro de acciones, puede seleccionar un programa y un entorno específicos que tengan el efecto de filtrar para ese ámbito.

## Configuración {#configuration}

Para configurar la recepción de notificaciones por correo electrónico del Centro de acciones, cree los perfiles de producto tal como se describe en [Perfiles de notificación](/help/journey-onboarding/notification-profiles.md), concretamente Notificación de incidentes - Cloud Service y Notificación proactiva - Cloud Service. Asigne también los ID de Adobe adecuados desde su organización a esos perfiles. Esto permite a un administrador determinar qué usuarios cumplen los requisitos para recibir estas notificaciones por correo electrónico.

>[!NOTE]
>Las notificaciones por correo electrónico del Centro de acciones funcionan a nivel de organización, por lo que los suscriptores recibirán notificaciones para todos los programas y entornos dentro de esos programas.

## Flujo de usuario detallado {#detailed-user-flow}

Al hacer clic en el correo electrónico, se le lleva al Centro de acciones, con una ventana emergente que muestra el contexto de la notificación en la que ha hecho clic y, en algunos casos, vínculos a información adicional que describe cómo realizar acciones correctivas. También puede acceder al Centro de acciones directamente en [https://experience.adobe.com/aem/actions-center](https://experience.adobe.com/aem/actions-center/), donde puede seleccionar el programa y el entorno relevantes.

![Detalles del problema](/help/operations/assets/incident-details.png)

Al hacer clic en el vínculo **Más información** se conduce al usuario a este artículo, donde el tipo de notificación se puede comprobar en la siguiente [tabla de tipos de notificaciones aceptadas](#supported-notification-types), que proporciona instrucciones sobre la acción realizar.

En el Centro de acciones, puede ver una lista de otras notificaciones recientes. Se recomienda que, en la lista Acciones, reconozca una notificación para indicar a Adobe que su organización está al tanto de la tarea y que luego la resuelva cuando se hayan adoptado medidas correctivas.

![Lista de notificaciones](/help/operations/assets/notification-list.png)

En la mayoría de los casos, la ventana emergente debe proporcionar todo el contexto necesario para resolver el problema. Sin embargo, si tiene preguntas sobre la asistencia de Adobe, puede hacer clic en el vínculo **Póngase en contacto con el servicio de asistencia** en la ventana emergente. Esto mostrará un formulario desde el cual puede describir la pregunta y enviarla para crear el ticket de Soporte, que también incluirá una referencia a la notificación específica para que un ingeniero de Soporte de Adobe tenga el contexto relevante.

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
| Estados de canalización de Cloud Manager | Información sobre el estado de sus canalizaciones | Usuario con roles de Propietario del negocio, Administrador de programa o Administrador de implementación, casilla &quot;Otros&quot; seleccionada en [Preferencias de Experience Cloud](https://experience.adobe.com/preferences), consulte [Notificaciones](/help/implementing/cloud-manager/notifications.md). |                           |

## Tipos de notificación compatibles {#supported-notification-types}

En la tabla siguiente se enumeran los tipos de notificación admitidos actualmente en el Centro de acciones. Actualmente, las notificaciones se limitan a entornos de producción.

| Tipo de notificación | Perfil de producto relacionado | Acción correctiva |
|---------------------------------|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Cola de replicación bloqueada | Problema | Desbloquear la cola siguiendo las instrucciones de la [Documentación de replicación](/help/operations/replication.md#troubleshooting) |
| Consulta GraphQL persistente no válida | Problema | Corrija la consulta de GraphQL no válida haciendo referencia a la [documentación de solución de problemas de consultas de GraphQL persistentes](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/headless/graphql-api/persisted-queries-troubleshoot.html) |
| Pico de tráfico en origen | Problema | Proteja su origen configurando reglas de filtro de tráfico de límite de velocidad que se aplican a umbrales más bajos que el pico de tráfico predeterminado en la alerta de déclencheur.  Consulte la sección [Bloqueo de ataques DoS y DDoS mediante reglas de tráfico](/help/security/traffic-filter-rules-including-waf.md#blocking-dos-and-ddos-attacks-using-traffic-filter-rules) de la documentación Reglas de filtro de tráfico, que hace referencia a un tutorial. |
| Reglas de filtros de tráfico de CDN activadas | Problema | Si la regla de filtro de tráfico coincidente refleja un ataque y el sitio no está bloqueando ese tráfico, proteja el sitio configurando una regla de filtro de tráfico en modo de bloqueo. Consulte la sección [Protección de sitios web con reglas de filtro de tráfico (incluidas las reglas de WAF)](/help/security/traffic-filter-rules-including-waf.md#tutorial-protecting-websites) de la documentación Reglas de filtro de tráfico, que hace referencia a un tutorial. |
| Errores de reenvío de registro de Splunk | Problema | Compruebe que el extremo de Splunk funcione y esté accesible desde el entorno de AEM Cloud Service. Para obtener más información sobre el reenvío de registros, visite la [documentación sobre el reenvío de registros de Splunk](/help/implementing/developing/introduction/logging.md#splunk-logs). Si necesita ayuda para solucionar problemas o necesita realizar cambios en la configuración de registro, genere un ticket de asistencia con Adobe. |
| Las páginas contienen un gran número de nodos | Proactivo | Reduzca el número total de nodos dentro de una página. Consulte [Documentación de complejidad de la página](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/pcx) | |
| Gran número de instancias de flujo de trabajo en ejecución | Proactivo | Finalice los flujos de trabajo en ejecución que ya no sean necesarios. Aprenda a [configurar un trabajo de depuración](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance) |               |
| Certificado S2S caducado | Proactivo | Obtenga información sobre cómo actualizar una credencial en la [documentación de Generación de tokens de acceso para las API del lado del servidor](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md#refresh-credentials) | Recuento alto de conexiones | Proactivo | Obtenga información acerca de la agrupación de conexiones en [agrupación de conexiones junto con la documentación de redes avanzadas](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking) |
| Asignación de usuarios de servicio obsoleta | Proactivo | Aprenda a utilizar el formato más reciente de asignación de usuarios de Sling Service, tal como se indica en [Prácticas recomendadas para la asignación de usuarios de Sling Service y la definición de usuario de servicio](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/best-practices-for-sling-service-user-mapping-and-service-user-definition) |
| Recuento alto de conexiones | Proactivo | Obtenga información acerca de la agrupación de conexiones en la [documentación de redes avanzadas](/help/security/configuring-advanced-networking.md#connection-pooling-advanced-networking) |  |
| Usuarios añadidos directamente al grupo personalizado | Proactivo | Los usuarios deben agregarse a los grupos de IMS relevantes y estos grupos de IMS deben agregarse como miembros de grupos de AEM. Alinear con [prácticas recomendadas de IMS](/help/security/ims-support.md) | |
| Contenido JCR faltante | Proactivo | Añada el nodo de contenido JCR que falta. Consulte [Documentación del validador de contenido de Assets](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | |
| Flujos de trabajo completados no depurados | Proactivo | Minimice el número de instancias del flujo de trabajo y mejore el rendimiento depurando las instancias del flujo de trabajo con más de 90 días de antigüedad. Aprenda a [configurar tareas de mantenimiento](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance) | |
| Falta el tipo de recurso de Sling en la página | Proactivo | Añada el nodo de tipo de recurso Sling que falta. Consulte [Documentación del validador de contenido de Assets](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | |
| Consulta lenta | Proactivo | Corrija las consultas lentas definiendo definiciones de índice correctas tal como sugiere la [hoja de trucos de consultas JCQ](https://experienceleague.adobe.com/docs/experience-manager-65/assets/JCR_query_cheatsheet-v1.1.pdf) | |
| Consulta sin índice | Proactivo | Evite ejecutar consultas que no utilicen un índice - [vínculo a la documentación de indización](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/operations/indexing) |