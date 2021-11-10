---
title: Acceso del usuario a una nueva reliquia
description: Acceso del usuario a una nueva reliquia
index: false
hide: true
source-git-commit: e8f5a0ca99b3772665613e24b73d4ab7525a22be
workflow-type: tm+mt
source-wordcount: '981'
ht-degree: 0%

---


# Nueva APM de reliquia para AEM as a Cloud Service {#new-relic}

## Introducción {#introduction}

El Adobe pone un alto énfasis en el monitoreo, disponibilidad y performance de su aplicación. Para ayudar a lograr este objetivo, AEM as a Cloud Service proporciona acceso a un grupo de supervisión personalizado de Nueva relación como parte de la oferta de productos estándar para garantizar que sus equipos tengan la máxima visibilidad de las métricas de rendimiento de entorno y del sistema de Cloud Service de Adobe Experience Manager. En este documento técnico se describen las funciones de monitorización de Nuevas reliquias habilitadas en los entornos as a Cloud Service de AEM para ayudar a reforzar el rendimiento y permitirle sacar el máximo provecho de AEM as a Cloud Service.

## AEM Supervisión as a Cloud Service de Transacciones a través de New Relic {#transaction-monitoring}

* Acceso directo a una cuenta específica de New Relic One (acceso administrado por la asistencia técnica de Adobe).

* Agente de APM de nueva relación lógica instrumentado que muestra llamadas de método exactas con números de línea, incluidas dependencias externas y bases de datos.

* Optimización del rendimiento holístico mediante la combinación de métricas clave de la monitorización a nivel de infraestructura, así como la monitorización de aplicaciones (Adobe Experience Manager).

* Exposición de AEM as a Cloud Service Mbeans y Comprobaciones de estado de JMX directamente a las métricas de Nuevas perspectivas de reliquia, lo que permite realizar una inspección profunda del rendimiento de la pila de aplicaciones y las métricas de estado.

## Acceso a su cuenta de nueva reliquia as a Cloud Service AEM {#accessing-new-relic}

Su cuenta de New Relic dedicada se aprovisionará y administrará mediante Adobe mediante la participación del Servicio de atención al cliente. Adobe seguirá siendo el propietario y el administrador y proporcionará la cuenta en su nombre para proporcionar acceso a su subcuenta específica.

Para obtener acceso a su subcuenta de Nueva reliquia asociada con su Programa as a Cloud Service AEM, abra una solicitud accediendo a la pestaña Asistencia en el Admin Console. Asegúrese de que su ticket incluya los detalles de su ID de programa, así como la lista de usuarios a los que solicita a los equipos de Adobe que abran el acceso a Nueva relación. Todos los usuarios deben tener un nombre completo y una dirección de correo electrónico válida.  Para obtener más información sobre AEM Portal de asistencia técnica, consulte Asistencia para el Experience Cloud.

Una vez que se ha proporcionado el acceso, New Relic envía un correo electrónico de confirmación a cada usuario para que pueda completar el proceso de configuración e iniciar sesión. Si no encuentran el correo electrónico de confirmación de la cuenta original:

1. Vaya a la página de inicio de sesión de New Relic en login.newrelic.com/login.

1. Seleccione Olvidó su contraseña.

1. Escriba la dirección de correo electrónico de la cuenta y seleccione Enviar mi contraseña.

1. Cuando el sistema de New Relic devuelva un mensaje de correo electrónico, seleccione el vínculo para confirmar de nuevo su cuenta.

   >[!NOTE]
   >Si no recibe un correo electrónico de New Relic:
   >Compruebe los filtros de correo no deseado. Si corresponde, agregue Nueva relación a la lista de permitidos de correo electrónico.
   >Por favor, haga sus comentarios sobre el ticket de asistencia y nuestros equipos le ayudarán a continuar

