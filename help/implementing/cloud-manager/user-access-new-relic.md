---
title: Nueva reliquia uno
description: Obtenga información sobre el servicio de supervisión del rendimiento de la aplicación (APM) de New Relic One para AEM as a Cloud Service y cómo puede acceder a él.
exl-id: 9fa0c5eb-415d-4e56-8136-203d59be927e
source-git-commit: 6cf164093cc543fe4847859b248e70efd86efbb1
workflow-type: tm+mt
source-wordcount: '1038'
ht-degree: 2%

---


# Nueva reliquia uno {#user-access}

Obtenga información sobre el servicio de supervisión del rendimiento de la aplicación (APM) de New Relic One para AEM as a Cloud Service y cómo puede acceder a él.

## Introducción {#introduction}

El Adobe pone un bueno énfasis en el monitoreo, la disponibilidad y el performance de su aplicación. Para ayudar a lograr este objetivo, AEM as a Cloud Service proporciona acceso a un grupo de supervisión personalizado de Nueva relación uno como parte de la oferta de productos estándar para garantizar que sus equipos tengan la máxima visibilidad de sus métricas de rendimiento de entorno y sistema as a Cloud Service AEM.

En este documento se describen las funciones de supervisión del rendimiento de la aplicación (APM) de la nueva relación relic-uno habilitadas en los entornos as a Cloud Service AEM para ayudarle a soportar el rendimiento y permitirle sacar el máximo provecho de AEM as a Cloud Service.

## Características {#transaction-monitoring}

Nueva reliquia Una APM para AEM as a Cloud Service tiene muchas características.

* Acceso directo a una cuenta específica de New Relic One (acceso administrado por la asistencia de Adobe)

* Agente de nueva relación con la aplicación instrumentada Un APM que muestra llamadas de método exactas con números de línea, incluidas dependencias externas y bases de datos

* Optimización del rendimiento holístico mediante la combinación de métricas clave de la monitorización a nivel de infraestructura y la monitorización de aplicaciones (Adobe Experience Manager)

* Exposición de AEM as a Cloud Service mazones de JMX y comprobaciones de estado directamente dentro de las métricas de New Relic Insights, lo que permite una inspección profunda del rendimiento de la pila de aplicaciones y las métricas de estado.

## Acceso a la nueva reliquia uno {#accessing-new-relic}

Siga estos pasos para obtener acceso a su nueva subcuenta de Relic One asociada a su Programa as a Cloud Service AEM.

1. Abra una solicitud accediendo a la pestaña Asistencia del Admin Console.
1. En su solicitud, incluya los detalles de su ID de programa, así como la lista de usuarios que requieren acceso a Nueva reliquia.
   * Se deben proporcionar los nombres completos y las direcciones de correo electrónico válidas de todos los usuarios.

