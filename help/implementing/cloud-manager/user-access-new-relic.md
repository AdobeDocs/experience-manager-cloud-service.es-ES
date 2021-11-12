---
title: Acceso del usuario a una nueva reliquia
description: Siga esta página para obtener más información sobre el nuevo Monitoreo del Rendimiento de las Aplicaciones Relic para AEM as a Cloud Service
source-git-commit: bb9532685c10baf13bc31898c0038fde2c5fd43d
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 0%

---


# Acceso del usuario a una nueva reliquia {#user-access}

## Introducción {#introduction}

El Adobe pone un alto énfasis en el monitoreo, disponibilidad y performance de su aplicación. Para ayudar a lograr este objetivo, AEM as a Cloud Service proporciona acceso a un grupo de supervisión personalizado de Nueva relación como parte de la oferta de productos estándar para garantizar que sus equipos tengan la máxima visibilidad de las métricas de rendimiento de entorno y del sistema de Cloud Service de Adobe Experience Manager. En esta sección se describen las nuevas funciones de monitorización de reliquia habilitadas en los entornos as a Cloud Service de AEM para ayudar a reforzar el rendimiento y permitirle sacar el máximo provecho de AEM as a Cloud Service.

## AEM supervisión as a Cloud Service de las transacciones mediante la nueva propuesta de valor - relación de calidad {#transaction-monitoring}

Aquí está el resumen de la propuesta de valor de New Relic Application Performance Monitoring para AEM as a Cloud Service:

* Acceso directo a una cuenta específica de New Relic One (acceso administrado por la asistencia técnica de Adobe).

* Agente de APM de nueva relación lógica instrumentado que muestra llamadas de método exactas con números de línea, incluidas dependencias externas y bases de datos.

* Optimización del rendimiento holístico mediante la combinación de métricas clave de la monitorización a nivel de infraestructura, así como la monitorización de aplicaciones (Adobe Experience Manager).

* Exposición de AEM as a Cloud Service Mbeans y Comprobaciones de estado de JMX directamente a las métricas de Nuevas perspectivas de reliquia, lo que permite realizar una inspección profunda del rendimiento de la pila de aplicaciones y las métricas de estado.

## Acceso a su cuenta de nueva reliquia as a Cloud Service AEM {#accessing-new-relic}

Su cuenta de New Relic dedicada se aprovisionará y administrará mediante Adobe mediante la participación del Servicio de atención al cliente. Adobe seguirá siendo el propietario y el administrador y proporcionará la cuenta en su nombre para proporcionar acceso a su subcuenta específica.

Para obtener acceso a su subcuenta de New Relic asociada con su Programa as a Cloud Service AEM:

* Abra una solicitud accediendo a la pestaña Asistencia del Admin Console.
* Asegúrese de que su ticket incluya los detalles de su ID de programa, así como la lista de usuarios a los que solicita a los equipos de Adobe que abran el acceso a Nueva relación.
* Todos los usuarios deben tener un nombre completo y una dirección de correo electrónico válida.

   >[!NOTE]
   >Consulte [Portal de asistencia AEM para Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) para obtener más información.

Una vez que se ha proporcionado el acceso, New Relic envía un correo electrónico de confirmación a cada usuario para que este pueda completar el proceso de configuración e iniciar sesión.

Si el usuario no encuentra el correo electrónico de confirmación de la cuenta original:

1. Vaya a la página de inicio de sesión de Nueva reliquia en [login.newrelic.com/login](https://login.newrelic.com/login).

1. Select **Olvidó su contraseña**.

   ![](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Escriba la dirección de correo electrónico de la cuenta y seleccione **Enviar mi vínculo de restablecimiento**.

   ![](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. Cuando el sistema de New Relic devuelva un mensaje de correo electrónico, seleccione el vínculo para confirmar de nuevo su cuenta.

   >[!NOTE]
   >Si no recibe un correo electrónico de New Relic:
   >Compruebe su [filtros de correo no deseado](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/). Si procede, [añadir nueva relación a la lista de permitidos de correo electrónico](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
   >Por favor, haga sus comentarios sobre el ticket de asistencia y nuestros equipos le ayudarán a continuar

1. Si completa el proceso de registro y no puede iniciar sesión en su cuenta debido a mensajes de error de correo electrónico o contraseña, registre un vale de asistencia a través de [Admin Console](https://adminconsole.adobe.com/).

### Verificación del correo electrónico {#verify-email}

Si se le pide que verifique su correo electrónico durante el inicio de sesión, significa que el correo electrónico está asociado con varias cuentas y se le dará la opción de verificar su correo electrónico durante el inicio de sesión. Esto le permitirá elegir a qué cuenta acceder. Si no verifica su dirección de correo electrónico, New Relic intentará iniciar sesión con el registro de usuario creado más recientemente y asociado a su dirección de correo electrónico. Para evitar verificar el correo electrónico durante cada inicio de sesión, haga clic en la casilla Recordarme en la pantalla de inicio de sesión.

Para obtener más ayuda, abra un ticket de asistencia a través de [Portal de asistencia AEM](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Excepciones {#exceptions}

AEM as a Cloud Service centra la oferta en torno a la solución New Relic APM únicamente y no proporciona soporte para las funciones de alerta, registro o integración de API.

Para obtener más ayuda o instrucciones adicionales sobre las nuevas ofertas de reliquia para su programa as a Cloud Service AEM, abra un ticket de asistencia a través de [Portal de asistencia AEM](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) para obtener ayuda.

## Preguntas más frecuentes sobre la nueva cuenta de reliquia {#faqs}

### ¿Qué monitoriza el Adobe con New Relic? {#adobe-monitor}

Adobe supervisa los servicios de Autor, Publicación y Vista previa (cuando están disponibles) as a Cloud Service de AEM mediante el complemento Java New Relic APM. El Adobe permite la telemetría y monitorización personalizada de la nueva relación costo-calidad de APM en entornos as a Cloud Service que no sean de producción y producción AEM. La cuenta de Nueva reliquia se adjunta a una cuenta de mantenimiento de Adobe principal y tiene varias aplicaciones que informan al respecto.

Tres cada uno por AEM entorno as a Cloud Service:

* Una aplicación para el servicio Author por entorno
* Una aplicación para el servicio Publicar por entorno (incluida la Publicación Dorada)
* Una aplicación para el servicio Vista previa por entorno
   >[!IMPORTANT]
   >Cada aplicación utiliza una clave de licencia, AEM los entornos as a Cloud Service solo informarán a una cuenta de New Relic. Las métricas y los eventos de monitorización completos para la Nueva Ric APM se conservan durante 7 días.

### ¿Quién puede acceder a los datos del nuevo Cloud Service de reliquia? {#access-new-relic-cloud}

Se concederá acceso de lectura completo para hasta 10 miembros de su equipo. El acceso de lectura incluirá todas las métricas de APM recopiladas por el agente de nueva relación.

### ¿Se admite la configuración SSO personalizada? {#custom-sso}

Actualmente, la configuración SSO personalizada no es compatible con la cuenta Nueva reliquia aprovisionada por Adobe.

### ¿Qué sucede si ya dispone de una nueva suscripción a reliquia local? {#new-relic-subscription}

La nueva plataforma de observabilidad de Nueva reliquia llamada Nueva reliquia uno permite a los Grupos de Soporte de Adobe y a sus equipos observar, monitorear y ver métricas y eventos, todo en un solo lugar. La nueva reliquia uno ofrece a los usuarios la capacidad de buscar en todas las cuentas donde tengan acceso y visualizar los datos de todos los servicios y hosts de una sola vista. Mientras que los equipos de soporte de Adobe supervisarán la aplicación as a Cloud Service AEM utilizando New Relic y otras herramientas internas como parte de su servicio, sus equipos pueden seguir aprovechando New Relic para servicios alojados e infraestructura locales. Podrán visualizar los datos desde las cuentas de Adobe y de Nueva reliquia gestionadas por el cliente.

>[!NOTE]
>El usuario debe tener los permisos adecuados y utilizar la misma metodología de inicio de sesión para ambas cuentas (Adobe y cuenta nueva relic administrada por el cliente).