1. Si completa el proceso de suscripción y no puede iniciar sesión en su cuenta debido a mensajes de error de correo electrónico o contraseña, consiga un ticket de asistencia a través del Admin Console.

Si se le pide que verifique su correo electrónico durante el inicio de sesión, significa que el correo electrónico está asociado con varias cuentas y se le dará la opción de verificar su correo electrónico durante el inicio de sesión. Esto le permitirá elegir a qué cuenta acceder. Si no verifica su dirección de correo electrónico, New Relic intentará iniciar sesión con el registro de usuario creado más recientemente y asociado a su dirección de correo electrónico. Para evitar verificar el correo electrónico durante cada inicio de sesión, haga clic en la casilla Recordarme en la pantalla de inicio de sesión.

Para obtener más ayuda, abra un ticket de asistencia a través AEM Portal de asistencia.

## Excepciones {#exceptions}

AEM as a Cloud Service centra la oferta en torno a la solución New Relic APM únicamente y no proporciona soporte para las funciones de alerta, registro o integración de API.

Para obtener más ayuda o sugerencias adicionales sobre las ofertas de Nueva reliquia para su Programa as a Cloud Service AEM, abra un ticket de asistencia a través de AEM Portal de Soporte para obtener ayuda.

## Preguntas más frecuentes sobre la nueva cuenta de reliquia {#faqs}

### ¿Qué monitoriza el Adobe con New Relic? {#adobe-monitor}

Adobe supervisa los servicios de Autor, Publicación y Vista previa (cuando están disponibles) as a Cloud Service de AEM mediante el complemento Java New Relic APM. El Adobe permite la telemetría y monitorización personalizada de la nueva relación costo-calidad de APM en entornos as a Cloud Service que no sean de producción y producción AEM. La cuenta de Nueva reliquia se adjunta a una cuenta de mantenimiento de Adobe principal y tiene varias aplicaciones que informan al respecto. Tres cada uno por AEM entorno as a Cloud Service:

Una aplicación para el servicio Autor por entorno Una aplicación para el servicio Publicación por entorno (incluida la Publicación Dorada) Una aplicación para el servicio de Vista previa por entorno Cada aplicación utiliza una clave de licencia, AEM los entornos as a Cloud Service solo informarán a una cuenta de Nueva relación. Las métricas y los eventos de monitorización completos para la Nueva APM de Reliquia y la Infraestructura se conservan durante 7 días.

### ¿Quién puede acceder a los datos del nuevo Cloud Service de reliquia? {#access-new-relic-cloud}

Se concederá acceso de lectura completo para hasta 10 miembros de su equipo. El acceso de lectura incluirá todas las métricas de APM recopiladas por el agente de nueva relación.

### ¿Se admite la configuración SSO personalizada? {#custom-sso}

Actualmente, la configuración SSO personalizada no es compatible con la cuenta Nueva reliquia aprovisionada por Adobe.

### ¿Qué sucede si ya dispone de una nueva suscripción a reliquia local? {#new-relic-subscription}

La nueva plataforma de observabilidad de Nueva reliquia llamada Nueva reliquia uno permite a los Grupos de Soporte de Adobe y a sus equipos observar, monitorear y ver métricas y eventos, todo en un solo lugar. La nueva reliquia uno ofrece a los usuarios la capacidad de buscar en todas las cuentas donde tengan acceso y visualizar los datos de todos los servicios y hosts de una sola vista. Mientras que los equipos de soporte de Adobe supervisarán la aplicación as a Cloud Service AEM utilizando New Relic y otras herramientas internas como parte de su servicio, sus equipos pueden seguir aprovechando New Relic para servicios alojados e infraestructura locales. Podrán visualizar los datos desde las cuentas de Adobe y de Nueva reliquia gestionadas por el cliente.

>[!NOTE]
>El usuario debe tener los permisos adecuados y utilizar la misma metodología de inicio de sesión para ambas cuentas (Adobe y cuenta nueva relic administrada por el cliente).