Consulte el documento [Portal de asistencia AEM para Experience Cloud](https://helpx.adobe.com/es/enterprise/using/support-for-experience-cloud.html) para obtener más información sobre cómo abrir tickets.

Una vez que se ha proporcionado el acceso, New Relic envía un correo electrónico de confirmación a cada usuario para que este pueda completar el proceso de configuración e iniciar sesión.

Si el usuario no encuentra el correo electrónico de confirmación de la cuenta original, siga estos pasos.

1. Vaya a la página de inicio de sesión de Nueva reliquia en [`login.newrelic.com/login`](https://login.newrelic.com/login).

1. Select **¿Olvidó su contraseña?**.

   ![Nuevo inicio de sesión de Relic](/help/implementing/cloud-manager/assets/new-relic/newrelic-1.png)

1. Escriba la dirección de correo electrónico de la cuenta y seleccione **Enviar mi vínculo de restablecimiento**.

   ![Escriba la dirección de correo electrónico](/help/implementing/cloud-manager/assets/new-relic/newrelic-2.png)

1. New Relic enviará al usuario un correo electrónico que contiene un vínculo para confirmar la cuenta.

Si completa el proceso de registro y no puede iniciar sesión en su cuenta debido a mensajes de error de correo electrónico o contraseña, registre un ticket de asistencia a través de la [Admin Console](https://adminconsole.adobe.com/).

>[!TIP]
>
>Si no recibe un correo electrónico de New Relic:
>
>* Compruebe su [filtros de correo no deseado](https://docs.newrelic.com/docs/accounts/accounts-billing/account-setup/create-your-new-relic-account/).
>* Si procede, [añadir nueva relación a la lista de permitidos de correo electrónico](https://docs.newrelic.com/docs/accounts/accounts/account-maintenance/account-email-settings/#email-whitelist).
>* Si ninguna de estas sugerencias ayuda, sírvase proporcionar comentarios sobre el ticket de asistencia y el equipo de soporte de Adobe le ayudará a obtener más información.


### Verificación del correo electrónico {#verify-email}

Si se le pide que verifique su correo electrónico durante el inicio de sesión, significa que el correo electrónico está asociado con varias cuentas. Esto le permite elegir a qué cuenta acceder.

Si no verifica su dirección de correo electrónico, New Relic intentará iniciar sesión con el registro de usuario creado más recientemente y asociado a su dirección de correo electrónico. Para evitar verificar el correo electrónico durante cada inicio de sesión, haga clic en el botón **Recordarme** en la pantalla de inicio de sesión.

Para obtener más ayuda, abra un ticket de asistencia a través de la [Portal de asistencia AEM](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Excepciones {#exceptions}

AEM as a Cloud Service solo ofrece la solución New Relic One APM y no proporciona soporte para alertas, registros o integraciones de API.

Para obtener más ayuda o instrucciones adicionales sobre las nuevas ofertas de Relic Uno para su Programa as a Cloud Service AEM, abra un ticket de asistencia a través de la [Portal de asistencia AEM](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html).

## Preguntas más frecuentes sobre la nueva cuenta de reliquia {#faqs}

### ¿Qué monitoriza el Adobe con la nueva reliquia uno? {#adobe-monitor}

Adobe supervisa los servicios de creación, publicación y vista previa (cuando están disponibles) as a Cloud Service de AEM a través del complemento Java de New Relic One. Adobe permite la telemetría y monitorización personalizada de New Relic One APM en entornos as a Cloud Service que no sean de producción y producción AEM.

La nueva cuenta de Relic One está adjunta a una cuenta principal mantenida por Adobe y tiene varias aplicaciones informando al respecto: tres por AEM entorno as a Cloud Service.

* Una aplicación para el servicio de creación por entorno
* Una aplicación para el servicio de publicación por entorno (incluida la publicación de oro)
* Una aplicación para el servicio de vista previa por entorno

Importante:

* Cada aplicación utiliza una clave de licencia.
* AEM entornos as a Cloud Service solo informan de una cuenta nueva de Relic One.
* Las métricas y los eventos de monitorización completos para la Nueva reliquia uno se conservan durante 7 días.

### ¿Quién puede acceder a los datos del servicio en la nube New Relic One? {#access-new-relic-cloud}

Se concederá acceso de lectura completo para hasta 10 miembros de su equipo. El acceso de lectura incluirá todas las métricas de APM recopiladas por el agente New Relic One.

### ¿Se admite la configuración de SSO personalizada? {#custom-sso}

La configuración de SSO personalizada no es compatible con la nueva cuenta de Relic One aprovisionada por Adobe.

### ¿Qué sucede si ya tengo una suscripción a New Relic local? {#new-relic-subscription}

Nueva reliquia uno es la nueva plataforma de observabilidad de Nueva reliquia y permite al soporte de Adobe y a sus equipos observar, monitorear y ver métricas y eventos, todo en un solo lugar.

La nueva reliquia uno ofrece a los usuarios la capacidad de buscar en todas las cuentas donde tengan acceso y visualizar los datos de todos los servicios y hosts de una sola vista.

Mientras que el soporte de Adobe supervisará la aplicación as a Cloud Service AEM utilizando New Relic One y otras herramientas internas como parte de su servicio, sus equipos pueden seguir aprovechando New Relic para servicios e infraestructura alojados in situ. Podrán visualizar los datos tanto de la cuenta de Adobe Nueva reliquia uno como de las cuentas de Nueva reliquia gestionadas por el cliente.

>[!NOTE]
>
>Para ver ambos conjuntos de datos dentro de la nueva relación uno, un usuario debe tener los permisos adecuados y utilizar la misma metodología de inicio de sesión para ambas cuentas (Adobe de la nueva relación uno y las cuentas de nueva relación gestionadas por el cliente).
